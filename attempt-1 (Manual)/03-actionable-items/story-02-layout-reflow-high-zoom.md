# Story 02: Fix Layout Reflow at High Zoom Levels

## User Story

**As a** user who relies on browser zoom at 200% or higher,
**I want** all page content to reflow into a single column without horizontal scrolling,
**So that** I can read and navigate the site by scrolling vertically only.

## Description

At 200-300% browser zoom, multi-column grid layouts (services, problems, logos, case studies, statistics) do not collapse into a single column. This forces users to scroll both horizontally and vertically, creating a two-dimensional navigation puzzle. Users reported 50-60 horizontal pans and 100+ vertical scrolls just to view the homepage.

## Acceptance Criteria

- [ ] At 200% browser zoom, no horizontal scrollbar appears
- [ ] At 300% browser zoom, no horizontal scrollbar appears
- [ ] At 400% browser zoom, no horizontal scrollbar appears
- [ ] Service boxes stack vertically in a single column at high zoom
- [ ] Problem boxes stack vertically in a single column at high zoom
- [ ] Company logos wrap or stack vertically at high zoom
- [ ] Case studies stack vertically at high zoom
- [ ] Statistics stack vertically at high zoom
- [ ] No content is cut off or hidden at any zoom level
- [ ] No fixed-width containers prevent content reflow

## Testing Instructions

1. **Zoom test:** Open the site in Chrome, set zoom to 200%, 300%, and 400% — verify no horizontal scrollbar at any level
2. **Responsive test:** Use Chrome DevTools to set viewport width to 320px (simulates high zoom) — all content should be single-column
3. **Content check:** At each zoom level, verify all text is fully visible and no words are cut off at viewport edges
4. **Navigation:** At 300% zoom, navigate the entire homepage using only vertical scrolling — you should never need to scroll left or right
5. **Cross-browser:** Repeat zoom tests in Firefox and Safari

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | Critical |
| **Complexity** | Medium-High |
| **WCAG Criteria** | 1.4.10 (Reflow) |
| **Affected Users** | Low vision magnifier users, stressed users with zoom needs |

## Source Reports

- Low Vision Screen Magnifier Report
- Stressed User Report
