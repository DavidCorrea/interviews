# L-58: Excessive Line Length on Wide Viewports

**Issue ID:** L-58
**Priority:** Low
**WCAG Criteria:** 1.4.8 Visual Presentation (AAA)
**Affected Personas:** Dyslexic

---

## User Story

As a **user with dyslexia**, I want body text lines to be constrained to a comfortable reading width (no more than ~80 characters per line) so that I can track from the end of one line to the beginning of the next without losing my place.

---

## Acceptance Criteria

- [ ] Body text on all pages does not exceed 80 characters per line (approximately 60–75ch or ~700px) on any viewport width.
- [ ] A `max-width` constraint is applied to text content containers, not the full-width section wrappers.
- [ ] The constraint does not break full-bleed layout sections (heroes, image backgrounds, colored bands) — only the text content within them is constrained.
- [ ] At 1440px, 1920px, and 2560px viewport widths, body paragraphs remain within the character limit.
- [ ] Headings may extend wider than body text but should still have a reasonable `max-width`.
- [ ] The layout remains visually centered and balanced on ultra-wide screens.

---

## How to Test the Change

### Manual Testing
1. Open launchpadlab.com in a browser.
2. Resize the window to **1440px wide** (or use DevTools responsive mode).
3. Select a body paragraph with DevTools and count the characters on the longest line — should not exceed ~80.
4. Resize to **1920px** — repeat the check.
5. Resize to **2560px** (ultra-wide) — repeat the check.
6. Verify that full-bleed sections (colored backgrounds, hero images) still span the full viewport width.
7. Verify that the constrained text is visually centered within each section.
8. Check at least 3 page types: homepage, a services page, and the about page.

### Automated Testing
1. Write a visual regression or DOM test:
   ```javascript
   // Playwright example at 1920px viewport
   await page.setViewportSize({ width: 1920, height: 1080 });
   const paragraphs = await page.$$('main p');
   for (const p of paragraphs) {
     const box = await p.boundingBox();
     // 75ch ≈ 750px at 16px font
     expect(box.width).toBeLessThanOrEqual(800);
   }
   ```
2. Use `ch` units in CSS to make the constraint font-size-relative and inherently correct.

---

## Developer Notes

### General Explanation
On wide viewports (1440px+), body text lines stretch to 90–100+ characters. The optimal line length for readability is 45–75 characters (WCAG AAA recommends no more than 80). This is fixed by adding `max-width` to text content containers.

The key is to constrain the **text container**, not the **section wrapper** — sections can remain full-width for visual design purposes.

### Code Examples

**Global content constraint (recommended):**
```css
/* Apply to the content container, not the section */
.content-wrapper,
.entry-content,
.text-content {
  max-width: 70ch; /* ~70 characters wide */
  margin-inline: auto; /* center the content */
}
```

**Per-section approach (if content wrapper doesn't exist):**
```css
/* Constrain text within full-bleed sections */
section .section-content {
  max-width: 720px;
  margin-left: auto;
  margin-right: auto;
  padding-inline: 1.5rem;
}
```

**Using a utility class:**
```css
.readable-width {
  max-width: 70ch;
  margin-inline: auto;
}
```
```html
<section class="full-bleed bg-blue">
  <div class="readable-width">
    <h2>Our Approach</h2>
    <p>Body text is constrained to a comfortable reading width...</p>
  </div>
</section>
```

**Handling headings differently:**
```css
.content-wrapper h1,
.content-wrapper h2 {
  max-width: 85ch; /* Slightly wider for headings */
}

.content-wrapper p,
.content-wrapper li,
.content-wrapper blockquote {
  max-width: 70ch;
}
```

### Components/Files to Audit
- Global stylesheet — look for `.container`, `.wrapper`, `.content-area` classes
- Section templates — verify each has a constrained inner content wrapper
- WordPress `the_content()` output — ensure it's wrapped in a constrained container
- Blog post templates — single.php, page.php
- Service and About page templates

---

## Examples from Other Sites

- **Medium:** Constrains article body to `680px` max-width (`max-width: 680px; margin: auto;`), which works out to ~65–70 characters per line.
- **Stripe documentation:** Uses `max-width: 46rem` on the content column, resulting in approximately 65–75 characters per line regardless of viewport width.
- **GOV.UK:** Constrains content to a `two-thirds` column width (roughly 66% of the page), achieving optimal reading length on all screens.
- **Wikipedia:** Uses `max-width: 60em` on the content area, preventing text from spanning the full width of ultra-wide screens.

---

## Additional Context

This is a CSS-only fix that requires no JavaScript. The `ch` unit is ideal here because it's relative to the font's `0` character width, making the constraint adapt automatically to different font sizes. If the site already uses a responsive grid system, the fix may be as simple as adding `max-width: 70ch` to the existing content column class.
