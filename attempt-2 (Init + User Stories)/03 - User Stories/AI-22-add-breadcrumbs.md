# AI-22: Add Breadcrumbs on Inner Pages

## User Story

As a **site visitor**, I want **breadcrumb navigation on all inner pages**, so that **I can understand where I am in the site hierarchy and easily navigate back to parent sections**.

## Acceptance Criteria

- [ ] Breadcrumbs appear on all inner pages (About, Services, Contact, Work, etc.)
- [ ] Breadcrumb trail shows current location in site hierarchy (e.g., Home > About)
- [ ] Breadcrumbs are keyboard navigable
- [ ] Screen reader announces breadcrumbs properly
- [ ] Current page is indicated and not a link
- [ ] Parent levels are clickable links

## How to Test

1. Visit the **About** page → verify breadcrumb trail is visible (e.g., Home > About)
2. Visit the **Services** page → verify breadcrumb trail is visible
3. Visit the **Contact** page → verify breadcrumb trail is visible
4. Visit the **Work** page → verify breadcrumb trail is visible
5. Use **Tab** to navigate through breadcrumb links → confirm all links receive focus and are activatable
6. Use a **screen reader** (VoiceOver, NVDA, or JAWS) → confirm breadcrumb structure and current page are announced correctly

## Developer Notes

- Create a reusable breadcrumb component using semantic markup:
  - `<nav aria-label="Breadcrumb"><ol>` with `<li>` items
- Use **Schema.org BreadcrumbList** structured data for SEO
- Style with separator characters (e.g., `>`)
- Ensure all links are keyboard accessible (focusable, activatable with Enter/Space)
- Mark the current page with `aria-current="page"` and do not make it a link
- Integrate with routing/cms to generate breadcrumb path dynamically

## WCAG References

- **2.4.8 Location** (Level AAA): Information about the user's location within a set of Web pages is available.

## Priority & Effort

| Priority | Effort Estimate |
|----------|-----------------|
| P3 Medium | Small–Medium (2–4h) |
