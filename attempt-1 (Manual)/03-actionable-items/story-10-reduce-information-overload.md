# Story 10: Reduce Information Overload on Homepage

## User Story

**As a** user with cognitive limitations, ADHD, or limited tech literacy,
**I want** the homepage to present fewer sections and choices,
**So that** I can understand the company's offering without feeling overwhelmed or paralyzed by options.

## Description

The homepage presents 6 service boxes, 6 problem boxes, 3 case studies, 7+ award badges, a process section, statistics, related content, and multiple CTAs. Users reported decision paralysis, cognitive exhaustion, and inability to process so much information.

## Acceptance Criteria

- [ ] Homepage has no more than 5-6 distinct sections
- [ ] Service offerings are consolidated to 2-3 main categories on the homepage
- [ ] Detailed content (full process breakdown, all case studies, individual awards) lives on dedicated subpages
- [ ] Only one primary CTA is visible per viewport/section
- [ ] Progressive disclosure is used where detail is needed (expand/collapse)
- [ ] Visual hierarchy clearly guides the user's eye to the most important content first

## Testing Instructions

1. **Section count:** Count the distinct content sections on the homepage — should be 5-6 or fewer
2. **User test:** Ask a non-technical user to review the homepage for 60 seconds and summarize what the company does — they should answer confidently
3. **Choice count:** Count the number of clickable "Learn More" / "View" / "Explore" buttons visible at any one time — ideally 1 primary CTA per screen
4. **Scroll depth:** Measure the homepage scroll length — it should be meaningfully shorter than the current version
5. **Progressive disclosure:** Verify that collapsed/accordion sections expand correctly and are keyboard accessible

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | High |
| **Complexity** | High |
| **WCAG Criteria** | — |
| **Affected Users** | Seniors, ADHD, cognitive disability, stressed users |

## Source Reports

- Senior User Report
- ADHD User Report
- Cognitive Disability Report
- Stressed User Report
