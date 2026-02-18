# AI-04: Respect prefers-reduced-motion Media Query

## Metadata
- **ID:** AI-04
- **Priority:** 1 Critical
- **Personas Affected:** 6+ of 16 personas (vestibular disorders, motion sensitivity, cognitive load)
- **WCAG Criteria:** 2.3.3 Animation from Interactions (AAA), 2.2.2 Pause, Stop, Hide (A)
- **Effort:** Medium (4–8 hours)

---

## User Story

**As a** user with vestibular disorder, motion sensitivity, or who prefers reduced motion for comfort,

**I want** the LaunchPad Lab site to respect my system "Reduce motion" preference,

**So that** I can use the site without experiencing animations, parallax effects, or motion that could trigger dizziness, nausea, or cognitive overload.

---

## Acceptance Criteria

- [ ] When `prefers-reduced-motion: reduce` is set, no scroll-triggered animations (fade-in, slide-in) play
- [ ] When reduced motion is set, no parallax effects occur
- [ ] When reduced motion is set, hover transforms (scale, translate) are disabled or minimized
- [ ] When reduced motion is set, content appears instantly (no delayed reveals)
- [ ] When reduced motion is set, `scroll-behavior: smooth` is overridden to `auto`
- [ ] When reduced motion is set, carousel/slider auto-advance is paused or significantly slowed
- [ ] JavaScript animation libraries (AOS, GSAP, ScrollTrigger, etc.) check the preference before initializing

---

## Test Plan

### Enable Reduced Motion
**macOS:** System Preferences → Accessibility → Display → Reduce motion ✓  
**Windows:** Settings → Ease of Access → Display → Show animations → Off  
**Chrome DevTools:** More tools → Rendering → Emulate CSS media feature `prefers-reduced-motion: reduce`

### Manual Verification
1. Enable reduced motion in OS or DevTools
2. Reload `https://launchpadlab.com/`
3. Scroll down the homepage — **Expected:** No fade-in, slide-in, or staggered reveal animations
4. Hover over interactive elements — **Expected:** No scale, translate, or rotation transforms (or instant state change)
5. Check for parallax sections — **Expected:** No parallax movement
6. Navigate to other pages — **Expected:** Same behavior site-wide
7. If carousel/slider exists — **Expected:** No auto-advance or very slow advance

### Automated Check
- Use axe DevTools or Lighthouse — check for "prefers-reduced-motion" related recommendations
- Manually verify no `animation` or `transition` runs when preference is set (except 0.01ms overrides)

### Disable Reduced Motion
- Turn off the preference and reload — **Expected:** Animations work as before for users who have not set the preference

---

## Developer Notes

### CSS Approach
Add to global CSS (early in cascade):

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

This effectively disables CSS animations and transitions. Content will appear in final state.

### JavaScript Approach
Before initializing any animation library:

```javascript
const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

if (!prefersReducedMotion) {
  // Initialize AOS, GSAP ScrollTrigger, etc.
  AOS.init();
  // or
  gsap.registerPlugin(ScrollTrigger);
  // ... animation setup
}
```

### IntersectionObserver
If using IntersectionObserver for scroll-triggered effects:

```javascript
if (!prefersReducedMotion) {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('animate-in');
      }
    });
  });
  // ...
} else {
  // Add class immediately without animation
  document.querySelectorAll('.animate-on-scroll').forEach(el => {
    el.classList.add('animate-in');
  });
}
```

### Hover Effects
Replace `transform` and `transition` on hover with instant changes when reduced motion is set:

```css
@media (prefers-reduced-motion: reduce) {
  .card:hover {
    transform: none;
    transition: none;
  }
  .card:hover .overlay {
    opacity: 1; /* instant, no transition */
  }
}
```

### Carousels/Sliders
- Pause `setInterval`/`setTimeout` for auto-advance when `prefers-reduced-motion` is set
- Or set interval to a very long duration (e.g., 60 seconds) so it effectively doesn't auto-advance

### Files to Modify
- Global CSS
- Animation library initialization (e.g., `main.js`, `App.tsx`, layout component)
- Component-specific animation code (cards, hero, testimonials)
- Carousel/slider components

---

## Examples

| Site | Approach |
|------|----------|
| **Slack.com** | Respects reduced motion; animations disabled when preference set |
| **Stripe.com** | Marketing animations disabled; content appears instantly |
| **CSS-Tricks** | Articles and demos on implementing `prefers-reduced-motion` |
| **MDN Web Docs** | Documents the media query and provides implementation examples |
