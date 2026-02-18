# L-65: Contact Form Assumes Business Context

**Issue ID:** L-65
**Priority:** Low
**WCAG Criteria:** N/A (UX concern)
**Affected Personas:** Senior Person

---

## User Story

As a **senior individual or freelancer** without a corporate affiliation, I want the contact form to allow me to reach out without requiring a company name or company email so that I am not excluded from contacting the company simply because I don't work for a business.

---

## Acceptance Criteria

- [ ] The "Company" field is either made optional (not required) or relabeled to "Organization (optional)."
- [ ] The "Company Email" field is relabeled to "Email" or "Email Address" and accepts any valid email format (not just corporate domains).
- [ ] No client-side or server-side validation rejects submissions based on email domain (e.g., gmail.com, yahoo.com should be accepted).
- [ ] Optional fields are clearly marked as optional (e.g., "(optional)" in the label text) rather than marking required fields with asterisks alone.
- [ ] The form still collects company information when provided — the change makes it optional, not removed.
- [ ] Form submission succeeds with only the truly required fields: name, email, and message.
- [ ] The form's thank-you/confirmation message does not reference company-specific language (e.g., "We'll reach out to your team" should become "We'll reach out to you").

---

## How to Test the Change

### Manual Testing
1. Navigate to the **Contact** page on launchpadlab.com.
2. Attempt to submit the form with:
   - A personal name (e.g., "Jane Smith")
   - A personal email (e.g., "jane@gmail.com")
   - No company name
   - A message
3. Confirm the form submits successfully without requiring the company field.
4. Confirm no validation error appears for a personal email address.
5. Confirm the "Company" field is labeled as optional.
6. Confirm the email field label reads "Email" or "Email Address" (not "Company Email").
7. Check the confirmation/thank-you message for inclusive language.
8. Test with a screen reader to confirm the optional status is announced for the company field.

### Automated Testing
1. Submit the form programmatically without a company name:
   ```javascript
   // Playwright example
   await page.goto('https://launchpadlab.com/contact/');
   await page.fill('input[name="name"]', 'Jane Smith');
   await page.fill('input[name="email"]', 'jane@gmail.com');
   await page.fill('textarea[name="message"]', 'I have a question about your services.');
   // Leave company field empty
   await page.click('button[type="submit"]');

   // Should succeed — check for success message
   await expect(page.locator('.success-message, .nf-response-msg')).toBeVisible();
   ```
2. Test that personal email domains are accepted:
   ```javascript
   const personalDomains = ['gmail.com', 'yahoo.com', 'outlook.com', 'icloud.com'];
   for (const domain of personalDomains) {
     await page.fill('input[name="email"]', `test@${domain}`);
     await page.click('button[type="submit"]');
     await expect(page.locator('.error-message')).not.toBeVisible();
   }
   ```

---

## Developer Notes

### General Explanation
The contact form currently requires "Company Email" and "Company" as mandatory fields. This creates an implicit assumption that all visitors are employed by a business, excluding freelancers, retirees, individuals, students, and anyone who simply wants to reach out without a corporate context. This is a UX barrier, not a technical accessibility issue, but it disproportionately affects senior users and non-traditional prospects.

### Where to Look
The form is built with **Ninja Forms** (WordPress plugin). Changes should be made in the Ninja Forms admin editor:

1. Go to **WordPress Admin > Ninja Forms > Dashboard**.
2. Open the **Contact** form.
3. Modify the following fields:

**"Company Email" field:**
- Change the label from "Company Email" to "Email Address"
- Keep the field required
- Remove any custom validation that rejects personal email domains

**"Company" field:**
- Change the label from "Company" to "Company or Organization (optional)"
- Set the field to **not required**
- Add "(optional)" to the label text for clarity

### Code-Level Alternative (if form is template-based):
```html
<!-- BEFORE -->
<label for="company-email">Company Email *</label>
<input type="email" id="company-email" name="company-email" required>

<label for="company">Company *</label>
<input type="text" id="company" name="company" required>

<!-- AFTER -->
<label for="email">Email Address *</label>
<input type="email" id="email" name="email" required>

<label for="company">Company or Organization <span class="optional">(optional)</span></label>
<input type="text" id="company" name="company">
```

### Best Practice for Optional vs Required Fields
```css
/* Style optional indicators */
.optional {
  font-weight: normal;
  color: #666;
  font-size: 0.875em;
}
```

Research (Baymard Institute) shows that marking optional fields is more effective than marking required fields with asterisks, as it reduces cognitive load and error rates.

### Components/Files to Audit
- Ninja Forms plugin — Contact form configuration
- Any custom Ninja Forms PHP hooks or filters that validate email domains
- Form submission handler (check for company-field-required logic)
- Email notification template (ensure it handles missing company name gracefully)
- CRM integration (if form data feeds into a CRM, ensure the company field is mapped as optional)

---

## Examples from Other Sites

- **Basecamp:** Their contact form asks for "Name," "Email," and "Message" only — no company field at all. Company information is collected later in the sales conversation.
- **Stripe:** The "Contact Sales" form has a "Company" field but it is explicitly marked as optional.
- **Netlify:** Uses "Email" (not "Company Email") and makes the organization field optional with clear "(optional)" labeling.
- **Intercom:** Their contact form adapts based on the email domain — if a personal email is entered, the company field is hidden automatically.

---

## Additional Context

This issue reflects a broader UX pattern of "assumption-driven form design" where forms are built for the ideal customer profile (enterprise buyer with a company email) rather than for the full range of visitors. Making the company field optional loses minimal data (most business users will still fill it in voluntarily) while removing a barrier for everyone else. The team should also review the form's email notification template to ensure it handles a blank company field gracefully (e.g., does not display "Company: " with an empty value).
