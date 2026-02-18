# AI-01: Restructure Contact Page

## Title
Restructure Contact page so that contact form, phone, email, and address appear above testimonials

## User Story
As a **visitor with mobility or cognitive limitations**, I want **the contact form, phone, email, and address to appear above testimonials**, so that **I can quickly find and use contact information without scrolling past lengthy testimonial content**.

## Acceptance Criteria

- [ ] Contact form is visible without scrolling on initial page load
- [ ] Phone number is visible without scrolling on initial page load
- [ ] Email address is visible without scrolling on initial page load
- [ ] Physical address is visible without scrolling on initial page load
- [ ] Testimonials section appears below all contact information
- [ ] DOM order reflects visual order (form, phone, email, address before testimonials)
- [ ] Phone and email are displayed in large, high-contrast text (#000 or #222 on #FFF)

## How to Test

1. Navigate to `https://launchpadlab.com/contact`
2. On page load, verify the following are visible in the viewport without scrolling:
   - Contact form
   - Phone number
   - Email address
   - Physical address
3. Scroll down and verify testimonials appear below the contact information
4. Confirm the logical reading order matches the visual layout

## Developer Notes

- Reorder the DOM so the testimonial section is moved below the form section
- Ensure phone and email use large, high-contrast text (#000 or #222 on #FFF background)
- Maintain semantic structure (headings, landmarks) when reordering
- Consider responsive behavior—contact info should remain above testimonials on all viewport sizes

## WCAG References

- **[2.4.1 Bypass Blocks (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)**: A mechanism is available to bypass blocks of content that are repeated on multiple Web pages.
- **[2.4.6 Headings and Labels (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)**: Headings and labels describe topic or purpose.

## Priority & Effort

| Attribute | Value |
|-----------|-------|
| **Priority** | P1 Critical |
| **Effort Estimate** | Small (2–4 hours) |
