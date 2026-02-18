# AI-17: Minimum Target Size

## Title
Ensure all interactive elements have minimum 44×44px clickable area

## User Story
As a **user with motor impairments or who uses a touch device**, I want **all interactive elements to have a large enough clickable area**, so that **I can tap or click them accurately without accidentally activating adjacent elements**.

## Acceptance Criteria

- [ ] All interactive elements (links, buttons, nav items, carousel arrows) have a minimum 44×44px clickable area
- [ ] Adjacent interactive elements have at least 8px spacing between them
- [ ] Service cards are fully clickable (entire card is a link), not just a small "Learn More" text
- [ ] Form buttons and inputs meet minimum size requirements

## How to Test

1. Open DevTools and inspect interactive elements.
2. Check "Learn More" links, nav links, form buttons, and carousel arrows.
3. Verify computed hit area (including padding) is ≥ 44×44px for each.
4. Verify 8px+ spacing between adjacent targets.
5. Test on touch device to confirm easy activation without mis-taps.

## Developer Notes

- Add padding to links and buttons to achieve 44px minimum:
  ```css
  min-height: 44px;
  min-width: 44px;
  padding: 10px 16px;
  ```
- Make entire service cards clickable (`<a>` wrapping card) instead of small "Learn More" text.
- Add `gap: 8px` between adjacent interactive elements.
- Ensure focus indicators remain visible and do not reduce effective target size.

## WCAG References

- **2.5.5 Target Size (Level AAA):** The size of the target for pointer inputs is at least 44 by 44 CSS pixels.
- **2.5.8 Target Size (Minimum) (Level AA, WCAG 2.2):** Target size is at least 24 by 24 CSS pixels, unless the target is in a sentence or its size is otherwise constrained.

## Priority
**P2 High**

## Effort Estimate
**Medium (3–6h)**
