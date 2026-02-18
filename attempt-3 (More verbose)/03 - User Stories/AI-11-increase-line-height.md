# AI-11: Increase Line Height to 1.5+

## Metadata
- **ID:** AI-11
- **Priority:** 2 High
- **Personas Affected:** 4+ of 16 personas
- **WCAG Criteria:** 1.4.8 Visual Presentation (AAA)
- **Effort:** Small (1 hour)

---

## User Story

**As a** user with dyslexia, low vision, or who loses their place when lines are crowded,

**I want** body text to have a line height of at least 1.5 (150%),

**So that** lines are clearly separated, I can track across text easily, and reading feels comfortable rather than cramped.

---

## Acceptance Criteria

- [ ] Body text has `line-height: 1.5` or higher (1.6 recommended)
- [ ] Paragraph spacing is at least 1.5× line height
- [ ] No `overflow: hidden` containers clip text when line-height increases
- [ ] Text passes WCAG 1.4.12 Text Spacing test (no clipping/overlap when user applies spacing overrides)
- [ ] Headings may use 1.2–1.3 (tighter is acceptable for short headings)

---

## Test Plan

### DevTools Inspection
1. Open `https://launchpadlab.com/` in Chrome
2. Right-click body paragraph → Inspect
3. In Computed panel, check `line-height` value
4. **Expected:** 1.5 or higher (e.g., 1.5, 1.6, 24px for 16px font)
5. Repeat for all paragraph blocks, list items, and body content

### Visual Check
- Text should feel "airy" — adequate space between lines
- No cramped "wall of text" appearance
- Paragraphs should have clear separation (margin or padding)

### WCAG Text Spacing Bookmarklet
1. Install the [WCAG Text Spacing bookmarklet](https://www.w3.org/WAI/WCAG21/Understanding/text-spacing.html) or manually apply:
   - `line-height: 1.5`
   - `paragraph-spacing: 2em`
   - `letter-spacing: 0.12em`
   - `word-spacing: 0.16em`
2. Apply to page
3. **Expected:** No content clipped, cut off, or overlapping
4. All text remains readable and functional
5. Buttons/links still fully visible

### Overflow Check
- Inspect any container with `overflow: hidden` or `overflow: auto`
- Ensure increased line-height doesn't cause text to be clipped
- Adjust or remove overflow if necessary

---

## Developer Notes

### Set Line Height
```css
body {
  line-height: 1.5; /* or 1.6 for better readability */
}

p {
  margin-bottom: 1.5em; /* Paragraph spacing ~1.5× line height */
}

/* Headings can be tighter */
h1, h2, h3, h4, h5, h6 {
  line-height: 1.2; /* or 1.3 */
}
```

### Avoid Clipping
- Remove or adjust `overflow: hidden` on text containers
- Use `overflow: visible` where possible
- If overflow is needed (e.g., dropdown), ensure content area has enough height

### WCAG 1.4.12 Text Spacing
- Users may override spacing via browser or extension
- Ensure layout accommodates: line-height 1.5, paragraph spacing 2em, letter-spacing 0.12em, word-spacing 0.16em
- No loss of content or functionality when these are applied

### Unit Notes
- `line-height: 1.5` is unitless — multiplies with font-size (e.g., 16px × 1.5 = 24px)
- Prefer unitless values for line-height (better for inheritance)

### Files to Modify
- Global typography CSS
- Body and paragraph styles
- Card/content containers that may clip text

---

## Examples

| Site | Approach |
|------|----------|
| **GOV.UK** | line-height: 1.625; generous spacing; highly readable |
| **Medium.com** | Generous line spacing; comfortable reading experience |
| **Notion.com** | Adequate line height; clean, scannable blocks |
