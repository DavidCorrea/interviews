# M-36: Decorative Font (Permanent Marker) Loaded

**Issue ID:** M-36
**Priority:** Medium
**WCAG Criteria:** 1.4.8 Visual Presentation (AAA)
**Affected Personas:** Dyslexic

---

## User Story

As a **user with dyslexia**, I want **all text on the site to use a legible, consistent typeface** so that **I don't encounter irregular letter shapes and spacing that cause me to misread words or lose my place.**

---

## Acceptance Criteria

- [ ] The "Permanent Marker" Google Font is no longer applied to any visible text elements on the site.
- [ ] Any text previously styled with `font-family: 'Permanent Marker'` is replaced with the site's primary sans-serif font (or a legible alternative).
- [ ] The visual design intent of decorative elements is preserved through other means (color, size, weight, or layout) rather than an illegible typeface.
- [ ] The Google Fonts `<link>` or `@import` for Permanent Marker is removed from the `<head>` to eliminate the unnecessary font download (~20KB).
- [ ] No regressions in layout or visual hierarchy after the font swap.

---

## How to Test the Change

### Manual Testing

1. Open Chrome DevTools and search the DOM for any element with `font-family` containing "Permanent Marker."
2. Verify none exist.
3. Check the Network tab — confirm no request is made to `fonts.googleapis.com` for "Permanent+Marker."
4. Visually inspect pages where the decorative font was previously used (likely homepage hero accents, section labels, or decorative quotes).
5. Confirm replacement text is styled with a legible font and maintains visual hierarchy.

### Automated Testing

1. Search the codebase for references:
   ```bash
   grep -rni "permanent.marker" path/to/theme/
   ```
2. Run a Lighthouse performance audit — confirm the font is no longer loaded (reduces render-blocking resources).
3. Add a CSS linting rule to disallow known decorative fonts:
   ```json
   {
     "font-family-no-disallowed-list": [["Permanent Marker", "Comic Sans MS", "Papyrus"]]
   }
   ```

---

## Developer Notes

### General Explanation

"Permanent Marker" is a handwriting-style font with irregular letter shapes, inconsistent spacing, and low x-height — making it particularly difficult for users with dyslexia. While it may serve a branding purpose (casual, creative feel), the same effect can be achieved with font weight, size, color, or a more legible display font. The fix involves removing the font entirely and restyling affected elements.

### Code Examples

**Remove the Google Fonts import:**
```html
<!-- REMOVE this line from <head> -->
<link href="https://fonts.googleapis.com/css2?family=Permanent+Marker&display=swap" rel="stylesheet">
```

**Or remove from CSS @import:**
```css
/* REMOVE */
@import url('https://fonts.googleapis.com/css2?family=Permanent+Marker&display=swap');
```

**Update affected elements:**
```css
/* Before */
.decorative-label {
  font-family: 'Permanent Marker', cursive;
  font-size: 1.2rem;
}

/* After — use the site's primary font with distinctive styling */
.decorative-label {
  font-family: 'Museo Slab', Georgia, serif;
  font-size: 1.2rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}
```

**In WordPress, check `functions.php` for font enqueue:**
```php
// Find and remove or comment out:
wp_enqueue_style('permanent-marker', 'https://fonts.googleapis.com/css2?family=Permanent+Marker&display=swap');
```

### Components / Files to Audit

- `functions.php` — Google Fonts enqueue
- `<head>` section in `header.php` — direct `<link>` tags
- Global CSS — `@import` statements and `font-family` declarations
- Any inline styles in page templates or Elementor/Gutenberg blocks
- Check WordPress Customizer > Typography settings

---

## Examples from Other Sites

- **Mailchimp:** Uses a single sans-serif system font stack for all text, including decorative elements. Visual personality is achieved through illustration and color, not typeface variation.
- **Slack.com:** Employs one font family (Larsseit/system sans-serif) across the entire site. Decorative emphasis comes from weight, size, and color — never from a novelty font.
- **GOV.UK:** Strictly uses GDS Transport for all text, with design guidelines explicitly prohibiting decorative or display fonts for accessibility reasons.
- **Airbnb (Cereal):** Uses one custom font across the site with different weights for hierarchy. Decorative elements rely on photography and layout, not font variation.
