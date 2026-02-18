# Story 14: Remove Hover-Dependent Interactions

## User Story

**As a** voice control or motor-impaired user,
**I want** all interactive content to be accessible via click or keyboard (not hover),
**So that** I can access menus and features without needing precise mouse control.

## Description

Navigation menus may require hovering to reveal submenus. Hover effects on cards cause confusion for tremor users (constant on/off triggering). Voice control users cannot trigger hover states at all.

## Acceptance Criteria

- [ ] All dropdown/navigation menus open on click (not hover)
- [ ] Menus are also operable via keyboard (Enter/Space to open, arrow keys to navigate, Escape to close)
- [ ] Card hover animations are either removed or simplified to instant state changes (no transitions)
- [ ] All content that was previously revealed on hover is accessible without hovering
- [ ] No functionality is hidden behind hover-only interactions

## Testing Instructions

1. **Click menus:** On desktop, click (not hover) on any navigation item with a submenu — it should open
2. **Keyboard menus:** Tab to a navigation item with a submenu, press Enter — submenu should open; use arrow keys to navigate; press Escape to close
3. **Voice control:** Using macOS Voice Control or Dragon, say "Click Services" (or equivalent) — the menu should open without requiring hover
4. **Hover effects:** Move mouse over service cards — verify there are no distracting lift/scale/shadow transitions (changes should be instant or absent)
5. **Content access:** Verify all links, text, and controls previously hidden behind hover are always visible or accessible via click

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | High |
| **Complexity** | Medium |
| **WCAG Criteria** | 2.1.1 (Keyboard) |
| **Affected Users** | Voice control users, motor impairment users |

## Source Reports

- Voice Control Report
- Motor Impairment Report
