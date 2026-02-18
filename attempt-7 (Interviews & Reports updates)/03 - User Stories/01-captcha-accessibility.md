# Replace Image-Based CAPTCHA with an Accessible Alternative

## Priority: Critical

## User Story
As a user with visual or motor impairments, I want the contact form to use an accessible spam-prevention method so that I can submit my inquiry without being blocked by a CAPTCHA I cannot complete.

## Acceptance Criteria
- [ ] Contact form no longer displays image-based CAPTCHA (tile selection or similar)
- [ ] Form can be submitted successfully without completing a visual CAPTCHA challenge
- [ ] Spam prevention remains effective (honeypot, reCAPTCHA v3 score, or equivalent)
- [ ] Form is fully operable via keyboard only
- [ ] Screen reader users receive appropriate feedback during form submission
- [ ] Solution works across all contact form instances (homepage, contact page, AI Automation page, etc.)

## Developer Notes

### General Explanation
Image-based CAPTCHAs create significant barriers for users with visual impairments (who cannot perceive images), motor impairments (who struggle with precise mouse/touch targets), and cognitive impairments (who may find puzzles confusing). Replace with one or more of these approaches:

1. **reCAPTCHA v3** — Invisible, score-based. Runs in background; no user interaction required. Returns a score (0–1); set threshold on server.
2. **hCaptcha accessibility mode** — Offers audio challenges and other alternatives for users who cannot complete visual challenges.
3. **Honeypot field** — Hidden field that bots fill but humans don't. Simple, zero-friction.
4. **Time-based validation** — Reject submissions that complete too quickly (likely bots).

### Code Examples

**reCAPTCHA v3 (HTML/JS):**
```html
<!-- Add script -->
<script src="https://www.google.com/recaptcha/api.js?render=YOUR_SITE_KEY" async defer></script>

<form id="contact-form">
  <!-- form fields -->
  <input type="hidden" name="recaptcha_token" id="recaptcha-token">
  <button type="submit">Submit</button>
</form>

<script>
document.getElementById('contact-form').addEventListener('submit', async (e) => {
  e.preventDefault();
  const token = await grecaptcha.execute('YOUR_SITE_KEY', { action: 'contact' });
  document.getElementById('recaptcha-token').value = token;
  e.target.submit();
});
</script>
```

**Honeypot field (HTML/CSS):**
```html
<!-- Visually hidden but present in DOM for bots -->
<div class="hp-field" aria-hidden="true">
  <label for="website">Website</label>
  <input type="text" id="website" name="website" tabindex="-1" autocomplete="off">
</div>

<style>
.hp-field {
  position: absolute;
  left: -9999px;
  width: 1px;
  height: 1px;
  overflow: hidden;
}
</style>
```

**Server-side validation (pseudo-code):**
```javascript
// Reject if honeypot filled
if (req.body.website) return res.status(400).send('Spam detected');

// reCAPTCHA v3: verify token, check score
const response = await fetch('https://www.google.com/recaptcha/api/siteverify', {
  method: 'POST',
  body: new URLSearchParams({ secret: SECRET_KEY, response: token })
});
const { success, score } = await response.json();
if (!success || score < 0.5) return res.status(400).send('Verification failed');
```

### Components to Audit
- Contact form on homepage
- Contact form on dedicated contact page
- Contact form on AI Automation page
- Any other forms with CAPTCHA across the site

## Examples From Other Sites
- **Stripe** — Uses reCAPTCHA v3 (invisible) for fraud prevention on checkout flows; no user-facing CAPTCHA.
- **Shopify** — Employs honeypot fields and rate limiting; many stores use invisible reCAPTCHA v3 for additional protection.
- **gov.uk** — Avoids CAPTCHAs where possible; uses honeypots, time-based checks, and server-side validation. When CAPTCHA is required, they use accessible alternatives with audio options.

## References
- Main Report Item 1 (Critical Priority)
- Interview feedback: users with progressive lenses and wrist strain reported difficulty with image-based CAPTCHA
- Primary conversion action (contact form submission) at risk of being blocked
