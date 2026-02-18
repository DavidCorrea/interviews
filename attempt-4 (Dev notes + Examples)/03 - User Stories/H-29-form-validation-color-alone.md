# H-29: Form Validation Likely Uses Color Alone

**Issue ID:** H-29
**Priority:** High
**WCAG Criteria:** 1.4.1 Use of Color (A), 3.3.1 Error Identification (A)
**Affected Personas:** Red-Green Color Blind, Blue-Yellow Color Blind

---

## User Story

**As a** color-blind user submitting the contact form,
**I want** form validation errors to be indicated with icons, text labels, and other non-color cues in addition to color,
**so that** I can identify which fields have errors and understand what needs to be corrected.

---

## Acceptance Criteria

- [ ] Each field in an error state displays a visible error icon (e.g., ⚠️ or ✕) adjacent to the field, not just a red border.
- [ ] Each field in an error state displays a descriptive text error message below the field (e.g., "Please enter your email address").
- [ ] The error message text has sufficient contrast (at least 4.5:1) against its background.
- [ ] Errors are programmatically associated with their fields via `aria-describedby` pointing to the error message element.
- [ ] The error message container has `role="alert"` or uses `aria-live="assertive"` so screen readers announce errors immediately.
- [ ] A summary of all errors is displayed at the top of the form when submission fails.
- [ ] Focus is moved to the first errored field (or the error summary) after a failed submission.
- [ ] The error state is perceivable in grayscale (verify via grayscale filter).

---

## How to Test the Change

### Manual Testing

1. **Submit empty form:** Submit the contact form with all fields empty. Confirm each required field shows an error icon + text message, not just a red border.
2. **Grayscale test:** Enable grayscale mode (macOS or Chrome DevTools). Submit the form with errors. Confirm error states are still clearly visible.
3. **Color blindness simulation:** Use Chrome DevTools → Rendering → Emulate Protanopia and Deuteranopia. Confirm errors are identifiable without color perception.
4. **Screen reader test:** Using NVDA or VoiceOver, submit the form with errors. Confirm each error message is announced and associated with the correct field.
5. **Focus management:** After submitting with errors, confirm focus moves to the first errored field or error summary.

### Automated Testing

```javascript
// After triggering validation, check for non-color error indicators
const errorFields = document.querySelectorAll('.nf-error, [aria-invalid="true"]');
errorFields.forEach(field => {
  const errorMsg = field.closest('.field-wrap')?.querySelector('.error-message, .nf-error-msg');
  console.assert(errorMsg, `Field ${field.name} has error state but no error text message`);

  const describedby = field.getAttribute('aria-describedby');
  console.assert(describedby, `Field ${field.name} missing aria-describedby for error message`);
});
```

- Run `axe-core` and check for "Form elements must have labels" and "ARIA input fields must have an accessible description."

---

## Developer Notes

### General Approach

Enhance Ninja Forms' default error styling to include visible error text messages, error icons, and ARIA attributes. This may require custom CSS overrides and potentially a Ninja Forms action hook or custom template.

### Current State (Problem)

```css
/* Ninja Forms default: only a red border indicates errors */
.nf-error .nf-field-element input,
.nf-error .nf-field-element textarea {
  border-color: #E74C3C; /* Red border only */
}
```

```html
<!-- Error state lacks text message and ARIA -->
<div class="nf-error">
  <input type="text" name="first_name" class="nf-element">
  <!-- No error message text, no icon, no aria-describedby -->
</div>
```

### Recommended Fix — CSS

```css
/* Error border + icon indicator */
.nf-error .nf-field-element input,
.nf-error .nf-field-element textarea {
  border: 2px solid #D32F2F;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='20' height='20' viewBox='0 0 24 24' fill='%23D32F2F'%3E%3Cpath d='M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm1 15h-2v-2h2v2zm0-4h-2V7h2v6z'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 10px center;
  padding-right: 40px;
}

/* Error message styling */
.nf-error-msg {
  color: #D32F2F;
  font-size: 0.875rem;
  margin-top: 4px;
  display: flex;
  align-items: center;
  gap: 4px;
}

.nf-error-msg::before {
  content: "⚠";
  font-size: 1rem;
}
```

### Recommended Fix — HTML/ARIA

```html
<div class="nf-field-wrap nf-error">
  <label for="first-name">First Name <span class="required">*</span></label>
  <input
    type="text"
    id="first-name"
    name="first_name"
    aria-invalid="true"
    aria-describedby="first-name-error"
    class="nf-element"
  >
  <div id="first-name-error" class="nf-error-msg" role="alert">
    Please enter your first name.
  </div>
</div>
```

### Error Summary at Top of Form

```html
<div class="form-error-summary" role="alert" tabindex="-1">
  <h3>There are 3 errors in your submission:</h3>
  <ul>
    <li><a href="#first-name">First Name is required</a></li>
    <li><a href="#email">Please enter a valid email address</a></li>
    <li><a href="#message">Message is required</a></li>
  </ul>
</div>
```

### JavaScript: Focus Management

```javascript
// After form validation fails
function handleValidationErrors(errors) {
  const summary = document.querySelector('.form-error-summary');
  if (summary) {
    summary.focus(); // Move focus to error summary
  } else {
    // Move focus to first errored field
    const firstError = document.querySelector('[aria-invalid="true"]');
    if (firstError) firstError.focus();
  }
}
```

### Components / Files to Audit

- Ninja Forms CSS (`.nf-error` class and related styles)
- Ninja Forms JavaScript validation handler
- Custom form template overrides (if any exist in the theme)
- Contact page template

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **GOV.UK** | Error summary at top + inline error text + red left border on the field group (not just the input) | Multiple non-color cues: text, position, border thickness/position, and icon. |
| **Stripe** | Error icon + text message below each field + `aria-describedby` | Icon and text provide redundant non-color indicators. |
| **Shopify** | Error text in red with a ⚠ icon prefix + error summary banner | Icon ensures color-blind users see the error state. |
| **GitHub** | Flash banner at top + inline text + icon on the field | Triple redundancy: position, text, and iconography. |
