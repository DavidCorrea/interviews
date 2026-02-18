# Story 20: Shorten Homepage / Reduce Scrolling

## User Story

**As a** user who gets overwhelmed by long pages,
**I want** the homepage to be concise and focused,
**So that** I can understand the company's value proposition without endless scrolling.

## Description

The homepage is extremely long with 10+ sections. Users got lost, forgot earlier content, and felt exhausted by the time they reached the bottom. High-zoom users had to scroll 100+ times. This overlaps with Story 10 (Reduce Information Overload) and can be addressed together.

## Acceptance Criteria

- [ ] Homepage has no more than 5-6 distinct sections
- [ ] Detailed content is moved to dedicated subpages (accessible via links)
- [ ] Collapsible/accordion sections are used for supplementary content if it must remain on the page
- [ ] Long pages include anchor navigation or a table of contents
- [ ] Total scroll depth is measurably reduced from the current version

## Testing Instructions

1. **Section count:** Count distinct sections on the redesigned homepage — should be 5-6 or fewer
2. **Scroll measurement:** Measure total page height (DevTools > body height) — compare to previous version; should be significantly shorter
3. **Subpage links:** Verify that any removed content is accessible via clear links to subpages
4. **Accordion functionality:** If accordions are used, verify they are keyboard accessible (Enter to toggle, proper aria-expanded state)
5. **Anchor navigation:** If a table of contents is present, click each item and verify it scrolls to the correct section

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | Medium |
| **Complexity** | High |
| **WCAG Criteria** | — |
| **Affected Users** | Seniors, ADHD, cognitive disability, low vision magnifier users, stressed users |

## Source Reports

- Senior User Report
- ADHD User Report
- Cognitive Disability Report
- Low Vision Screen Magnifier Report
- Stressed User Report
