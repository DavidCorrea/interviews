# L-53: Footer Phone Link Malformed HTML

**Issue ID:** L-53
**Priority:** Low
**WCAG Criteria:** 4.1.1 Parsing (A)
**Affected Personas:** Screen Reader, Senior Person, Skeptical User

---

## User Story

As a **screen reader user**, I want the footer phone number link to have valid HTML so that my assistive technology can reliably identify and activate the link to call the company.

---

## Acceptance Criteria

- [ ] The footer phone link `href` attribute contains exactly one opening and one closing double-quote with no extra quote characters.
- [ ] The rendered HTML passes W3C validation with zero parsing errors on the phone link element.
- [ ] Clicking/activating the phone link correctly initiates a `tel:` action (opens phone dialer or softphone) on desktop and mobile.
- [ ] Screen readers (NVDA, VoiceOver, JAWS) announce the link as a phone number and allow activation without errors.
- [ ] The phone number displayed visually matches the number in the `href` value.

---

## How to Test the Change

### Manual Testing
1. Navigate to the footer of any page on launchpadlab.com.
2. Right-click the phone number link and select **Inspect Element**.
3. Verify the `href` attribute reads `href="tel:312-888-9651"` (single closing quote — no doubled `""`).
4. Click the link on a mobile device and confirm it opens the phone dialer with the correct number.
5. Click the link on desktop and confirm it triggers the OS phone/softphone handler.
6. Test with VoiceOver (macOS/iOS):
   - Navigate to the footer link.
   - Confirm it announces as a phone number link.
   - Activate it and verify correct behavior.
7. Test with NVDA (Windows):
   - Tab to the footer phone link.
   - Confirm announcement and activation.

### Automated Testing
1. Run the W3C HTML validator on the page:
   ```bash
   curl -s "https://validator.w3.org/nu/?doc=https://launchpadlab.com/&out=json" | jq '.messages[] | select(.type=="error")'
   ```
2. Add a DOM assertion in your test suite:
   ```javascript
   // Example: Playwright or Cypress
   const phoneLink = await page.$('footer a[href^="tel:"]');
   const href = await phoneLink.getAttribute('href');
   expect(href).toBe('tel:312-888-9651');
   expect(href).not.toContain('""');
   ```
3. Run `htmlhint` or `axe-core` as part of CI to catch malformed attributes.

---

## Developer Notes

### General Explanation
The footer phone link has a double closing quote in the `href` attribute: `href="tel:312-888-9651""`. The extra `"` character after the closing quote creates invalid HTML. While most modern browsers silently recover from this, it can cause unpredictable behavior in assistive technologies and older browsers.

### Where to Look
- **Footer template:** Search for the phone link in the WordPress theme footer template:
  ```bash
  grep -rn 'tel:' wp-content/themes/*/footer.php
  grep -rn 'tel:' wp-content/themes/*/template-parts/footer*
  ```
- **WordPress widgets/customizer:** The phone number may be in a widget, customizer field, or ACF (Advanced Custom Fields) option.
- **Hardcoded in theme:** Check `footer.php`, `footer-contact.php`, or similar partials.

### Code Fix

```html
<!-- BEFORE (malformed) -->
<a href="tel:312-888-9651"">312-888-9651</a>

<!-- AFTER (correct) -->
<a href="tel:312-888-9651">312-888-9651</a>
```

If the phone number is generated dynamically:
```php
<!-- BEFORE -->
<a href="tel:<?php echo $phone; ?>"">

<!-- AFTER -->
<a href="tel:<?php echo esc_attr( $phone ); ?>">
```

Note the use of `esc_attr()` — this both fixes the quoting and adds proper escaping for security.

### Components/Files to Audit
- `footer.php` or footer template partial
- WordPress Customizer settings for contact info
- ACF options page fields (if used)
- Any widget outputting phone contact info
- Check for similar issues on other `tel:` or `mailto:` links site-wide

---

## Examples from Other Sites

- **Apple:** Footer phone links use clean `<a href="tel:1-800-275-2273">` with no extra attributes or malformed quotes.
- **HubSpot:** Phone links in the footer include both `href="tel:..."` and visible formatting — `<a href="tel:+1-888-482-7768">+1-888-482-7768</a>`.
- **W3C best practice:** The `tel:` URI scheme is standardized in [RFC 3966](https://www.rfc-editor.org/rfc/rfc3966) — the `href` should contain only the URI with no extraneous characters.

---

## Additional Context

While browsers are forgiving of this specific HTML error, it reflects poorly on code quality and could cause subtle issues for assistive technologies that parse attributes more strictly. This is a one-character fix that should take less than 5 minutes.
