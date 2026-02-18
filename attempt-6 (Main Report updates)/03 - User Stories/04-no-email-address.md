# No Email Address Visible

## Priority
**High**

## User Story
As a visitor who prefers email over phone or forms, I want to see a general contact email address on the site, so that I can reach LaunchPad Lab directly via email when convenient for me.

## Acceptance Criteria

- [ ] A general contact email (e.g., hello@launchpadlab.com or info@launchpadlab.com) is visible on the site
- [ ] Email appears in the footer on all pages
- [ ] Email appears on the contact page (when implemented)
- [ ] Email appears on the About page (when implemented)
- [ ] Email is a clickable `mailto:` link for easy access
- [ ] Email is announced correctly by screen readers
- [ ] Email is visible without requiring interaction (e.g., not hidden behind a "Contact" modal only)

## How to Test

1. Visit https://launchpadlab.com/ and scroll to the footer.
2. Verify an email address is visible (e.g., hello@launchpadlab.com).
3. Click the email link — confirm the default mail client opens with the address pre-filled.
4. Navigate to the contact page and About page — verify email is present.
5. Use a screen reader to confirm the email is announced as a link.
6. Test on mobile: tap the email link and verify behavior.
7. Use browser "Find in page" (Ctrl/Cmd+F) to search for "@" — ensure results appear.

## Developer Notes

### General Explanation
Many users prefer email for initial contact: it's asynchronous, leaves a record, and doesn't require immediate availability. Relying only on phone and forms excludes these users and may reduce inquiries. Adding a visible email address is a simple, high-impact change.

**Solution:** Add a general contact email (e.g., hello@launchpadlab.com or info@launchpadlab.com) to the footer, contact page, and About page. Use a `mailto:` link for one-click access. Ensure the link has descriptive text for screen readers.

### Code Examples

**Footer HTML:**
```html
<footer>
  <address>
    <p>
      <a href="mailto:hello@launchpadlab.com">hello@launchpadlab.com</a>
    </p>
    <p>
      <a href="tel:+1234567890">(123) 456-7890</a>
    </p>
    <p>123 Main St, City, State ZIP</p>
  </address>
</footer>
```

**React component:**
```jsx
const FooterContact = () => (
  <address>
    <a href="mailto:hello@launchpadlab.com">hello@launchpadlab.com</a>
    <a href="tel:+1234567890">(123) 456-7890</a>
  </address>
);
```

**Accessible link (if using icon + text):**
```html
<a href="mailto:hello@launchpadlab.com">
  <span class="icon" aria-hidden="true">✉</span>
  hello@launchpadlab.com
</a>
```

**If using only an icon:**
```html
<a href="mailto:hello@launchpadlab.com" aria-label="Email us at hello@launchpadlab.com">
  <span class="icon" aria-hidden="true">✉</span>
</a>
```

### Components to Audit
- Footer component
- Contact page template
- About page template
- Any global "Contact" or "Get in touch" sections
- Config/CMS for contact information (centralize email in one place)

## Examples from Other Sites

- **IDEO.com** — Displays hello@ideo.com prominently in the footer and on contact-related pages.
- **Most professional services firms** — Display a general email (info@, hello@, contact@) in the footer and on contact pages for easy access.
