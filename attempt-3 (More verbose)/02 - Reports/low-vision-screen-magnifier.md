# Accessibility Technical Report: Low Vision User (Screen Magnifier)

**Persona:** Elena Vasquez (Low Vision, Screen Magnifier)  
**Website:** https://launchpadlab.com/  
**Date:** February 16, 2025  
**Testing Focus:** Reflow, zoom support, sticky header impact, horizontal scrolling, and usability at 200–400% zoom.

---

## Executive Summary

The site fails to support users who rely on browser zoom (200–400%) for magnification. Content does not reflow to a single column at 200%+ zoom, causing horizontal scrollbars and forced horizontal panning. The sticky header consumes 30–40% of the viewport at 300% zoom, severely reducing visible content. These issues violate WCAG 2.1 Level AA success criteria 1.4.10 (Reflow) and 1.4.4 (Resize Text). Severity ranges from High to Critical. The primary task (find what the company does and how to contact them) is completable but requires disproportionate effort and causes significant frustration.

---

## Issues Identified

### 1. Content Does Not Reflow at 200%+ Zoom (Horizontal Scrolling)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.10 Reflow — Level AA |
| **Severity** | Critical |
| **Finding** | Content does not reflow to a single column at 200%, 300%, or 400% zoom. Multi-column grids (6 service boxes, statistics, award badges, client logos, testimonials, case studies) retain multi-column layout. Horizontal scrollbars appear. Users must pan horizontally to read text and access content. |
| **Impact** | Magnifier users cannot read comfortably. Horizontal scrolling is a deal-breaker—users lose place, reorient constantly, and may abandon. Violates WCAG 2.1 Level AA. |
| **Fix** | Implement responsive reflow. At 320px viewport width (equivalent to 400% zoom on 1280px screen), content must reflow to single column. Use flexible layouts (flexbox, grid with minmax), avoid fixed widths, ensure no horizontal overflow for text content. Test at 200%, 300%, 400% zoom. |
| **WCAG Criterion** | [1.4.10 Reflow](https://www.w3.org/WAI/WCAG21/Understanding/reflow.html) |

---

### 2. Sticky Header Consumes 30–40% of Viewport at 300% Zoom

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.10 Reflow (interpreted), 2.4.1 Bypass Blocks |
| **Severity** | High |
| **Finding** | Sticky header remains fixed at full size when scrolling. At 300% zoom, header height consumes approximately 30–40% of viewport height. Header does not shrink or collapse on scroll. User sees minimal new content per scroll. |
| **Impact** | Severe reduction in usable viewport. User must scroll excessively to read content. Header becomes obstacle rather than aid. Magnifier users see only a fraction of the page at once; header further reduces that fraction. |
| **Fix** | Shrink header on scroll-down (e.g., reduce to logo + thin bar). Or collapse to minimal height. Or allow header to scroll off. Ensure header does not exceed ~20% of viewport at 300% zoom. Provide skip link to bypass header and reach main content. |
| **WCAG Criterion** | 1.4.10 Reflow; 2.4.1 Bypass Blocks |

---

### 3. Multi-Column Grids Force Horizontal Panning

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.10 Reflow — Level AA |
| **Severity** | Critical |
| **Finding** | Six service boxes displayed in multi-column grid. At 400% zoom, grid does not collapse to single column. Statistics, award badges, client logos, testimonials, case studies—all retain multi-column layout. User must scroll horizontally to access all content. |
| **Impact** | User cannot read or interact with content without horizontal panning. Violates 1.4.10. Content is effectively inaccessible to magnifier users at high zoom. |
| **Fix** | Use CSS media queries or container queries. At viewport width ≤320px (400% zoom equivalent), switch to single-column layout. Stack service boxes, statistics, testimonials vertically. Ensure no horizontal scroll for primary content. |
| **WCAG Criterion** | 1.4.10 Reflow |

---

### 4. Text Resizing Causes Layout Breakdown

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.4 Resize Text — Level AA |
| **Severity** | High |
| **Finding** | At 200%+ zoom, layout does not adapt. Text may scale, but containers do not reflow. Fixed-width elements cause overflow. Horizontal scrollbars appear. Content may truncate or clip. |
| **Impact** | Users who rely on zoom cannot access content without horizontal scrolling. Violates 1.4.4—content must be readable and functional when text is resized up to 200%. |
| **Fix** | Use relative units (rem, em) for font sizes. Ensure containers use max-width and flexible layouts. Avoid overflow: hidden that clips content. Test at 200% zoom; verify no horizontal scroll for text. |
| **WCAG Criterion** | [1.4.4 Resize Text](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html) |

---

### 5. Context Loss When Scrolling (No Persistent Landmarks)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.1 Bypass Blocks, 1.3.1 Info and Relationships |
| **Severity** | Medium |
| **Finding** | No persistent section labels or sticky subheadings. When user scrolls, section headings disappear. User loses orientation: "Am I in testimonials or case studies?" No skip link to main content. |
| **Impact** | Disorientation. User must scroll back to reorient. Inefficient. Increases cognitive load. Magnifier users see only a sliver of the page; landmarks are essential. |
| **Fix** | Add skip link ("Skip to main content") at top of page. Consider sticky section labels that persist while scrolling through section. Ensure heading hierarchy is clear and programmatically exposed. |
| **WCAG Criterion** | 2.4.1 Bypass Blocks; 1.3.1 Info and Relationships |

---

### 6. Touch Target Size (Nav, CTA, Form Controls)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.5.5 Target Size — Level AAA (2.5.8 Level AA for touch) |
| **Severity** | Medium |
| **Finding** | Nav links (Work, Services, About, "Connect with an Expert") may not meet 44×44px minimum. Form controls and buttons on Contact page—size not verified but reported as feeling cramped at 300% zoom. |
| **Impact** | Misclicks. User must retry. Frustration. Low vision users need larger targets for accurate selection. |
| **Fix** | Ensure all interactive elements meet 44×44px minimum (or 24×24px with adequate spacing). Increase padding on nav links. Ensure "Connect with an Expert" CTA is large and high contrast. Audit form controls. |
| **WCAG Criterion** | 2.5.5 Target Size; 2.5.8 Target Size (Minimum) — Level AA |

---

### 7. Contact Page: Testimonials Above Form Create Excessive Scrolling

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.1 Bypass Blocks, 1.4.10 Reflow |
| **Severity** | Medium |
| **Finding** | Contact page places five long testimonials above the contact form. At 300% zoom with sticky header consuming viewport, user must scroll extensively to reach form. No skip link to form. |
| **Impact** | User loses patience. May abandon before reaching form. Contact path is obscured. |
| **Fix** | Add "Skip to contact form" link. Or move testimonials below form. Or reduce testimonial count on Contact page. Ensure form is reachable within 2–3 scrolls at 300% zoom. |
| **WCAG Criterion** | 2.4.1 Bypass Blocks |

---

## Summary Table

| Issue | WCAG | Severity | Priority |
|-------|------|----------|----------|
| Content does not reflow (horizontal scroll) | 1.4.10 | Critical | P0 |
| Multi-column grids force horizontal panning | 1.4.10 | Critical | P0 |
| Sticky header consumes 30–40% viewport | 1.4.10, 2.4.1 | High | P0 |
| Text resizing causes layout breakdown | 1.4.4 | High | P0 |
| Context loss (no persistent landmarks) | 2.4.1, 1.3.1 | Medium | P1 |
| Touch target size | 2.5.5, 2.5.8 | Medium | P1 |
| Contact form obscured by testimonials | 2.4.1 | Medium | P1 |

---

## Recommended Remediation Order

1. **Implement reflow** — Ensure content reflows to single column at 320px viewport width (400% zoom). Fix multi-column grids, statistics, testimonials, case studies. Eliminate horizontal scrolling for text content.
2. **Address sticky header** — Shrink or collapse header on scroll. Or allow it to scroll off. Ensure it does not exceed ~20% of viewport at 300% zoom.
3. **Fix text resizing** — Use relative units. Ensure layout adapts at 200% zoom. No horizontal scroll for body content.
4. **Add skip link** — "Skip to main content" at top. "Skip to contact form" on Contact page.
5. **Audit touch targets** — Ensure nav links, CTA, form controls meet 44×44px minimum.
6. **Reorganize Contact page** — Move testimonials below form or add skip link. Reduce scroll required to reach form.

---

## References

- [WCAG 2.1 Success Criterion 1.4.10 Reflow (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/reflow.html)
- [WCAG 2.1 Success Criterion 1.4.4 Resize Text (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
- [WCAG 2.1 Success Criterion 2.4.1 Bypass Blocks (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
- [WCAG 2.1 Success Criterion 2.5.5 Target Size (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/target-size.html)
- [W3C Understanding Reflow](https://www.w3.org/WAI/WCAG21/Understanding/reflow.html)
