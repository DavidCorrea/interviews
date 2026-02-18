# Story 22: Fix Sticky Header at High Zoom Levels

## User Story

**As a** user browsing at high zoom levels (200%+),
**I want** the sticky header to either collapse or become non-sticky,
**So that** it doesn't consume most of my visible screen area.

## Description

If the navigation header is sticky/fixed, it may consume 30-40% of the visible area at 300% zoom, leaving little space for actual content.

## Acceptance Criteria

- [ ] At viewport widths equivalent to 200%+ zoom (≤640px), the header is either non-sticky or auto-hides on scroll down
- [ ] At 300% zoom, the header takes up no more than 15% of the viewport height
- [ ] Content beneath the header is not obscured or overlapped
- [ ] The header remains accessible (can be reached by scrolling to top or via a menu button)

## Testing Instructions

1. **Zoom test:** Set browser zoom to 300% — verify the header does not occupy an excessive portion of the screen
2. **Scroll test:** At 300% zoom, scroll down — if the header auto-hides, verify it reappears when scrolling up
3. **Content access:** At 300% zoom, verify the main content is fully visible and not hidden behind the header
4. **Navigation:** At 300% zoom, verify the navigation menu is still accessible (via hamburger menu or scroll-to-top)
5. **Breakpoint test:** Use DevTools to gradually narrow the viewport — identify at what width the header behavior changes

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | Medium |
| **Complexity** | Low-Medium |
| **WCAG Criteria** | 1.4.10 (Reflow) |
| **Affected Users** | Low vision magnifier users |

## Source Reports

- Low Vision Screen Magnifier Report
