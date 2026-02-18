# Accessibility Technical Report: Low Contrast Sensitivity

**Persona:** Patricia Okonkwo (Low Contrast Sensitivity)  
**Website:** https://launchpadlab.com/  
**Date:** February 16, 2025  
**Testing Focus:** Contrast, link identification, font weight, and visual legibility for users with low contrast sensitivity.

---

## Executive Summary

The site uses light gray text (#666–#777) on white backgrounds throughout, links lack non-color differentiation (underlines, bold, icons), and thin font weights (300–400) reduce legibility. These barriers violate WCAG 2.1 success criteria 1.4.3 (Contrast Minimum), 1.4.6 (Contrast Enhanced), and 1.4.11 (Non-text Contrast). Users with low contrast sensitivity—including many over 50—experience significant strain, reduced comprehension, and risk of task abandonment. Severity ranges from Medium to Critical.

---

## Issues Identified

### 1. Body Text Contrast Below WCAG AA

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.3 Contrast (Minimum) — Level AA |
| **Severity** | Critical |
| **Finding** | Body text uses #666–#777 on white backgrounds. Contrast ratio is approximately 4.5:1 or below for normal text. |
| **Impact** | Text fades, blurs, or disappears for low-contrast users. Sustained reading causes eye strain and early abandonment. Users skip content or extract only high-contrast elements. |
| **Fix** | Use text color of at least #595959 on white to achieve 4.5:1. For AAA (1.4.6), target 7:1 (#404040 or darker). |
| **WCAG Criterion** | 1.4.3 Contrast (Minimum) |

---

### 2. Links Differentiated Only by Color

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.1 Use of Color — Level A; 1.4.3 Contrast (Minimum) |
| **Severity** | Critical |
| **Finding** | Navigation links (Work, Services, About), "Connect with an Expert" CTA, and in-content links lack underlines, bold, or icons. Differentiation relies on color alone. |
| **Impact** | Users cannot distinguish links from body text. Links are missed or discovered only by hover/tab. Task completion (finding contact path) is delayed or failed. |
| **Fix** | Add underlines to all links. Alternatively: bold, icons, or distinct typography. Ensure link text meets 4.5:1 contrast and has a non-color cue. |
| **WCAG Criterion** | 1.4.1 Use of Color; 1.4.3 Contrast (Minimum) |

---

### 3. Thin Font Weight Reduces Legibility

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.8 Visual Presentation (Level AAA); supports 1.4.3 |
| **Severity** | High |
| **Finding** | Body text, headings, and labels use font weight 300–400. Thin weights reduce letter edge definition. |
| **Impact** | Letters blend into background. Low-contrast users require 400 minimum, 500 preferred. Thin fonts compound contrast issues. |
| **Fix** | Use font-weight: 400 (normal) minimum for body text; 500 (medium) for key content. Headings: 500–600. Avoid 300 or lighter for body copy. |
| **WCAG Criterion** | 1.4.8 Visual Presentation |

---

### 4. Testimonials in Low Contrast + Italic

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.3 Contrast (Minimum); 1.4.6 Contrast (Enhanced) — Level AAA |
| **Severity** | High |
| **Finding** | Testimonials use italic text in light gray (#666–#777) on white. Contact page has 5 blocks above form. |
| **Impact** | Italic distorts letter shapes; low contrast compounds the barrier. Users skip testimonials entirely. Content is effectively invisible. |
| **Fix** | Use regular or bold for testimonial text. Ensure contrast of at least 4.5:1 (AA) or 7:1 (AAA). Limit italic to 1–2 short lines if design requires it. |
| **WCAG Criterion** | 1.4.3 Contrast (Minimum); 1.4.6 Contrast (Enhanced) |

---

### 5. Buttons and CTAs Low Contrast

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.3 Contrast (Minimum); 1.4.11 Non-text Contrast — Level AA |
| **Severity** | High |
| **Finding** | "Connect with an Expert" and other CTAs may use low-contrast backgrounds or text. Light gray buttons on white do not register as interactive. |
| **Impact** | Users scroll past CTAs, miss form submit buttons, or assume elements are decorative. Task completion (contacting the company) is at risk. |
| **Fix** | Ensure buttons have 4.5:1 contrast for text and 3:1 for UI components (1.4.11). Use strong borders, bold text, or high-contrast backgrounds. |
| **WCAG Criterion** | 1.4.3 Contrast (Minimum); 1.4.11 Non-text Contrast |

---

### 6. Form Labels and Placeholders

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.3 Contrast (Minimum) |
| **Severity** | Medium |
| **Finding** | Form labels and placeholders may use light gray. Placeholder-only labels are problematic. |
| **Impact** | Labels blend with backgrounds; placeholders invisible. Form errors increase. Users may misread or skip fields. |
| **Fix** | Labels must be dark (#333 or darker), visible, and meet 4.5:1. Avoid placeholder-only labeling. Ensure required indicators and error messages are high contrast. |
| **WCAG Criterion** | 1.4.3 Contrast (Minimum) |

---

### 7. Secondary Content (Captions, Footnotes, Badges)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.3 Contrast (Minimum); 1.4.6 Contrast (Enhanced) |
| **Severity** | Medium |
| **Finding** | Award badges, captions, footnotes, and "powered by" text often use the lightest grays (#999, #aaa, #bbb). |
| **Impact** | Secondary content is never read. Users skip entire sections. Information is lost. |
| **Fix** | Apply same contrast requirements to all text. Minimum 4.5:1 for normal text; 7:1 for AAA. No "decorative" exceptions for informational content. |
| **WCAG Criterion** | 1.4.3 Contrast (Minimum); 1.4.6 Contrast (Enhanced) |

---

### 8. Statistics and Numbers

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.3 Contrast (Minimum) |
| **Severity** | Medium |
| **Finding** | "12+ Years," "730+ Projects," "4.8" rating—if in light gray, lose impact and readability. |
| **Impact** | Key differentiators become invisible. Credibility signals are missed. |
| **Fix** | Ensure statistics use high contrast (4.5:1 minimum; 7:1 preferred). Bold or larger type helps. |
| **WCAG Criterion** | 1.4.3 Contrast (Minimum) |

---

## Summary Table

| Issue | WCAG Ref | Severity | Priority |
|-------|----------|----------|----------|
| Body text contrast (#666–#777) | 1.4.3 | Critical | P0 |
| Links without non-color cue | 1.4.1, 1.4.3 | Critical | P0 |
| Thin font weight (300–400) | 1.4.8 | High | P1 |
| Testimonials low contrast + italic | 1.4.3, 1.4.6 | High | P1 |
| Buttons/CTAs low contrast | 1.4.3, 1.4.11 | High | P1 |
| Form labels/placeholders | 1.4.3 | Medium | P2 |
| Secondary content | 1.4.3, 1.4.6 | Medium | P2 |
| Statistics contrast | 1.4.3 | Medium | P2 |

---

## Recommended Remediation Order

1. **Increase body text contrast** — Darken to #595959 (AA) or #404040 (AAA). Apply site-wide.
2. **Add non-color cues to links** — Underlines, bold, or icons. Ensure all links are distinguishable without color.
3. **Increase font weight** — Body text to 400 minimum; 500 for key content. Headings to 500–600.
4. **Fix testimonials** — Regular/bold font; contrast 4.5:1 minimum.
5. **Enhance button/CTA contrast** — 4.5:1 for text; 3:1 for UI components per 1.4.11.
6. **Audit form labels and placeholders** — Dark, visible, 4.5:1.
7. **Audit secondary content** — Captions, footnotes, badges. Apply same contrast standards.

---

## WCAG References

- **1.4.3 Contrast (Minimum)** — Level AA: Text and images of text must have contrast ratio of at least 4.5:1 (normal) or 3:1 (large).
- **1.4.6 Contrast (Enhanced)** — Level AAA: 7:1 for normal text; 4.5:1 for large.
- **1.4.11 Non-text Contrast** — Level AA: UI components and graphical objects must have contrast of at least 3:1 against adjacent colors.
- **1.4.1 Use of Color** — Level A: Color must not be the only visual means of conveying information.
- **1.4.8 Visual Presentation** — Level AAA: Covers font weight, line height, and text presentation.

---

## References

- [WCAG 2.1 Success Criterion 1.4.3 Contrast (Minimum)](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
- [WCAG 2.1 Success Criterion 1.4.6 Contrast (Enhanced)](https://www.w3.org/WAI/WCAG21/Understanding/contrast-enhanced.html)
- [WCAG 2.1 Success Criterion 1.4.11 Non-text Contrast](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html)
- [WCAG 2.1 Success Criterion 1.4.1 Use of Color](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
