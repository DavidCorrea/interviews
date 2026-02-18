# Story 13: Increase Font Size and Weight

## User Story

**As a** user with low vision or age-related vision decline,
**I want** body text to be large enough and bold enough to read comfortably,
**So that** I don't have to lean forward, squint, or zoom my browser to read content.

## Description

Body text appears to be 14px or smaller with a font weight of 300-400. Multiple users had to lean forward, squint, or zoom their browser significantly just to read basic content.

## Acceptance Criteria

- [ ] Base body font size is at least 16px (ideally 18px)
- [ ] Body text font weight is at least 400 (ideally 500)
- [ ] No text smaller than 24px uses a font weight lighter than 400
- [ ] Headings are proportionally larger and bolder than body text
- [ ] The font remains readable at default browser zoom (100%) without user adjustment

## Testing Instructions

1. **DevTools:** Inspect body text across the homepage — verify computed `font-size` is >= 16px and `font-weight` is >= 400
2. **Comparison:** Compare a before/after screenshot to confirm the visual improvement in readability
3. **User test:** Ask a person aged 60+ to read the homepage body text at default zoom — they should not need to lean in or squint
4. **Layout check:** Verify that the increased font size has not broken any layouts (text overflow, overlapping elements)
5. **Responsive:** Check that the font size remains appropriate on mobile viewports

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | High |
| **Complexity** | Low |
| **WCAG Criteria** | 1.4.8 (Visual Presentation) |
| **Affected Users** | Low vision users, seniors, low contrast sensitivity users, situational (bright light) users |

## Source Reports

- Low Vision User Report
- Senior User Report
- Low Contrast Sensitivity Report
- Situational Contrast Report
