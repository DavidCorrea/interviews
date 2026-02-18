# AI-14: Add Form Validation with Icons and Text (Not Color Alone)

## Metadata
- **ID:** AI-14
- **Priority:** 2 High
- **Personas Affected:** 2/16 critical (color blind), beneficial for all
- **WCAG Criteria:** 1.4.1 Use of Color (A), 3.3.1 Error Identification (A), 3.3.3 Error Suggestion (AA)
- **Effort:** Medium (4–6 hours)

---

## User Story

**As a** color blind user or someone who cannot reliably distinguish red from green,

**I want** form validation errors and success states to be indicated with icons and text messages in addition to (or instead of) color-coded borders,

**So that** I can clearly identify which fields have errors and what I need to fix, without relying on color alone.

---

## Acceptance Criteria

- [ ] Every form validation error displays: icon (✗ or error icon) + text message + visual border/outline
- [ ] Every successful validation displays: icon (✓ or check icon) + text message when applicable
- [ ] No error or success state is conveyed by color alone
- [ ] Invalid fields have `aria-invalid="true"` when errors exist
- [ ] Error messages are associated via `aria-describedby` pointing to the error element ID
- [ ] Error messages use `role="alert"` for dynamic content so screen readers announce them
- [ ] On form submit with errors, focus moves to the first field with an error
- [ ] Error messages are descriptive and suggest how to fix the issue (e.g., "Please enter a valid email address")
- [ ] Success states (e.g., "Looks good") are announced to screen readers when applicable

---

## Test Plan

### Manual: Submit Form with Empty Required Fields
1. Navigate to `https://launchpadlab.com/` and find the contact form (or any form)
2. Leave required fields empty and submit
3. **Expected:** Each error shows: icon + text message + border (or other non-color indicator)
4. Verify no field relies solely on a red border to indicate error
5. Verify success states (if any) show icon + text, not just green border

### Color Blindness Simulation
1. Install the Colorblindly browser extension (or similar)
2. Enable protanopia or deuteranopia simulation
3. Submit form with errors
4. **Expected:** Errors remain clearly visible without color — icons and text provide the information
5. Repeat with different color blindness types

### Screen Reader
1. Use NVDA, VoiceOver, or JAWS
2. Submit form with invalid data
3. **Expected:** Error messages are announced (role="alert")
4. **Expected:** When focusing an invalid field, the error is announced via aria-describedby
5. **Expected:** Focus moves to first errored field after submit
6. Tab through form — each invalid field should announce its error

### Automated
- Run axe DevTools on form with validation errors visible
- **Expected:** No "Color contrast" or "Information conveyed by color alone" violations
- **Expected:** No "Form field missing label" or "aria-invalid" misuse

### Focus Management
- After submit with errors, verify focus lands on first invalid field
- Verify user can tab to next error without getting stuck

---

## Developer Notes

### Error Container Structure
For each validated field, add an error container that is hidden by default and shown on error:

```html
<label for="email">Email</label>
<input
  type="email"
  id="email"
  name="email"
  aria-invalid="false"
  aria-describedby="email-error"
  required
/>
<span id="email-error" role="alert" class="error-message" aria-live="polite">
  <!-- Populated on validation failure -->
</span>
```

### On Validation Failure
```javascript
// Set attributes
input.setAttribute('aria-invalid', 'true');
errorSpan.setAttribute('role', 'alert');
errorSpan.textContent = '✗ Please enter a valid email address';
errorSpan.classList.add('visible');
```

### Success State (Optional)
```html
<span id="email-success" class="success-message" aria-live="polite">
  ✓ Looks good
</span>
```

### Never Rely on Border Color Alone
- Use `border-left: 4px solid var(--error-color)` PLUS icon PLUS text
- Or use `outline` + icon + text
- Ensure icon has sufficient contrast and is recognizable

### Focus Management on Submit
```javascript
function handleSubmit(e) {
  const errors = validateForm();
  if (errors.length > 0) {
    e.preventDefault();
    const firstErrorField = document.getElementById(errors[0].fieldId);
    firstErrorField.focus();
    // Also announce to screen reader
    firstErrorField.setAttribute('aria-invalid', 'true');
  }
}
```

### Components to Audit (LaunchPad Lab)
- [ ] Contact form
- [ ] Newsletter signup
- [ ] Any modal with form fields
- [ ] Multi-step forms (if present)

### CSS for Error/Success
```css
.error-message { display: flex; align-items: center; gap: 0.5rem; }
.error-message::before { content: "✗"; }
.success-message::before { content: "✓"; }
input[aria-invalid="true"] { border-color: var(--error); }
```

---

## Examples

| Site | Approach |
|------|----------|
| **GOV.UK forms** | Text + icon for every error; red border is supplementary; errors in summary at top |
| **Stripe checkout** | Inline text errors below each field; clear, actionable messages |
| **GitHub signup form** | Icon + text for validation; real-time feedback with descriptive messages |
