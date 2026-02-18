# Company Required Field

## Priority
**Low**

## User Story
As a potential client in the ideation phase or a solo founder without a company name, I want the Company field on contact forms to be optional, so that I can reach out without being blocked by a requirement that doesn't apply to my situation.

## Acceptance Criteria

- [ ] Company field is not required on contact forms
- [ ] Form can be submitted successfully without a company name
- [ ] Helper text is added to reassure users (e.g., "If you don't have a company yet, that's okay.")
- [ ] Required field indicator (*) is removed from Company label
- [ ] Form validation does not block submission when Company is empty
- [ ] If using HubSpot, field requirements are updated in HubSpot form settings

## How to Test

1. Navigate to the contact form on https://launchpadlab.com/.
2. Fill in required fields (e.g., Name, Email) but leave Company blank.
3. Attempt to submit the form — verify submission succeeds.
4. Check that the Company label does not show a required indicator (*) or "required" text.
5. Verify helper text is visible near the Company field.
6. If using HubSpot forms, log into HubSpot and confirm the Company field is set to optional in form settings.
7. Test with a screen reader — ensure the field is announced as optional, not required.

## Developer Notes

### General Explanation
"Company *" is a required field on contact forms. Users in the ideation phase or solo founders without a company name face friction when trying to reach out. Making the field optional reduces barriers for early-stage prospects and aligns with modern SaaS and consulting best practices.

**Solution:** Make the Company field optional in form configuration. Add helper text such as "If you don't have a company yet, that's okay." to reduce anxiety. If using HubSpot forms, change the field requirements in the HubSpot form builder — HubSpot allows toggling required/optional per field.

### Code Examples

**HTML form — remove required attribute:**
```html
<label for="company">Company</label>
<input
  id="company"
  type="text"
  name="company"
  autocomplete="organization"
  aria-describedby="company-hint"
/>
<span id="company-hint" class="form-hint">
  If you don't have a company yet, that's okay.
</span>
```

**React form — optional field with helper text:**
```jsx
<div className="form-group">
  <label htmlFor="company">Company</label>
  <input
    id="company"
    type="text"
    name="company"
    autoComplete="organization"
    aria-describedby="company-hint"
    required={false}
  />
  <span id="company-hint" className="form-hint">
    If you don't have a company yet, that's okay.
  </span>
</div>
```

**HubSpot form configuration:**
- In HubSpot: Forms > [Your Form] > Fields > Company
- Set "Required" to **No**
- Add help text in the field settings: "If you don't have a company yet, that's okay."

**Validation logic — exclude Company from required check:**
```javascript
const requiredFields = ['name', 'email', 'message'];
const isValid = requiredFields.every((field) => formData[field]?.trim());
```

### Components to Audit
- Contact form component
- HubSpot form embed configuration
- Form validation logic
- Any server-side validation that enforces Company

## Examples from Other Sites

- **Calendly.com** — Company is optional or not asked in initial contact/booking flow. Focuses on name and email for first touch.
- **Notion.so** — Contact and demo request forms typically do not require company; optional fields for context.
- **Most modern SaaS** — Company is often optional in contact forms to reduce friction for solo founders and early-stage users.
