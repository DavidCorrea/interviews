# H-17: Contact Info Buried Below Form and Testimonials

**Issue ID:** H-17
**Priority:** High
**WCAG Criteria:** 2.4.5 Multiple Ways (AA)
**Affected Personas:** Big Company Owner, Senior Person, Low Vision Screen Magnifier, Non-Native Speaker

---

## User Story

**As a** senior business executive visiting the Contact page,
**I want** the company's phone number and email address to be immediately visible near the top of the page,
**so that** I can reach the company directly without scrolling past a long form and testimonials to find basic contact information.

---

## Acceptance Criteria

- [ ] The company phone number and email address are visible above the fold (or within the first viewport) on the Contact page at a standard desktop resolution (1440px).
- [ ] Contact information appears **before** or **alongside** the contact form — not below it.
- [ ] The phone number uses a `tel:` link and the email uses a `mailto:` link so they are one-click actionable on any device.
- [ ] Contact information is also accessible from the site header or a persistent element on every page (not just the Contact page).
- [ ] The contact info block is clearly labeled (e.g., with a heading like "Call or Email Us Directly").
- [ ] At 200%+ zoom, the contact info remains visible and does not get pushed below the fold.
- [ ] Testimonials and other supporting content appear **after** the primary contact channels.

---

## How to Test the Change

### Manual Testing

1. **Above-the-fold check:** Load the Contact page at 1440px width and 100% zoom. Without scrolling, confirm the phone number and email are visible.
2. **Mobile test:** Load the Contact page on a mobile device (375px viewport). Confirm contact info appears before or adjacent to the form, not after scrolling past testimonials.
3. **Magnification test:** Zoom to 200% and 400%. Confirm the contact info is still accessible within 1–2 scrolls.
4. **Screen reader test:** Navigate the Contact page with VoiceOver or NVDA. Confirm the phone/email info is announced before or at the same level as the form.
5. **Five-second task:** Ask someone unfamiliar with the site to find the phone number on the Contact page. Measure time. Target: under 5 seconds.
6. **Site-wide check:** Navigate to the homepage, services page, and about page. Confirm a phone number or "Call Us" link is accessible from the header or footer on every page.

### Automated Testing

```javascript
// Verify contact info position relative to the form
const contactInfo = document.querySelector('.contact-info, [class*="phone"], [href^="tel:"]');
const form = document.querySelector('form, .nf-form-cont');

if (contactInfo && form) {
  const contactPos = contactInfo.getBoundingClientRect().top;
  const formPos = form.getBoundingClientRect().top;
  console.assert(
    contactPos <= formPos,
    `Contact info (${contactPos}px) should appear above form (${formPos}px)`
  );
}
```

---

## Developer Notes

### General Approach

Restructure the Contact page layout to place direct contact information (phone, email, address) at the top of the page, either above or alongside the contact form. Move testimonials below the form and contact info.

### Current State (Problem)

```
┌─────────────────────────────────────┐
│  Contact Page                       │
├─────────────────────────────────────┤
│  [Contact Form — 6+ fields]        │  ← User sees this first
│  [Testimonial 1]                    │
│  [Testimonial 2]                    │
│  [Testimonial 3]                    │
│  [Testimonial 4]                    │
│  [Testimonial 5]                    │
│  ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─│
│  Phone: 312-888-9651               │  ← Buried far below the fold
│  Email: hello@launchpadlab.com      │
└─────────────────────────────────────┘
```

### Recommended Fix — Side-by-Side Layout

```
┌────────────────────┬──────────────────┐
│  Contact Form      │  Get in Touch    │
│  [Name]            │                  │
│  [Email]           │  📞 312-888-9651 │
│  [Company]         │  ✉ hello@lpl.com │
│  [Message]         │  📍 Chicago, IL  │
│  [Submit]          │                  │
├────────────────────┴──────────────────┤
│  [Testimonials below]                 │
└───────────────────────────────────────┘
```

### HTML Structure

```html
<section class="contact-section">
  <div class="contact-grid">
    <!-- Form column -->
    <div class="contact-form-column">
      <h1>Contact Us</h1>
      <!-- Ninja Forms container -->
    </div>

    <!-- Info column — visible immediately -->
    <aside class="contact-info-column">
      <h2>Reach Us Directly</h2>
      <ul class="contact-details">
        <li>
          <a href="tel:+13128889651">
            <strong>Phone:</strong> (312) 888-9651
          </a>
        </li>
        <li>
          <a href="mailto:hello@launchpadlab.com">
            <strong>Email:</strong> hello@launchpadlab.com
          </a>
        </li>
        <li>
          <strong>Location:</strong> Chicago, IL
        </li>
      </ul>
    </aside>
  </div>
</section>

<!-- Testimonials AFTER contact section -->
<section class="testimonials-section">
  <!-- Testimonial cards -->
</section>
```

### CSS Layout

```css
.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
  align-items: start;
}

.contact-info-column {
  position: sticky;
  top: 2rem;  /* Stays visible while user fills form */
}

/* Stack on mobile */
@media (max-width: 768px) {
  .contact-grid {
    grid-template-columns: 1fr;
  }

  .contact-info-column {
    order: -1;  /* Contact info appears FIRST on mobile */
    position: static;
  }
}
```

### Header Contact Info (Site-Wide)

```html
<!-- Add to site header for every page -->
<div class="header-contact">
  <a href="tel:+13128889651" class="header-phone">
    (312) 888-9651
  </a>
</div>
```

### Components / Files to Audit

- Contact page template (e.g., `page-contact.php`)
- Contact page section ordering in the CMS
- Testimonials section placement
- Site header template (for adding phone number)
- Footer template (verify phone/email are present and correct)
- Mobile responsive styles for the contact layout

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **HubSpot** | Contact page shows phone, email, and chat options in a sidebar next to the form | Multiple contact channels visible immediately; no scrolling needed. |
| **Salesforce** | Phone number is in the global header on every page; Contact page leads with phone + email | Enterprise buyers can call instantly from any page. |
| **Deloitte** | Contact page has a "Call us" block at the top, above the form | Prioritizes direct contact for decision-makers. |
| **Basecamp** | Contact page lists email address first, then an optional form below | Respects users who prefer direct communication over forms. |
