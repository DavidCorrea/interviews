# C-08: Form Input Fields Have No Visible Border

**Priority:** Critical
**WCAG Criteria:** 1.4.11 Non-text Contrast (AA), 1.3.1 Info and Relationships (A), 3.3.2 Labels or Instructions (A)
**Affected Personas:** Low Contrast Sensitivity, Situational Contrast

---

## User Story

**As a** user with low contrast sensitivity or someone viewing the site in bright ambient lighting,
**I want** the contact form input fields to have clearly visible borders or boundaries,
**so that** I can easily identify where to type my information without struggling to see the field edges.

---

## Acceptance Criteria

- [ ] All form `<input>` and `<textarea>` fields have a visible border or boundary with at least 3:1 contrast ratio against the surrounding background.
- [ ] The field boundary is visible in both light and dark ambient conditions.
- [ ] The border is not relying solely on a subtle background color difference — it must use a distinct border line or high-contrast background fill.
- [ ] Each form field is visually distinguishable from the next (clear separation between fields).
- [ ] Focus states enhance the border further (e.g., thicker border, color change) — see C-06.
- [ ] Placeholder text also meets minimum contrast requirements (4.5:1 for normal text).

---

## How to Test the Change

### Manual Testing

1. **Visual Inspection:**
   - Navigate to the Contact page.
   - Look at the form fields — borders should be clearly visible without squinting.
   - View the page on a mobile device in sunlight (or simulate by increasing monitor brightness to maximum).

2. **Contrast Measurement:**
   - Use the Colour Contrast Analyser tool or Chrome DevTools color picker.
   - Measure the contrast ratio between the input border color and the surrounding background.
   - Verify it is ≥ 3:1.

3. **Accessibility Tree:**
   - Open Chrome DevTools → Accessibility panel.
   - Verify each input has a proper role and associated label.

### Automated Testing

```javascript
// Playwright test — verify form fields have visible borders
test('form inputs have sufficient border contrast', async ({ page }) => {
  await page.goto('https://launchpadlab.com/contact/');

  const inputs = page.locator('input:not([type="hidden"]), textarea');
  const count = await inputs.count();

  for (let i = 0; i < count; i++) {
    const input = inputs.nth(i);
    const styles = await input.evaluate(el => {
      const s = window.getComputedStyle(el);
      return {
        borderWidth: s.borderWidth,
        borderStyle: s.borderStyle,
        borderColor: s.borderColor,
      };
    });
    // Verify border exists (not "none")
    expect(styles.borderStyle).not.toBe('none');
    expect(styles.borderWidth).not.toBe('0px');
  }
});
```

---

## Developer Notes

### General Approach

Add visible borders to all form inputs on the contact page. The current design uses `border: none` with `background-color: rgba(255,255,255,0.2)` on a blue background, yielding ~1.51:1 contrast. The fix is to add a solid border with sufficient contrast or switch to opaque white-background fields.

### Code Examples

**Before (current state):**

```css
.contact-form input,
.contact-form textarea {
  background-color: rgba(255, 255, 255, 0.2);
  border: none;
  color: #fff;
  padding: 12px 16px;
}
```

**After — Option A: Add visible border (keep transparent background):**

```css
.contact-form input,
.contact-form textarea {
  background-color: rgba(255, 255, 255, 0.2);
  border: 2px solid rgba(255, 255, 255, 0.7); /* ~4:1 contrast on blue */
  border-radius: 4px;
  color: #fff;
  padding: 12px 16px;
  transition: border-color 0.2s ease;
}

.contact-form input:focus-visible,
.contact-form textarea:focus-visible {
  border-color: #ffffff;
  outline: 2px solid #f5a623;
  outline-offset: 2px;
}
```

**After — Option B: Opaque white fields (higher contrast):**

```css
.contact-form input,
.contact-form textarea {
  background-color: #ffffff;
  border: 2px solid #666666; /* High-contrast border */
  border-radius: 4px;
  color: #333333;
  padding: 12px 16px;
}

.contact-form input:focus-visible,
.contact-form textarea:focus-visible {
  border-color: #1a73e8;
  box-shadow: 0 0 0 3px rgba(26, 115, 232, 0.3);
}
```

**Fix placeholder contrast:**

```css
/* Before — invisible placeholder */
::placeholder {
  color: #fff; /* or too low contrast */
}

/* After — visible placeholder */
.contact-form ::placeholder {
  color: rgba(255, 255, 255, 0.75); /* On blue background */
  /* OR for white input fields: */
  /* color: #767676; */ /* 4.54:1 contrast on white */
}
```

### Components/Files to Audit

- Contact form CSS — input/textarea styles on the blue background section.
- Global `::placeholder` color rule.
- Ninja Forms plugin CSS overrides.
- Any `border: none` declarations on form elements site-wide.
- Responsive styles — ensure borders work at all breakpoints.

---

## Examples from Other Sites

| Site | Implementation |
|------|----------------|
| **gov.uk** | Form inputs have a solid 2px black border (`#0b0c0c`) on white — extremely high contrast. |
| **Stripe** | Light gray border (#e0e0e0) on white fields with a blue border on focus — clean and visible. |
| **Linear** | Form fields on dark backgrounds use a distinct lighter border + subtle fill to ensure visibility. |
| **Mailchimp** | Form fields use 1px solid gray borders (#d5d5d5) on white with a more prominent blue border on focus. |
