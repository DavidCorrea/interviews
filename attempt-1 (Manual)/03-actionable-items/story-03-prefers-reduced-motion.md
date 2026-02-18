# Story 03: Implement prefers-reduced-motion and Reduce Animations

## User Story

**As a** user with a vestibular disorder or motion sensitivity,
**I want** the site to respect my operating system's reduced motion preference and provide a way to disable animations,
**So that** I can browse the site without experiencing dizziness, nausea, or headaches.

## Description

The site has scroll-triggered fade-in/slide-in animations on nearly every section, hover lift/scale effects on cards and buttons, possible counting animations on statistics, and potential auto-rotating carousels. A user with a vestibular disorder had to close the page within seconds due to vertigo, nausea, and headaches. The site was rated 2/10 for motion sensitivity and deemed "completely unusable" with JavaScript enabled.

## Acceptance Criteria

- [ ] A `@media (prefers-reduced-motion: reduce)` CSS media query disables all animations site-wide
- [ ] Scroll-triggered fade-in/slide-in animations are disabled when reduced motion is preferred
- [ ] Hover lift, scale, and shadow transition effects are removed or made instant (no transition duration)
- [ ] Number counting animations (statistics section) show final values immediately
- [ ] Auto-rotating carousels are paused by default; manual controls are provided
- [ ] No layout shifts occur when images or content load
- [ ] A visible "Reduce Motion" toggle is available in the site header
- [ ] The toggle preference persists across pages (via localStorage or cookie)

## Testing Instructions

1. **OS setting:** Enable "Reduce Motion" in OS accessibility settings (macOS: System Preferences > Accessibility > Display > Reduce motion; Windows: Settings > Accessibility > Visual Effects > Animation effects OFF)
2. **Reload the site** — verify no fade-ins, slide-ins, counting animations, or hover transitions occur
3. **Scroll test:** Scroll through the entire homepage — no elements should animate into view
4. **Hover test:** Hover over service cards, buttons, and links — changes should be instant with no transition
5. **Toggle test:** Click the "Reduce Motion" toggle in the header, navigate to another page, and confirm animations remain disabled
6. **Without OS setting:** Turn off the OS reduced motion setting, use only the site toggle — verify it works independently
7. **Statistics:** Navigate to the statistics section — numbers should display immediately, not count up

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | Critical |
| **Complexity** | Medium |
| **WCAG Criteria** | 2.3.3 (Animation from Interactions) |
| **Affected Users** | Motion sensitivity, vestibular disorders |

## Source Reports

- Motion Sensitivity Report
