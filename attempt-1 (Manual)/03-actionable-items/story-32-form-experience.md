# Story 32: Improve Contact Form Experience

## User Story

**As a** user who finds forms stressful (due to cognitive load, motor impairment, or privacy concerns),
**I want** the contact form to be simple, reassuring, and offer clear alternatives,
**So that** I can contact the company in the way that's easiest for me.

## Description

The contact form creates anxiety for multiple user groups. Users with cognitive disabilities are unsure what information to provide. Users with tremors struggle to type accurately. Seniors worry about data privacy. No alternative is clearly presented alongside the form.

## Acceptance Criteria

- [ ] Phone number and email are presented as equal alternatives above the form (e.g., "Call us, email us, or fill out this form")
- [ ] Reassurance text is visible near the form (e.g., "We will never share your information")
- [ ] Required fields are minimized (only email is required; other fields are optional)
- [ ] Each form field has a clear label, placeholder text, and example input
- [ ] Form fields use proper `autocomplete` attributes for browser autofill support
- [ ] The form explicitly marks optional fields as "(optional)"

## Testing Instructions

1. **Alternatives:** On the contact page, verify phone number and email are displayed above the form with clear "or" language
2. **Reassurance:** Verify privacy reassurance text is visible near the form
3. **Required fields:** Attempt to submit with only email filled — verify it succeeds
4. **Autofill:** Start typing in the name/email fields — verify browser autofill suggestions appear
5. **Labels:** Verify each field has a visible label and helpful placeholder text
6. **Optional marking:** Verify non-required fields are labeled "(optional)"
7. **Keyboard:** Complete the form using only keyboard — verify all fields and the submit button are accessible
8. **Error messages:** Submit with an invalid email — verify the error message is clear, specific, and associated with the field

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | Medium |
| **Complexity** | Medium |
| **WCAG Criteria** | 3.3.2 (Labels or Instructions) |
| **Affected Users** | Cognitive disability, stressed users, motor impairment, seniors |

## Source Reports

- Cognitive Disability Report
- Stressed User Report
- Motor Impairment Report
- Senior User Report
