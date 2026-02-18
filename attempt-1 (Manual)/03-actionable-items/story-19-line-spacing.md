# Story 19: Increase Line Spacing

## User Story

**As a** user with dyslexia,
**I want** sufficient spacing between lines of text,
**So that** my eyes can track from one line to the next without jumping to the wrong line.

## Description

Lines of text are too close together, causing dyslexic users to jump to the wrong line while reading and lose their place.

## Acceptance Criteria

- [ ] All body text has a `line-height` of at least 1.5
- [ ] Paragraph spacing is at least 1.5x the font size
- [ ] Body text uses left alignment only (no justified text)
- [ ] The increased spacing does not break any existing layouts

## Testing Instructions

1. **DevTools:** Inspect body text — verify computed `line-height` is at least 1.5 (or equivalent in px)
2. **Justify check:** Search CSS for `text-align: justify` — should not be present on body text
3. **Visual:** Read through several paragraphs — lines should feel spacious and easy to track
4. **Layout check:** Verify increased line spacing hasn't caused overflow or overlap issues in cards, buttons, or constrained containers
5. **Responsive:** Confirm spacing looks appropriate on both desktop and mobile viewports

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | Medium |
| **Complexity** | Low |
| **WCAG Criteria** | 1.4.8 (Visual Presentation) |
| **Affected Users** | Dyslexic users |

## Source Reports

- Dyslexic User Report
