# AI-24: Create and Publish Accessibility Statement Page

## User Story

As a **visitor who relies on assistive technology or has accessibility needs**, I want **an accessibility statement linked from the footer**, so that **I can understand the site's commitment to accessibility and know how to report issues**.

## Acceptance Criteria

- [ ] Accessibility statement page exists at `/accessibility`
- [ ] "Accessibility" link is present in the footer navigation
- [ ] Page includes a commitment statement
- [ ] Page lists standards targeted (WCAG 2.1 AA)
- [ ] Page provides contact method(s) for accessibility feedback (email, phone)
- [ ] Page includes date last updated

## How to Test

1. Visit the site footer → locate the **"Accessibility"** link
2. Click the link → confirm navigation to `/accessibility`
3. Verify page content includes:
   - Commitment to accessibility
   - Target standard (WCAG 2.1 AA)
   - Known limitations (if any)
   - How to report issues (email, phone)
   - Date last updated

## Developer Notes

- Create new page at `/accessibility`
- Content to include:
  - **Commitment statement** — organization's dedication to digital accessibility
  - **Standards targeted** — WCAG 2.1 AA
  - **Known limitations** — any current barriers or workarounds
  - **Feedback process** — how users can report issues (email, phone, form)
  - **Date last updated** — for transparency
- Add "Accessibility" link to footer navigation
- Ensure the page itself meets basic accessibility (headings, contrast, readable content)

## WCAG References

- **Best practice** — Accessibility statements are recommended by W3C/WAI as a trust and transparency measure, though not a formal WCAG criterion.

## Priority & Effort

| Priority | Effort Estimate |
|----------|-----------------|
| P4 Low | Small (1–2h) |
