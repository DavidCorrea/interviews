# AI-11: Increase Body Text Line Height

## User Story

As a **user with low vision, dyslexia, or reading difficulties**, I want **body text to have adequate line spacing (at least 1.5)**, so that **I can read content more comfortably and without lines blending together**.

## Acceptance Criteria

- [ ] Body text line-height is at least 1.5

## How to Test

1. Open the site (https://launchpadlab.com/) in Chrome
2. Open Chrome DevTools (F12 or right-click → Inspect)
3. Select the "Elements" tab
4. Inspect body text elements (paragraphs, main content)
5. In the "Computed" panel, verify **line-height** is **≥ 1.5** for all body text
6. Check multiple paragraphs and content blocks across the site

## Developer Notes

- Set `line-height: 1.5` or `1.6` on body/paragraph selectors
- Example: `body { line-height: 1.5; }` or `p { line-height: 1.6; }`
- Verify no text overlap or layout breakage with increased line height
- Consider using unitless values (1.5) for better inheritance and scaling

## WCAG References

- **1.4.8 Visual Presentation (Level AAA):** Foreground and background colors can be selected by the user; text can be resized up to 200% without loss of content or functionality.

## Priority & Effort

| Priority | Effort Estimate |
|----------|-----------------|
| P2 High | Small (1h) |
