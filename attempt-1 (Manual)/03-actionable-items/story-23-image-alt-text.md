# Story 23: Improve Image Alt Text

## User Story

**As a** screen reader user,
**I want** all meaningful images to have descriptive alt text,
**So that** I understand what each image conveys without being able to see it.

## Description

Award badge images may only have filename-based alt text. Case study screenshots have generic descriptions like "Prosci Interface Screenshot" rather than meaningful descriptions of what is shown.

## Acceptance Criteria

- [ ] Award badges have descriptive alt text (e.g., "2025 Clutch Top Salesforce Company award for the United States")
- [ ] Case study screenshots describe the content shown (e.g., "Screenshot of Prosci's 360-degree customer view dashboard in Salesforce")
- [ ] Company logos have alt text with the company name
- [ ] Purely decorative images have `alt=""` or `aria-hidden="true"`
- [ ] No image uses filename-based alt text (e.g., "image-2025-badge.png")

## Testing Instructions

1. **Screen reader:** Navigate the homepage with NVDA — listen to what is announced for each image; verify it is meaningful
2. **Alt text audit:** Use an accessibility tool (axe, WAVE) to flag images with missing or generic alt text
3. **Decorative images:** Verify decorative images (backgrounds, visual separators) are hidden from screen readers
4. **Manual check:** Right-click on each award badge and case study image > Inspect — verify the `alt` attribute contains a descriptive sentence
5. **Logo check:** In the client logos section, verify each logo image has an `alt` with the company name

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | Medium |
| **Complexity** | Low |
| **WCAG Criteria** | 1.1.1 (Non-text Content) |
| **Affected Users** | Screen reader users |

## Source Reports

- Screen Reader Report
