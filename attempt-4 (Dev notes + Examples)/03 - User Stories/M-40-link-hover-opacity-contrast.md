# M-40: Link Hover State Reduces Contrast via Opacity

**Issue ID:** M-40
**Priority:** Medium
**WCAG Criteria:** 1.4.3 Contrast (Minimum) (AA)
**Affected Personas:** Low Contrast Sensitivity

---

## User Story

As a **user with low contrast sensitivity**, I want **link text to remain readable in all interactive states** so that **I can still read the link text when I hover over it, rather than watching it fade into the background.**

---

## Acceptance Criteria

- [ ] The `a:hover` state no longer uses `opacity` to change the visual appearance of links.
- [ ] Link text in its hover state maintains a contrast ratio of at least **4.5:1** against its background (for normal-sized text).
- [ ] The hover state provides a clear visual change that does not rely on reducing contrast (e.g., underline addition/removal, color shift to a compliant color, background highlight).
- [ ] All link types (inline text links, navigation links, footer links, CTA links) have hover states that meet contrast requirements.
- [ ] The `opacity` approach is not applied to any other text-containing interactive elements (buttons, cards).

---

## How to Test the Change

### Manual Testing

1. Open any page and hover over inline text links.
2. While hovering, use the DevTools color picker or eyedropper to sample the effective text color.
3. Compare against the background color using the [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/).
4. Confirm the contrast ratio is at least **4.5:1** during the hover state.
5. Also test links in the navigation, footer, and any colored sections.
6. Use keyboard navigation (Tab) — verify `:focus-visible` states also maintain contrast.

### Automated Testing

1. Search the CSS for opacity on hover:
   ```bash
   grep -rn "hover.*opacity\|opacity.*hover" path/to/css/
   ```
2. Write a Puppeteer/Playwright test to hover on links and measure computed color:
   ```javascript
   await page.hover('a.inline-link');
   const color = await page.$eval('a.inline-link', el => getComputedStyle(el).opacity);
   expect(parseFloat(color)).toBe(1);
   ```

---

## Developer Notes

### General Explanation

The current CSS applies `opacity: 0.6` to links on hover. This reduces the effective contrast of `#555555` text on white from 7.46:1 to approximately **3.2:1**, which fails the WCAG 1.4.3 AA minimum of 4.5:1. The fix is to replace the `opacity` hover effect with a contrast-safe alternative such as a color change, underline modification, or background highlight.

### Code Examples

**Before (current):**
```css
a:hover {
  opacity: 0.6; /* Drops #555 on white from 7.46:1 to ~3.2:1 — FAIL */
}
```

**After — Option A (color change):**
```css
a:hover {
  color: #1A73E8; /* Blue hover — 4.56:1 on white — PASS */
  opacity: 1; /* Ensure opacity is not reduced */
}
```

**After — Option B (underline toggle):**
```css
a {
  text-decoration: underline;
}

a:hover {
  text-decoration: none;
  color: #333333; /* Darker on hover — 12.63:1 — PASS */
}
```

**After — Option C (background highlight):**
```css
a:hover {
  background-color: rgba(26, 115, 232, 0.08);
  color: #555555; /* Maintains original contrast */
  border-radius: 2px;
}
```

**Ensure focus state matches:**
```css
a:focus-visible {
  outline: 2px solid #1A73E8;
  outline-offset: 2px;
  color: #555555; /* No contrast reduction */
}
```

### Components / Files to Audit

- Global `a:hover` rule in the main stylesheet
- Navigation link hover styles
- Footer link hover styles
- Any component-specific link hover overrides
- Check for `opacity` usage on other interactive elements (buttons, cards)

---

## Examples from Other Sites

- **MDN Web Docs:** Link hover changes from `#3d7e9a` to `#1a4666` (darker shade), increasing contrast rather than reducing it.
- **GitHub:** Link hover adds an underline while maintaining the same text color, keeping contrast identical.
- **GOV.UK:** Link hover adds a thicker underline and shifts to a darker color (`#003078`), ensuring contrast increases on interaction.
- **Stripe.com:** Link hover changes to a distinct accent color with full opacity, never reducing contrast below the default state.
