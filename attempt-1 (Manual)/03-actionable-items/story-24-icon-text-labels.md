# Story 24: Add Text Labels to Icon-Only Interactive Elements

## User Story

**As a** voice control or screen reader user,
**I want** all icon-only buttons and links to have accessible text labels,
**So that** I can identify and activate them by name.

## Description

Arrow icons next to "Learn More" links, social media icons, and the hamburger menu icon may lack text labels. Voice control users cannot reference them ("Click arrow" is ambiguous), and screen reader users may hear nothing useful.

## Acceptance Criteria

- [ ] The hamburger menu button has an `aria-label` (e.g., "Open navigation menu") or visible text
- [ ] Social media icons have `aria-label` attributes (e.g., "Follow us on LinkedIn")
- [ ] Decorative arrow icons next to links are either hidden from assistive tech (`aria-hidden="true"`) or the parent link has a descriptive label
- [ ] All icon-only interactive elements are identifiable by name in a screen reader or voice control interface

## Testing Instructions

1. **Screen reader:** Tab through all interactive elements with NVDA — verify each icon button/link is announced with a meaningful name
2. **Voice control:** Say "Click Open navigation menu" or "Click Follow us on LinkedIn" — verify the correct element activates
3. **DevTools audit:** Inspect each icon-only element — verify it has either visible text, `aria-label`, or `aria-labelledby`
4. **axe audit:** Run axe DevTools — verify no "buttons/links must have discernible text" violations

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | Medium |
| **Complexity** | Low |
| **WCAG Criteria** | 1.1.1 (Non-text Content), 4.1.2 (Name, Role, Value) |
| **Affected Users** | Voice control users, low vision users |

## Source Reports

- Voice Control Report
- Low Vision User Report
