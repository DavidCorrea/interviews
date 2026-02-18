# M-41: Placeholder Text White on Light Backgrounds

**Issue ID:** M-41
**Priority:** Medium
**WCAG Criteria:** 1.4.3 Contrast (Minimum) (AA), 3.3.2 Labels or Instructions (A)
**Affected Personas:** Low Contrast Sensitivity

---

## User Story

As a **user with low contrast sensitivity**, I want **form placeholder text to be readable against its input background** so that **I can see the hint text that tells me what information to enter in each field.**

---

## Acceptance Criteria

- [ ] The global `::placeholder { color: #FFF }` rule is removed or scoped to only apply on dark backgrounds where white placeholder text is legible.
- [ ] Placeholder text on all form inputs achieves a contrast ratio of at least **4.5:1** against the input's background color.
- [ ] On light/white input backgrounds, placeholder color is set to a medium gray (e.g., `#767676` on white = 4.54:1).
- [ ] On the blue contact section where inputs have dark backgrounds, placeholder text remains appropriately light.
- [ ] All forms across the site are checked (Contact page, newsletter signups, search, any other input fields).

---

## How to Test the Change

### Manual Testing

1. Navigate to every page with form inputs (Contact, newsletter signups, search).
2. Click into each input field and observe the placeholder text.
3. Use DevTools to inspect the `::placeholder` computed color.
4. Measure the contrast ratio between the placeholder color and the input's background using [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/).
5. Confirm at least **4.5:1** on all inputs.
6. Test on both the blue contact section (dark background) and any other forms on light backgrounds.

### Automated Testing

1. Search for the offending global rule:
   ```bash
   grep -rn "placeholder.*#[Ff][Ff][Ff]\|placeholder.*white\|placeholder.*fff" path/to/css/
   ```
2. Run axe DevTools with focus on the contact form — check for contrast violations on placeholder text.
3. Playwright test to verify placeholder visibility:
   ```javascript
   const input = page.locator('input[placeholder]').first();
   const placeholderColor = await input.evaluate(el =>
     getComputedStyle(el, '::placeholder').color
   );
   // Validate not white (#fff)
   expect(placeholderColor).not.toBe('rgb(255, 255, 255)');
   ```

---

## Developer Notes

### General Explanation

A global CSS rule sets `::placeholder { color: #FFF }`, which was likely intended for the blue-background contact form section where white text is readable. However, this rule applies to ALL inputs site-wide, making placeholder text invisible on any white or light-colored input field. The fix is to scope the white placeholder rule to only the dark-background context and set a compliant default.

### Code Examples

**Before (current):**
```css
/* Global rule — applies to ALL inputs */
::placeholder {
  color: #FFFFFF;
}
```

**After (fixed):**
```css
/* Default placeholder color for light backgrounds */
::placeholder {
  color: #767676; /* 4.54:1 on white — PASS */
  opacity: 1; /* Firefox sets opacity: 0.54 by default */
}

/* Scoped white placeholder for dark-background inputs */
.contact-section input::placeholder,
.contact-section textarea::placeholder,
.dark-bg input::placeholder,
.dark-bg textarea::placeholder {
  color: rgba(255, 255, 255, 0.8); /* Light text on dark background */
}
```

**Important: Normalize Firefox placeholder opacity:**
```css
::-moz-placeholder {
  opacity: 1; /* Firefox default is 0.54, which further reduces contrast */
}
```

**Remember: Placeholders are NOT labels. Always provide visible labels:**
```html
<label for="email">Email Address</label>
<input type="email" id="email" placeholder="e.g., name@company.com">
```

### Components / Files to Audit

- Global CSS `::placeholder` rule
- Contact form section styles
- Any WordPress plugin form styles (Ninja Forms, Gravity Forms)
- Newsletter/subscription form widgets
- Search input fields
- Check for `::-webkit-input-placeholder` and `::-moz-placeholder` vendor prefixes

---

## Examples from Other Sites

- **GOV.UK:** Does not use placeholder text at all — instead, uses visible hint text below the label. This avoids the contrast issue entirely and provides persistent guidance.
- **Stripe.com:** Uses `placeholder-color: #6b7c93` (approximately 4.5:1 on white), providing readable hint text.
- **GitHub:** Placeholder text uses `color: #6e7781` on white input backgrounds (~4.5:1), with explicit labels always visible.
- **Basecamp:** Uses `color: #999` placeholders on white inputs (~2.85:1 — below recommendation) but supplements with persistent visible labels above each field.
