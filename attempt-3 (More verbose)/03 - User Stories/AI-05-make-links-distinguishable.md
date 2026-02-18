# AI-05: Make Links Visually Distinguishable from Body Text

## Metadata
- **ID:** AI-05
- **Priority:** 1 Critical
- **Personas Affected:** 8+ of 16 personas (color blindness, low vision, cognitive)
- **WCAG Criteria:** 1.4.1 Use of Color (A), 1.4.3 Contrast (Minimum) (AA)
- **Effort:** Small (1–2 hours)

---

## User Story

**As a** visitor who is color blind, has low vision, or scans pages quickly,

**I want** all inline text links to be visually distinguishable from body text using more than color alone,

**So that** I can identify and activate links without relying solely on color perception.

---

## Acceptance Criteria

- [ ] All inline text links have an underline (or equivalent non-color cue)
- [ ] Link color is darker and more distinct (e.g., #0055AA or darker on white)
- [ ] Links achieve at least 4.5:1 contrast against background
- [ ] Hover and focus states include a non-color cue (e.g., underline remains or thickens)
- [ ] Navigation menu items and button-styled links may be exempt (they are clearly interactive by shape/placement)
- [ ] Visited link color meets contrast requirements and remains distinguishable
- [ ] Links are identifiable when using color vision simulation (e.g., protanopia, deuteranopia)

---

## Test Plan

### Visual Inspection
1. Visit every page: Home, About, Services, Contact, Blog
2. Identify all inline text links (links within paragraphs, lists, or body content)
3. **Expected:** Each has an underline (or bold + underline, or icon)
4. **Expected:** Link color is noticeably different and darker than body text (#333)

### Color Vision Simulation
1. Install Colorblindly extension or use Chrome DevTools
2. Enable simulation: Protanopia, Deuteranopia, or Tritanopia
3. Navigate site — **Expected:** Links still identifiable via underline or other cue
4. Verify no link is distinguishable only by color

### Hover/Focus States
1. Hover over each link type — **Expected:** Underline persists or becomes more prominent
2. Tab to each link — **Expected:** Focus indicator visible (see AI-06) and underline present
3. Check visited links — **Expected:** Still distinguishable (e.g., different underline style or color that meets contrast)

### Exemptions
- Nav menu links (clearly in a nav bar) — document if exempt
- Button-styled links (e.g., "Contact Us" CTA) — ensure they look like buttons (shape, padding, border)
- Icon-only links — ensure they have accessible names and focus indicators

---

## Developer Notes

### CSS for Inline Links
```css
a {
  color: #0055AA;
  text-decoration: underline;
  text-underline-offset: 2px;
}

a:hover,
a:focus {
  text-decoration: underline;
  color: #003d7a; /* darker on hover */
}

a:visited {
  color: #551a8b; /* ensure contrast; test against background */
  text-decoration: underline;
}
```

### Exemptions
For navigation and button-styled links:

```css
nav a,
.btn,
a[role="button"],
.button-style-link {
  text-decoration: none; /* OK if clearly a button/nav by context */
}
```

Ensure these still have focus indicators and are clearly interactive.

### Contrast
- #0055AA on #FFFFFF ≈ 5.1:1 (passes AA for normal text)
- #003d7a on #FFFFFF ≈ 7.5:1 (passes AAA)
- Test visited color: #551a8b on white ≈ 5.9:1

### Do Not
- Use `text-decoration: none` for inline body links without another non-color cue
- Rely on color change alone for hover/focus
- Use very light or low-contrast link colors

### Files to Modify
- Global CSS (link styles)
- Component styles that override default link styling
- Design system or Tailwind config if links are styled via utilities

---

## Examples

| Site | Approach |
|------|----------|
| **Wikipedia** | All links underlined; blue for unvisited, purple for visited |
| **GOV.UK** | Underlined links; dark blue; high contrast |
| **W3C.org** | Underlined links; clear distinction from body text |
| **MDN Web Docs** | Underlined links; blue; accessible across color vision types |
