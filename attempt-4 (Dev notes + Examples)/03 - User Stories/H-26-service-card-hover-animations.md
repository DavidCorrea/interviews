# H-26: Service Card Hover Animations Not Reducible

**Issue ID:** H-26
**Priority:** High
**WCAG Criteria:** 2.3.3 Animation from Interactions (AAA)
**Affected Personas:** Motion Sensitivity

---

## User Story

**As a** user with vestibular sensitivity,
**I want** service card hover animations to be disabled when I have "reduce motion" enabled,
**so that** I can browse services without triggering discomfort from unexpected motion.

---

## Acceptance Criteria

- [ ] When `prefers-reduced-motion: reduce` is active, service card hover effects do not animate (no transform, opacity, or box-shadow transitions).
- [ ] Hover state changes (if any) are applied instantly without transition duration.
- [ ] The hover state itself (e.g., a subtle background change) can remain as long as it does not involve motion — only the animated transition is removed.
- [ ] Focus state changes follow the same reduced-motion behavior.
- [ ] The cards remain fully functional and visually coherent with transitions removed.

---

## How to Test the Change

### Manual Testing

1. **macOS:** Enable Reduce Motion. Hover over each service card. Confirm no animated transitions play — any visual changes happen instantly.
2. **Chrome DevTools:** Rendering → Emulate `prefers-reduced-motion: reduce`. Hover over service cards. Confirm no motion.
3. **Side-by-side comparison:** Record screen with reduced motion OFF (hover shows animation) and ON (hover changes instantly). Compare.
4. **Keyboard focus test:** Tab through service cards with reduced motion ON. Confirm no animated focus transitions.

### Automated Testing

```javascript
// Verify service card transition is removed with reduced motion
const card = document.querySelector('.service-card');
const computedStyle = getComputedStyle(card);
// With prefers-reduced-motion: reduce emulated
console.assert(
  computedStyle.transitionDuration === '0s' || computedStyle.transitionDuration === '0.01ms',
  'Service card should have no transition duration with reduced motion'
);
```

---

## Developer Notes

### General Approach

Add a `prefers-reduced-motion: reduce` media query that removes transition properties from service card hover states.

### Current State (Problem)

```css
.service-card {
  transition: transform 0.3s ease, box-shadow 0.3s ease, opacity 0.3s ease;
}

.service-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
  opacity: 1;
}
```

### Recommended Fix

```css
.service-card {
  transition: transform 0.3s ease, box-shadow 0.3s ease, opacity 0.3s ease;
}

.service-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
  opacity: 1;
}

@media (prefers-reduced-motion: reduce) {
  .service-card {
    transition: none;
  }

  .service-card:hover {
    transform: none; /* Remove vertical shift */
    /* Keep box-shadow and opacity for subtle static difference */
  }
}
```

### Alternative: Global Override

If H-24 (global reduced-motion override) is implemented, the service cards will be covered by the global rule. However, adding a component-specific override is still recommended for maintainability:

```css
@media (prefers-reduced-motion: reduce) {
  .service-card,
  .service-card:hover,
  .service-card:focus-within {
    transition: none;
    transform: none;
    animation: none;
  }
}
```

### Components / Files to Audit

- Service card CSS (search for `.service-card` transition/transform rules)
- Service card hover overlay CSS (the opacity: 0 → 1 reveal)
- Homepage services section template
- Services page template

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **Stripe** | Card hover effects are disabled entirely with `prefers-reduced-motion: reduce`; only a subtle background color shift remains | Motion is removed but the hover state is still perceptible. |
| **Linear** | Feature cards use instant state changes when reduced motion is active | Zero transition duration, but the end state is preserved. |
| **Notion** | Hover effects respect system motion preference globally | Consistent experience across all interactive components. |
