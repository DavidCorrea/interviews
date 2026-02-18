# Company Email Field Label

## Priority
**Medium**

## User Story
As a founder, student, or freelancer without a corporate email domain, I want the contact form to use a neutral label like "Email" or "Work Email" instead of "Company Email," so that I do not feel excluded or assume that I am not a valid contact for LaunchPad Lab.

## Acceptance Criteria

- [ ] Form label is changed from "Company Email *" to "Email" or "Work Email"
- [ ] Required indicator (*) remains if the field is required
- [ ] No client-side validation that rejects non-corporate domains (e.g., Gmail, Yahoo)
- [ ] If business email validation is needed, it is handled server-side with a friendly message
- [ ] Placeholder text (if any) does not imply corporate-only (e.g., avoid "you@company.com")
- [ ] Screen reader users hear a clear, inclusive label

## How to Test

1. Open https://launchpadlab.com/ and navigate to the contact form.
2. Verify the email field label is "Email" or "Work Email" (not "Company Email").
3. Submit the form with a Gmail, Yahoo, or personal domain — verify it is accepted.
4. If using HubSpot, check HubSpot form field configuration for label changes.
5. Use a screen reader to confirm the label is announced correctly.
6. Test on mobile: verify form layout and label visibility.

## Developer Notes

### General Explanation
The contact form uses the label "Company Email *" as required. Users without corporate email domains (founders, students, freelancers) may feel excluded. This creates a psychological barrier for non-enterprise users who may assume LaunchPad Lab only serves large companies.

**Solution:** Change label to "Work Email" or just "Email." If business email validation is needed, handle it server-side with a friendly message. If using HubSpot forms, this may be a HubSpot field configuration change.

### Code Examples

**Before (exclusive):**
```html
<label for="email">Company Email *</label>
<input id="email" type="email" required placeholder="you@company.com" />
```

**After (inclusive):**
```html
<label for="email">Email *</label>
<input id="email" type="email" required placeholder="you@example.com" />
```

**Alternative:**
```html
<label for="email">Work Email *</label>
<input id="email" type="email" required placeholder="you@example.com" />
```

**HubSpot form field:**
- In HubSpot: edit the form → click the email field → change "Label" from "Company Email" to "Email" or "Work Email"
- Ensure "Required" is set as needed; no validation that rejects non-corporate domains

**Server-side validation (if needed):**
```javascript
// If you must validate business email, do it server-side with a friendly message
if (requiresBusinessEmail && !isBusinessDomain(email)) {
  return res.status(400).json({
    error: 'Please use a work email address. If you don\'t have one, we\'d still love to hear from you — try our contact form or give us a call.'
  });
}
```

### Components to Audit
- Contact form component
- HubSpot form embed (if used)
- Any custom form field configuration
- Form validation logic
- CMS/form builder for contact forms

## Examples from Other Sites

- **Calendly.com signup** — Uses "Email" as the label. No corporate-only implication.
- **Notion.so** — Uses "Email" for contact and signup forms. Inclusive and welcoming.
- **Most modern SaaS signups** — Use generic "Email" label. Avoid "Company Email" or "Work Email" unless the product explicitly targets enterprise only.
