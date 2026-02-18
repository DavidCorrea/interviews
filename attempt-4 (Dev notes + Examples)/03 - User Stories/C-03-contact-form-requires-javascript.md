# C-03: Contact Form Requires JavaScript with No Fallback

**Priority:** Critical
**WCAG Criteria:** 4.1.2 Name, Role, Value (A), 1.3.1 Info and Relationships (A), 3.3.2 Labels or Instructions (A)
**Affected Personas:** ADHD, Cognitive Disability, Dyslexic, Low Vision, Motor Impairment, Non-Native Speaker, Screen Reader, Senior Person, Skeptical User, Voice Control

---

## User Story

**As a** user with JavaScript disabled, a slow connection, or assistive technology that struggles with JS-heavy forms,
**I want** the contact form to either work without JavaScript or provide clear alternative contact methods (phone, email) within the `<noscript>` fallback,
**so that** I always have a way to reach the company regardless of my browser configuration or connection quality.

---

## Acceptance Criteria

- [ ] The `<noscript>` block includes at least one actionable alternative: a `mailto:` link and/or a clickable `tel:` phone link.
- [ ] The fallback text explains what happened ("This form requires JavaScript") and provides the alternative contact methods prominently.
- [ ] The alternative contact info (email and phone) is styled clearly and is not buried or small.
- [ ] If feasible, a basic HTML-only form is provided as a fallback that submits via standard `POST` to a server-side handler.
- [ ] When JavaScript IS enabled, the Ninja Forms form renders with proper `<label>` elements associated to each input via `for`/`id` pairing.
- [ ] The form's accessible name, roles, and values are correct when inspected via assistive technology.

---

## How to Test the Change

### Manual Testing

1. **Disable JavaScript:**
   - In Chrome DevTools → Settings → Debugger → check "Disable JavaScript."
   - Navigate to the Contact page.
   - Verify the `<noscript>` content is visible and contains email/phone links.
   - Click the email link — verify it opens a mail client.
   - Click the phone link — verify it initiates a call (on mobile) or shows the number.

2. **Re-enable JavaScript:**
   - Confirm the Ninja Forms form renders correctly.
   - Tab through all form fields — verify each has a visible label and correct focus behavior.
   - Use a screen reader to verify each field is announced with its label.

3. **Slow Connection Simulation:**
   - In DevTools → Network → Throttle to "Slow 3G."
   - Load the Contact page and observe what users see while JS is loading.

### Automated Testing

```javascript
// Playwright test — verify noscript fallback
test('noscript block contains contact alternatives', async ({ browser }) => {
  const context = await browser.newContext({ javaScriptEnabled: false });
  const page = await context.newPage();
  await page.goto('https://launchpadlab.com/contact/');

  // Check for mailto link
  const mailtoLink = page.locator('noscript a[href^="mailto:"]');
  await expect(mailtoLink).toBeVisible();

  // Check for tel link
  const telLink = page.locator('noscript a[href^="tel:"]');
  await expect(telLink).toBeVisible();

  await context.close();
});
```

---

## Developer Notes

### General Approach

Replace the current `<noscript>` message that only says "JavaScript is required" with a helpful fallback that includes the company's email address and phone number as clickable links. Optionally, provide a plain HTML form that submits server-side.

### Code Examples

**Before (current state):**

```html
<noscript>
  JavaScript is required to submit this form.
</noscript>
```

**After (improved fallback):**

```html
<noscript>
  <div class="noscript-fallback" style="padding: 2rem; background: #f5f5f5; border-radius: 8px; text-align: center;">
    <h3>Contact Us Directly</h3>
    <p>This form requires JavaScript to load. You can reach us directly:</p>
    <ul style="list-style: none; padding: 0; margin: 1rem 0;">
      <li style="margin-bottom: 0.75rem;">
        <strong>Email:</strong>
        <a href="mailto:hello@launchpadlab.com">hello@launchpadlab.com</a>
      </li>
      <li>
        <strong>Phone:</strong>
        <a href="tel:+13128889651">312-888-9651</a>
      </li>
    </ul>
  </div>
</noscript>
```

**Optional: Server-side HTML fallback form:**

```html
<noscript>
  <form action="/contact-handler.php" method="POST" class="fallback-form">
    <label for="fallback-name">Name</label>
    <input type="text" id="fallback-name" name="name" required>

    <label for="fallback-email">Email</label>
    <input type="email" id="fallback-email" name="email" required>

    <label for="fallback-message">Message</label>
    <textarea id="fallback-message" name="message" required></textarea>

    <button type="submit">Send Message</button>
  </form>
</noscript>
```

### Components/Files to Audit

- Contact page template (likely `page-contact.php` or a page builder layout).
- Ninja Forms shortcode / embed block — locate the `<noscript>` block.
- `functions.php` or plugin settings — Ninja Forms configuration.
- Server-side contact form handler (if implementing the HTML form fallback).

---

## Examples from Other Sites

| Site | Implementation |
|------|----------------|
| **gov.uk** | All forms work without JavaScript. Progressive enhancement adds validation, but the base form submits via standard HTML POST. |
| **Basecamp** | Contact page includes a prominent email address and phone number above the contact form as a non-JS alternative. |
| **Stripe** | JS-dependent forms include a clear fallback message with email support address: "Having trouble? Email us at support@stripe.com." |
| **Netlify** | Supports HTML form submissions server-side even for static sites, ensuring no-JS users can submit forms. |
