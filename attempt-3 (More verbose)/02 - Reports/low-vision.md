# Accessibility Technical Report: Low Vision User (Browser Zoom)

**Persona:** Marcus Webb (Low Vision, No Screen Magnifier)  
**Website:** https://launchpadlab.com/  
**Date:** February 16, 2025  
**Testing Focus:** Text readability, font weight, contrast, touch target size, zoom behavior, and layout reflow for users who rely on browser zoom (150–200%).

---

## Executive Summary

The site is navigable and the primary task (find what the company does and how to contact them) is completable at 150–200% browser zoom. However, multiple barriers create significant strain for low vision users: low contrast text, thin font weights, small touch targets, and insufficient line height. Layout reflows at zoom (no horizontal scrollbar on main content), which is positive. Severity ranges from Medium to High. WCAG 2.1 Level AA and AAA criteria are not fully met.

---

## Issues Identified

### 1. Low Contrast (Body Text)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.3 Contrast (Minimum) — Level AA |
| **Severity** | High |
| **Finding** | Body text appears in light gray (#666–#777) on white backgrounds. Contrast ratio likely below 4.5:1 for normal text. Service descriptions, testimonials, form labels, and footer text affected. |
| **Impact** | Letters are harder to distinguish; reading requires leaning in and increased zoom. Users fatigue quickly. Content may be skipped or misread. |
| **Fix** | Use text color of at least #595959 on white to achieve 4.5:1. For AAA (7:1), use #404040 or darker. Apply to all body text, labels, captions, and secondary content. |
| **WCAG Criterion** | 1.4.3 Contrast (Minimum) |

---

### 2. Thin or Light Font Weight

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.8 Visual Presentation (Level AAA) |
| **Severity** | High |
| **Finding** | Body text uses font weight 300–400. Thin weights reduce letter shape distinction and stroke visibility. |
| **Impact** | Letters blur; strokes are too fine to distinguish at 12–18 inch viewing distance. Reading speed drops; re-reading increases. Users report text "fading" into background. |
| **Fix** | Use font-weight: 500 (medium) minimum for body text. Prefer 600 for headings. Avoid 300 or lighter for body copy. |
| **WCAG Criterion** | 1.4.8 Visual Presentation — "techniques for visual presentation of text" |

---

### 3. Insufficient Touch Target Size

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.5.5 Target Size (Level AAA) |
| **Severity** | High |
| **Finding** | Navigation links (Work, Services, About), "View project" links, footer links, and possibly form submit button have clickable areas smaller than 44×44 CSS pixels. |
| **Impact** | Users with reduced visual acuity or motor precision misclick, activate wrong elements, or require multiple attempts. Extra time and concentration needed to align cursor. |
| **Fix** | Ensure all interactive elements have minimum 44×44px touch target. Add padding to links; increase button size. Provide 8px+ spacing between adjacent targets. |
| **WCAG Criterion** | 2.5.5 Target Size |

---

### 4. Insufficient Line Height

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.8 Visual Presentation (Level AAA) |
| **Severity** | Medium |
| **Finding** | Line height appears below 1.5 (possibly 1.3–1.4) for body text. |
| **Impact** | Lines run together; user loses place when tracking across lines. Re-reading and line-skipping increase. |
| **Fix** | Set line-height to at least 1.5 for body text. Prefer 1.6–1.8 for dense content. |
| **WCAG Criterion** | 1.4.8 Visual Presentation |

---

### 5. Text Resize and Reflow

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.4 Resize Text (Level AA), 1.4.10 Reflow (Level AA) |
| **Severity** | Low–Medium |
| **Finding** | Layout reflows at 150–200% zoom; no horizontal scrollbar on main content. Positive. However, fixed header may overlap content when scrolled. Some text in images or SVGs may not scale. |
| **Impact** | If reflow fails, zoom users cannot use the site. Current behavior is acceptable but should be verified at 200% across all pages. Fixed elements obscuring content would be a failure. |
| **Fix** | Ensure all content reflows at 200% zoom. Use relative units (rem, em) for font sizes. Verify fixed header does not obscure body content. Avoid fixed-width containers that cause overflow. |
| **WCAG Criterion** | 1.4.4 Resize Text, 1.4.10 Reflow |

---

### 6. Small Body Text

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.4 Resize Text, 1.4.8 Visual Presentation |
| **Severity** | Medium |
| **Finding** | Body text may be below 16px at default zoom. Low vision users require 16px minimum; 18px+ preferred for comfortable reading. |
| **Impact** | Users must zoom to 175–200% to read comfortably. Combined with thin fonts and low contrast, even zoomed text strains. |
| **Fix** | Set base body font size to 16px minimum (1rem). Use rem/em for scaling. Ensure text scales with user preferences (font-size: 100%; support for user font-size settings). |
| **WCAG Criterion** | 1.4.4 Resize Text, 1.4.8 Visual Presentation |

---

### 7. Testimonials (Italic, Low Contrast)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.3 Contrast, 1.4.8 Visual Presentation |
| **Severity** | High |
| **Finding** | Testimonials use italic text in light gray. Long blocks (4–7 lines each). Contact page has 5 testimonial blocks above form. |
| **Impact** | Italic reduces stroke definition; combined with low contrast, text is illegible for many low vision users. Content is skipped entirely. |
| **Fix** | Use regular or bold for testimonial text. Ensure contrast meets 4.5:1 minimum. Limit italic to 1–2 short lines if design requires. Consider shorter excerpts or bullet summaries. |
| **WCAG Criterion** | 1.4.3 Contrast (Minimum), 1.4.8 Visual Presentation |

---

### 8. Form Labels and Placeholders

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.3 Contrast, 3.3.2 Labels or Instructions |
| **Severity** | Medium |
| **Finding** | Form labels may use light gray. Placeholders in light gray are problematic. Submit button size and contrast may be borderline. |
| **Impact** | Labels hard to read; risk of misreading (e.g., "Company" vs "Contact"). Placeholder-only labels fail when placeholder disappears. Submit button may be difficult to locate or activate. |
| **Fix** | Use visible, persistent labels with 4.5:1 contrast. Avoid placeholder-only labeling. Ensure submit button is at least 44×44px with sufficient contrast. |
| **WCAG Criterion** | 1.4.3 Contrast, 3.3.2 Labels or Instructions |

---

### 9. Faint Focus Indicators

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.7 Focus Visible (Level AA) |
| **Severity** | Medium |
| **Finding** | Focus indicators may be faint or low contrast. Known risk from scope. |
| **Impact** | Keyboard users lose place when tabbing. Low vision users cannot see which element is focused. |
| **Fix** | Ensure focus indicator has 3:1 contrast against adjacent colors. Minimum 2px outline or border. Do not rely on color alone. |
| **WCAG Criterion** | 2.4.7 Focus Visible |

---

## Summary Table

| Issue | WCAG | Severity | Priority |
|-------|------|----------|----------|
| Low contrast (gray text) | 1.4.3 | High | P0 |
| Thin font weight | 1.4.8 | High | P0 |
| Insufficient touch target size | 2.5.5 | High | P0 |
| Italic/low-contrast testimonials | 1.4.3, 1.4.8 | High | P0 |
| Insufficient line height | 1.4.8 | Medium | P1 |
| Small body text | 1.4.4, 1.4.8 | Medium | P1 |
| Form labels/placeholders | 1.4.3, 3.3.2 | Medium | P1 |
| Faint focus indicators | 2.4.7 | Medium | P1 |
| Text resize/reflow | 1.4.4, 1.4.10 | Low–Medium | P2 |

---

## Recommended Remediation Order

1. **Increase contrast** — Darken all body text, labels, and secondary content to meet WCAG AA (4.5:1) minimum; target AAA (7:1) where possible.
2. **Increase font weight** — Body text to 500 minimum; headings to 600. Eliminate 300–400 weight for body copy.
3. **Enlarge touch targets** — All interactive elements to 44×44px minimum. Add padding to nav links, "View project" links, footer links. Ensure submit button meets target size.
4. **Fix testimonials** — Use regular/bold text; ensure contrast. Limit italic to 1–2 lines if required.
5. **Increase line height** — Body text to 1.5 minimum; 1.6+ for dense sections.
6. **Set base font size** — 16px minimum for body text. Use rem/em for scaling.
7. **Improve form labels** — Visible labels with sufficient contrast. Avoid placeholder-only. Enlarge submit button.
8. **Strengthen focus indicators** — 3:1 contrast, 2px minimum. Visible on all interactive elements.
9. **Verify zoom and reflow** — Test at 150%, 175%, 200% zoom. Confirm no horizontal scroll, no overlapping fixed elements.

---

## References

- [WCAG 2.1 Success Criterion 1.4.3 Contrast (Minimum)](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
- [WCAG 2.1 Success Criterion 1.4.4 Resize Text](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
- [WCAG 2.1 Success Criterion 1.4.8 Visual Presentation (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/visual-presentation.html)
- [WCAG 2.1 Success Criterion 1.4.10 Reflow](https://www.w3.org/WAI/WCAG21/Understanding/reflow.html)
- [WCAG 2.1 Success Criterion 2.5.5 Target Size (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/target-size.html)
- [WCAG 2.1 Success Criterion 2.4.7 Focus Visible](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)
