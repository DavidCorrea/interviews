# Add `aria-required` Attribute to Required Form Fields

## Priority: Low

## User Story
As a screen reader user, I want required form fields to be programmatically marked as required so that my screen reader explicitly announces "required" for each field.

## Acceptance Criteria
- [ ] All required form fields have `aria-required="true"` or the HTML5 `required` attribute
- [ ] Screen reader users hear "required" when focusing required fields
- [ ] Visual asterisk (or equivalent) remains for sighted users
- [ ] Validation error messages clearly reference which fields are required when validation fails
- [ ] Required state is consistent across all contact forms site-wide

## Developer Notes

### General Explanation
Required form fields currently convey their state only through an asterisk in the label. Screen readers need programmatic exposure of the required state. Add `aria-required="true"` to required inputs, or use the HTML5 `required` attribute (which conveys the same information). Keep the visual asterisk for sighted users. Ensure error messages reference required fields when validation fails.

### Code Examples

**Option 1: HTML5 required attribute**
```html
<label for="email">Email <span aria-hidden="true">*</span></label>
<input type="email" id="email" name="email" required>

<label for="message">Message <span aria-hidden="true">*</span></label>
<textarea id="message" name="message" required></textarea>
```

**Option 2: aria-required (e.g., when using custom validation)**
```html
<label for="email">Email <span aria-hidden="true">*</span></label>
<input type="email" id="email" name="email" aria-required="true">

<label for="message">Message <span aria-hidden="true">*</span></label>
<textarea id="message" name="message" aria-required="true"></textarea>
```

**Note:** Use `aria-hidden="true"` on the asterisk so screen readers don't announce "asterisk" as part of the label—they get "required" from the attribute instead.

**React/JSX example:**
```jsx
<input
  type="email"
  id="email"
  name="email"
  required
  aria-required="true"
/>
```

### Components to Audit
- All contact forms across the site (homepage, contact page, service pages)
- Newsletter signup forms
- Any reusable form component or form field component
- Modal or inline forms with required fields

## Examples From Other Sites
- **W3C WAI forms tutorial:** Recommends `required` or `aria-required="true"` for required fields; use `aria-invalid` when validation fails
- **Deque University form patterns:** Required fields use both visual indicator and programmatic exposure; error messages are associated via `aria-describedby`
- **gov.uk form design system:** Required fields use the `required` attribute; labels include "(optional)" for optional fields to avoid ambiguity

## References
- Main Report Item 18
- WCAG 3.3.2 Labels or Instructions
