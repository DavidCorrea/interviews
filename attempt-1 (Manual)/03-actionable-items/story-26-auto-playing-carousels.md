# Story 26: Remove Auto-Playing Carousels

## User Story

**As a** user with motion sensitivity or who uses voice control,
**I want** carousels to not auto-rotate,
**So that** I don't experience motion-triggered symptoms and can reliably interact with carousel items.

## Description

Company logos and/or award badges may be in auto-rotating carousels that create constant motion and make it difficult for voice control users to target elements. This overlaps with Story 03 (prefers-reduced-motion).

## Acceptance Criteria

- [ ] No carousel auto-rotates on page load
- [ ] Carousels have visible pause/play and previous/next controls
- [ ] Controls have accessible labels (e.g., "Pause carousel," "Next slide")
- [ ] `prefers-reduced-motion: reduce` disables all carousel animation
- [ ] Alternatively, carousels are replaced with static grid layouts

## Testing Instructions

1. **Page load:** Load the homepage and observe for 30 seconds — no carousel should auto-rotate
2. **Controls:** If carousels exist, verify visible pause, play, previous, and next buttons are present
3. **Keyboard:** Focus the carousel — verify controls are operable with Enter/Space and arrow keys
4. **Reduced motion:** Enable "Reduce Motion" in OS settings — verify carousel stops all animation
5. **Voice control:** Say "Click Pause carousel" or "Click Next slide" — verify the controls respond

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | Medium |
| **Complexity** | Low-Medium |
| **WCAG Criteria** | 2.2.2 (Pause, Stop, Hide) |
| **Affected Users** | Motion sensitivity users, voice control users |

## Source Reports

- Motion Sensitivity Report
- Voice Control Report
