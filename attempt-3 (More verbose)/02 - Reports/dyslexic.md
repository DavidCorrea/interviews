# Accessibility Technical Report: Dyslexic User

**Persona:** Jordan Chen (Dyslexic)  
**Website:** https://launchpadlab.com/  
**Date:** February 16, 2025  
**Testing Focus:** Typography, contrast, structure, and readability for users with dyslexia.

---

## Executive Summary

The site is navigable and the primary task (find what the company does and how to contact them) is completable. However, multiple typographic and structural barriers create significant cognitive load for dyslexic users. Light gray text, thin font weights, tight line spacing, long paragraphs, and italic testimonial blocks violate WCAG 2.1 Level AAA success criteria and best practices for readability. Severity ranges from Medium to High.

---

## Issues Identified

### 1. Low Contrast (Body Text)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.3 Contrast (Minimum) — Level AA |
| **Severity** | High |
| **Finding** | Body text appears in light gray (#666–#777) on white backgrounds. Contrast ratio likely below 4.5:1 for normal text. |
| **Impact** | Letters are harder to distinguish; increases letter confusion (b/d, p/q) and reading fatigue. Dyslexic users report text "dissolving" or "fading" into the background. |
| **Fix** | Use text color of at least #595959 (or darker) on white to achieve 4.5:1. For AAA, target 7:1 (#404040 or darker). |
| **WCAG Criterion** | 1.4.3 Contrast (Minimum) |

---

### 2. Thin or Light Font Weight

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.8 Visual Presentation (Level AAA) |
| **Severity** | Medium–High |
| **Finding** | Body text uses font weight 300–400. Thin weights reduce letter shape distinction. |
| **Impact** | Letters blend; "m" and "n," "r" and "n" become harder to parse. Reading speed drops; re-reading increases. |
| **Fix** | Use font-weight: 400 (normal) minimum for body text. Prefer 500 (medium) for improved legibility. Avoid 300 or lighter for body copy. |
| **WCAG Criterion** | 1.4.8 Visual Presentation — "techniques for visual presentation of text and images of text" |

---

### 3. Insufficient Line Height

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.8 Visual Presentation (Level AAA) |
| **Severity** | Medium |
| **Finding** | Line height appears below 1.5 (possibly 1.3–1.4). |
| **Impact** | Lines run together; user loses place, skips lines, or reads the same line twice. Tracking across lines becomes difficult. |
| **Fix** | Set line-height to at least 1.5 for body text. Prefer 1.6–1.8 for dense content. Ensure adequate spacing between paragraphs. |
| **WCAG Criterion** | 1.4.8 Visual Presentation |

---

### 4. Long Paragraphs (Dense Prose)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.8 Visual Presentation (Level AAA) |
| **Severity** | Medium |
| **Finding** | Service descriptions and other content use paragraphs of 5+ lines without breaks. |
| **Impact** | Walls of text overwhelm; user loses place, re-reads, or abandons. Sustained reading accuracy drops. |
| **Fix** | Limit paragraphs to 2–4 sentences. Use bullet points or numbered lists for service descriptions. Add subheadings to break long sections. |
| **WCAG Criterion** | 1.4.8 Visual Presentation — "blocks of text are no wider than 80 characters" and "text is not justified" |

---

### 5. Italic Text Blocks (Testimonials)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.8 Visual Presentation (Level AAA) |
| **Severity** | High |
| **Finding** | Testimonials are presented as long blocks of italic text (4–7 lines each). Contact page has 5 testimonial blocks above the form. |
| **Impact** | Italics distort letter shapes; readability drops significantly. Dyslexic users may skip entirely or misread. |
| **Fix** | Use regular or bold for testimonial text. If italics are required for design, limit to 1–2 short lines. Provide bullet summaries or shorter excerpts. |
| **WCAG Criterion** | 1.4.8 Visual Presentation — "text is not justified" and "text can be resized without loss of content or functionality" |

---

### 6. Line Length Exceeds Recommendation

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.8 Visual Presentation (Level AAA) |
| **Severity** | Low–Medium |
| **Finding** | Full-width or near-full-width text blocks create line lengths exceeding 75–80 characters. |
| **Impact** | Eyes travel too far; user loses start of line when reaching end. Increases tracking errors. |
| **Fix** | Constrain line length to 45–75 characters (approx. 45–75ch or max-width on text containers). Use readable measure. |
| **WCAG Criterion** | 1.4.8 Visual Presentation — "blocks of text are no wider than 80 characters" |

---

### 7. Text Resizing and Reflow

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.4 Resize Text (Level AA), 1.4.10 Reflow (Level AA) |
| **Severity** | To be verified |
| **Finding** | User may rely on 125–150% zoom. Layout behavior at increased zoom should be tested. |
| **Impact** | If text does not reflow or horizontal scrolling is required, zoom users cannot read comfortably. |
| **Fix** | Ensure text reflows at 200% zoom; no horizontal scrolling for body content. Use relative units (rem, em) for font sizes. |
| **WCAG Criterion** | 1.4.4 Resize Text, 1.4.10 Reflow |

---

### 8. Contact CTA Label Clarity

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.4 Link Purpose (In Context) — Level A |
| **Severity** | Low |
| **Finding** | Primary contact CTA is "Connect with an Expert" rather than "Contact." May require extra decoding for users expecting conventional labels. |
| **Impact** | Slight cognitive load; user may hesitate or search for "Contact" before recognizing the CTA. |
| **Fix** | Consider adding "Contact" to the CTA label (e.g., "Contact Us" or "Connect with an Expert — Contact") or ensure "Contact" appears in nav/footer. |
| **WCAG Criterion** | 2.4.4 Link Purpose (In Context) |

---

### 9. Contact Alternatives Visibility

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.1.1 Keyboard, 2.4.4 Link Purpose |
| **Severity** | Low |
| **Finding** | Phone number and email may not be prominently visible above the fold or in the main contact flow. |
| **Impact** | Users who prefer phone/email over forms may struggle to find alternatives. |
| **Fix** | Display phone and email clearly on the Contact page, near or above the form. Ensure footer contact details are easy to locate. |
| **WCAG Criterion** | General usability; supports multiple interaction preferences |

---

## Summary Table

| Issue | WCAG | Severity | Priority |
|-------|------|----------|----------|
| Low contrast (gray text) | 1.4.3 | High | P0 |
| Italic testimonial blocks | 1.4.8 | High | P0 |
| Thin font weight | 1.4.8 | Medium–High | P1 |
| Insufficient line height | 1.4.8 | Medium | P1 |
| Long paragraphs | 1.4.8 | Medium | P1 |
| Excessive line length | 1.4.8 | Low–Medium | P2 |
| Contact CTA label | 2.4.4 | Low | P2 |
| Contact alternatives | — | Low | P2 |

---

## Recommended Remediation Order

1. **Increase contrast** — Darken body text to meet WCAG AA (4.5:1) minimum; target AAA (7:1) where possible.
2. **Remove or shorten italic blocks** — Use regular/bold for testimonials; limit italic to 1–2 lines if design requires it.
3. **Increase font weight** — Body text to 400 minimum; consider 500 for key content.
4. **Increase line height** — Body text to 1.5 minimum; 1.6+ for dense sections.
5. **Chunk content** — Break long paragraphs; add bullets and subheadings to service descriptions.
6. **Constrain line length** — Max 75–80 characters per line for body text.
7. **Verify zoom and reflow** — Test at 125%, 150%, 200% zoom for layout integrity.

---

## References

- [WCAG 2.1 Success Criterion 1.4.3 Contrast (Minimum)](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
- [WCAG 2.1 Success Criterion 1.4.8 Visual Presentation (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/visual-presentation.html)
- [WCAG 2.1 Success Criterion 1.4.12 Text Spacing (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/text-spacing.html)
- [W3C Cognitive Accessibility Guidance](https://www.w3.org/WAI/cognitive/)
