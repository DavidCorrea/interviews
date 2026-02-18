# M-42: reCAPTCHA Inaccessible at Magnification/Voice

**Issue ID:** M-42
**Priority:** Medium
**WCAG Criteria:** 1.1.1 Non-text Content (A), 2.1.1 Keyboard (A)
**Affected Personas:** Low Vision Screen Magnifier, Voice Control

---

## User Story

As a **user who relies on screen magnification or voice control**, I want **the contact form's spam protection to be usable without solving a visual image puzzle** so that **I can submit the form without being blocked by a challenge that is impossible for me to complete.**

---

## Acceptance Criteria

- [ ] The current image-grid reCAPTCHA (v2) is replaced with a less intrusive alternative (reCAPTCHA v3 invisible, hCaptcha accessible mode, or a server-side honeypot).
- [ ] If reCAPTCHA v2 must be retained, the audio challenge alternative is verified to work with voice control and screen magnification.
- [ ] The CAPTCHA solution is usable at 300% and 400% browser zoom without horizontal scrolling or cropped content.
- [ ] Voice control users can complete the form and submit it without encountering untargetable elements.
- [ ] The `<iframe>` containing the CAPTCHA has an accessible `title` attribute (e.g., `title="reCAPTCHA verification"`).

---

## How to Test the Change

### Manual Testing

1. Navigate to the Contact page.
2. Zoom to 300% and 400% in the browser.
3. Attempt to complete the CAPTCHA challenge at each zoom level.
4. If using reCAPTCHA v3 (invisible), verify the form can be submitted without any visual CAPTCHA interaction.
5. If using reCAPTCHA v2, click the audio alternative and verify it plays and accepts voice/keyboard input.
6. Test with macOS Voice Control or Dragon NaturallySpeaking — attempt to target and complete the CAPTCHA.
7. Verify the CAPTCHA iframe has a `title` attribute visible to screen readers.

### Automated Testing

1. Run axe DevTools on the Contact page — check for iframe labeling issues and keyboard accessibility flags.
2. Verify the CAPTCHA iframe has a title:
   ```javascript
   const iframe = document.querySelector('iframe[src*="recaptcha"]');
   console.log('Title:', iframe?.title); // Should not be empty
   ```
3. Run a Lighthouse accessibility audit on the Contact page.

---

## Developer Notes

### General Explanation

The Google reCAPTCHA v2 image grid challenge requires users to identify objects in a 3x3 or 4x4 image grid. At high magnification (300%+), the grid tiles become tiny and require scrolling within the already-constrained iframe. Voice control users cannot target individual grid cells because they lack text labels. The recommended solution is to migrate to reCAPTCHA v3 (score-based, invisible) or implement a server-side honeypot technique that requires no user interaction.

### Code Examples

**Option A — Migrate to reCAPTCHA v3 (recommended):**
```html
<!-- Replace v2 script with v3 -->
<script src="https://www.google.com/recaptcha/api.js?render=YOUR_V3_SITE_KEY"></script>

<script>
grecaptcha.ready(function() {
  grecaptcha.execute('YOUR_V3_SITE_KEY', { action: 'contact_form' })
    .then(function(token) {
      document.getElementById('recaptcha-token').value = token;
    });
});
</script>

<form>
  <input type="hidden" id="recaptcha-token" name="g-recaptcha-response">
  <!-- No visible CAPTCHA widget needed -->
</form>
```

**Server-side verification (PHP/WordPress):**
```php
$response = wp_remote_post('https://www.google.com/recaptcha/api/siteverify', [
  'body' => [
    'secret' => RECAPTCHA_V3_SECRET,
    'response' => $_POST['g-recaptcha-response'],
  ],
]);
$result = json_decode(wp_remote_retrieve_body($response), true);
if ($result['success'] && $result['score'] >= 0.5) {
  // Process form submission
}
```

**Option B — Honeypot technique (no CAPTCHA needed):**
```html
<!-- Hidden field that bots will fill in -->
<div style="position: absolute; left: -9999px;" aria-hidden="true">
  <label for="website">Leave this empty</label>
  <input type="text" id="website" name="website" tabindex="-1" autocomplete="off">
</div>
```

```php
// Server-side: reject submissions where honeypot is filled
if (!empty($_POST['website'])) {
  wp_die('Spam detected.');
}
```

**If keeping reCAPTCHA v2, ensure the iframe is labeled:**
```html
<div class="g-recaptcha"
  data-sitekey="YOUR_SITE_KEY"
  data-callback="onCaptchaSuccess"
  role="group"
  aria-label="Spam verification">
</div>
```

### Components / Files to Audit

- Contact page template (PHP/HTML)
- Ninja Forms reCAPTCHA integration settings
- `functions.php` — reCAPTCHA script enqueue
- Google reCAPTCHA admin console (recaptcha.google.com) — site key configuration
- Form submission handler (server-side validation)

---

## Examples from Other Sites

- **Stripe.com:** Uses no visible CAPTCHA at all — relies on invisible reCAPTCHA v3 combined with server-side fraud detection.
- **GOV.UK:** Explicitly prohibits CAPTCHA on government forms. Uses server-side rate limiting and honeypot fields instead.
- **Basecamp:** Uses a honeypot field technique instead of any CAPTCHA, citing accessibility as the primary reason.
- **Shopify:** Uses reCAPTCHA v3 (invisible) on all checkout and contact forms, with no user-facing challenge.
