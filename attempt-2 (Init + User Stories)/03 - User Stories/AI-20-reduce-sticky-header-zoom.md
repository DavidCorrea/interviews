# AI-20: Reduce Sticky Header at Zoom

## Title
Reduce sticky header footprint at high zoom levels (200%+)

## User Story
As a **user who zooms the page for readability**, I want **the sticky header to take up minimal screen space**, so that **I can see more content without excessive scrolling**.

## Acceptance Criteria

- [ ] At 200% zoom, header consumes no more than 25% of viewport height
- [ ] At 300% zoom, header consumes no more than 25% of viewport height
- [ ] Header remains functional and accessible at all zoom levels
- [ ] Content below header is not obscured or unreachable

## How to Test

1. Open the site in a browser.
2. Zoom to 200% (Ctrl/Cmd + "+" or browser zoom controls).
3. Measure header height as percentage of viewport; verify ≤ 25%.
4. Zoom to 300% and repeat measurement.
5. Verify header remains usable (links clickable, navigation accessible).
6. Verify main content is visible and scrollable.

## Developer Notes

- Add responsive CSS to limit header height at narrow viewports:
  ```css
  @media (max-width: 480px) {
    .header {
      position: relative; /* or */
      max-height: 60px;
    }
  }
  ```
- Consider auto-hiding header on scroll down, showing on scroll up.
- Consider collapsing to compact version at narrow viewports.
- Use `max-height` and `overflow` to constrain header at high zoom.
- Test with `prefers-reduced-motion` in mind if using scroll-based hiding.

## WCAG References

- **1.4.10 Reflow (Level AA):** Content can be presented without loss of information or functionality, and without requiring scrolling in two dimensions for content at 320 CSS pixels width and 256 CSS pixels height (or equivalent). At 400% zoom, content reflows to single column.

## Priority
**P3 Medium**

## Effort Estimate
**Small–Medium (2–4h)**
