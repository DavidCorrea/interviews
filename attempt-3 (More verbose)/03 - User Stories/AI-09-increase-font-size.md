# AI-09: Increase Base Font Size to 16px Minimum

## Metadata
- **ID:** AI-09
- **Priority:** 2 High
- **Personas Affected:** 4+ of 16 personas
- **WCAG Criteria:** 1.4.4 Resize Text (AA), 1.4.8 Visual Presentation (AAA)
- **Effort:** Small (1–2 hours)

---

## User Story

**As a** user with low vision, aging eyes, or who prefers larger text for readability,

**I want** all body text and critical UI elements to be at least 16px (1rem),

**So that** I can read content comfortably without straining, and text remains legible when I increase browser font size.

---

## Acceptance Criteria

- [ ] Base font size is 16px (1rem) or larger for body text
- [ ] No body content text computes below 16px (except superscripts, footnotes, or decorative elements)
- [ ] Form labels are at least 14px (0.875rem), preferably 16px (1rem)
- [ ] Captions and helper text are at least 16px
- [ ] Footer text is at least 16px
- [ ] All font sizes use `rem` or `em` units (not `px`) for scalability
- [ ] Site respects user font-size preference when set to "Large" in browser settings

---

## Test Plan

### DevTools Inspection
1. Open `https://launchpadlab.com/` in Chrome
2. Right-click any text element → Inspect
3. In Computed panel, check `font-size` value
4. **Expected:** No body content computes below 16px
5. Repeat for:
   - [ ] Paragraph text
   - [ ] Form labels (name, email, message)
   - [ ] Captions under images
   - [ ] Helper text / placeholders
   - [ ] Footer links and copyright
   - [ ] Navigation links
   - [ ] Button text

### Browser Font-Size Preference
1. In Chrome: Settings → Appearance → Font size → **Large**
2. Reload `https://launchpadlab.com/`
3. **Expected:** Text scales up proportionally; no clipping or overlap
4. Verify body text remains readable and layout holds

### Exceptions (Allowable)
- Superscripts (e.g., footnote markers) may be smaller
- Decorative elements with no meaningful content
- Icons (not text) — no change needed

---

## Developer Notes

### Set Base Font Size
```css
html {
  font-size: 100%; /* Respects user browser preference (typically 16px) */
}

body {
  font-size: 1rem; /* 16px when html is 100% */
}
```

### Audit All font-size Declarations
- Search codebase for `font-size: XXpx` where XX < 16
- Replace with `rem`: `font-size: 1rem` (16px), `font-size: 0.875rem` (14px for labels only if necessary)
- Prefer `1rem` for all body content

### Form Labels
- Minimum: `font-size: 0.875rem` (14px) — WCAG allows this for labels
- Preferred: `font-size: 1rem` (16px) for better readability

### Unit Conversion Reference
| px | rem (at 16px base) |
|----|---------------------|
| 12px | 0.75rem |
| 14px | 0.875rem |
| 16px | 1rem |
| 18px | 1.125rem |
| 20px | 1.25rem |

### Files to Modify
- Global CSS (reset, base styles)
- Typography/utility classes
- Form component styles
- Footer styles
- Any component with small text

---

## Examples

| Site | Approach |
|------|----------|
| **Medium.com** | 18px body text; generous base size |
| **Notion.com** | 16px minimum across interface; readable defaults |
| **Apple.com** | 17px body text; slightly larger for premium feel |
