# AI-18: Fix Heading Hierarchy

## Title
Fix duplicate H2 headings and remove heading markup from statistics

## User Story
As a **screen reader user or someone who navigates by headings**, I want **correct and logical heading structure**, so that **I can understand page structure and jump to sections efficiently**.

## Acceptance Criteria

- [ ] One H2 per section; no duplicate consecutive H2s
- [ ] Statistics (e.g., "12+ Years," "730+ Projects") are not marked as headings
- [ ] H1 → H2 → H3 hierarchy with no skipped levels
- [ ] Each section has a single, descriptive H2
- [ ] Subtitle-style text uses `<p>` or H3, not H2

## How to Test

1. Install a heading outline tool (browser extension, e.g., HeadingsMap or aXe).
2. Run the tool on each page (Homepage, About, Services, Contact).
3. Verify one H2 per section; no duplicate consecutive headings.
4. Verify statistics are not marked as headings.
5. Verify H1 → H2 → H3 hierarchy with no skipped levels.
6. Navigate with screen reader heading list to confirm logical structure.

## Developer Notes

- Audit all pages for heading structure.
- Where two consecutive H2s exist (section title + subtitle), make subtitle a `<p>` or H3.
- Change statistics ("12+ Years," "730+ Projects") from H2 to `<div>`, `<span>`, or `<dl>`.
- Use one H2 per section with descriptive text.
- Ensure H1 appears once per page and describes the page purpose.

## WCAG References

- **2.4.6 Headings and Labels (Level AA):** Headings and labels describe topic or purpose.
- **1.3.1 Info and Relationships (Level A):** Information, structure, and relationships conveyed through presentation can be programmatically determined or are available in text.

## Priority
**P2 High**

## Effort Estimate
**Small–Medium (2–4h)**
