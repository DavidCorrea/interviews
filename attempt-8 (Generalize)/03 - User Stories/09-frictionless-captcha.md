# User Story: Replace Visible CAPTCHA with Frictionless Alternative

**Priority:** Low  
**Related Finding:** [Finding 9](../main-report.md#finding-9)

## Story
As a user trying to contact the agency, I want the contact form to protect against spam without requiring me to solve a visual challenge, so that the submission process is fast, accessible, and frictionless.

## Context
The contact form includes a visible CAPTCHA iframe (likely reCAPTCHA v2). While necessary for spam prevention, visible CAPTCHAs add friction to the user experience and are a known accessibility barrier — particularly for users with visual impairments, motor disabilities, or cognitive differences. Modern alternatives achieve the same spam protection with zero user interaction.

## Acceptance Criteria
- The visible CAPTCHA challenge is removed from the contact form
- An invisible spam protection method is implemented (reCAPTCHA v3, Cloudflare Turnstile, or honeypot fields)
- The form still effectively prevents spam submissions
- The form meets WCAG 2.1 AA standards for accessibility
- No visual challenge or checkbox appears to the user

## How to Test
1. Navigate to the contact page
2. Confirm no visible CAPTCHA element appears in the form
3. Submit the form — confirm it goes through without a visual challenge
4. Test with a screen reader — confirm no CAPTCHA-related announcements
5. Monitor spam submissions for 2 weeks post-deployment to verify protection still works

## Developer Notes

### General Approach
Replace the visible reCAPTCHA v2 widget with reCAPTCHA v3 (score-based, invisible), Cloudflare Turnstile (privacy-focused invisible challenge), or a honeypot field technique. Can also combine multiple methods.

### Components to Audit
- Contact form component (all instances — footer and Contact page)
- Form submission handler (backend)
- reCAPTCHA script tags in `<head>`
- Any form builder configuration (HubSpot, etc.)

### Code Examples

**Option A: reCAPTCHA v3 (invisible, score-based)**
```html
<!-- In <head> -->
<script src="https://www.google.com/recaptcha/api.js?render=YOUR_SITE_KEY"></script>

<!-- In form submission handler -->
<script>
function onSubmit(e) {
  e.preventDefault();
  grecaptcha.ready(function() {
    grecaptcha.execute('YOUR_SITE_KEY', { action: 'contact' }).then(function(token) {
      document.getElementById('recaptcha-token').value = token;
      document.getElementById('contact-form').submit();
    });
  });
}
</script>
<input type="hidden" id="recaptcha-token" name="g-recaptcha-response" />
```

**Option B: Honeypot field (no external dependency)**
```html
<!-- Hidden field that bots will fill but humans won't -->
<div style="position: absolute; left: -9999px;" aria-hidden="true">
  <label for="website">Website</label>
  <input type="text" id="website" name="website" tabindex="-1" autocomplete="off" />
</div>
```

```python
# Server-side: reject if honeypot field is filled
if request.POST.get('website'):
    return HttpResponse(status=400)  # Bot detected
```

**Option C: Cloudflare Turnstile (privacy-focused)**
```html
<script src="https://challenges.cloudflare.com/turnstile/v0/api.js" async defer></script>
<div class="cf-turnstile" data-sitekey="YOUR_SITE_KEY" data-theme="light"></div>
```

## How Other Sites Achieve This
- **Linear** (linear.app) — contact form uses no visible CAPTCHA; relies on rate limiting and server-side detection
- **Vercel** — forms use invisible reCAPTCHA v3 with no user-facing challenge
- **Stripe** — contact forms use honeypot fields combined with behavioral analysis, no visible CAPTCHA
