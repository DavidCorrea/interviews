# AI-07: Ensure Contact Form is Keyboard/Screen Reader/Voice Accessible

## Metadata
- **ID:** AI-07
- **Priority:** 1 Critical
- **Personas Affected:** 4+ of 16 personas (keyboard, screen reader, voice control, motor)
- **WCAG Criteria:** 2.1.1 Keyboard (A), 4.1.2 Name, Role, Value (A), 3.3.2 Labels or Instructions (A)
- **Effort:** Medium (4–8 hours)

---

## User Story

**As a** visitor who uses a keyboard, screen reader, or voice control to complete forms,

**I want** the LaunchPad Lab contact form to be fully accessible and operable without a mouse,

**So that** I can submit my inquiry regardless of how I interact with the web.

---

## Acceptance Criteria

- [ ] All form fields are reachable via Tab key (no keyboard traps)
- [ ] Every form field has a visible, programmatically associated label
- [ ] Screen reader announces each field with its label (e.g., "Name, edit text")
- [ ] Voice control command "Click Name field" (or similar) successfully focuses the Name field
- [ ] Submit button is keyboard-activatable (Enter or Space)
- [ ] Validation error messages are announced to screen readers
- [ ] On validation error, focus moves to the first field with an error
- [ ] After successful submit, focus moves to confirmation message or success region
- [ ] If form is in an iframe, iframe has a descriptive `title` attribute
- [ ] Form includes appropriate `autocomplete` attributes where applicable

---

## Test Plan

### Keyboard Testing
1. Navigate to `https://launchpadlab.com/contact`
2. Tab to the form — **Expected:** Focus reaches first form field within reasonable tab stops
3. Tab through all fields: Name, Email, Phone (if present), Message, Submit
4. **Expected:** No keyboard trap; can tab out of form
5. Press Enter on Submit — **Expected:** Form submits (or validation runs)
6. If validation errors appear — **Expected:** Focus moves to first error field; errors are fixable via keyboard

### Screen Reader Testing (NVDA or VoiceOver)
1. Navigate to contact form
2. Use Tab or virtual cursor to move through form
3. **Expected:** Each field is announced with its label (e.g., "Name, edit text, blank")
4. **Expected:** Required fields are announced as "required" if applicable
5. Submit form with invalid data — **Expected:** Error messages are announced
6. Submit form with valid data — **Expected:** Success message is announced

### Voice Control Testing (Voice Control on macOS, or similar)
1. Say "Click Name field" — **Expected:** Name field receives focus
2. Say "Click Email field" — **Expected:** Email field receives focus
3. Say "Click Submit" or "Click Send" — **Expected:** Submit button is activated
4. **Note:** Voice control relies on accessible names; labels must match what users might say

### Iframe Testing (if HubSpot or other embed)
1. Inspect form — if in iframe, check `title` attribute
2. **Expected:** `title="Contact Form"` or similar
3. Tab from main page — **Expected:** Focus enters iframe and reaches form fields
4. **Expected:** No tab trap inside iframe

---

## Developer Notes

### If Form is in HubSpot (or other) Iframe
```html
<iframe
  src="https://forms.hubspot.com/..."
  title="Contact Form"
  id="contact-form-iframe"
></iframe>
```

- Add `title` for screen reader context
- Ensure iframe is in tab order (default for iframes with focusable content)
- If form is unreachable, consider moving to native HTML form or ensuring iframe content is accessible

### Native HTML Form — Labels
Every input must have an associated label:

```html
<label for="name">Name</label>
<input type="text" id="name" name="name" autocomplete="name" required>

<label for="email">Email</label>
<input type="email" id="email" name="email" autocomplete="email" required>

<label for="message">Message</label>
<textarea id="message" name="message" rows="5" required></textarea>

<button type="submit">Send Message</button>
```

- `for` and `id` must match
- Placeholder is not a substitute for label
- Use `aria-label` or `aria-labelledby` only when visible label is not possible

### Autocomplete
Add `autocomplete` for better UX and accessibility:

- `autocomplete="name"` — full name
- `autocomplete="email"` — email
- `autocomplete="tel"` — phone
- `autocomplete="organization"` — company name, if applicable

### Validation and Errors
```html
<input
  type="email"
  id="email"
  aria-invalid="true"
  aria-describedby="email-error"
>
<span id="email-error" role="alert">Please enter a valid email address.</span>
```

- Use `aria-invalid="true"` when field has error
- Use `aria-describedby` to associate error message with field
- Use `role="alert"` so screen reader announces error when it appears
- On validation, move focus: `document.getElementById('email').focus()`

### Success/Confirmation
After successful submit:

- Move focus to success message: `successElement.focus()` or `successElement.setAttribute('tabindex', '-1'); successElement.focus()`
- Use `role="status"` or `aria-live="polite"` on success region so screen reader announces it

### Submit Button
- Must have visible text (e.g., "Send Message", "Submit")
- Must be `<button type="submit">` or `<input type="submit">` for native form behavior
- Ensure it’s not disabled without clear reason; if disabled during submit, announce loading state

### Files to Modify
- Contact page template (form markup)
- Contact page or form component (validation, focus management)
- HubSpot or third-party embed configuration (if applicable)
- Global form styles (labels, focus, errors)

---

## Examples

| Site | Approach |
|------|----------|
| **Netlify.com/contact** | Native HTML form; all fields labeled; clean, accessible |
| **Vercel.com/contact** | Accessible form; labels; keyboard-friendly |
| **Shopify.com/contact** | Form with proper labels; error handling |
| **GOV.UK forms** | Exemplary form design; labels, errors, and instructions follow best practices |
