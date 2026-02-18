# Story 25: Replace Narrow Dropdown Menus with Larger Controls

## User Story

**As a** user with motor impairments,
**I want** form selection controls to be large and easy to target,
**So that** I can select the correct option without accidentally choosing the wrong one.

## Description

The contact form uses dropdown menus with narrow, tightly-stacked options. Users with hand tremors accidentally select wrong options and struggle with precision.

## Acceptance Criteria

- [ ] Dropdown `<select>` elements in the contact form are replaced with radio buttons or large card-style options
- [ ] Each option has a minimum clickable height of 44px with spacing between options
- [ ] The form still submits correctly with the new control type
- [ ] If dropdowns must remain, options have increased height and spacing

## Testing Instructions

1. **Visual:** Open the contact form — verify dropdown fields have been replaced with radio buttons or card-style options
2. **Click test:** Attempt to select each option — each should be easy to tap/click without precision
3. **Spacing:** Measure spacing between options — at least 8px gap between each
4. **Form submission:** Fill out and submit the form using the new controls — verify data is submitted correctly
5. **Keyboard:** Tab to the new controls and use arrow keys or Enter — verify keyboard operability
6. **Mobile:** Test on mobile — verify touch targets are comfortable

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | Medium |
| **Complexity** | Medium |
| **WCAG Criteria** | 2.5.8 (Target Size) |
| **Affected Users** | Motor impairment users |

## Source Reports

- Motor Impairment Report
