# User Story: Inclusive Contact Form Fields

**Priority:** Medium  
**Related Finding:** [Finding 4](../main-report.md#finding-4)

## Story
As a solo founder or freelancer without a corporate email address, I want the contact form to use inclusive field labels, so that I don't feel excluded or hesitant to reach out.

## Context
The contact form labels the email field as "Company Email," which signals that solo founders, freelancers, and individuals using personal email addresses (e.g., gmail.com) aren't the intended audience. This creates friction at a critical conversion point — the moment a potential client decides to reach out.

## Acceptance Criteria
- The email field label reads "Email" or "Work Email" (not "Company Email")
- The "Company" field is either optional (marked as such) or relabeled to "Company / Project Name"
- The form submits successfully with a personal email address (e.g., @gmail.com)
- No validation rejects non-corporate email domains

## How to Test
1. Navigate to any page with the contact form
2. Verify the email field label reads "Email" or "Work Email"
3. Verify the Company field is marked optional or relabeled
4. Submit the form with a personal email (@gmail.com) — confirm it goes through
5. Screen reader test: have a screen reader announce the form labels and confirm they are inclusive

## Developer Notes

### General Approach
Update form field labels in the CMS or form builder (likely HubSpot or similar marketing automation). If the form is custom-built, update label strings.

### Components to Audit
- Contact form component (appears on every page in footer + dedicated Contact page)
- Form validation rules (ensure no corporate-email-only validation)
- CMS/form builder settings (HubSpot, Marketo, etc.)

### Code Examples
```html
<!-- Before -->
<label for="email">Company Email</label>
<input type="email" id="email" name="email" required />

<label for="company">Company</label>
<input type="text" id="company" name="company" required />

<!-- After -->
<label for="email">Email</label>
<input type="email" id="email" name="email" required />

<label for="company">Company / Project Name <span class="optional">(optional)</span></label>
<input type="text" id="company" name="company" />
```

## How Other Sites Achieve This
- **Linear** (linear.app) — contact form uses "Work email" with no domain restriction
- **Vercel** — waitlist/contact uses simply "Email"
- **Notion** — sign-up and contact forms accept any email domain, label is just "Email"
