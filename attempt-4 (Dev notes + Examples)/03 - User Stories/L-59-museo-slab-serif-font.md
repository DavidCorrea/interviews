# L-59: Museo Slab Serif Font

**Issue ID:** L-59
**Priority:** Low
**WCAG Criteria:** 1.4.8 Visual Presentation (AAA)
**Affected Personas:** Dyslexic

---

## User Story

As a **user with dyslexia**, I want the site to use a clean sans-serif font for body text so that I can read content without the added visual noise of thin serif strokes that blur together and slow my reading.

---

## Acceptance Criteria

- [ ] Body text uses a sans-serif font as the primary typeface (e.g., Inter, Source Sans Pro, Open Sans, or system sans-serif stack).
- [ ] The serif font (Museo Slab) is either removed entirely or limited to decorative/display usage in large headings only.
- [ ] Body text at all sizes (13px–18px) remains legible with clear letterform differentiation.
- [ ] The replacement font maintains equivalent or better character spacing and x-height for readability.
- [ ] The font change does not break existing layout, line lengths, or text wrapping across pages.
- [ ] The font loads performantly — either via system stack or with `font-display: swap` for web fonts.
- [ ] Users with dyslexia-specific browser extensions (e.g., OpenDyslexic, Dyslexie) can still override the font without visual breakage.

---

## How to Test the Change

### Manual Testing
1. Navigate to launchpadlab.com.
2. Inspect any body `<p>` element in DevTools.
3. Verify the `font-family` computed value is a sans-serif typeface (not Museo Slab or any serif font).
4. Check the following pages for consistent sans-serif body text:
   - Homepage
   - Any Services sub-page
   - About page
   - Contact page
   - A blog post
5. Read a full paragraph at default zoom (100%) and at 200% zoom — confirm the text feels clean, open, and easy to track line-by-line.
6. Test with the OpenDyslexic browser extension enabled — confirm the override applies without layout breakage.

### Automated Testing
1. Write a computed style assertion:
   ```javascript
   // Playwright example
   const bodyFont = await page.evaluate(() => {
     const p = document.querySelector('main p');
     return getComputedStyle(p).fontFamily;
   });
   expect(bodyFont).not.toContain('Museo');
   expect(bodyFont).not.toContain('serif');
   // Note: "sans-serif" contains "serif" — check more precisely:
   expect(bodyFont).toMatch(/sans-serif|Inter|Source Sans|Open Sans|Helvetica|Arial/);
   ```
2. Run a Lighthouse performance audit to confirm font loading does not regress (check for render-blocking font requests).

---

## Developer Notes

### General Explanation
Museo Slab is a slab-serif font with thin connecting strokes that reduce letterform clarity at small sizes. Research on dyslexia-friendly typography consistently recommends sans-serif typefaces with distinct letterforms, generous x-heights, and consistent stroke widths. The site should switch its body text to a sans-serif font while optionally retaining Museo Slab for large display headings where legibility is less of a concern.

### Code Examples

**Current state:**
```css
body {
  font-family: 'Museo Slab', Georgia, serif;
}
```

**Recommended fix (Option A — system sans-serif stack):**
```css
body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto,
               Oxygen-Sans, Ubuntu, Cantarell, 'Helvetica Neue', sans-serif;
}
```

**Recommended fix (Option B — web font):**
```css
body {
  font-family: 'Inter', 'Helvetica Neue', Arial, sans-serif;
}
```

**Keep Museo Slab for large headings only (optional):**
```css
h1, .display-heading {
  font-family: 'Museo Slab', Georgia, serif;
}

body, p, li, td, label, input, textarea {
  font-family: 'Inter', 'Helvetica Neue', Arial, sans-serif;
}
```

**Font loading optimization:**
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
```

### Components/Files to Audit
- Global stylesheet — find all `font-family` declarations referencing `Museo Slab`
- `functions.php` or `<head>` template — locate where Museo Slab is enqueued/loaded
- WordPress theme Customizer settings (if font is set via admin UI)
- Any inline `style` attributes using the serif font
- Blog post templates — ensure content inherits the new sans-serif font

---

## Examples from Other Sites

- **Medium:** Uses a system sans-serif stack for body text (`-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, ...`), reserving their serif charter font for article titles only.
- **GOV.UK:** Uses the GDS Transport sans-serif typeface across all body text, specifically chosen for accessibility and dyslexia-friendliness.
- **Airbnb (Cereal):** Their custom sans-serif font was designed with accessibility in mind — consistent stroke widths, open counters, and high x-height.
- **British Dyslexia Association:** Explicitly recommends sans-serif fonts such as Arial, Verdana, or Calibri for body text, and advises against serif fonts at small sizes.

---

## Additional Context

This change has both accessibility and performance implications. Removing Museo Slab as a web font eliminates a render-blocking font request, potentially improving page load time. If the team has strong brand attachment to Museo Slab, a compromise is to keep it for `<h1>` and display-size elements where the thin strokes are less problematic, while switching all body-size text to sans-serif.
