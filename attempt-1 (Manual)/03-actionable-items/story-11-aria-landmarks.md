# Story 11: Add ARIA Landmarks

## User Story

**As a** screen reader user,
**I want** the site to use proper ARIA landmark regions,
**So that** I can jump directly to the navigation, main content, or footer without reading the entire page sequentially.

## Description

The site does not appear to use proper ARIA landmark regions. Screen reader users cannot jump between navigation, main content, and footer using landmark navigation (D key in NVDA). This forces sequential reading of the entire page.

## Acceptance Criteria

- [ ] The site uses semantic HTML5 elements: `<header>`, `<nav>`, `<main>`, `<footer>`
- [ ] There is exactly one `<main>` element per page
- [ ] Multiple `<nav>` elements have distinguishing `aria-label` attributes (e.g., "Primary Navigation," "Footer Navigation")
- [ ] Screen readers announce landmark regions when using landmark navigation (D key in NVDA)

## Testing Instructions

1. **HTML inspection:** View page source or use DevTools — verify `<header>`, `<nav>`, `<main>`, and `<footer>` elements are present
2. **Screen reader:** Open the page with NVDA, press D to cycle through landmarks — verify "banner," "navigation," "main," and "contentinfo" regions are announced
3. **Multiple navs:** If more than one `<nav>` exists, verify each has a unique `aria-label` announced by the screen reader
4. **Validator:** Run the page through the W3C validator — no landmark-related errors

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | High |
| **Complexity** | Low |
| **WCAG Criteria** | 1.3.1 (Info and Relationships), 4.1.2 (Name, Role, Value) |
| **Affected Users** | Screen reader users |

## Source Reports

- Screen Reader Report
