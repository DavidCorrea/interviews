# AI-10: Increase Font Weight to 500+ for Body Text

## Metadata
- **ID:** AI-10
- **Priority:** 2 High
- **Personas Affected:** 5+ of 16 personas
- **WCAG Criteria:** 1.4.8 Visual Presentation (AAA)
- **Effort:** Small (1 hour)

---

## User Story

**As a** user with low vision, dyslexia, or who finds thin fonts hard to read,

**I want** body text to use a medium font weight (500 or higher),

**So that** characters are clearly distinguishable and I can read content without eye strain or losing my place.

---

## Acceptance Criteria

- [ ] Body text uses `font-weight: 500` (medium) or higher
- [ ] No body content uses font-weight 300 (light) or 400 (regular) as primary
- [ ] Headings use font-weight 600–700 (semibold/bold)
- [ ] The chosen font includes a 500 weight variant (no browser synthesis)
- [ ] Text remains readable on Windows (ClearType), macOS, and mobile

---

## Test Plan

### DevTools Inspection
1. Open `https://launchpadlab.com/` in Chrome
2. Right-click body paragraph text → Inspect
3. In Computed panel, check `font-weight` value
4. **Expected:** 500 or higher for body text
5. Check headings: **Expected:** 600 or 700
6. Repeat across different sections (hero, services, about, footer)

### Visual Comparison
1. Capture screenshot of current body text
2. Apply `font-weight: 500` via DevTools override
3. Compare legibility — characters should be more distinct, less "washed out"
4. Verify the font renders well (no pixelation or blur from synthesis)

### Cross-Platform Check
- **Windows:** Test with ClearType rendering; ensure 500 weight renders cleanly
- **macOS:** Verify font appears crisp
- **Mobile:** Check readability on iOS and Android at default zoom

### Font File Verification
- Inspect Network tab: ensure `@font-face` includes `font-weight: 500` variant
- If font only has 400 and 700, browser will synthesize 500 (often poor quality) — consider loading 500 from font provider

---

## Developer Notes

### Update Body Font Weight
```css
body {
  font-weight: 500;
}

h1, h2, h3, h4, h5, h6 {
  font-weight: 600; /* or 700 for stronger hierarchy */
}
```

### Critical: Font File Support
- Check that the web font (e.g., Inter, Open Sans, Roboto) includes weight 500
- In `@font-face`, ensure you load the 500 variant:
```css
@font-face {
  font-family: 'YourFont';
  src: url('yourfont-medium.woff2') format('woff2');
  font-weight: 500;
  font-style: normal;
}
```
- If font doesn't support 500, browser will synthesize — often results in blurry or inconsistent rendering
- Use Google Fonts or similar: select "Medium (500)" when adding the font

### Avoid
- `font-weight: 300` (light) for body — too thin for many users
- `font-weight: 400` (regular) as default — 500 improves readability for low vision and dyslexia

### Files to Modify
- Global typography CSS
- Body/base styles
- Any component that overrides font-weight to 300 or 400

---

## Examples

| Site | Approach |
|------|----------|
| **Linear.app** | Medium weight body text; clean, readable |
| **Vercel.com** | 500 weight for body; modern, accessible |
| **Stripe.com** | Readable body weight; avoids thin fonts |
