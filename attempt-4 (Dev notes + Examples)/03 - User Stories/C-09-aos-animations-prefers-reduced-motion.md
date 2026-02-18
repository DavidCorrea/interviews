# C-09: AOS Animations Do Not Respect `prefers-reduced-motion`

**Priority:** Critical
**WCAG Criteria:** 2.3.3 Animation from Interactions (AAA), 2.2.2 Pause, Stop, Hide (A)
**Affected Personas:** Motion Sensitivity, ADHD, Senior Person, Low Vision Screen Magnifier

---

## User Story

**As a** user who has enabled the "Reduce Motion" setting on my device,
**I want** all scroll-triggered animations on the site to be completely disabled or replaced with simple opacity fades,
**so that** I can read the content without experiencing dizziness, nausea, or distraction from unnecessary movement.

---

## Acceptance Criteria

- [ ] When `prefers-reduced-motion: reduce` is active, no AOS scroll animations play (elements are immediately visible in their final position).
- [ ] Content blocks that use AOS never start at `opacity: 0` when reduced motion is preferred — they load fully visible.
- [ ] The AOS library initialization includes the `disable` option checking for `prefers-reduced-motion`.
- [ ] The site's CSS includes at least one `@media (prefers-reduced-motion: reduce)` query that neutralizes all `data-aos` animations.
- [ ] This applies to all pages, not just the homepage.
- [ ] Users who have NOT requested reduced motion still see the animations as designed.

---

## How to Test the Change

### Manual Testing

1. **Enable Reduced Motion:**
   - **macOS:** System Settings → Accessibility → Display → Reduce Motion (ON).
   - **Windows:** Settings → Ease of Access → Display → Show animations in Windows (OFF).
   - **Chrome DevTools:** Rendering panel → Emulate CSS media feature `prefers-reduced-motion: reduce`.

2. **Browse the Site:**
   - Navigate to the homepage and scroll down.
   - Verify all content sections are immediately visible — no fade-in, slide-in, or zoom effects.
   - Check other pages (Services, About, Contact) for the same behavior.

3. **Disable Reduced Motion:**
   - Turn off the reduce motion setting.
   - Reload the page and verify animations play as normal.

### Automated Testing

```javascript
// Playwright test — verify animations disabled with reduced motion
test('AOS animations are disabled when prefers-reduced-motion is set', async ({ browser }) => {
  const context = await browser.newContext({
    reducedMotion: 'reduce',
  });
  const page = await context.newPage();
  await page.goto('https://launchpadlab.com');

  // Check that AOS elements don't have opacity: 0
  const aosElements = page.locator('[data-aos]');
  const count = await aosElements.count();

  for (let i = 0; i < Math.min(count, 10); i++) {
    const opacity = await aosElements.nth(i).evaluate(el =>
      window.getComputedStyle(el).opacity
    );
    expect(Number(opacity)).toBe(1);
  }

  await context.close();
});
```

---

## Developer Notes

### General Approach

There are two layers to fix: (1) the AOS JavaScript initialization and (2) CSS fallback. Both should check for `prefers-reduced-motion` and disable or neutralize animations accordingly.

### Code Examples

**Fix 1: AOS JavaScript initialization:**

```javascript
// Before
AOS.init({
  duration: 800,
  easing: 'ease-in-out',
  once: true,
});

// After — disable AOS when reduced motion is preferred
AOS.init({
  duration: 800,
  easing: 'ease-in-out',
  once: true,
  disable: function () {
    return window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  },
});
```

**Fix 2: CSS fallback (belt-and-suspenders approach):**

```css
@media (prefers-reduced-motion: reduce) {
  /* Disable all AOS animations */
  [data-aos] {
    opacity: 1 !important;
    transform: none !important;
    transition: none !important;
  }

  /* Also kill any CSS transitions/animations site-wide */
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

**Fix 3: Prevent FOUC (Flash of Unstyled Content) when AOS is disabled:**

```css
/* Ensure elements are visible even if AOS JS hasn't loaded yet */
@media (prefers-reduced-motion: reduce) {
  [data-aos] {
    opacity: 1 !important;
    transform: translate(0) scale(1) !important;
  }
}
```

### Components/Files to Audit

- AOS initialization JavaScript (likely in a main bundle or inline script).
- All elements with `data-aos` attributes across all page templates.
- Site-wide CSS — confirm no existing `@media (prefers-reduced-motion)` queries exist.
- Any custom animation CSS (`@keyframes` declarations, `transition` rules).
- Third-party animation libraries beyond AOS (check for GSAP, anime.js, etc.).

---

## Examples from Other Sites

| Site | Implementation |
|------|----------------|
| **Stripe** | All animations are disabled when `prefers-reduced-motion: reduce` is active. Elements appear in their final state instantly. |
| **GitHub** | Uses `@media (prefers-reduced-motion: reduce)` to set `transition-duration: 0.01ms` globally. |
| **MDN Web Docs** | Global CSS rule: `@media (prefers-reduced-motion: reduce) { * { animation: none !important; transition: none !important; } }` |
| **gov.uk** | Minimal animations to begin with, but includes a reduced-motion query that disables all remaining transitions. |
