# AI-19: Reduce Visual Clutter

## Title
Reduce visual clutter by consolidating logos, awards, and CTAs per viewport

## User Story
As a **visitor with cognitive differences or attention difficulties**, I want **a focused, uncluttered layout with clear priorities**, so that **I can understand the main message and take action without feeling overwhelmed**.

## Acceptance Criteria

- [ ] Each viewport shows a maximum of 1–2 primary CTAs
- [ ] Homepage displays 4–6 logos (not 12+)
- [ ] 2–3 key awards visible; rest linked to dedicated Awards/Recognition page
- [ ] Adequate white space (padding/margin) between sections
- [ ] Primary actions are visually distinct from secondary actions

## How to Test

1. View Homepage, About, Services, and Contact at common viewport sizes (320px, 768px, 1440px).
2. Count primary CTAs per viewport; verify max 1–2.
3. Count visible logos on Homepage; verify 4–6 (or "See all clients" link).
4. Count visible award badges; verify 2–3 with rest on dedicated page.
5. Assess visual density; verify adequate spacing between sections.

## Developer Notes

- Reduce logo carousel to 4–6 visible items or use a "See all clients" link.
- Move excess award badges to an Awards/Recognition page.
- Limit CTAs: one primary "Contact Us" per viewport, with secondary actions smaller/lower.
- Increase `padding` and `margin` between sections for white space.
- Consider progressive disclosure: show key content first, with expandable "See more" for additional items.

## WCAG References

- **Cognitive accessibility best practices:** Reduce cognitive load, avoid clutter, provide clear visual hierarchy and focus.

## Priority
**P3 Medium**

## Effort Estimate
**Medium (4–8h)**
