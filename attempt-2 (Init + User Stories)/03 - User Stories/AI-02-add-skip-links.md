# AI-02: Add Skip Links

## Title
Add "Skip to main content" as first focusable element on all pages, plus "Skip to contact form" on Contact page

## User Story
As a **keyboard user or screen reader user**, I want **skip links as the first focusable element on each page**, so that **I can bypass repetitive navigation and jump directly to main content or the contact form without tabbing through every navigation item**.

## Acceptance Criteria

- [ ] "Skip to main content" link is the first focusable element on all pages
- [ ] Skip link is visually hidden until it receives focus
- [ ] Skip link becomes visible when focused (e.g., via Tab key)
- [ ] Activating the skip link moves focus to the main content area
- [ ] On the Contact page, a second "Skip to contact form" link is present
- [ ] "Skip to contact form" moves focus to the contact form when activated
- [ ] Skip links do not break the visual design when hidden

## How to Test

1. Navigate to any page on `https://launchpadlab.com/`
2. Press **Tab** once on page load
3. Verify the first focused element is a skip link (e.g., "Skip to main content")
4. Verify the skip link is visible when focused (not hidden)
5. Press **Enter** to activate the skip link
6. Verify focus moves to the main content area
7. On the Contact page (`/contact`), press **Tab** and verify "Skip to main content" appears first
8. Continue tabbing to find "Skip to contact form" (if present as second skip link)
9. Activate "Skip to contact form" and verify focus moves to the form

## Developer Notes

- Use a visually hidden skip link that becomes visible on `:focus`
- Target the `<main>` element with `id="main-content"`
- On the Contact page, add a second skip link targeting the form (e.g., `id="contact-form"`)
- Use the pattern:
  ```css
  .skip-link {
    position: absolute;
    left: -9999px;
    z-index: 999;
  }
  .skip-link:focus {
    position: static;
    /* Add padding, background, outline for visibility */
  }
  ```
- Place skip links at the very beginning of the `<body>`, before the header/nav

## WCAG References

- **[2.4.1 Bypass Blocks (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)**: A mechanism is available to bypass blocks of content that are repeated on multiple Web pages.

## Priority & Effort

| Attribute | Value |
|-----------|-------|
| **Priority** | P1 Critical |
| **Effort Estimate** | Small (1–2 hours) |
