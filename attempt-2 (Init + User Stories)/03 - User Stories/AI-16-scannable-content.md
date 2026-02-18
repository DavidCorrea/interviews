# AI-16: Scannable Content

## Title
Break up dense text blocks into short paragraphs, bullet points, and scannable sections

## User Story
As a **visitor who scans content quickly or has difficulty with long text blocks**, I want **content broken into short paragraphs, bullets, and clear sections**, so that **I can find the information I need without reading every word**.

## Acceptance Criteria

- [ ] No paragraph exceeds 3 sentences
- [ ] Key information is presented in bullet points or callout boxes
- [ ] Each section has a clear subheading (H3 or equivalent)
- [ ] Dense sections include a TL;DR summary at the top
- [ ] Testimonials are kept short (1–2 sentences) with "Read more" expandable if needed

## How to Test

1. Audit all body copy across Homepage, About, Services, and Contact pages.
2. Verify no paragraph exceeds 3 sentences.
3. Verify key information (features, benefits, offerings) is in bullet lists or callout boxes.
4. Verify each section has a clear subheading.
5. Check that dense sections have TL;DR summaries at the top.
6. Verify testimonials are 1–2 sentences with expandable "Read more" for longer content.

## Developer Notes

- Audit all body copy across Homepage, About, Services, Contact.
- Break paragraphs > 3 sentences into smaller chunks.
- Convert feature/benefit lists to `<ul>` elements.
- Add H3 subheadings within sections.
- Add TL;DR summaries at top of dense sections.
- Keep testimonials short (1–2 sentences) with "Read more" expandable if needed.

## WCAG References

- **1.4.8 Visual Presentation (Level AAA):** A mechanism is available for users to select foreground and background colors.
- **2.4.10 Section Headings (Level AAA):** Section headings are used to organize the content.

## Priority
**P2 High**

## Effort Estimate
**Medium (4–8h)**
