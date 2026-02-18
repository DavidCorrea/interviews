# Story 05: Fix Heading Hierarchy

## User Story

**As a** screen reader user,
**I want** the page to have a logical, non-duplicated heading hierarchy,
**So that** I can efficiently navigate between sections and understand the page structure.

## Description

Almost every section has duplicate H2 headings (a section label and a subtitle both marked as H2). Statistics like "12+ Years in Business" are incorrectly marked as H2 headings. The heading hierarchy jumps inconsistently. This makes heading-based navigation confusing and inefficient for screen reader users.

## Acceptance Criteria

- [ ] Each page has exactly one H1 element (the main page title)
- [ ] Each major section has a single H2; subtitles use H3 or paragraph text
- [ ] Statistics (12+, 730+, 240+) are NOT marked as headings — use `<dl>`, `<div>`, or `<p>` instead
- [ ] Heading levels never skip (e.g., no H2 followed directly by H4)
- [ ] The heading outline reads as a logical table of contents when extracted

## Testing Instructions

1. **Heading outline:** Use the HeadingsMap browser extension (or W3C Validator) to extract the heading outline of the homepage — verify it reads as a logical, non-duplicated table of contents
2. **Screen reader:** Navigate the homepage using H key in NVDA — each heading should introduce a unique section, no duplicates
3. **Statistics check:** Navigate to the statistics section — "12+ Years in Business," "730+ Projects," and "240+ Clients" should NOT be announced as headings
4. **Subpages:** Check heading hierarchy on the contact page, service pages, and at least one case study page
5. **Validator:** Run the page through an HTML validator and check for heading-related warnings

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | Critical |
| **Complexity** | Low |
| **WCAG Criteria** | 1.3.1 (Info and Relationships) |
| **Affected Users** | Screen reader users |

## Source Reports

- Screen Reader Report
