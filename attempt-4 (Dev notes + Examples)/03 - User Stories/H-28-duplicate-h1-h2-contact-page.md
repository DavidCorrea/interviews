# H-28: Duplicate h1/h2 on Contact Page

**Issue ID:** H-28
**Priority:** High
**WCAG Criteria:** 1.3.1 Info and Relationships (A), 2.4.6 Headings and Labels (AA)
**Affected Personas:** Screen Reader, ADHD, Non-Native Speaker

---

## User Story

**As a** screen reader user navigating the contact page by headings,
**I want** each heading to have unique, descriptive text and the correct heading level,
**so that** I can understand the page structure and quickly find the section I need.

---

## Acceptance Criteria

- [ ] The contact page has exactly one `<h1>` that describes the page's primary purpose (e.g., "Contact Us").
- [ ] No two headings on the page have identical text content.
- [ ] The heading hierarchy is logical and sequential: `<h1>` → `<h2>` → `<h3>` with no skipped levels.
- [ ] Each heading clearly describes the content of the section it introduces.
- [ ] The `<h2>` previously duplicating the `<h1>` text is either renamed to describe its specific section (e.g., "Send Us a Message") or changed to a non-heading element if it's decorative.

---

## How to Test the Change

### Manual Testing

1. **Screen reader heading list:** Using NVDA (`Insert+F7`) or VoiceOver (`VO+U` → Headings), open the headings list on the contact page. Confirm each heading is unique and the hierarchy is logical.
2. **Visual inspection:** Inspect the page source. Confirm only one `<h1>` exists and no heading text is duplicated.
3. **Heading outline tool:** Use the [HeadingsMap browser extension](https://chromewebstore.google.com/detail/headingsmap/) to visualize the heading hierarchy. Confirm it forms a clean tree with no duplicates.

### Automated Testing

```javascript
// Check for duplicate heading text
const headings = document.querySelectorAll('h1, h2, h3, h4, h5, h6');
const texts = [...headings].map(h => h.textContent.trim().toLowerCase());
const duplicates = texts.filter((t, i) => texts.indexOf(t) !== i);
console.assert(duplicates.length === 0, 'Duplicate heading text found:', duplicates);

// Check for single h1
const h1s = document.querySelectorAll('h1');
console.assert(h1s.length === 1, `Expected 1 h1, found ${h1s.length}`);
```

- Run `axe-core` and check for "Page should contain a level-one heading" and "Heading levels should only increase by one."

---

## Developer Notes

### General Approach

Differentiate the two headings so each describes its own section. The `<h1>` should be the page title, and the `<h2>` should describe the specific section it introduces (e.g., the contact form or a supporting message).

### Current State (Problem)

```html
<h1>Ready to Build Something Great?</h1>
<!-- ... hero area ... -->

<h2>Ready to Build Something Great?</h2>
<!-- ... form section or CTA area ... -->
```

Both headings have identical text, making the heading list confusing for screen reader users.

### Recommended Fix — Option A: Rename the h2

```html
<h1>Contact Us</h1>
<!-- Hero section with intro text -->

<h2>Send Us a Message</h2>
<!-- Contact form follows -->
```

### Recommended Fix — Option B: Remove Decorative Heading

If the `<h2>` is purely decorative/visual and doesn't introduce new content:

```html
<h1>Ready to Build Something Great?</h1>

<!-- Replace h2 with a styled paragraph or span -->
<p class="section-tagline" aria-hidden="false">
  Tell us about your project and we'll get back to you within one business day.
</p>
```

### Recommended Heading Structure for the Contact Page

```
h1: Contact Us
  h2: Send Us a Message          (introduces the form)
  h2: What Our Clients Say       (introduces testimonials)
  h2: Other Ways to Reach Us     (introduces phone/email/address)
```

### Components / Files to Audit

- Contact page template (e.g., `page-contact.php`)
- Hero section partial that renders the `<h1>`
- Form section partial that renders the `<h2>`
- CMS fields that populate heading text (may need editor guidance)

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **Mailchimp** | Contact page uses `h1: Contact Us`, `h2: Sales`, `h2: Support` — each heading is unique and descriptive | Clear hierarchy, no duplicates. |
| **Shopify** | `h1: Contact Shopify Support`, `h2: Browse help topics`, `h2: Talk to us` | Each section is clearly identified. |
| **GOV.UK** | Strict heading hierarchy enforced by design system — duplicates are flagged in QA | Systematic prevention of the issue. |
