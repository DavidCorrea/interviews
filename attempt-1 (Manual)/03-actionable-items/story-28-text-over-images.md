# Story 28: Avoid Text Overlaid on Images

## User Story

**As a** user with low vision or browsing in bright light,
**I want** important text to be placed on solid-color backgrounds (not over photographs),
**So that** I can always read the text regardless of viewing conditions.

## Description

In some sections, text is placed over photographs or background images. When the background washes out (bright environments, high zoom), the text becomes unreadable.

## Acceptance Criteria

- [ ] All important text sits on a solid-color background, not directly over a photograph
- [ ] If text must overlay an image, a solid (not semi-transparent) dark overlay ensures at least 4.5:1 contrast ratio
- [ ] Text over images meets WCAG contrast requirements against the darkest AND lightest areas of the underlying image
- [ ] Alternative layouts are used for hero sections if they previously relied on text-over-image

## Testing Instructions

1. **Visual audit:** Scroll through all pages — identify any text placed over photographs or background images
2. **Contrast check:** For any remaining text-over-image instances, measure contrast ratio against both the darkest and lightest areas of the image using a contrast picker tool
3. **Bright light:** View text-over-image sections in bright lighting — text must remain readable
4. **High zoom:** At 300% zoom, verify text-over-image sections are still readable (image may be cropped but text contrast must hold)
5. **Overlay opacity:** If overlays are used, inspect the CSS `background-color` — it should be solid or near-solid (opacity > 0.85)

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | Medium |
| **Complexity** | Medium |
| **WCAG Criteria** | 1.4.3 (Contrast Minimum) |
| **Affected Users** | Low vision magnifier users, seniors, situational contrast users |

## Source Reports

- Low Vision Screen Magnifier Report
- Senior User Report
- Situational Contrast Report
