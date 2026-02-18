# Phone Number Visibility

## Priority
Medium

## User Story
As a **visitor who prefers to call**, I want **the phone number easily visible in the header and on the contact page**, so that **I can reach the company without scrolling through the entire page**.

## Acceptance Criteria

- [ ] Phone number appears in the header (visible on desktop)
- [ ] Phone number appears on the dedicated contact page
- [ ] Phone number is wrapped in `<a href="tel:+13128889651">` for click-to-call on mobile
- [ ] On mobile, phone is accessible (e.g., in header or contact page; avoid requiring full scroll)
- [ ] Phone number is keyboard accessible and screen reader announced
- [ ] Consider a sticky contact bar or floating CTA for key conversion pages (optional)

## How to Test

1. Load the homepage (desktop view).
2. Verify the phone number is visible in the header without scrolling.
3. Resize to mobile view and confirm the phone is accessible (header or contact page).
4. Navigate to the contact page and confirm the phone number is present.
5. On mobile, tap the phone number and verify it initiates a call (click-to-call).
6. Use keyboard to tab to the phone link and verify focus is visible.
7. Use a screen reader and confirm the link is announced (e.g., "Call 312-888-9651").

## Developer Notes

### General Explanation
B2B service companies typically display the phone number prominently in the header. The contact page should also include it. Use `tel:` links for click-to-call on mobile. Ensure the link is keyboard accessible and has a clear label for screen readers.

### Code Example (HTML)

```html
<!-- In header -->
<header>
  <nav>
    <!-- ... -->
  </nav>
  <a href="tel:+13128889651" class="header-phone">(312) 888-9651</a>
</header>

<!-- On contact page -->
<section>
  <h2>Contact Us</h2>
  <p>Call us: <a href="tel:+13128889651">(312) 888-9651</a></p>
</section>
```

### Accessibility (Screen Reader)

```html
<a href="tel:+13128889651" aria-label="Call us at (312) 888-9651">
  (312) 888-9651
</a>
```

### Optional: Sticky Contact Bar

```html
<aside class="sticky-contact" aria-label="Quick contact">
  <a href="tel:+1312889651">Call</a>
  <a href="/contact/">Get in Touch</a>
</aside>
```

### React Example

```jsx
const PHONE = '+13128889651';
const PHONE_DISPLAY = '(312) 888-9651';

function Header() {
  return (
    <header>
      <nav>{/* ... */}</nav>
      <a href={`tel:${PHONE}`} aria-label={`Call us at ${PHONE_DISPLAY}`}>
        {PHONE_DISPLAY}
      </a>
    </header>
  );
}
```

### Components to Audit

- [ ] Header component
- [ ] Contact page template
- [ ] Footer (if phone should stay there as well)
- [ ] Mobile navigation / hamburger menu

## Examples from Other Sites

- **Salesforce.com** — Phone number in header and contact page; click-to-call on mobile.
- **Law firms and consulting firms** — Typically display phone prominently in header.
- **HubSpot.com** — Phone in header and footer; contact page has full contact options.
