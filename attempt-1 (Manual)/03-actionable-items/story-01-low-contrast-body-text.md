# Story 01: Increase Body Text Contrast

## User Story

**As a** user with low vision, low contrast sensitivity, or someone browsing in bright environments,
**I want** all body text to have sufficient contrast against its background,
**So that** I can read the site's content without straining my eyes or missing information.

## Description

The majority of body text across the site uses light gray colors (estimated #666 or #777) on white backgrounds. This makes 60-70% of content nearly unreadable for users with low vision, low contrast sensitivity, or those browsing in bright environments. Service descriptions, testimonials, process details, and introductory paragraphs all suffer from this problem.

## Acceptance Criteria

- [ ] All body text uses a color of #333333 or darker
- [ ] No readable text uses a gray lighter than #555555
- [ ] Body text font weight is at least 400 (ideally 500)
- [ ] All normal-sized text meets WCAG AA contrast ratio (4.5:1 minimum)
- [ ] All large text meets WCAG AA contrast ratio (3:1 minimum)
- [ ] Service descriptions, testimonials, process details, and introductory paragraphs are all clearly legible

## Testing Instructions

1. **Automated:** Run an accessibility audit tool (e.g., axe DevTools, Lighthouse) and confirm zero contrast violations
2. **Manual:** Use a contrast checker (e.g., WebAIM Contrast Checker) to verify body text color against background color meets 4.5:1 ratio
3. **Visual:** View the site on a laptop in bright sunlight or with screen brightness at 50% — all body text should remain readable
4. **Browser:** Test in Chrome, Firefox, and Safari to ensure consistent rendering

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | Critical |
| **Complexity** | Low |
| **WCAG Criteria** | 1.4.3 (Contrast Minimum), 1.4.6 (Contrast Enhanced) |
| **Affected Users** | Low vision, senior, cognitive disability, situational (bright light), dyslexic, low contrast sensitivity |

## Source Reports

- Low Vision User Report
- Senior User Report
- Low Vision Screen Magnifier Report
- Situational Contrast Report
- Cognitive Disability Report
- Stressed User Report
- Low Contrast Sensitivity Report
- Dyslexic User Report
