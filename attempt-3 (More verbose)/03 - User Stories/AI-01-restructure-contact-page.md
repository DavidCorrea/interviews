# AI-01: Restructure Contact Page — Move Form Above Testimonials

## Metadata
- **ID:** AI-01
- **Priority:** 1 Critical
- **Personas Affected:** All 16 personas
- **WCAG Criteria:** 2.4.1 Bypass Blocks (A), 2.4.6 Headings and Labels (AA)
- **Effort:** Small (2–4 hours)

---

## User Story

**As a** visitor to the LaunchPad Lab website who needs to contact the company,

**I want** the contact form to appear immediately after the page heading and contact information (phone, email, address),

**So that** I can reach the form quickly without scrolling past multiple testimonials, whether I use a keyboard, screen reader, or have limited mobility.

---

## Acceptance Criteria

- [ ] Contact form is visible without scrolling past any testimonials on desktop viewport (≥1024px)
- [ ] Contact form is visible without scrolling past any testimonials on tablet viewport (768px–1023px)
- [ ] Contact form is visible without scrolling past any testimonials on mobile viewport (320px–767px)
- [ ] Phone number, email address, and physical address are displayed in large, readable text above the contact form
- [ ] An `<h2>` heading "Send Us a Message" (or equivalent) appears directly above the contact form
- [ ] Testimonials section appears below the contact form in the DOM order
- [ ] Screen reader users encounter the form as the first meaningful content after the main heading
- [ ] Keyboard users can reach the form within 3–5 tab stops from the skip link (if skip links are implemented)

---

## Test Plan

### Visual/Manual Testing
1. Navigate to `https://launchpadlab.com/contact`
2. Resize browser to 1920×1080 — verify form is visible above the fold without scrolling
3. Resize to 768×1024 — verify form is visible without scrolling past testimonials
4. Resize to 375×667 (mobile) — verify form appears before testimonials in scroll order
5. Verify phone, email, and address are displayed in prominent text above the form
6. Verify "Send Us a Message" (or similar) heading appears above the form

### Screen Reader Testing
1. Enable VoiceOver (macOS) or NVDA (Windows)
2. Navigate to `/contact` and activate "Skip to main content" if available
3. Use heading navigation (VoiceOver: VO+U → Headings) — confirm form-related heading appears before testimonials
4. Use rotor/headings — confirm logical reading order: Page title → Contact info → Form heading → Form fields → Testimonials

### Keyboard Testing
1. Tab from page load (or after skip link)
2. Count tab stops until focus reaches the first form field
3. Verify form is reachable within 3–5 tab stops from skip link (or from first focusable element if no skip link)

---

## Developer Notes

### HTML Structure
- Reorder DOM so the structure is: `<main>` → Contact info block → Form section → Testimonials section
- Add `<h2 id="send-message">Send Us a Message</h2>` immediately above the form
- Ensure contact info (phone, email, address) uses semantic markup; consider `<address>` for physical address

### CSS Approach
- Use flexbox or grid with `order` only if DOM reorder is not feasible; prefer DOM reorder for accessibility
- If testimonials are currently above form in HTML, move the testimonials block in the source after the form block
- Ensure contact info uses `font-size` ≥ 16px (or 1rem) for readability

### Content Considerations
- Display phone and email as clickable links (`tel:` and `mailto:`) for convenience
- Ensure contact info has sufficient color contrast (see AI-03)

### Files to Modify
- Contact page template/component (e.g., `contact.html`, `ContactPage.tsx`, or CMS template)
- Contact page styles (if separate from global CSS)

---

## Examples

| Site | Approach |
|------|----------|
| **Stripe.com/contact** | Form appears first; testimonials/social proof in sidebar or below |
| **Basecamp.com/contact** | Form is immediately visible above the fold; minimal distraction |
| **HubSpot contact pages** | Form typically placed above testimonials; CTA-focused layout |
| **Vercel.com/contact** | Clean layout with form prominent; supporting content below |
