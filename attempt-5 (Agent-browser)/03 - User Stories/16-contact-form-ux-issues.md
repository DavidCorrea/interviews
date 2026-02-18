# 16. Fix Contact Form UX Issues: Guidance, reCAPTCHA, and Duplication

**Priority:** Medium
**Location:** All contact forms across the site
**Reported by:** Jamie Rivera (ADHD), Richard Okonkwo (Non-Technical Business Executive)

---

## User Story

**As a** prospective client ready to reach out,
**I want** a contact form that clearly guides me on what to write, doesn't add unnecessary friction, and appears only once per page
**so that** I can quickly and confidently submit my inquiry without decision paralysis, frustration, or confusion about which form to use.

---

## Acceptance Criteria

### A. Field Guidance
- [ ] The "How Can We Help You?" textarea includes placeholder text with examples (e.g., "Tell us about your project — what problem are you solving, your timeline, and any budget range")
- [ ] Placeholder text disappears on focus (standard browser behavior) and does not replace a proper `<label>`
- [ ] Optionally, a helper text block appears below the label with 2-3 prompt suggestions
- [ ] The field label is associated with the textarea via `for`/`id` attributes

### B. reCAPTCHA
- [ ] The visible reCAPTCHA v2 checkbox ("I'm not a robot") is replaced with invisible reCAPTCHA v3
- [ ] reCAPTCHA v3 runs in the background without any visible UI element
- [ ] A small privacy/terms notice appears near the submit button (required by Google reCAPTCHA v3 terms)
- [ ] Form submission still validates against spam/bots effectively
- [ ] Users are never interrupted with image-selection challenges under normal conditions

### C. Duplicate Form Removal
- [ ] The Contact page (`/contact/`) contains exactly one contact form
- [ ] If a secondary form existed at the bottom of the Contact page, it is removed
- [ ] The remaining form is positioned prominently (above the fold or immediately below introductory text)
- [ ] Other pages that embed contact forms (Homepage, Services, etc.) still function correctly

---

## How to Test

### Field Guidance
1. Navigate to `/contact/`
2. Locate the "How Can We Help You?" field
3. Verify placeholder text is visible before the user begins typing
4. Click into the field — confirm placeholder disappears and does not interfere with typing
5. Tab to the field using keyboard only — confirm the label is announced by screen readers (VoiceOver: `VO + Shift + Down Arrow` to inspect form controls)
6. Verify helper text (if implemented) is programmatically associated with the field via `aria-describedby`

### reCAPTCHA
1. Navigate to any page with a contact form
2. Confirm no visible reCAPTCHA checkbox appears
3. Fill out the form with valid data and submit
4. Verify the form submits successfully without any CAPTCHA challenge
5. Check the browser's Network tab — confirm a request to `google.com/recaptcha` with `v3` parameters
6. Check the page source — confirm the reCAPTCHA v3 site key is loaded, not v2
7. Verify the privacy/terms badge or text notice is present near the submit button

### Duplicate Form
1. Navigate to `/contact/`
2. Scroll through the entire page
3. Count the number of contact forms — there should be exactly one
4. Submit the form — confirm it works correctly
5. Navigate to the Homepage and Services page — confirm their embedded forms still work

### Accessibility
1. Navigate the entire form using keyboard only (Tab, Shift+Tab, Enter)
2. Confirm all form fields are reachable and operable
3. Use a screen reader to verify all labels, helper text, and error messages are announced
4. Submit the form with empty required fields — confirm error messages are announced and focus moves to the first error

---

## Developer Notes

### A. Adding Field Guidance

Replace the bare textarea with guided markup:

```html
<div class="form-group">
  <label for="message" class="form-label">
    How Can We Help You?
  </label>
  <p id="message-hint" class="form-hint">
    A few sentences is perfect. For example:
    "We need a web app for inventory management. Our timeline is 3-6 months and our budget is around $200K."
  </p>
  <textarea
    id="message"
    name="message"
    class="form-textarea"
    rows="5"
    placeholder="Tell us about your project, timeline, and any budget range..."
    aria-describedby="message-hint"
    required
  ></textarea>
</div>
```

```css
.form-hint {
  font-size: 0.875rem;
  line-height: 1.6;
  color: #666666;
  margin-top: 0.25rem;
  margin-bottom: 0.5rem;
  font-style: italic;
}

.form-textarea {
  width: 100%;
  min-height: 120px;
  padding: 0.75rem 1rem;
  font-size: 1rem;
  line-height: 1.6;
  border: 1px solid #cccccc;
  border-radius: 6px;
  font-family: inherit;
  resize: vertical;
}

.form-textarea:focus {
  outline: 2px solid #1a73e8;
  outline-offset: 2px;
  border-color: #1a73e8;
}

.form-textarea::placeholder {
  color: #999999;
  font-style: italic;
}
```

#### Alternative: Dropdown for Project Type

For users who experience decision paralysis, a structured dropdown can reduce the open-endedness:

```html
<div class="form-group">
  <label for="project-type" class="form-label">What type of project?</label>
  <select id="project-type" name="project_type" class="form-select">
    <option value="" disabled selected>Choose one...</option>
    <option value="new-app">Build a new application</option>
    <option value="modernize">Modernize an existing system</option>
    <option value="mobile">Mobile app development</option>
    <option value="ai">AI or data project</option>
    <option value="strategy">Product strategy or consulting</option>
    <option value="other">Something else</option>
  </select>
</div>
```

### B. Replacing reCAPTCHA v2 with v3

#### Step 1: Remove reCAPTCHA v2

Remove the existing v2 script tag and the `<div class="g-recaptcha">` element from the form.

```html
<!-- REMOVE THIS -->
<script src="https://www.google.com/recaptcha/api.js" async defer></script>
<div class="g-recaptcha" data-sitekey="YOUR_V2_SITE_KEY"></div>
```

#### Step 2: Add reCAPTCHA v3

```html
<script src="https://www.google.com/recaptcha/api.js?render=YOUR_V3_SITE_KEY"></script>
```

#### Step 3: Generate Token on Submit

```javascript
document.querySelector('.contact-form').addEventListener('submit', function (e) {
  e.preventDefault();
  const form = this;

  grecaptcha.ready(function () {
    grecaptcha.execute('YOUR_V3_SITE_KEY', { action: 'contact_form' })
      .then(function (token) {
        let input = form.querySelector('input[name="g-recaptcha-response"]');
        if (!input) {
          input = document.createElement('input');
          input.type = 'hidden';
          input.name = 'g-recaptcha-response';
          form.appendChild(input);
        }
        input.value = token;
        form.submit();
      });
  });
});
```

#### Step 4: Server-Side Verification

```javascript
// Node.js / Express example
const axios = require('axios');

async function verifyRecaptcha(token) {
  const response = await axios.post(
    'https://www.google.com/recaptcha/api/siteverify',
    null,
    {
      params: {
        secret: process.env.RECAPTCHA_V3_SECRET_KEY,
        response: token,
      },
    }
  );

  const { success, score, action } = response.data;

  // score ranges from 0.0 (bot) to 1.0 (human)
  // 0.5 is Google's recommended threshold
  return success && score >= 0.5 && action === 'contact_form';
}
```

#### Step 5: Add Required Privacy Notice

Google requires a visible notice when using reCAPTCHA v3:

```html
<p class="recaptcha-notice">
  This site is protected by reCAPTCHA and the Google
  <a href="https://policies.google.com/privacy" target="_blank" rel="noopener">Privacy Policy</a> and
  <a href="https://policies.google.com/terms" target="_blank" rel="noopener">Terms of Service</a> apply.
</p>
```

```css
.recaptcha-notice {
  font-size: 0.75rem;
  color: #888888;
  margin-top: 0.5rem;
  line-height: 1.5;
}

.recaptcha-notice a {
  color: #1a73e8;
  text-decoration: underline;
}
```

### C. Removing the Duplicate Form

Audit the Contact page template. If two form components are rendered, remove the second instance. In a React/Next.js codebase:

```jsx
// BEFORE — Contact page with duplicate forms
export default function ContactPage() {
  return (
    <>
      <HeroSection />
      <ContactForm />       {/* Primary form — keep this */}
      <TestimonialsSection />
      <ContactForm />       {/* Duplicate form — REMOVE this */}
    </>
  );
}

// AFTER — Single form
export default function ContactPage() {
  return (
    <>
      <HeroSection />
      <ContactForm />
      <TestimonialsSection />
      {/* CTA linking back to the form above, instead of a duplicate */}
      <section className="cta-section">
        <h2>Ready to start?</h2>
        <a href="#contact-form" className="cta-button">
          Go to contact form
        </a>
      </section>
    </>
  );
}
```

### Components to Audit

- **Contact page template** — Identify and remove the duplicate form instance
- **Shared `ContactForm` component** — Add `aria-describedby`, placeholder text, and helper text to the message field
- **reCAPTCHA integration** — Likely in a shared form component or layout-level script; update from v2 to v3 sitewide
- **Form validation logic** — Ensure error messages are accessible (use `aria-live="polite"` regions or `aria-invalid` on fields)
- **Homepage, Services page, Industries page** — Verify embedded forms still work after the reCAPTCHA change

### WCAG References

- **WCAG 2.1 SC 1.3.1 Info and Relationships (A):** Form labels, helper text, and error messages must be programmatically associated with their controls
- **WCAG 2.1 SC 3.3.2 Labels or Instructions (A):** When user input is required, labels or instructions must be provided — the "How Can We Help You?" field needs guidance
- **WCAG 2.1 SC 3.3.5 Help (AAA):** Context-sensitive help is available — placeholder text and helper prompts address this
- **WCAG 2.1 SC 2.4.6 Headings and Labels (AA):** Labels must describe topic or purpose

---

## Examples from Other Sites

### Basecamp (basecamp.com/contact)
Uses a clean, single-form contact page with a project type dropdown and a message field that includes placeholder text: "Tell us about your project...". No visible CAPTCHA. The form is the entire focus of the page.

### Thoughtbot (thoughtbot.com/hire-us)
Their inquiry form asks structured questions: "What's the project?", "What's the timeline?", "What's the budget range?" as separate fields rather than one open-ended textarea. This eliminates decision paralysis by breaking the task into small, answerable questions.

### Tighten (tighten.com/contact)
Provides checkboxes for project type (New App, Existing App, Staff Augmentation, etc.) before the open-ended field. This gives users a mental framework before writing, reducing cognitive load.

### HubSpot (hubspot.com)
Uses invisible reCAPTCHA across all their forms — no checkbox, no image challenges. The transition from v2 to v3 is seamless from the user's perspective. Their forms convert at industry-leading rates partly because friction is minimized.

### Key Patterns
1. **Structured inputs reduce paralysis** — dropdowns and checkboxes before open text fields
2. **Invisible spam protection** — reCAPTCHA v3 or honeypot fields instead of visible challenges
3. **One form per page** — a single clear conversion point, not competing forms
4. **Helper text normalizes responses** — showing example answers makes users feel confident their message is "good enough"
