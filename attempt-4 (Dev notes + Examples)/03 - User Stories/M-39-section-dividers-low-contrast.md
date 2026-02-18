# M-39: Section Dividers/Separators Below 3:1

**Issue ID:** M-39
**Priority:** Medium
**WCAG Criteria:** 1.4.11 Non-text Contrast (AA)
**Affected Personas:** Low Contrast Sensitivity, Situational Contrast

---

## User Story

As a **user with low contrast sensitivity or viewing the site in bright conditions**, I want **section dividers and separators to be clearly visible** so that **I can perceive the visual structure of the page and understand where one section ends and another begins.**

---

## Acceptance Criteria

- [ ] All `<hr>` elements, section `border-bottom/top`, and decorative dividers achieve a contrast ratio of at least **3:1** against their adjacent backgrounds.
- [ ] Current divider colors in the 1.56:1–1.84:1 range are replaced with colors that meet the 3:1 threshold.
- [ ] The visual weight of dividers remains appropriate — they should separate sections without being visually heavy or distracting.
- [ ] Dividers are consistently styled across all pages.
- [ ] The fix is verified on both white and off-white/gray section backgrounds.

---

## How to Test the Change

### Manual Testing

1. Open the homepage and scroll through all sections.
2. For each visible divider or separator line, use the browser eyedropper tool to sample the divider color and the adjacent background color.
3. Enter both values into the [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) and confirm at least 3:1.
4. Repeat on Services, About, Contact, and Blog pages.
5. Emulate reduced contrast via DevTools (Rendering > Emulate vision deficiency) and confirm dividers remain visible.
6. View the site on a phone screen in direct sunlight (or simulate by reducing monitor brightness to minimum).

### Automated Testing

1. Use a CSS audit to find all border/`<hr>` color declarations:
   ```bash
   grep -rn "border.*#\|hr.*color\|border-color" path/to/css/
   ```
2. Run axe DevTools across all page templates and filter for 1.4.11 violations.

---

## Developer Notes

### General Explanation

Section dividers and `<hr>` elements use border colors (`#CFCFCF`, `#D5D5D5`, etc.) that only reach 1.56:1–1.84:1 contrast against white backgrounds. Since these visual separators convey meaningful page structure (the boundary between sections), they are considered non-text UI elements and must meet the 3:1 minimum per WCAG 1.4.11.

### Code Examples

**Before (current):**
```css
hr {
  border: none;
  border-top: 1px solid #CFCFCF; /* ~1.56:1 on white — FAIL */
}

.section {
  border-bottom: 1px solid #D5D5D5; /* ~1.84:1 on white — FAIL */
}
```

**After (fixed):**
```css
hr {
  border: none;
  border-top: 1px solid #949494; /* 3.03:1 on white — PASS */
}

.section {
  border-bottom: 1px solid #949494; /* 3.03:1 on white — PASS */
}
```

**Alternative — use a thicker, lighter border for a softer look:**
```css
hr {
  border: none;
  border-top: 2px solid #AAAAAA; /* 2.32:1 per pixel, but 2px creates stronger visual cue */
  /* Note: WCAG still requires 3:1 per the spec, so prefer: */
  border-top: 1px solid #767676; /* 4.54:1 — comfortable margin */
}
```

**On non-white section backgrounds, adjust accordingly:**
```css
.gray-section hr {
  border-top: 1px solid #6B6B6B; /* 3:1+ on #F5F5F5 background */
}
```

### Components / Files to Audit

- Global `<hr>` styles
- Section-level `border-bottom` and `border-top` rules
- Any decorative line/divider components (Elementor dividers, Gutenberg separator blocks)
- Footer section borders
- Between-card or between-row divider styles

---

## Examples from Other Sites

- **Apple.com:** Uses `border-bottom: 1px solid #424245` on dark sections (high contrast) and `1px solid #86868b` on light sections (~3.5:1).
- **GOV.UK:** Section borders use `#b1b4b6` on white (#FFFFFF), achieving approximately 3.1:1. The design system documents this as the minimum acceptable border color.
- **Notion.so:** Uses `border-bottom: 1px solid rgba(55, 53, 47, 0.16)` which renders approximately as `#D3D1CB` on white — close to 3:1. They supplement with generous padding to reinforce section breaks.
- **Medium.com:** Avoids thin border dividers entirely, using whitespace (48px+ padding) to separate sections, which is an alternative approach.
