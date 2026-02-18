# AI-08: Fix Layout Reflow at 320px Viewport

## User Story

As a **user with low vision who zooms to 400% or uses a narrow viewport**, I want **all content to reflow into a single column without horizontal scrolling**, so that **I can read and interact with the entire page without losing content or needing to scroll horizontally**.

## Acceptance Criteria

- [ ] At 320px viewport width (equivalent to 400% zoom on 1280px screen), no horizontal scrollbar appears
- [ ] Multi-column grids (services, logos, statistics) stack vertically into a single column
- [ ] No text or buttons are cut off or overflow the viewport
- [ ] Images scale appropriately and do not cause horizontal overflow
- [ ] All interactive elements remain accessible and usable at narrow widths

## How to Test

1. Open the site (https://launchpadlab.com/) in Chrome
2. Open Chrome DevTools (F12 or right-click → Inspect)
3. Toggle device toolbar (Ctrl+Shift+M or Cmd+Shift+M) to enable responsive mode
4. Set viewport width to **320px**
5. Verify **no horizontal scrollbar** appears at the bottom of the viewport
6. Scroll through the page and confirm:
   - Services section grid stacks vertically
   - Logo carousel displays without overflow
   - Statistics section stacks vertically
   - Case study cards stack vertically
   - No text or buttons are cut off or clipped

## Developer Notes

- **Audit all grid/flex layouts** across the site for fixed widths and multi-column breakpoints
- Add responsive breakpoint: `@media (max-width: 480px) { .grid { grid-template-columns: 1fr; } }`
- Use `max-width: 100%` on all images to prevent overflow
- Remove fixed-width containers that exceed viewport at 320px
- Use `flex-wrap: wrap` on flex containers to allow wrapping
- **Key sections to test:** services section, logo carousel, statistics, case study cards
- Consider using `min()` or `clamp()` for fluid typography and spacing

## WCAG References

- **1.4.10 Reflow (Level AA):** Content can be presented without loss of information or functionality, and without requiring scrolling in two dimensions for a width equivalent to 320 CSS pixels.

## Priority & Effort

| Priority | Effort Estimate |
|----------|-----------------|
| P1 Critical | Large (8–16h) |
