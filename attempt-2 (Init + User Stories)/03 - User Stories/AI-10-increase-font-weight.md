# AI-10: Increase Body Text Font Weight

## User Story

As a **user with low vision or difficulty reading thin text**, I want **body text to be at least medium weight (500)**, so that **I can read content more clearly and with less eye strain**.

## Acceptance Criteria

- [ ] Body text font-weight is 500 (medium) or higher
- [ ] No readable content uses font-weight 300 (light)
- [ ] Layouts remain intact with increased font weight
- [ ] Heading hierarchy remains visually distinct (headings can be bolder than body)

## How to Test

1. Open the site (https://launchpadlab.com/) in Chrome
2. Open Chrome DevTools (F12 or right-click → Inspect)
3. Select the "Elements" tab
4. Inspect body text elements (paragraphs, main content)
5. In the "Computed" panel, verify **font-weight** is **500 or higher** for body copy
6. Confirm no body text uses font-weight 300

## Developer Notes

- Update CSS `font-weight` variable for body text to 500 (e.g., `--font-weight-body: 500;`)
- Avoid font-weight 300 for any readable content
- Test that bolder weight doesn't break layouts (e.g., text overflow, wrapping)
- Ensure headings remain distinguishable (e.g., 600–700 for headings)

## WCAG References

- **1.4.8 Visual Presentation (Level AAA):** Foreground and background colors can be selected by the user; text can be resized up to 200% without loss of content or functionality.

## Priority & Effort

| Priority | Effort Estimate |
|----------|-----------------|
| P2 High | Small (1h) |
