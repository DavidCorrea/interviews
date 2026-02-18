# L-64: Small Font Size Preset (13px)

**Issue ID:** L-64
**Priority:** Low
**WCAG Criteria:** 1.4.4 Resize Text (AA)
**Affected Personas:** Senior Person

---

## User Story

As a **senior user** with age-related vision changes, I want all body text to be set at a minimum of 16px so that I can read the site content comfortably without needing to zoom in or strain my eyes.

---

## Acceptance Criteria

- [ ] No body text element on the site renders below 16px (1rem) at default zoom (100%).
- [ ] All text currently set at 13px is increased to at least 16px.
- [ ] The font size increase does not break any layout, cause text overflow, or introduce horizontal scrolling.
- [ ] Small/fine-print text (legal disclaimers, copyright notices) is set to at minimum 14px, and ideally 16px.
- [ ] The base `font-size` on the `<html>` or `<body>` element is 16px (the browser default).
- [ ] Relative units (`rem`, `em`) are used instead of `px` for font sizes where possible, so that user browser zoom preferences scale correctly.
- [ ] The fix applies site-wide across all page templates.

---

## How to Test the Change

### Manual Testing
1. Navigate to launchpadlab.com.
2. Open DevTools and inspect body text elements (`<p>`, `<li>`, `<span>`, `<label>`, etc.).
3. Check the **computed** `font-size` for each — confirm none are below 16px.
4. Pay special attention to:
   - Footer text
   - Form field labels and placeholder text
   - Card description text
   - Blog post metadata (date, author, category)
   - Navigation sub-menu descriptions
5. Test on mobile viewport (375px) — confirm text remains at or above 16px.
6. Test at 200% zoom — confirm text scales properly and layout reflows.

### Automated Testing
1. Scan all text elements for minimum font size:
   ```javascript
   // Playwright example
   const textElements = await page.$$('p, li, span, label, td, th, figcaption, small, .text');
   for (const el of textElements) {
     const fontSize = await el.evaluate(e => parseFloat(getComputedStyle(e).fontSize));
     if (await el.isVisible()) {
       expect(fontSize).toBeGreaterThanOrEqual(16);
     }
   }
   ```
2. Run a CSS audit to find all `font-size` declarations below 16px:
   ```bash
   # Search for small font-size declarations in stylesheets
   grep -rn "font-size.*1[0-5]px" wp-content/themes/*/style.css
   grep -rn "font-size.*0\.[0-8].*rem" wp-content/themes/*/style.css
   ```

---

## Developer Notes

### General Explanation
Some body text on the site is set at 13px — well below the widely recommended 16px minimum for comfortable screen reading. At 13px, letterforms are noticeably smaller and harder to distinguish, especially for users over 40 with presbyopia (age-related farsightedness). The fix is to increase all sub-16px text to 16px and use relative units so the text scales properly with user preferences.

### Code Examples

**Find and fix small font sizes:**
```css
/* BEFORE: various small text sizes */
.card-description { font-size: 13px; }
.meta-text { font-size: 12px; }
.footer-fine-print { font-size: 11px; }

/* AFTER: minimum 16px (1rem) for body text */
.card-description { font-size: 1rem; }     /* 16px */
.meta-text { font-size: 1rem; }            /* 16px */
.footer-fine-print { font-size: 0.875rem; } /* 14px — acceptable for fine print */
```

**Set a proper base font size:**
```css
/* Ensure the root font size is 16px (browser default) */
html {
  font-size: 100%; /* = 16px in all browsers */
}

body {
  font-size: 1rem; /* Inherits 16px from html */
  line-height: 1.5;
}
```

**Convert px to rem for scalability:**
```css
/* 13px → 1rem (16px) */
/* 14px → 0.875rem (14px) — only for truly secondary text */
/* 16px → 1rem */
/* 18px → 1.125rem */

/* Use a function or mixin if using a preprocessor */
/* Sass example: */
@function rem($px) {
  @return calc($px / 16) * 1rem;
}

.body-text { font-size: rem(16); }
```

### Components/Files to Audit
- Global stylesheet — search for all `font-size` declarations with values below 16px
- Typography utilities or variables file
- Card component styles
- Footer styles
- Blog post/article styles
- Form styles (labels, inputs, helpers)
- Navigation sub-menu styles (mega menu descriptions)
- WordPress editor styles (ensure the editor reflects the actual font sizes)

---

## Examples from Other Sites

- **Apple:** All body text across apple.com is set at 17px minimum, with generous line-height. Even fine print and legal text is at 14px.
- **GOV.UK:** Uses 19px as the default body text size, based on research showing improved readability for older users and those with visual impairments.
- **Medium:** Article body text is set at 21px with 1.58 line-height — prioritizing readability above all else.
- **WCAG guidance:** While WCAG 1.4.4 requires text to be resizable to 200% without loss of content, the [Web Content Accessibility Guidelines](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html) note that starting from a reasonable base size (16px+) ensures the 200% zoom result is still usable.

---

## Additional Context

The 16px minimum is not an accessibility standard per se, but it is an industry best practice backed by extensive readability research. The browser default of 16px exists for a reason — it was chosen as the minimum comfortable reading size for average screen distances. Going below it puts the site at a readability disadvantage, particularly for the senior demographic that LaunchPad Lab may be trying to reach as enterprise decision-makers.
