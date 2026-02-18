# reCAPTCHA Accessibility

**Priority:** Medium

## User Story

As a user who relies on keyboard navigation or assistive technology, I want the bot-prevention mechanism on contact forms to be accessible and non-intrusive, so that I can submit the form without being blocked by an inaccessible CAPTCHA challenge.

## Acceptance Criteria

- [ ] The reCAPTCHA iframe has a descriptive `title` attribute (e.g., `title="reCAPTCHA verification"`)
- [ ] Keyboard users can tab through the form without getting trapped in the CAPTCHA iframe
- [ ] Ideally, the visible CAPTCHA challenge is removed in favor of reCAPTCHA v3 (invisible, score-based) or an accessible alternative
- [ ] If a visible CAPTCHA must remain, the audio alternative is functional and clearly labeled
- [ ] Form submission works for users with screen readers
- [ ] Bot prevention does not create a barrier for legitimate users

## How to Test

1. Navigate to any page with the contact form
2. Tab through the form fields — verify the reCAPTCHA area is reachable and navigable by keyboard
3. Inspect the iframe in DevTools — confirm a `title` attribute is present and descriptive
4. Use a screen reader (VoiceOver/NVDA) — verify the CAPTCHA purpose is announced
5. If using reCAPTCHA v3: confirm no visible challenge appears and the form submits successfully
6. If using reCAPTCHA v2: verify the audio challenge is available and functional
7. Test form submission with assistive technology — confirm it completes without errors

## Developer Notes

### General Approach

The best solution is to upgrade from reCAPTCHA v2 (checkbox/challenge) to reCAPTCHA v3 (invisible, score-based) or an accessible alternative like Cloudflare Turnstile. reCAPTCHA v3 runs entirely in the background, assigning a risk score without requiring any user interaction.

If the visible CAPTCHA must remain, at minimum add a `title` attribute to the iframe.

### Option 1: Upgrade to reCAPTCHA v3 (Recommended)

```html
<!-- Load reCAPTCHA v3 -->
<script src="https://www.google.com/recaptcha/api.js?render=YOUR_SITE_KEY"></script>

<form id="contact-form">
  <!-- form fields -->
  <input type="hidden" name="recaptcha_token" id="recaptcha-token">
  <button type="submit">Send Message</button>
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

Server-side: verify the token and check the score (0.0 = bot, 1.0 = human). Reject submissions below your threshold (typically 0.5).

### Option 2: Cloudflare Turnstile (Alternative)

```html
<div class="cf-turnstile" data-sitekey="YOUR_SITE_KEY" data-theme="light"></div>
<script src="https://challenges.cloudflare.com/turnstile/v0/api.js" async defer></script>
```

Turnstile is designed to be more accessible than reCAPTCHA. It often resolves without user interaction and has better screen reader support.

### Option 3: Label the Existing iframe (Minimum Fix)

```html
<iframe title="reCAPTCHA verification — check the box to confirm you are not a robot" src="..."></iframe>
```

### Option 4: Honeypot Field (Supplementary)

```html
<div style="position: absolute; left: -9999px;" aria-hidden="true">
  <label for="website">Leave this field empty</label>
  <input type="text" id="website" name="website" tabindex="-1" autocomplete="off">
</div>
```

Server-side: reject submissions where the honeypot field is filled.

### Components to Audit

- Contact form component (all pages)
- HubSpot form embed configuration (if forms are HubSpot-powered)
- reCAPTCHA integration code
- Server-side form handling for token verification

## Examples from Other Sites

- **Stripe.com** — Uses custom bot detection without any visible CAPTCHA. Forms are clean and fully keyboard-accessible.
- **Cloudflare.com** — Uses their own Turnstile product, which resolves invisibly in most cases. When a challenge is needed, it's more accessible than traditional CAPTCHAs.
- **GitHub.com** — Uses invisible bot protection on signup/login forms. No visible CAPTCHA widget.
- **GOV.UK** — Government forms use honeypot fields and server-side rate limiting instead of CAPTCHAs, ensuring maximum accessibility.
- **Linear.app** — Contact/signup forms use invisible bot protection with no user-facing CAPTCHA.
