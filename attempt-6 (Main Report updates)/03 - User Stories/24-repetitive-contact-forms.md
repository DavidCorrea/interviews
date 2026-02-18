# Repetitive Contact Forms

## Priority
Low

## User Story
As a **visitor browsing content pages**, I want **a simpler CTA (e.g., "Get in Touch" button) instead of a full contact form on every page**, so that **I am not overwhelmed by repeated forms and can choose when to engage**.

## Acceptance Criteria

- [ ] Full contact form appears on key conversion pages only (homepage, contact page, services)
- [ ] Content pages (blog, case studies, etc.) show a simpler CTA (e.g., "Get in Touch" button linking to contact page)
- [ ] Empty or redundant alert elements are removed or consolidated
- [ ] Contact page remains the primary destination for form submission
- [ ] CTA is clear and accessible (keyboard, screen reader)

## How to Test

1. Navigate to a content page (e.g., blog post, case study).
2. Scroll to the bottom. Verify a full form is NOT present; instead, a CTA button or link to contact page.
3. Navigate to homepage and contact page. Verify full form is present where appropriate.
4. Inspect the page for empty `<div role="alert">` or similar elements. Ensure they are removed or used correctly.
5. Click the CTA on a content page and confirm it navigates to the contact page.
6. Use keyboard navigation to verify the CTA is focusable and functional.

## Developer Notes

### General Explanation
Showing the same full contact form on every page feels excessive and pushy. Use a tiered approach: full form on key conversion pages (homepage, contact, services); simple CTA on content pages. Remove or consolidate empty alert elements that add noise.

### Code Example

#### Content Page (Simple CTA)

```html
<section class="cta-section">
  <h2>Ready to get started?</h2>
  <p>We'd love to hear about your project.</p>
  <a href="/contact/" class="cta-button">Get in Touch</a>
</section>
```

#### Key Conversion Page (Full Form)

```html
<section class="contact-form-section">
  <h2>Contact Us</h2>
  <form action="/contact/" method="post">
    {% csrf_token %}
    <label for="name">Name</label>
    <input id="name" name="name" type="text" required>
    <label for="email">Email</label>
    <input id="email" name="email" type="email" required>
    <label for="message">Message</label>
    <textarea id="message" name="message" required></textarea>
    <button type="submit">Send Message</button>
  </form>
</section>
```

#### Remove Empty Alerts

```html
<!-- Before: Multiple empty alerts -->
<div role="alert" id="alert-1"></div>
<div role="alert" id="alert-2"></div>

<!-- After: Single alert, populated only when needed -->
<div role="alert" id="form-alert" aria-live="polite" class="hidden">
  <!-- Message inserted on form success/error -->
</div>
```

### React Example

```jsx
function PageCTA({ showFullForm }) {
  if (showFullForm) {
    return <ContactForm />;
  }
  return (
    <section className="cta-section">
      <h2>Ready to get started?</h2>
      <a href="/contact/" className="cta-button">Get in Touch</a>
    </section>
  );
}

// Usage: showFullForm={['home', 'contact', 'services'].includes(pageType)}
```

### Components to Audit

- [ ] Page layout templates (where form/CTA is rendered)
- [ ] Contact form component
- [ ] Alert/notification elements (remove empty ones)
- [ ] Routing or page-type logic

## Examples from Other Sites

- **Stripe.com** — CTA buttons on content pages ("Get started", "Contact sales"); full form only on dedicated contact/signup pages.
- **Basecamp.com** — Clear CTA on content pages; form on dedicated page only.
- **Vercel.com** — CTA links on content; contact form on contact page.
- **Linear.app** — Minimal CTAs; signup form on dedicated page.
