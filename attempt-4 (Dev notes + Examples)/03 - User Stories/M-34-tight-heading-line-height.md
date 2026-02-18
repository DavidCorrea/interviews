# M-34: Tight Line-Height on Headings (1.1)

**Issue ID:** M-34
**Priority:** Medium
**WCAG Criteria:** 1.4.12 Text Spacing (AA), 1.4.8 Visual Presentation (AAA)
**Affected Personas:** Dyslexic

---

## User Story

As a **user with dyslexia**, I want **multi-line headings to have adequate line spacing** so that **I can distinguish between lines of text without them appearing to merge together, reducing my reading errors and fatigue.**

---

## Acceptance Criteria

- [ ] All `<h1>`, `<h2>`, and `<h3>` elements have a `line-height` of at least **1.5** (per WCAG 1.4.12 recommendation for text spacing).
- [ ] At a minimum, heading `line-height` must not be lower than **1.2** (absolute floor for readability).
- [ ] Multi-line headings on all pages (Homepage, Services, About, Contact, Case Studies, Blog) render with visible space between lines.
- [ ] The updated line-height does not break any existing layouts (hero sections, card headings, sidebar headings).
- [ ] When a user applies WCAG 1.4.12 text spacing overrides (line-height 1.5x, letter spacing 0.12em, word spacing 0.16em, paragraph spacing 2x), no content is clipped or lost.

---

## How to Test the Change

### Manual Testing

1. Open every page type (Homepage, Services, About, Contact, Case Studies, Blog post) in Chrome.
2. Inspect each `<h1>`, `<h2>`, and `<h3>` element using DevTools.
3. Verify the computed `line-height` is at least 1.5 (or the agreed-upon minimum).
4. Visually confirm multi-line headings have clear space between lines.
5. Resize the browser to mobile (375px), tablet (768px), and desktop (1440px) widths — verify headings remain properly spaced at all breakpoints.
6. Use the [Text Spacing Bookmarklet](https://www.html5accessibility.com/tests/tsbookmarklet.html) to apply WCAG 1.4.12 overrides. Verify no heading text is clipped or overlaps.

### Automated Testing

1. Run axe DevTools or Lighthouse accessibility audit — check for any text-spacing related flags.
2. Add a CSS linting rule (e.g., Stylelint) to flag `line-height` values below 1.2 on heading selectors:
   ```json
   {
     "declaration-property-value-disallowed-list": {
       "line-height": ["/^(0|1(\\.0|\\.[01])?)$/"]
     }
   }
   ```
3. Create a visual regression test (Percy, Chromatic, or BackstopJS) snapshot for heading-heavy pages before and after the change.

---

## Developer Notes

### General Explanation

The current CSS applies a `line-height` of approximately `1.1` to headings, which is too tight for comfortable reading — especially for users with dyslexia, where crowded lines cause letter confusion and line-skipping. The fix is to increase `line-height` to at least `1.5` for body text and `1.2–1.5` for headings in the global stylesheet.

### Code Examples

**Before (current):**
```css
h1, h2, h3 {
  line-height: 1.1;
}
```

**After (fixed):**
```css
h1, h2, h3 {
  line-height: 1.4;
}

/* If tighter spacing is needed for hero headlines, use a minimum of 1.2 */
.hero h1 {
  line-height: 1.2;
}
```

**Alternative — use relative units for flexibility:**
```css
h1 { line-height: 1.3; }
h2 { line-height: 1.35; }
h3 { line-height: 1.4; }
```

### Components / Files to Audit

- Global stylesheet (e.g., `style.css`, `_typography.scss`, or theme CSS)
- Any heading-specific component styles (hero sections, card titles, page headers)
- WordPress theme `functions.php` or Customizer settings if line-height is set dynamically
- Check for inline styles on heading elements in page templates

---

## Examples from Other Sites

- **GOV.UK Design System:** Uses `line-height: 1.25` for large headings (`xl`) and `1.3125` for smaller headings, ensuring readability without excessive vertical space. ([Design System — Typography](https://design-system.service.gov.uk/styles/typography/))
- **Apple.com:** Hero headings use `line-height: 1.05` for single-line display text but increase to `1.2–1.3` for multi-line editorial headings.
- **Stripe.com:** All headings use a minimum `line-height` of `1.2`, with body headings at `1.3`.
- **Material Design (Google):** Recommends headline line-heights between `1.2` and `1.25` to balance density with readability.
