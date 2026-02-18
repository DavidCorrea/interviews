# AI-07: Fix Contact Form Accessibility

## Title
Ensure contact form is keyboard accessible, has visible persistent labels, and is exposed to screen readers

## User Story
As a **keyboard user or screen reader user**, I want **the contact form to be fully keyboard accessible with visible labels**, so that **I can complete and submit the form without a mouse and understand what each field requires**.

## Acceptance Criteria

- [ ] All form fields are focusable via keyboard (Tab key)
- [ ] All form fields have associated visible labels (not placeholder-only)
- [ ] Labels are visible at all times (persistent, not only on focus)
- [ ] Screen reader announces field labels when focus moves to each field
- [ ] Submit button has visible text (e.g., "Submit" or "Send")
- [ ] If form is in an iframe, the iframe has a descriptive `title` attribute
- [ ] Form can be completed and submitted using only the keyboard
- [ ] If form loads dynamically, focus moves to the form on load (or user is notified)

## How to Test

1. Navigate to `https://launchpadlab.com/contact`
2. **Keyboard test**: Tab through the page and verify:
   - All form fields (name, email, message, etc.) receive focus in logical order
   - Submit button is focusable and activatable with Enter/Space
   - Form can be completed using only keyboard
3. **Label test**: Verify each field has a visible label above or beside it (not placeholder-only)
4. **Screen reader test** (NVDA on Windows, VoiceOver on macOS):
   - Focus each field and verify the label is announced (e.g., "Name, edit")
   - Verify submit button announces its purpose
5. If form is in an iframe, verify iframe has a `title` attribute
6. Verify submit button displays visible text ("Submit", "Send", etc.)

## Developer Notes

- **If form is in iframe (e.g., HubSpot)**: Add `title="Contact form"` or similar to the iframe element
- **Label association**: Ensure every input has a proper `<label for="field-id">` association:
  ```html
  <label for="contact-name">Name</label>
  <input id="contact-name" type="text" name="name" />
  ```
- **Persistent visible labels**: Do not rely on placeholders as the only label—placeholders can disappear when typing and are not sufficient for accessibility
- **Submit button**: Ensure it has visible text; avoid icon-only buttons without `aria-label`
- **Dynamic form loading**: If the form loads asynchronously, consider:
  - Moving focus to the form when it loads (`form.focus()` or first field)
  - Or announcing form availability to screen readers via `aria-live`
- Test with NVDA (Windows) and VoiceOver (macOS) to verify screen reader compatibility

## WCAG References

- **[2.1.1 Keyboard (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/keyboard.html)**: All functionality of the content is operable through a keyboard interface.
- **[4.1.2 Name, Role, Value (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)**: For all user interface components, the name and role can be programmatically determined.
- **[3.3.2 Labels or Instructions (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)**: Labels or instructions are provided when content requires user input.

## Priority & Effort

| Attribute | Value |
|-----------|-------|
| **Priority** | P1 Critical |
| **Effort Estimate** | Medium (4–8 hours) |
