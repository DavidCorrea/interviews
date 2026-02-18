# No Dedicated Contact Page & Missing Post-Submission Expectations

**Priority:** High
**Location:** `/contact/` URL, all embedded contact forms
**WCAG:** [3.3.2 Labels or Instructions (A)](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions), [3.3.5 Help (AAA)](https://www.w3.org/WAI/WCAG21/Understanding/help), [2.4.2 Page Titled (A)](https://www.w3.org/WAI/WCAG21/Understanding/page-titled)

---

## User Story

> As a **potential client ready to reach out**,
> I want **a dedicated contact page with clear expectations about what happens after I submit the form**
> so that **I feel confident my message will be received and I know when and how I'll hear back.**

---

## Problem

1. **No dedicated contact page.** Clicking "Contact" in the navigation does not lead to a focused, standalone contact page. The form is embedded within other page content, making it harder to find and reducing trust.
2. **Vague post-submission message.** After submitting, the confirmation says "We will get in touch as soon as possible" — no timeline, no format (email? phone?), no next steps.
3. **No alternative contact methods.** No phone number, no email address, no office address — the form is the only option.
4. **No guidance for open-ended fields.** If the form includes a "Tell us about your project" textarea, there is no guidance on what to include, which can cause anxiety and abandonment.

---

## Acceptance Criteria

- [ ] A dedicated `/contact/` route exists with a focused contact page.
- [ ] The page has a clear `<h1>`: "Contact Us" or "Get in Touch."
- [ ] The contact form includes: Name, Email, Company (optional), and a project description field with helper text.
- [ ] The project description field includes placeholder guidance (e.g., "Tell us what you're looking to build, your timeline, and budget range — even rough estimates help").
- [ ] At least one alternative contact method is provided (email address and/or phone number).
- [ ] The post-submission confirmation message includes: expected response time (e.g., "within 1 business day"), response format (e.g., "via email"), and what happens next (e.g., "We'll schedule a 30-minute call").
- [ ] All form fields have visible `<label>` elements associated via `for`/`id`.
- [ ] Required fields are marked visually and with `aria-required="true"`.
- [ ] Form validation errors are announced to screen readers via `aria-describedby` and `role="alert"`.
- [ ] The page is accessible via keyboard-only navigation.

---

## How to Test

1. **Navigation test:** Click "Contact" in the main navigation. Verify it leads to a dedicated page at `/contact/`, not an anchor on another page.
2. **Form label audit:** Inspect each form field. Verify every `<input>` and `<textarea>` has an associated `<label>` with a matching `for`/`id` pair.
3. **Screen reader test:** Navigate the form with VoiceOver or NVDA. Verify labels are announced, required fields are indicated, and error messages are read aloud.
4. **Submit the form:** Fill in the form and submit. Verify the confirmation message includes a specific response time, format, and next steps.
5. **Empty submission test:** Submit with required fields empty. Verify inline error messages appear and are associated with the correct fields via `aria-describedby`.
6. **Keyboard test:** Tab through the entire form. Verify focus order is logical and the submit button is reachable. Verify focus is visible on every interactive element.

---

## Developer Notes

### Recommended page structure

```html
<main id="main-content">
  <section class="contact-page" aria-labelledby="contact-heading">
    <h1 id="contact-heading">Contact Us</h1>
    <p class="contact-page__intro">
      Tell us about your project and we'll get back to you
      <strong>within 1 business day</strong> via email.
    </p>

    <div class="contact-page__layout">
      <!-- Form -->
      <form class="contact-form" action="/api/contact" method="POST"
            novalidate aria-label="Contact form">

        <div class="form-group">
          <label for="contact-name">
            Full name <span aria-hidden="true">*</span>
          </label>
          <input type="text" id="contact-name" name="name"
                 required aria-required="true"
                 autocomplete="name" />
        </div>

        <div class="form-group">
          <label for="contact-email">
            Email address <span aria-hidden="true">*</span>
          </label>
          <input type="email" id="contact-email" name="email"
                 required aria-required="true"
                 autocomplete="email" />
        </div>

        <div class="form-group">
          <label for="contact-company">
            Company <span class="form-optional">(optional)</span>
          </label>
          <input type="text" id="contact-company" name="company"
                 autocomplete="organization" />
        </div>

        <div class="form-group">
          <label for="contact-message">
            Tell us about your project <span aria-hidden="true">*</span>
          </label>
          <p class="form-hint" id="message-hint">
            What are you looking to build? Include your timeline and
            budget range if you have them — even rough estimates help
            us prepare for our conversation.
          </p>
          <textarea id="contact-message" name="message" rows="6"
                    required aria-required="true"
                    aria-describedby="message-hint"></textarea>
        </div>

        <button type="submit" class="btn btn--primary">
          Send Message
        </button>
      </form>

      <!-- Alternative contact info -->
      <aside class="contact-info" aria-label="Other ways to reach us">
        <h2>Other Ways to Reach Us</h2>

        <div class="contact-info__item">
          <h3>Email</h3>
          <a href="mailto:hello@launchpadlab.com">hello@launchpadlab.com</a>
        </div>

        <div class="contact-info__item">
          <h3>Phone</h3>
          <a href="tel:+13125551234">(312) 555-1234</a>
        </div>

        <div class="contact-info__item">
          <h3>Office</h3>
          <address>
            123 N. Wacker Drive, Suite 400<br />
            Chicago, IL 60606
          </address>
        </div>

        <div class="contact-info__item">
          <h3>What happens next?</h3>
          <ol>
            <li>We review your message (within 1 business day).</li>
            <li>We reply via email to schedule a 30-minute call.</li>
            <li>On the call, we discuss your goals and how we can help.</li>
          </ol>
        </div>
      </aside>
    </div>
  </section>
</main>
```

### Post-submission confirmation

```html
<div class="form-success" role="status" aria-live="polite">
  <h2>Message Sent</h2>
  <p>
    Thank you! We've received your message and will reply
    <strong>within 1 business day</strong> to the email address you provided.
  </p>
  <h3>Here's what happens next:</h3>
  <ol>
    <li>Our team reviews your project details.</li>
    <li>We send you an email to schedule a 30-minute introductory call.</li>
    <li>On the call, we'll discuss your goals, timeline, and budget.</li>
  </ol>
  <p>
    In the meantime, check out some of
    <a href="/work/">our recent projects</a>.
  </p>
</div>
```

### Form validation

```javascript
const form = document.querySelector('.contact-form');

form.addEventListener('submit', (e) => {
  const errors = [];

  form.querySelectorAll('[required]').forEach(field => {
    const errorId = `${field.id}-error`;
    let errorEl = document.getElementById(errorId);

    if (!field.value.trim()) {
      e.preventDefault();

      if (!errorEl) {
        errorEl = document.createElement('p');
        errorEl.id = errorId;
        errorEl.className = 'form-error';
        errorEl.setAttribute('role', 'alert');
        field.parentNode.appendChild(errorEl);
      }

      const label = field.labels[0]?.textContent.replace('*', '').trim();
      errorEl.textContent = `Please enter your ${label.toLowerCase()}.`;
      field.setAttribute('aria-describedby',
        [field.getAttribute('aria-describedby'), errorId]
          .filter(Boolean).join(' '));
      field.setAttribute('aria-invalid', 'true');
      errors.push(field);
    } else if (errorEl) {
      errorEl.remove();
      field.removeAttribute('aria-invalid');
    }
  });

  if (errors.length) {
    errors[0].focus();
  }
});
```

### CSS for the contact page

```css
.contact-page__layout {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
  align-items: start;
  max-width: 72rem;
  margin: 0 auto;
}

@media (max-width: 768px) {
  .contact-page__layout {
    grid-template-columns: 1fr;
  }
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  font-weight: 600;
  margin-bottom: 0.375rem;
  font-size: 1rem;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 0.75rem;
  font-size: 1rem;
  border: 2px solid #ccc;
  border-radius: 6px;
  transition: border-color 0.2s ease;
}

.form-group input:focus,
.form-group textarea:focus {
  border-color: var(--color-primary);
  outline: 3px solid var(--color-focus-ring);
  outline-offset: 2px;
}

.form-group input[aria-invalid="true"],
.form-group textarea[aria-invalid="true"] {
  border-color: #d32f2f;
}

.form-hint {
  font-size: 0.875rem;
  color: #555;
  margin-bottom: 0.375rem;
  line-height: 1.5;
}

.form-error {
  color: #d32f2f;
  font-size: 0.875rem;
  margin-top: 0.25rem;
}

.form-success {
  padding: 2rem;
  background: #e8f5e9;
  border: 2px solid #4caf50;
  border-radius: 8px;
}
```

### Components to audit

| Component | Page(s) | What to fix |
|---|---|---|
| "Contact" nav link | All pages | Should link to `/contact/` page |
| Embedded contact forms | Homepage, Service pages | Replace with link to dedicated `/contact/` page or keep as secondary option |
| Post-submission message | Contact form | Add specific timeline, format, and next steps |
| Form field labels | All forms | Ensure proper `<label>` association |
| Form validation | All forms | Add accessible inline errors |

---

## Examples from Other Sites

### Thoughtbot (thoughtbot.com/hire-us)
- Dedicated hire/contact page with a clear form.
- Includes guidance: "Tell us a bit about your project, timeline, and budget."
- Post-submission: "Thanks! We'll respond within one business day."

### Basecamp (basecamp.com/support)
- Multiple contact options: form, email, Twitter.
- Sets expectations: "We respond to every message within an hour during business hours."

### Google Ventures (gv.com/contact)
- Minimal, focused page with just the form and clear instructions.
- Specifies what information to include and what to expect.

### Stripe (stripe.com/contact)
- Multiple channels: form, email, phone, chat.
- Categorized forms (Sales, Support, Partnerships) so the message reaches the right team.
- Clear response time expectations per channel.
