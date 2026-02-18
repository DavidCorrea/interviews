# M-46: No Phone Number in Site Header

**Issue ID:** M-46
**Priority:** Medium
**WCAG Criteria:** 2.4.5 Multiple Ways (AA)
**Affected Personas:** Big Company Owner, Senior Person

---

## User Story

As a **senior user or enterprise decision-maker**, I want **a phone number or direct contact method to be visible in the site header** so that **I can quickly call or email the company without having to scroll to the footer or navigate to a separate Contact page.**

---

## Acceptance Criteria

- [ ] A clickable phone number (using `tel:` link) is displayed in the site header, visible on desktop viewports.
- [ ] An email address (using `mailto:` link) is also available in the header or immediately accessible from it.
- [ ] On mobile viewports, the phone number remains accessible — either visible in the mobile header or as the first item in the mobile menu.
- [ ] The phone link uses proper semantic markup: `<a href="tel:+13128889651">312-888-9651</a>`.
- [ ] The header contact information is consistent with the phone number/email in the footer and Contact page.
- [ ] The phone number has a clear visual label (e.g., phone icon + number, or "Call Us: 312-888-9651").

---

## How to Test the Change

### Manual Testing

1. Open the homepage on a desktop browser.
2. Verify the phone number is visible in the header without scrolling.
3. Click the phone number link — verify it triggers the device's phone/dialer interface.
4. Resize to mobile width (375px) — verify the phone number is accessible (either visible or first item in mobile menu).
5. Use VoiceOver or NVDA — verify the phone link is announced with its number and purpose.
6. Navigate to 3–4 different pages — verify the phone number is present in the header on all pages.

### Automated Testing

1. Run a DOM check for phone link presence in header:
   ```javascript
   const header = document.querySelector('header, .site-header, #masthead');
   const phoneLink = header?.querySelector('a[href^="tel:"]');
   console.log('Phone in header:', phoneLink ? phoneLink.href : 'MISSING');
   ```
2. Run axe DevTools — verify no accessibility issues with the new header contact elements.
3. Visual regression test (Percy/BackstopJS) to confirm the header layout is clean with the addition.

---

## Developer Notes

### General Explanation

The company phone number is currently only available in the footer and buried on the Contact page (below the form and testimonials). Enterprise buyers and older users expect to find contact information prominently in the header — it's a trust signal and a convenience feature. Adding a phone number to the header provides an immediate, low-friction contact method and satisfies WCAG 2.4.5 (Multiple Ways) by offering an alternative path to reach the company.

### Code Examples

**Desktop header addition:**
```html
<header class="site-header">
  <div class="header-top-bar">
    <a href="tel:+13128889651" class="header-phone">
      <svg aria-hidden="true" class="icon-phone"><!-- phone icon SVG --></svg>
      <span>312-888-9651</span>
    </a>
    <a href="mailto:hello@launchpadlab.com" class="header-email">
      <svg aria-hidden="true" class="icon-email"><!-- email icon SVG --></svg>
      <span>hello@launchpadlab.com</span>
    </a>
  </div>
  <nav class="primary-nav">
    <!-- existing navigation -->
  </nav>
</header>
```

**CSS for header contact bar:**
```css
.header-top-bar {
  display: flex;
  justify-content: flex-end;
  gap: 1.5rem;
  padding: 0.5rem 2rem;
  background: #F5F5F5;
  font-size: 0.875rem;
}

.header-phone,
.header-email {
  display: flex;
  align-items: center;
  gap: 0.375rem;
  color: #333333;
  text-decoration: none;
}

.header-phone:hover,
.header-email:hover {
  text-decoration: underline;
}

.icon-phone,
.icon-email {
  width: 16px;
  height: 16px;
}

/* Mobile: show phone, hide email to save space */
@media (max-width: 768px) {
  .header-email {
    display: none;
  }
  .header-phone {
    font-size: 0.8125rem;
  }
}
```

**Alternative — phone icon only on mobile (tap-to-call):**
```html
<!-- Mobile-only tap-to-call button -->
<a href="tel:+13128889651"
   class="mobile-phone-btn"
   aria-label="Call us at 312-888-9651">
  <svg aria-hidden="true"><!-- phone icon --></svg>
</a>
```

**WordPress `header.php` addition:**
```php
<div class="header-top-bar">
  <?php
  $phone = get_theme_mod('header_phone', '312-888-9651');
  $email = get_theme_mod('header_email', 'hello@launchpadlab.com');
  ?>
  <?php if ($phone) : ?>
    <a href="tel:<?= esc_attr(preg_replace('/[^0-9+]/', '', $phone)) ?>"
       class="header-phone"><?= esc_html($phone) ?></a>
  <?php endif; ?>
  <?php if ($email) : ?>
    <a href="mailto:<?= esc_attr($email) ?>"
       class="header-email"><?= esc_html($email) ?></a>
  <?php endif; ?>
</div>
```

### Components / Files to Audit

- `header.php` — site header template
- Header CSS/SCSS
- Mobile navigation template and styles
- WordPress Customizer — add phone/email fields if not already present
- Ensure consistency with footer phone/email values

---

## Examples from Other Sites

- **Deloitte.com:** Displays a "Contact us" link and phone number in a slim top bar above the main navigation.
- **Accenture.com:** Has a persistent "Contact" button in the header with phone and email accessible in one click.
- **McKinsey.com:** Features a compact contact bar with phone number and office locations in the header region.
- **Many B2B SaaS sites (e.g., Salesforce, HubSpot):** Place a phone number or "Talk to Sales" link in the header, recognizing that enterprise buyers prefer direct contact.
