# Story 06: Make Contact Form Keyboard Accessible

## User Story

**As a** keyboard or screen reader user,
**I want** the contact form to be fully operable using only the keyboard,
**So that** I can submit my information without needing a mouse.

## Description

The contact page says "Complete the form below to tell us about your project," but a screen reader user could not locate any form fields when navigating with Tab or the F key. The form either does not exist, is loaded dynamically without focus management, or is entirely inaccessible to keyboard users.

## Acceptance Criteria

- [ ] All form fields are reachable using the Tab key
- [ ] Each form field has a visible `<label>` element properly associated via `for`/`id` attributes
- [ ] Required fields are indicated with `aria-required="true"` and visible text (not just color or asterisk alone)
- [ ] Error messages are associated with their fields via `aria-describedby`
- [ ] The submit button has a descriptive label (e.g., "Submit Contact Form")
- [ ] The form is present in the DOM on page load (not gated behind JS rendering that blocks access)
- [ ] Screen readers can navigate to the form using the F key (form elements navigation)

## Testing Instructions

1. **Keyboard-only:** Navigate the contact page using only Tab and Shift+Tab — verify every form field, dropdown, and the submit button are reachable and operable
2. **Screen reader:** Open the contact page with NVDA, press F to jump to form elements — verify all fields are announced with their labels
3. **Submit test:** Fill out and submit the form using only keyboard — verify success/error messages are announced
4. **Label check:** Click on each form `<label>` text — the corresponding input field should receive focus
5. **Required fields:** Leave required fields empty and submit — verify error messages are announced by screen reader and visually associated with the correct field
6. **Page load:** Disable JavaScript temporarily and load the contact page — check if the form HTML is present in the source (rules out JS-only rendering)

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | Critical |
| **Complexity** | Medium |
| **WCAG Criteria** | 2.1.1 (Keyboard) |
| **Affected Users** | Screen reader users, keyboard-only users |

## Source Reports

- Screen Reader Report
