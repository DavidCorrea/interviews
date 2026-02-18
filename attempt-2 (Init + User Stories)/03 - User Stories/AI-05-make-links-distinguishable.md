# AI-05: Make Links Distinguishable

## Title
Add underlines or other non-color cues to all text links so they are distinguishable from body text

## User Story
As a **user who is color blind or has low vision**, I want **links to be distinguishable from body text using more than color alone**, so that **I can identify and access links even when I cannot perceive color differences**.

## Acceptance Criteria

- [ ] All content/inline links have underlines or another non-color visual cue
- [ ] Links remain identifiable when viewed in grayscale
- [ ] Navigation links use cues such as bold, background, or underline
- [ ] Link color has at least 3:1 contrast against surrounding text
- [ ] Links have 3:1 contrast against the background
- [ ] Hover/focus states provide additional feedback beyond color change

## How to Test

1. View `https://launchpadlab.com/` in grayscale:
   - Use browser DevTools → Rendering → Emulate CSS media feature `prefers-color-scheme` or a grayscale filter
   - Or use OS/browser accessibility settings to simulate color blindness
2. Identify all inline/content links on multiple pages
3. Verify each link is identifiable without relying on color (underline, bold, or other cue)
4. Check that links are clearly styled differently from surrounding body text
5. Verify navigation links have distinguishable styling
6. Use WebAIM Contrast Checker to confirm link color has 3:1 contrast against surrounding text and background

## Developer Notes

- Add `text-decoration: underline` to all content links:
  ```css
  a:not([class*="nav"]):not([class*="button"]) {
    text-decoration: underline;
  }
  ```
- Navigation links can use other cues: bold, background, border-bottom, or underline
- Ensure link color has 3:1 contrast against surrounding text (not just background)
- Avoid `text-decoration: none` on content links without providing an alternative cue
- Consider `text-underline-offset` for better readability with descenders

## WCAG References

- **[1.4.1 Use of Color (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)**: Color is not used as the only visual means of conveying information, indicating an action, prompting a response, or distinguishing a visual element.
- **[1.4.3 Contrast (Minimum) (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)**: The visual presentation of text and images of text has a contrast ratio of at least 4.5:1 (3:1 for large text; links need 3:1 against surrounding text).

## Priority & Effort

| Attribute | Value |
|-----------|-------|
| **Priority** | P1 Critical |
| **Effort Estimate** | Small (1–2 hours) |
