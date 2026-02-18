# H-24: CSS Has Zero `prefers-reduced-motion` Media Queries

**Issue ID:** H-24
**Priority:** High
**WCAG Criteria:** 2.3.3 Animation from Interactions (AAA)
**Affected Personas:** Motion Sensitivity, ADHD

---

## User Story

**As a** user who has enabled "reduce motion" in my operating system,
**I want** all CSS animations and transitions on the site to be disabled or simplified,
**so that** I can browse comfortably without experiencing motion that triggers discomfort, distraction, or vestibular symptoms.

---

## Acceptance Criteria

- [ ] At least one `@media (prefers-reduced-motion: reduce)` block exists in the site's CSS that disables or simplifies all non-essential animations.
- [ ] All `@keyframes` animations are disabled (`animation: none`) when reduced motion is preferred.
- [ ] All `transition` properties are reduced to `transition-duration: 0.01s` or removed when reduced motion is preferred.
- [ ] Essential state changes (e.g., dropdown show/hide, accordion expand) still function but without animated transitions.
- [ ] The site remains fully functional and visually coherent with reduced motion active — no content becomes invisible or inaccessible.
- [ ] The `prefers-reduced-motion` query is placed in the main stylesheet (not an optional add-on).

---

## How to Test the Change

### Manual Testing

1. **macOS:** System Settings → Accessibility → Display → Reduce motion → ON. Browse all pages. Confirm no visible CSS animations or transitions play.
2. **Chrome DevTools:** Rendering panel → "Emulate CSS media feature prefers-reduced-motion" → "reduce." Browse the site and confirm static experience.
3. **Before/after comparison:** Record a screen capture with reduced motion OFF (normal), then with reduced motion ON. Compare to confirm animations are absent in the ON recording.
4. **Content visibility check:** With reduced motion ON, scroll through every section. Confirm all content is visible — no content remains at `opacity: 0` due to AOS or other scroll animations failing to complete.

### Automated Testing

```bash
# Check CSS files for prefers-reduced-motion queries
grep -r "prefers-reduced-motion" /path/to/css/
# Should return at least one match after the fix
```

```javascript
// Programmatic check
const sheets = [...document.styleSheets];
const hasReducedMotion = sheets.some(sheet => {
  try {
    return [...sheet.cssRules].some(rule =>
      rule.media?.mediaText?.includes('prefers-reduced-motion')
    );
  } catch { return false; }
});
console.assert(hasReducedMotion, 'No prefers-reduced-motion media query found in any stylesheet');
```

---

## Developer Notes

### General Approach

Add a global `@media (prefers-reduced-motion: reduce)` block to the main stylesheet that disables all animations and transitions in one sweep. Then review individual components for any animation that is essential to functionality (e.g., a loading spinner) and re-enable only those with minimal motion.

### Current State (Problem)

The site CSS contains multiple `@keyframes` and `transition` declarations but zero `@media (prefers-reduced-motion)` queries:

```css
/* Examples of animations that currently run unconditionally */
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}

.service-card {
  transition: transform 0.3s ease, box-shadow 0.3s ease, opacity 0.3s ease;
}

.hero-text {
  animation: fadeInUp 1s ease-out;
}
```

### Recommended Fix — Global Override

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

### More Granular Approach (Preferred for Fine Control)

```css
@media (prefers-reduced-motion: reduce) {
  /* Disable scroll-triggered animations (AOS) */
  [data-aos] {
    opacity: 1 !important;
    transform: none !important;
    transition: none !important;
  }

  /* Disable hero animations */
  .hero-text {
    animation: none;
  }

  /* Disable card hover transitions */
  .service-card {
    transition: none;
  }

  /* Disable marquee/carousel auto-scroll */
  .logo-marquee {
    animation: none;
  }

  /* Keep essential functional transitions minimal */
  .dropdown-menu {
    transition: opacity 0.01s;
  }
}
```

### Components / Files to Audit

- Main stylesheet (`style.css` or `main.css`)
- AOS library initialization (also needs JS-side `disable` option — see C-09)
- Any component-level stylesheets with `@keyframes` or `transition`
- Theme's `functions.php` or build pipeline where CSS is compiled

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **GOV.UK** | Global reduced-motion override in design system CSS disables all non-essential animations | Single source of truth; every component inherits the override. |
| **Smashing Magazine** | Uses the universal `*` selector approach to kill all animations/transitions when reduced motion is preferred | Comprehensive with one CSS block. |
| **GitHub** | Individual component animations have paired `prefers-reduced-motion` overrides | Fine-grained control preserves essential motion. |
| **CSS-Tricks** | Published the canonical "reduced motion" CSS pattern adopted widely across the industry | Widely referenced best practice. |
