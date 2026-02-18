# AI-09: Increase Minimum Font Size

## User Story

As a **user with low vision or difficulty reading small text**, I want **body text to be at least 16px (1rem) using relative units**, so that **I can read content comfortably without straining or zooming excessively**.

## Acceptance Criteria

- [ ] Body text minimum size is 16px (1rem) or larger
- [ ] Form labels are at least 14px
- [ ] Helper text and disclaimers are at least 14px
- [ ] Relative units (rem, em) are used throughout for scalability
- [ ] No body text or primary content uses font-size below 16px

## How to Test

1. Open the site (https://launchpadlab.com/) in Chrome
2. Open Chrome DevTools (F12 or right-click → Inspect)
3. Select the "Elements" tab
4. Inspect body text elements (paragraphs, headings, content)
5. In the "Computed" panel, verify **font-size** is **≥ 16px** for body copy
6. Inspect form labels → computed font-size should be **≥ 14px**
7. Inspect helper/disclaimer text → computed font-size should be **≥ 14px**

## Developer Notes

- Set `html { font-size: 100%; }` to establish 16px as the default (browser default)
- Use `rem` units throughout for scalable typography (e.g., `1rem`, `1.125rem`)
- Update any hardcoded `px` values below 16px for body text

## WCAG References

- **1.4.4 Resize Text (Level AA):** Text can be resized up to 200% without loss of content or functionality.
- **1.4.8 Visual Presentation (Level AAA):** Foreground and background colors can be selected by the user; text can be resized up to 200% without loss of content or functionality.

## Priority & Effort

| Priority | Effort Estimate |
|----------|-----------------|
| P2 High | Small (1–2h) |
