# 27. Contact Form Excludes Non-Corporate Users

**Priority:** High
**Location:** All contact forms sitewide
**Reported by:** Zara Mitchell (Gen Z First-Time Founder)

---

## User Story

**As a** 22-year-old aspiring founder with a startup idea but no registered company,
**I want** to submit a contact form without needing a corporate email address or company name,
**so that** I feel welcomed as a potential client regardless of what stage my business is at.

---

## Problem

The contact form across the LaunchPad Lab site requires two fields that actively exclude early-stage founders:

1. **"Company Email" (required):** The label explicitly signals that personal email addresses (Gmail, Outlook, iCloud) are not welcome. A 22-year-old founder working from a Brooklyn apartment with `zara.mitchell@gmail.com` sees this field and thinks, "This agency isn't for me." The field doesn't just ask for an email — the word "Company" acts as a gatekeeper.

2. **"Company" (required):** A pre-revenue founder may not have incorporated yet. They have an idea, maybe a prototype, but no legal entity. Requiring a company name forces them to either make something up or abandon the form entirely.

3. **No project stage context:** The form treats every inquiry identically. There's no way for a founder to signal "I'm early stage and exploring" vs. "I have funding and need to build." This means LaunchPad Lab's team has no context to tailor their response appropriately.

The cumulative effect: the form reads as "enterprise inquiries only." Early-stage founders — who could become long-term clients — bounce before submitting.

---

## Acceptance Criteria

### A. Email Field
- [ ] The "Company Email" field label is changed to "Email" or "Email Address"
- [ ] The field accepts any valid email format (personal, corporate, .edu, etc.)
- [ ] The `<label>` element text reads "Email" or "Email Address" — not "Company Email," "Work Email," or "Business Email"
- [ ] The field retains its `required` attribute
- [ ] The `type="email"` attribute is present for native validation and mobile keyboard optimization
- [ ] Placeholder text (if used) reads something neutral like "you@example.com"

### B. Company Field
- [ ] The "Company" field is either:
  - Made optional (with the label updated to "Company / Project Name (optional)"), **or**
  - Renamed to "Company or Project Name" and kept required
- [ ] If optional, the field is visually marked as optional (text "(optional)" in the label, not just removing the asterisk)
- [ ] The form submits successfully when the company field is left empty (if made optional)
- [ ] Backend/CRM processing handles blank company values gracefully (no errors, no "N/A" appearing in CRM records)

### C. Project Stage Dropdown
- [ ] A new "What stage is your project?" dropdown (or similar field) is added to the form
- [ ] Options include at minimum: "Just an idea," "Early prototype / MVP," "Existing product that needs work," "Funded startup," "Established company"
- [ ] The dropdown has a proper `<label>` associated via `for`/`id`
- [ ] The default option is a disabled placeholder (e.g., "Select one...")
- [ ] The field is optional or required — either way, the choice is deliberate and documented
- [ ] The dropdown does not block form submission if left unselected (if optional)

### D. Accessibility
- [ ] All new and modified fields have programmatically associated `<label>` elements
- [ ] Error messages for required fields are announced by screen readers (via `aria-live` or `aria-describedby`)
- [ ] The form is fully navigable with keyboard only (Tab, Shift+Tab, Enter, Space for dropdowns)
- [ ] The form passes WCAG 2.1 SC 1.3.1 (Info and Relationships) and SC 3.3.2 (Labels or Instructions)

---

## How to Test

### Email Field Rename
1. Navigate to `/contact/`
2. Locate the email field
3. Verify the visible label reads "Email" or "Email Address" — no mention of "Company"
4. Inspect the HTML: confirm `<label for="email">Email</label>` (or equivalent)
5. Enter a personal email like `founder@gmail.com` — confirm no validation error or warning about non-corporate addresses
6. Enter a corporate email like `jane@bigcorp.com` — confirm it also works
7. Submit the form with a personal email — confirm submission succeeds

### Company Field
1. On the same contact form, locate the company field
2. Verify the label reads "Company / Project Name (optional)" or "Company or Project Name"
3. If marked optional, leave the field blank and submit — confirm form submits without error
4. If optional, verify the word "(optional)" appears in or near the label
5. Enter a value like "My Side Project" — confirm it's accepted without issue
6. Check the CRM or form submission backend: confirm empty company values don't cause errors or display as "undefined"

### Project Stage Dropdown
1. Locate the new project stage dropdown on the form
2. Verify a default placeholder like "Select one..." is shown and is not selectable as a value
3. Open the dropdown — verify all stage options are present and clearly worded
4. Select "Just an idea" and submit the form — confirm submission succeeds
5. If the field is optional, leave it unselected and submit — confirm form still submits

### Accessibility
1. Tab through the entire form — confirm every field (including the new dropdown) receives visible focus
2. Use VoiceOver (macOS) or NVDA (Windows) to navigate the form — confirm every label is announced
3. Submit the form with required fields empty — confirm error messages are announced by the screen reader
4. Inspect the HTML — confirm all `<label>` elements use `for` attributes matching their input `id` values
5. Confirm `aria-describedby` links any helper text to the appropriate fields

---

## Developer Notes

### A. Renaming the Email Field

Find the current email field markup and update the label:

```html
<!-- BEFORE -->
<div class="form-group">
  <label for="email" class="form-label">Company Email *</label>
  <input
    type="email"
    id="email"
    name="email"
    class="form-input"
    required
    placeholder="name@company.com"
  />
</div>

<!-- AFTER -->
<div class="form-group">
  <label for="email" class="form-label">Email Address *</label>
  <input
    type="email"
    id="email"
    name="email"
    class="form-input"
    required
    placeholder="you@example.com"
    autocomplete="email"
  />
</div>
```

The `autocomplete="email"` attribute helps browsers and password managers autofill correctly.

### B. Making Company Optional with Rename

```html
<!-- BEFORE -->
<div class="form-group">
  <label for="company" class="form-label">Company *</label>
  <input
    type="text"
    id="company"
    name="company"
    class="form-input"
    required
  />
</div>

<!-- AFTER -->
<div class="form-group">
  <label for="company" class="form-label">
    Company or Project Name
    <span class="form-label__optional">(optional)</span>
  </label>
  <input
    type="text"
    id="company"
    name="company"
    class="form-input"
    placeholder="e.g., Acme Inc. or My App Idea"
    autocomplete="organization"
  />
</div>
```

```css
.form-label__optional {
  font-weight: 400;
  font-size: 0.875rem;
  color: #6b7280;
  margin-left: 0.25rem;
}
```

If using a CMS or form builder (HubSpot, Formspree, etc.), update the field configuration there as well. Ensure the backend schema accepts `null` or empty strings for the company field.

### C. Adding the Project Stage Dropdown

```html
<div class="form-group">
  <label for="project-stage" class="form-label">
    What stage is your project?
    <span class="form-label__optional">(optional)</span>
  </label>
  <p id="project-stage-hint" class="form-hint">
    This helps us tailor our response to where you are right now.
  </p>
  <select
    id="project-stage"
    name="project_stage"
    class="form-select"
    aria-describedby="project-stage-hint"
  >
    <option value="" disabled selected>Select one...</option>
    <option value="idea">Just an idea</option>
    <option value="prototype">Early prototype or MVP</option>
    <option value="existing-product">Existing product that needs improvement</option>
    <option value="funded-startup">Funded startup ready to build</option>
    <option value="established">Established company</option>
  </select>
</div>
```

```css
.form-select {
  width: 100%;
  padding: 0.75rem 2.5rem 0.75rem 1rem;
  font-size: 1rem;
  line-height: 1.5;
  color: #1f2937;
  background-color: #ffffff;
  border: 1px solid #d1d5db;
  border-radius: 6px;
  appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath fill='%236b7280' d='M1.41 0L6 4.58 10.59 0 12 1.41l-6 6-6-6z'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 1rem center;
  background-size: 0.75rem;
  cursor: pointer;
}

.form-select:focus {
  outline: 2px solid #2563eb;
  outline-offset: 2px;
  border-color: #2563eb;
}

.form-hint {
  font-size: 0.875rem;
  line-height: 1.5;
  color: #6b7280;
  margin-top: 0.25rem;
  margin-bottom: 0.5rem;
  font-style: italic;
}
```

### D. Full Revised Form Structure

Here's how the key fields should look together after all changes:

```html
<form class="contact-form" method="post" action="/api/contact" novalidate>
  <div class="form-row form-row--two-col">
    <div class="form-group">
      <label for="first-name" class="form-label">First Name *</label>
      <input type="text" id="first-name" name="first_name" class="form-input"
             required autocomplete="given-name" />
    </div>
    <div class="form-group">
      <label for="last-name" class="form-label">Last Name *</label>
      <input type="text" id="last-name" name="last_name" class="form-input"
             required autocomplete="family-name" />
    </div>
  </div>

  <div class="form-group">
    <label for="email" class="form-label">Email Address *</label>
    <input type="email" id="email" name="email" class="form-input"
           required placeholder="you@example.com" autocomplete="email" />
  </div>

  <div class="form-group">
    <label for="company" class="form-label">
      Company or Project Name
      <span class="form-label__optional">(optional)</span>
    </label>
    <input type="text" id="company" name="company" class="form-input"
           placeholder="e.g., Acme Inc. or My App Idea" autocomplete="organization" />
  </div>

  <div class="form-group">
    <label for="project-stage" class="form-label">
      What stage is your project?
      <span class="form-label__optional">(optional)</span>
    </label>
    <select id="project-stage" name="project_stage" class="form-select">
      <option value="" disabled selected>Select one...</option>
      <option value="idea">Just an idea</option>
      <option value="prototype">Early prototype or MVP</option>
      <option value="existing-product">Existing product that needs improvement</option>
      <option value="funded-startup">Funded startup ready to build</option>
      <option value="established">Established company</option>
    </select>
  </div>

  <div class="form-group">
    <label for="message" class="form-label">How Can We Help You? *</label>
    <textarea id="message" name="message" class="form-textarea" rows="5"
              required placeholder="Tell us about your project..."></textarea>
  </div>

  <button type="submit" class="form-submit">Send Message</button>
</form>
```

### E. Backend / CRM Considerations

If form submissions feed into a CRM (HubSpot, Salesforce, etc.):

```javascript
// Normalize form data before CRM insertion
function normalizeFormData(data) {
  return {
    first_name: data.first_name.trim(),
    last_name: data.last_name.trim(),
    email: data.email.trim().toLowerCase(),
    company: data.company?.trim() || 'Not provided',
    project_stage: data.project_stage || 'Not specified',
    message: data.message.trim(),
  };
}
```

Update any CRM workflow rules that filter on the "company" field being present. Early-stage leads should not be auto-rejected because company is blank.

### WCAG References

- **WCAG 2.1 SC 1.3.1 Info and Relationships (A):** All form fields must have programmatically associated labels
- **WCAG 2.1 SC 3.3.2 Labels or Instructions (A):** Labels must clearly describe what is expected — "Company Email" is misleading when personal email is acceptable
- **WCAG 2.1 SC 3.3.5 Help (AAA):** Context-sensitive help (the project stage hint text) assists users in completing the form
- **WCAG 2.1 SC 2.4.6 Headings and Labels (AA):** Labels must describe topic or purpose — "Email Address" is accurate; "Company Email" is not when personal emails are accepted

### Components to Audit

- **Contact form component** — Update field labels, add project stage dropdown, remove `required` from company field
- **Form validation logic** — Remove company from required field checks; add project stage to schema
- **CRM integration** — Ensure empty company and project stage values are handled; update lead scoring rules
- **All pages with embedded forms** — Homepage, Services pages, Industries pages — verify the changes propagate
- **Email notification templates** — If form submissions generate emails to the sales team, add the project stage to the email body
- **Analytics/tracking** — Update form tracking events if field names change (e.g., `company_email` → `email`)

---

## Examples from Other Sites

### Vercel (vercel.com/contact/sales)
Their contact form asks for "Email" (not "Work Email"), "Company" as an optional field, and a dropdown for "Company size" ranging from "Just me" to "1000+". A solo founder selecting "Just me" feels entirely welcomed.

### Netlify (netlify.com/enterprise)
While their enterprise form does ask for work email, their general contact form at `/contact/` simply says "Email." They also include a "How can we help?" dropdown with "I'm exploring for a new project" as an option — giving early-stage founders a clear entry point.

### Webflow (webflow.com/contact)
Webflow's sales form asks for "Email" and has a "Company" field but also offers "What best describes you?" with options including "Freelancer," "Startup founder," and "Agency." This segmentation shows they welcome non-enterprise users.

### Lemon Squeezy (lemonsqueezy.com)
Their contact form is radically simple: Name, Email, Message. No company field at all. The simplicity communicates "anyone can reach us." Their support team qualifies leads manually, which works well at their scale.

### Key Patterns
1. **"Email" not "Company Email"** — Every startup-friendly agency uses "Email" as the field label
2. **Optional or absent company fields** — The company name is gathered in the conversation, not as a form gate
3. **Self-identification dropdowns** — Letting users say "I'm a startup founder" or "Just exploring" gives the sales team context without excluding anyone
4. **Stage-based routing** — Some forms use the project stage to route inquiries: early-stage goes to a "startup specialist," enterprise goes to account executives
