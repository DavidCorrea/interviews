# Story 21: Add Skip Links for Key Content Sections

## User Story

**As a** keyboard or screen reader user,
**I want** skip links that let me jump directly to key sections (services, contact info),
**So that** I don't have to tab or scroll through the entire page to reach what I need.

## Description

While a "Skip to content" link exists, there are no skip links to important sections like "Contact Information" or "Services." Magnifier and ADHD users must scroll through enormous amounts of content to find what they need.

## Acceptance Criteria

- [ ] Skip links are present for: "Skip to Main Content," "Skip to Services," "Skip to Contact Information"
- [ ] Skip links are visually hidden by default but become visible on keyboard focus
- [ ] Each skip link targets an element with a matching `id` attribute
- [ ] Skip links are the first focusable elements on the page

## Testing Instructions

1. **Tab test:** Load the homepage and press Tab — skip links should appear as the first focused elements
2. **Activation:** Press Enter on "Skip to Contact Information" — focus should move to the contact section
3. **Visual:** Verify skip links are not visible before Tab is pressed, and appear clearly on focus
4. **Screen reader:** NVDA should announce each skip link text when focused
5. **Subpages:** Verify skip links are present on the contact page and service pages too

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | Medium |
| **Complexity** | Low |
| **WCAG Criteria** | 2.4.1 (Bypass Blocks) |
| **Affected Users** | Low vision magnifier users, ADHD users, screen reader users |

## Source Reports

- Low Vision Screen Magnifier Report
- ADHD User Report
- Screen Reader Report
