# H-25: Smooth Scrolling Ignores `prefers-reduced-motion`

**Issue ID:** H-25
**Priority:** High
**WCAG Criteria:** 2.3.3 Animation from Interactions (AAA)
**Affected Personas:** Motion Sensitivity

---

## User Story

**As a** user with motion sensitivity who has enabled "reduce motion" in my OS settings,
**I want** anchor link navigation to jump instantly to the target section instead of smooth-scrolling,
**so that** I don't experience dizziness or discomfort from animated page movement.

---

## Acceptance Criteria

- [ ] When `prefers-reduced-motion: reduce` is active, all anchor link navigation jumps instantly (no smooth scroll animation).
- [ ] When `prefers-reduced-motion: no-preference` is active, smooth scrolling works as currently designed.
- [ ] The CSS `scroll-behavior: smooth` rule (if present) is overridden to `scroll-behavior: auto` inside a `prefers-reduced-motion: reduce` media query.
- [ ] JavaScript `scrollIntoView({ behavior: 'smooth' })` calls are conditionally changed to `{ behavior: 'auto' }` when reduced motion is preferred.
- [ ] The final scroll position is identical whether smooth or instant scrolling is used.
- [ ] The fix applies to all pages where anchor links are used.

---

## How to Test the Change

### Manual Testing

1. **macOS:** Enable Reduce Motion (System Settings → Accessibility → Display). Click any anchor link (e.g., skip-to-content, in-page navigation). Confirm the page jumps instantly with no animation.
2. **Chrome DevTools:** Rendering panel → Emulate `prefers-reduced-motion: reduce`. Click anchor links throughout the site. Confirm instant jumps.
3. **Comparison test:** Toggle reduced motion on/off. Click the same anchor link with each setting. Confirm smooth animation plays only when reduced motion is OFF.

### Automated Testing

```javascript
// Check for prefers-reduced-motion-aware scrolling in JS
// Search codebase for scrollIntoView calls
// Each should be wrapped in or preceded by a matchMedia check
```

---

## Developer Notes

### General Approach

Fix in two places: (1) CSS `scroll-behavior` and (2) JavaScript `scrollIntoView` calls.

### Fix 1: CSS Override

```css
/* If the site uses CSS smooth scrolling */
html {
  scroll-behavior: smooth;
}

@media (prefers-reduced-motion: reduce) {
  html {
    scroll-behavior: auto;
  }
}
```

### Fix 2: JavaScript — Current State (Problem)

```javascript
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
  anchor.addEventListener('click', function (e) {
    e.preventDefault();
    document.querySelector(this.getAttribute('href')).scrollIntoView({
      behavior: 'smooth'
    });
  });
});
```

### Fix 2: JavaScript — Recommended Fix

```javascript
const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)');

document.querySelectorAll('a[href^="#"]').forEach(anchor => {
  anchor.addEventListener('click', function (e) {
    e.preventDefault();
    const target = document.querySelector(this.getAttribute('href'));
    if (target) {
      target.scrollIntoView({
        behavior: prefersReducedMotion.matches ? 'auto' : 'smooth'
      });
    }
  });
});
```

### Utility Helper (Reusable)

```javascript
/**
 * Returns 'auto' or 'smooth' based on user's motion preference.
 * Use with scrollIntoView, window.scrollTo, etc.
 */
function getScrollBehavior() {
  return window.matchMedia('(prefers-reduced-motion: reduce)').matches
    ? 'auto'
    : 'smooth';
}

// Usage
element.scrollIntoView({ behavior: getScrollBehavior() });
```

### Components / Files to Audit

- Main JavaScript file (search for `scrollIntoView`, `scrollTo`, `scroll-behavior`)
- Main CSS file (search for `scroll-behavior: smooth`)
- Any smooth scroll library/plugin (e.g., `smooth-scroll.js`)
- Skip-to-content link handler

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **MDN Web Docs** | CSS `scroll-behavior: smooth` is wrapped in a `prefers-reduced-motion: no-preference` media query | Opt-in approach: smooth scroll only for users who haven't requested reduced motion. |
| **web.dev** | Uses the same opt-in CSS pattern and conditionalizes JS scrolling | Consistent across CSS and JS layers. |
| **GitHub** | Anchor navigation respects reduced motion system-wide | Smooth scroll is absent when OS preference is set. |
