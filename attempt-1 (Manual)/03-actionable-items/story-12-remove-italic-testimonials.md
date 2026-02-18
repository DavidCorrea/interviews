# Story 12: Remove Italic Text from Testimonials

## User Story

**As a** user with dyslexia,
**I want** testimonials to be displayed in regular (non-italic) text,
**So that** I can read client quotes without the letters blending together.

## Description

Testimonial quotes are displayed in italic text, which is extremely difficult for dyslexic users to read. Italic letters appear "swirly" and blend together, causing the user to skip entire testimonials.

## Acceptance Criteria

- [ ] Testimonial quotes use `font-style: normal` (not italic)
- [ ] Quotes are visually distinguished from surrounding text using non-italic methods (left border, background color, quotation marks, or indentation)
- [ ] No substantial block of text (more than one sentence) on the site uses italic styling
- [ ] Emphasis within text uses bold rather than italics

## Testing Instructions

1. **Visual check:** Review the contact page testimonials — all quotes should be in regular (upright) text
2. **CSS inspection:** Inspect testimonial elements in DevTools — verify `font-style` is `normal`, not `italic`
3. **Site-wide search:** Search the CSS for `font-style: italic` — verify it is not applied to any paragraph or blockquote
4. **Distinction check:** Verify testimonials are still visually distinguishable from regular content via borders, background, or quotation marks

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | High |
| **Complexity** | Low |
| **WCAG Criteria** | 1.4.8 (Visual Presentation) |
| **Affected Users** | Dyslexic users |

## Source Reports

- Dyslexic User Report
