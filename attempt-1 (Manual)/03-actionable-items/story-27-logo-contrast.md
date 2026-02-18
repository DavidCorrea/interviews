# Story 27: Increase Logo Contrast on White Background

## User Story

**As a** user browsing in bright light or with low contrast sensitivity,
**I want** client logos to be clearly visible against their background,
**So that** I can see which companies the business has worked with.

## Description

Several client logos (Prosci, Whirlpool, and others) use light colors that wash out on white backgrounds, especially in bright environments.

## Acceptance Criteria

- [ ] The logo section has a subtle background color (e.g., #F5F5F5) instead of pure white, OR logos have visible borders/shadows
- [ ] All client logos are distinguishable from the background in bright light conditions
- [ ] Text labels with company names appear below or alongside each logo
- [ ] Logos pass a minimum contrast check against their background

## Testing Instructions

1. **Bright light test:** View the logo section on a laptop in bright lighting — all logos should be clearly visible
2. **Visual:** Compare logos against background — none should appear to "disappear" into the white
3. **Text labels:** Verify company names are written in text next to or below each logo
4. **CSS check:** Inspect the logo section container — verify it has a non-white background or logos have borders
5. **Grayscale:** View the section in grayscale — all logos should remain distinguishable

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | Medium |
| **Complexity** | Low |
| **WCAG Criteria** | 1.4.3 (Contrast Minimum) |
| **Affected Users** | Situational contrast users, low contrast sensitivity users |

## Source Reports

- Situational Contrast Report
- Low Contrast Sensitivity Report
