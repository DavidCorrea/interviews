# Story 15: Add Non-Color Visited Link Indicators

## User Story

**As a** color blind user,
**I want** visited links to be visually distinct from unvisited links through non-color cues,
**So that** I can tell which pages I've already visited.

## Description

Standard blue-to-purple visited link color change is invisible to users with tritanopia (blue-yellow color blindness). They cannot tell which "Learn More" links or blog posts they have already clicked.

## Acceptance Criteria

- [ ] Visited links have a visual indicator beyond just color change (e.g., underline style change, reduced opacity, different font weight, or a small icon)
- [ ] The visited state is clearly distinguishable from unvisited state in grayscale view
- [ ] The change applies to all navigational links (service links, blog links, case study links)

## Testing Instructions

1. **Visit links:** Click on several "Learn More" links and blog links, then return to the homepage
2. **Visual check:** Verify visited links look different from unvisited links through something other than color (e.g., underline, opacity, icon)
3. **Grayscale test:** Apply a grayscale CSS filter (`filter: grayscale(100%)`) to the page — verify visited and unvisited links are still distinguishable
4. **Color blind simulation:** Use a color blindness simulator (e.g., Chrome DevTools > Rendering > Emulate vision deficiencies > Tritanopia) — verify visited links are distinguishable

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | High |
| **Complexity** | Low |
| **WCAG Criteria** | 1.4.1 (Use of Color) |
| **Affected Users** | Blue-yellow color blind users |

## Source Reports

- Blue-Yellow Color Blind Report
