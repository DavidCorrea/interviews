# AI-03: Improve Body Text Contrast

## Title
Change body text from light gray (#666–#777) to #333 or darker for 7:1 contrast ratio

## User Story
As a **user with low vision or in bright lighting conditions**, I want **body text to have sufficient contrast against the background**, so that **I can read all content comfortably without straining my eyes**.

## Acceptance Criteria

- [ ] Body text meets at least 7:1 contrast ratio against background (AAA)
- [ ] No readable text is lighter than #555 on white (#FFF) background
- [ ] Secondary text (e.g., captions, metadata) meets minimum 4.5:1 contrast (AA)
- [ ] Testimonial text meets 7:1 contrast
- [ ] All previously gray (#666–#777) text has been updated to #333 or darker

## How to Test

1. Open `https://launchpadlab.com/` in a browser
2. Use [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) or browser DevTools
3. Sample body text colors from multiple pages (home, about, contact, blog, etc.)
4. Verify body text is at least #333 (or equivalent) on white background for 7:1 contrast
5. Check testimonial sections, captions, and secondary text
6. Confirm no readable text is lighter than #555

## Developer Notes

- Update CSS color variables for:
  - Body text → #333 or darker
  - Secondary text → #333 or #444 (minimum #555)
  - Testimonial text → #333 or darker
- Search for hex values: #666, #777, #888, #999 and replace with compliant colors
- Consider using CSS custom properties for easier maintenance:
  ```css
  :root {
    --color-body: #333;
    --color-body-secondary: #444;
  }
  ```
- No readable text should be lighter than #555 on white (#FFF) background

## WCAG References

- **[1.4.3 Contrast (Minimum) (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)**: The visual presentation of text and images of text has a contrast ratio of at least 4.5:1.
- **[1.4.6 Contrast (Enhanced) (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/contrast-enhanced.html)**: The visual presentation of text and images of text has a contrast ratio of at least 7:1.

## Priority & Effort

| Attribute | Value |
|-----------|-------|
| **Priority** | P1 Critical |
| **Effort Estimate** | Small (1–2 hours) |
