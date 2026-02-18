# No Dedicated Contact Page

## Priority
**High**

## User Story
As a potential client or partner, I want a dedicated contact page with multiple contact methods (phone, email, address, form), so that I can easily reach LaunchPad Lab through my preferred channel.

## Acceptance Criteria

- [ ] A `/contact/` route exists and is accessible
- [ ] The main navigation "Contact" link points to `/contact/`, not the homepage
- [ ] Contact page displays: phone number, email address, physical address
- [ ] Contact page includes the contact form (or a clear CTA to it)
- [ ] Optional: map embed for office location
- [ ] Page has a unique H1 (e.g., "Contact Us")
- [ ] Contact information is also available in the footer site-wide
- [ ] Page is keyboard navigable and screen-reader friendly

## How to Test

1. Click "Contact" in the main navigation.
2. Verify the URL changes to `/contact/` (or equivalent).
3. Confirm the page is not the homepage.
4. Check for presence of: phone, email, address, contact form.
5. Verify footer also contains contact information.
6. Test with keyboard: Tab through all contact elements.
7. Test with screen reader: ensure all contact methods are announced.
8. If map is present, verify it has a text alternative or is decorative with `aria-hidden="true"` and a separate address link.

## Developer Notes

### General Explanation
Users expect a "Contact" link to lead to a dedicated contact page. Currently, the link navigates to the homepage, forcing users to scroll or search for contact information. A centralized contact experience improves trust, accessibility, and conversion.

**Solution:** Create a `/contact/` route with a dedicated template. Include phone, email, address, and the contact form. Update the nav "Contact" link to point to this route. Ensure the footer links to the contact page or displays the same information.

### Code Examples

**Page structure:**
```html
<main>
  <h1>Contact Us</h1>
  <section aria-labelledby="contact-info-heading">
    <h2 id="contact-info-heading">Get in Touch</h2>
    <address>
      <p>
        <strong>Phone:</strong>
        <a href="tel:+1234567890">(123) 456-7890</a>
      </p>
      <p>
        <strong>Email:</strong>
        <a href="mailto:hello@launchpadlab.com">hello@launchpadlab.com</a>
      </p>
      <p>
        <strong>Address:</strong><br>
        123 Main St, Suite 100<br>
        City, State ZIP
      </p>
    </address>
  </section>
  <section aria-labelledby="map-heading">
    <h2 id="map-heading">Find Us</h2>
    <iframe
      src="https://maps.google.com/..."
      title="LaunchPad Lab office location"
      width="600"
      height="450"
    ></iframe>
  </section>
  <section aria-labelledby="form-heading">
    <h2 id="form-heading">Send a Message</h2>
    <form action="/api/contact" method="post">
      <!-- form fields -->
    </form>
  </section>
</main>
```

**React/Next.js example:**
```jsx
// pages/contact.js or app/contact/page.js
export default function ContactPage() {
  return (
    <Layout>
      <h1>Contact Us</h1>
      <ContactInfo />
      <MapEmbed />
      <ContactForm />
    </Layout>
  );
}
```

**Nav link update:**
```jsx
// Before
<NavLink href="/">Contact</NavLink>

// After
<NavLink href="/contact/">Contact</NavLink>
```

### Components to Audit
- Navigation component (Contact link `href`)
- Footer component (ensure contact info is present)
- Routing configuration
- Any redirects that might send `/contact/` to `/`

## Examples from Other Sites

- **HubSpot.com** — Dedicated contact page with phone, email, address, contact form, and chat option. Multiple contact methods are clearly presented.
- **Salesforce.com** — Contact page with multiple contact methods, regional offices, and a form. Clear structure for different user needs.
