# M-35: Body Line-Height Reset to 1

**Issue ID:** M-35
**Priority:** Medium
**WCAG Criteria:** 1.4.12 Text Spacing (AA)
**Affected Personas:** Dyslexic

---

## User Story

As a **user with dyslexia**, I want **body text to have proper default line spacing** so that **lines of text don't appear cramped and I can track from the end of one line to the beginning of the next without losing my place.**

---

## Acceptance Criteria

- [ ] The `body` element's `line-height` is set to at least **1.5** (WCAG 1.4.12 recommended value for body text).
- [ ] No descendant text elements inherit a `line-height` of `1` from the body unless explicitly overridden to a compliant value.
- [ ] All paragraph text, list items, and inline text across the site render with visible inter-line spacing.
- [ ] Form labels, button text, and navigation items maintain a readable `line-height` (minimum 1.2).
- [ ] No layout breakage occurs on any page after the `line-height` increase.

---

## How to Test the Change

### Manual Testing

1. Open Chrome DevTools on the homepage.
2. Select the `<body>` element and verify the computed `line-height` is `1.5` or greater.
3. Spot-check 5–10 text elements across different pages (paragraphs, list items, captions, footer text) to confirm none inherit a `line-height` of `1`.
4. Apply the WCAG 1.4.12 [Text Spacing Bookmarklet](https://www.html5accessibility.com/tests/tsbookmarklet.html) — confirm no text is clipped or overlapping.
5. Check responsive views at 375px, 768px, and 1440px for layout integrity.

### Automated Testing

1. Write a simple CSS audit script to scan for `line-height: 1` declarations:
   ```bash
   grep -rn "line-height:\s*1[^.]" path/to/css/
   ```
2. Run axe DevTools on each page template — review any contrast or spacing warnings.
3. Use BackstopJS or Percy to capture visual regression snapshots before and after the change.

---

## Developer Notes

### General Explanation

The root CSS rule `body { line-height: 1 }` strips all default inter-line spacing. While individual components may override this value, any element that does not receive a more specific `line-height` declaration will inherit the cramped `1` value. The fix is to set the body `line-height` to `1.5` (or at minimum `1.4`) to provide a readable default across the entire site.

### Code Examples

**Before (current):**
```css
body {
  line-height: 1;
}
```

**After (fixed):**
```css
body {
  line-height: 1.5;
}
```

**If the `line-height: 1` reset is part of a CSS reset/normalize, override it in the theme stylesheet:**
```css
/* Override reset */
body {
  line-height: 1.5;
  /* Alternatively, a unitless value like 1.6 gives slightly more breathing room */
}
```

**Ensure components that need tighter spacing opt in explicitly:**
```css
.nav-link,
.btn {
  line-height: 1.2; /* Tighter is acceptable for single-line UI elements */
}
```

### Components / Files to Audit

- CSS reset file (e.g., `reset.css`, `normalize.css`, or WordPress theme reset)
- Global stylesheet `body` declaration
- Any component that may have relied on `line-height: 1` for vertical alignment (buttons, navigation, badges)
- Check for `line-height` overrides in WordPress Customizer or theme options

---

## Examples from Other Sites

- **MDN Web Docs (Mozilla):** Uses `body { line-height: 1.5 }` as the global default, matching WCAG guidance.
- **GitHub.com:** Sets `body { line-height: 1.5 }` in their Primer CSS framework.
- **Tailwind CSS Default:** The framework's base layer applies `line-height: 1.5` to the body element.
- **W3C Web Accessibility Initiative:** Recommends a minimum `line-height` of 1.5 for body text in their "Understanding WCAG 1.4.12" documentation.
