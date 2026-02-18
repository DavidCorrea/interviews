# Story 31: Add Accessibility Statement and Reduced-Motion Toggle

## User Story

**As a** user with accessibility needs,
**I want** the site to have an accessibility statement and user-facing controls to customize my experience,
**So that** I know the company cares about accessibility and I can adjust the site to my needs.

## Description

There is no accessibility statement communicating the site's commitment to accessibility, and no user-facing controls to reduce motion or adjust the experience.

## Acceptance Criteria

- [ ] An accessibility statement page exists and is linked from the site footer
- [ ] The statement includes: commitment to accessibility, conformance target (e.g., WCAG 2.1 AA), known limitations, and contact info for reporting issues
- [ ] A "Reduce Motion" toggle is present in the site header
- [ ] The toggle disables all animations site-wide when activated
- [ ] The toggle preference persists across pages and sessions (via localStorage)
- [ ] The toggle is keyboard accessible

## Testing Instructions

1. **Footer link:** Verify a link to the accessibility statement is in the footer on every page
2. **Statement content:** Review the accessibility statement — verify it includes conformance target, known issues, and a contact method
3. **Toggle:** Click the "Reduce Motion" toggle — verify all animations stop immediately
4. **Persistence:** After enabling the toggle, navigate to another page — verify animations remain disabled
5. **Session persistence:** Close and reopen the browser — verify the preference is remembered
6. **Keyboard:** Tab to the toggle and press Enter/Space — verify it activates
7. **Screen reader:** Verify the toggle is announced correctly (e.g., "Reduce Motion, toggle button, off" / "on")

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | Medium |
| **Complexity** | Low-Medium |
| **WCAG Criteria** | — |
| **Affected Users** | Motion sensitivity users, screen reader users |

## Source Reports

- Motion Sensitivity Report
- Screen Reader Report
