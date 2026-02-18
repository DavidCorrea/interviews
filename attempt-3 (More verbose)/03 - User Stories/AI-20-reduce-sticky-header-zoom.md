# AI-20: Reduce Sticky Header Impact at High Zoom

## Metadata
- **ID:** AI-20
- **Priority:** 3 Medium
- **Personas Affected:** 2 of 16 personas (low-vision, screen magnifier)
- **WCAG Criteria:** 1.4.10 Reflow (AA)
- **Effort:** Small–Medium (2–4 hours)

---

## User Story

**As a** user with low vision who zooms the browser to 300% or uses a screen magnifier,

**I want** the sticky header to collapse or minimize at high zoom levels so it doesn't consume most of my viewport,

**So that** I can see meaningful page content instead of having 30–40% of my screen permanently obscured by the header.

---

## Acceptance Criteria

- [ ] At viewport widths below 480px (or equivalent 300% zoom on 1280px screen), header consumes maximum 25% of viewport height
- [ ] Header collapses to compact form (logo + minimal nav) or hides entirely at narrow viewports
- [ ] When scrolling down, header hides or collapses to maximize content visibility
- [ ] When scrolling up, header reappears for navigation access
- [ ] Skip link remains functional and reachable when header is visible
- [ ] No page content is permanently obscured by the header at any zoom level
- [ ] Alternative: `position: relative` instead of `fixed` at high-zoom breakpoints so header scrolls away naturally

---

## Test Plan

### Viewport Simulation
1. Open `https://launchpadlab.com/` in Chrome or Firefox
2. Open DevTools (F12) → Toggle device toolbar (Ctrl+Shift+M / Cmd+Shift+M)
3. Set viewport to 426px width (simulates ~300% zoom on 1280px screen)
4. **Expected:** Header height is ≤ 25% of viewport (e.g., ≤ ~107px on 426px viewport)
5. If header exceeds 25%, implement compact header or collapse

### Browser Zoom Test
1. Set browser zoom to 300% (Ctrl/Cmd + + three times, or View → Zoom → 300%)
2. Resize browser window to ~1280px width
3. **Expected:** Effective viewport is ~426px; header consumes max 25% of visible area
4. Measure: header height ÷ viewport height ≤ 0.25

### Scroll-Down / Scroll-Up Behavior
1. At 300% zoom or 426px viewport, scroll down the page
2. **Expected:** Header hides or collapses (slides up out of view)
3. Continue scrolling down — header stays hidden
4. Scroll up (even slightly)
5. **Expected:** Header reappears within 1–2 seconds or on scroll-up gesture
6. Verify: No content is permanently obscured; user can always scroll to see it

### Skip Link Verification
1. Tab from page load — skip link should receive focus first (if implemented)
2. When header is visible, activate skip link
3. **Expected:** Focus moves to main content; skip link works
4. When header is hidden, ensure skip link is still in DOM and focusable on next Tab (or appears when header shows)

### Cross-Browser
1. Test in Chrome, Firefox, Safari, Edge
2. **Expected:** Consistent behavior across browsers
3. Test with Windows High Contrast mode if applicable

---

## Developer Notes

### CSS Approach: Compact Header at Narrow Viewports
```css
/* Breakpoint: viewport width ≤ 480px (or 426px for 300% zoom sim) */
@media (max-width: 480px) {
  .site-header {
    position: relative; /* Alternative: let header scroll away */
    /* OR keep fixed but reduce height */
    max-height: 25vh;
    padding: 0.5rem 1rem;
  }
  .site-header .nav-links {
    display: none; /* Show hamburger only */
  }
  .site-header .logo {
    max-height: 32px;
  }
}
```

### JavaScript: Hide on Scroll-Down, Show on Scroll-Up
```javascript
const header = document.querySelector('.site-header');
let lastScrollY = window.scrollY;
const scrollThreshold = 50;

window.addEventListener('scroll', () => {
  const currentScrollY = window.scrollY;
  if (currentScrollY > lastScrollY && currentScrollY > scrollThreshold) {
    header.classList.add('header-hidden');
  } else {
    header.classList.remove('header-hidden');
  }
  lastScrollY = currentScrollY;
}, { passive: true });
```

```css
.header-hidden {
  transform: translateY(-100%);
  transition: transform 0.3s ease;
}
```

### Alternative: Position Relative at High Zoom
```css
@media (max-width: 480px) {
  .site-header {
    position: relative !important;
    /* Header scrolls with page — no fixed overlay */
  }
}
```

### Skip Link Considerations
- Ensure skip link is first focusable element in `<body>`
- When header hides, skip link may be off-screen; ensure it's still in tab order when header reappears
- Test: `document.querySelector('a[href="#main"]')` exists and is focusable

### Breakpoint Rationale
- 480px ≈ 300% zoom on 1440px screen
- 426px ≈ 300% zoom on 1280px screen
- WCAG 1.4.10 requires content reflow at 320px; 480px is a reasonable threshold for header collapse

---

## Examples

| Site | Approach |
|------|----------|
| **BBC.com** | Header hides on scroll down; reappears on scroll up; minimal footprint when visible |
| **Medium.com** | Thin sticky bar with minimal elements; reading-focused layout at high zoom |
| **DEV.to** | Thin fixed bar; compact navigation; content-first design |
| **GOV.UK** | Header collapses to minimal form; respects reduced motion |
