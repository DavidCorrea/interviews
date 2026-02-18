# H-23: Statistics Counter Animation Ignores `prefers-reduced-motion`

**Issue ID:** H-23
**Priority:** High
**WCAG Criteria:** 2.3.3 Animation from Interactions (AAA)
**Affected Personas:** Motion Sensitivity

---

## User Story

**As a** user with vestibular sensitivity who has enabled "reduce motion" in my OS settings,
**I want** the statistics counter animation to be disabled and show final values immediately,
**so that** I don't experience dizziness or discomfort from rapidly changing numbers.

---

## Acceptance Criteria

- [ ] When `prefers-reduced-motion: reduce` is active, statistics numbers display their final values immediately with no counting animation.
- [ ] When `prefers-reduced-motion: no-preference` is active (default), the counting animation plays as currently designed.
- [ ] The `prefers-reduced-motion` check is performed before the animation starts (not mid-animation).
- [ ] If the user changes their OS motion preference while on the page, the behavior updates accordingly (via `matchMedia` listener).
- [ ] The final numeric values are identical whether the animation plays or not.
- [ ] The `aria-live` or visible text is not disrupted by the reduced-motion branch.

---

## How to Test the Change

### Manual Testing

1. **macOS:** System Settings → Accessibility → Display → Reduce motion → ON. Load the homepage. Confirm statistics show final numbers instantly.
2. **Windows:** Settings → Accessibility → Visual effects → Animation effects → OFF. Load the homepage. Confirm no counting animation.
3. **Chrome DevTools:** Open Rendering panel → "Emulate CSS media feature prefers-reduced-motion" → select "reduce." Reload the page. Confirm static numbers.
4. **Toggle test:** With the page loaded, toggle the OS reduced motion setting. Confirm future scroll-triggered counters respect the new preference.

### Automated Testing

```javascript
// Unit test pseudo-code (Jest)
describe('Counter animation', () => {
  it('skips animation when prefers-reduced-motion is reduce', () => {
    window.matchMedia = jest.fn().mockImplementation(query => ({
      matches: query === '(prefers-reduced-motion: reduce)',
      media: query,
      addEventListener: jest.fn(),
    }));

    const counter = initCounter({ target: 250, duration: 2000 });
    expect(counter.element.textContent).toBe('250'); // Immediate final value
  });
});
```

---

## Developer Notes

### General Approach

Wrap the `requestAnimationFrame` counter animation in a `prefers-reduced-motion` check. When reduced motion is preferred, skip the animation and set the final value directly.

### Current State (Problem)

```javascript
function animateCounter(element, target, duration) {
  let start = 0;
  const step = (timestamp) => {
    if (!start) start = timestamp;
    const progress = Math.min((timestamp - start) / duration, 1);
    element.textContent = Math.floor(progress * target);
    if (progress < 1) {
      requestAnimationFrame(step);
    }
  };
  requestAnimationFrame(step);
}
```

### Recommended Fix

```javascript
function animateCounter(element, target, duration) {
  // Respect reduced motion preference
  const motionQuery = window.matchMedia('(prefers-reduced-motion: reduce)');

  if (motionQuery.matches) {
    element.textContent = target;
    return;
  }

  let start = 0;
  const step = (timestamp) => {
    if (!start) start = timestamp;
    const progress = Math.min((timestamp - start) / duration, 1);
    element.textContent = Math.floor(progress * target);
    if (progress < 1) {
      requestAnimationFrame(step);
    }
  };
  requestAnimationFrame(step);
}
```

### Optional: Listen for Preference Changes

```javascript
const motionQuery = window.matchMedia('(prefers-reduced-motion: reduce)');
motionQuery.addEventListener('change', (e) => {
  if (e.matches) {
    // Set all counters to final values immediately
    document.querySelectorAll('[data-counter-target]').forEach(el => {
      el.textContent = el.dataset.counterTarget;
    });
  }
});
```

### Components / Files to Audit

- Counter animation JavaScript (search for `requestAnimationFrame` + counter logic)
- Homepage statistics section template
- About page statistics section template
- Any IntersectionObserver that triggers the counter animation on scroll

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **Stripe** | Counter animations check `matchMedia` before running; values appear instantly with reduced motion | Clean conditional pattern. |
| **GitHub** | Annual report page respects reduced motion for all scroll-triggered animations | System-wide preference is honored consistently. |
| **MDN Web Docs** | Recommends the `matchMedia` pattern in their `prefers-reduced-motion` documentation | Canonical reference implementation. |
