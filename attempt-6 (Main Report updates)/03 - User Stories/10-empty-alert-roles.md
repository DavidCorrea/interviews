# Empty Alert Roles

## Priority
**Medium**

## User Story
As a screen reader user filling out a contact form, I want error messages to be announced only when validation fails, so that I am not distracted by empty announcements or phantom alerts before I have interacted with the form.

## Acceptance Criteria

- [ ] No `role="alert"` elements are present in the DOM before the user interacts with the form
- [ ] Error messages are dynamically injected only when validation fails
- [ ] Error containers use `aria-live="polite"` instead of `role="alert"` for non-critical validation errors
- [ ] `role="alert"` is used only for critical, time-sensitive errors (e.g., form submission failure)
- [ ] Empty alert containers are not pre-rendered in the HTML
- [ ] Screen reader users do not hear announcements for empty elements on page load

## How to Test

1. Open https://launchpadlab.com/ and navigate to the contact form.
2. Before interacting with any field, use a screen reader (VoiceOver or NVDA) to read the page.
3. Verify no empty alerts or announcements are read for form fields.
4. Inspect the DOM: search for `role="alert"` — ensure no empty elements with this role exist.
5. Submit the form with invalid data — verify error messages appear and are announced.
6. Check form bottom: ensure no multiple empty alert containers exist.
7. If using HubSpot forms, check if this can be configured in their form builder.

## Developer Notes

### General Explanation
Every form field is followed by `alert` role elements in the DOM before any interaction. Screen readers may announce empty alerts, creating noise. Multiple empty alerts at form bottom compound the issue. Users expect to hear announcements only when something actionable occurs.

**Solution:** Use `aria-live="polite"` instead of `role="alert"` for inline validation errors. Dynamically inject error messages only when validation fails. Do not pre-render empty alert containers. If using HubSpot forms, check if this can be configured or if custom CSS/JS can hide them until needed.

### Code Examples

**Before (incorrect):**
```html
<label for="email">Email</label>
<input id="email" type="email" aria-describedby="email-error" />
<div id="email-error" role="alert"></div>
```

**After (correct):**
```html
<label for="email">Email</label>
<input id="email" type="email" aria-describedby="email-error" aria-invalid="false" />
<div id="email-error" aria-live="polite" role="status" aria-atomic="true"></div>
```

**JavaScript for dynamic injection:**
```javascript
const emailInput = document.getElementById('email');
const errorDiv = document.getElementById('email-error');

emailInput.addEventListener('blur', () => {
  if (!emailInput.value || !isValidEmail(emailInput.value)) {
    emailInput.setAttribute('aria-invalid', 'true');
    errorDiv.textContent = 'Please enter a valid email address.';
  } else {
    emailInput.setAttribute('aria-invalid', 'false');
    errorDiv.textContent = '';
  }
});
```

**React example:**
```jsx
const [emailError, setEmailError] = useState('');

return (
  <>
    <label htmlFor="email">Email</label>
    <input
      id="email"
      type="email"
      aria-invalid={!!emailError}
      aria-describedby={emailError ? 'email-error' : undefined}
    />
    {emailError && (
      <div id="email-error" role="alert" aria-live="polite">
        {emailError}
      </div>
    )}
  </>
);
```

**When to use `role="alert"` vs `aria-live="polite"`:**
- `role="alert"` — Critical, time-sensitive (e.g., "Session expired" or "Form submission failed")
- `aria-live="polite"` — Non-critical validation (e.g., "Please enter a valid email")

### Components to Audit
- Contact form component
- HubSpot form embed (if used)
- Any custom form components
- Form validation logic
- Error message rendering

## Examples from Other Sites

- **GOV.UK Design System** — Error summary + inline errors appear only when form is submitted. No pre-rendered empty alerts. Uses `aria-live` for error announcements.
- **Stripe checkout** — Validation errors appear inline only after interaction. No empty alert containers in the DOM.
