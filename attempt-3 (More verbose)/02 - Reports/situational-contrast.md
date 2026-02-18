# Accessibility Technical Report: Situational Contrast (High-Glare Environment)

**Persona:** Jordan Chen (Situational Contrast—Normal Vision, Outdoor Sunlight)  
**Website:** https://launchpadlab.com/  
**Date:** February 16, 2025  
**Testing Focus:** Contrast, link identification, focus indicators, and visual legibility for users browsing in high-glare environments (outdoor sunlight, bright office, train by window). Screen brightness assumed maxed.

---

## Executive Summary

The site uses light gray text (#666–#777) on white backgrounds, links lack non-color differentiation (underlines, bold, icons), and focus indicators are faint or low-contrast. In high-glare environments, effective contrast collapses: text that may pass WCAG indoors fails outdoors. Users must cup hands over the screen, tilt the display, and guess at link locations. Body text becomes illegible; headings survive; focus indicators disappear. Violates WCAG 2.1 success criteria 1.4.3 (Contrast Minimum), 1.4.6 (Contrast Enhanced), 1.4.11 (Non-text Contrast), and 1.4.1 (Use of Color). Severity ranges from Medium to Critical. Task completion is possible but requires significant physical effort and strain.

---

## Issues Identified

### 1. Body Text Contrast Fails in Glare (Effective Contrast Collapse)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.3 Contrast (Minimum) — Level AA; 1.4.6 Contrast (Enhanced) — Level AAA |
| **Severity** | Critical |
| **Finding** | Body text uses #666–#777 on white. Indoors, this may meet 4.5:1. In high-glare environments (outdoor sunlight, bright office), glare reduces effective contrast. Perceived ratio can drop to 2:1 or worse. Text washes out completely. |
| **Impact** | Body text is illegible. Users cannot read service descriptions, testimonials, case study copy, or form labels. Sustained reading requires cupping hands, tilting screen, or abandoning content. Task completion depends on high-contrast elements (headings, statistics) only. |
| **Fix** | Use text color of at least #595959 on white for AA (4.5:1). For AAA (7:1), target #404040 or darker. Design for worst-case lighting. Glare reduces effective contrast—build in margin. |
| **WCAG Criterion** | 1.4.3 Contrast (Minimum); 1.4.6 Contrast (Enhanced) |

---

### 2. Links Differentiated Only by Color

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.1 Use of Color — Level A |
| **Severity** | Critical |
| **Finding** | Navigation links (Work, Services, About), "Connect with an Expert" CTA, and in-content links ("Learn more," "View project") lack underlines, bold, or icons. Differentiation relies on color alone. |
| **Impact** | In glare, color-only cues vanish. Links are indistinguishable from body text. Users cannot find contact path, service links, or case study links. Hover/tab may reveal cues, but in sunlight these are often invisible. Task completion delayed or failed. |
| **Fix** | Add underlines to all links. Alternatively: bold, icons, or distinct typography. Ensure link text has non-color cue visible in high-glare conditions. |
| **WCAG Criterion** | 1.4.1 Use of Color |

---

### 3. Faint Focus Indicators Invisible in Glare

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.11 Non-text Contrast — Level AA; 2.4.7 Focus Visible — Level AA |
| **Severity** | High |
| **Finding** | Focus indicators on links, buttons, and form fields are faint—thin outlines (1px), light gray borders, low-contrast rings. In glare, these disappear. |
| **Impact** | Keyboard users cannot determine focus position. Tab navigation becomes guesswork. Form completion is difficult. Users lose place, miss fields, or abandon. |
| **Fix** | Use high-contrast focus indicators: 2px+ outline, dark border (3:1 minimum against adjacent colors per 1.4.11). Ensure focus state is visible in bright light. Test in simulated glare. |
| **WCAG Criterion** | 1.4.11 Non-text Contrast; 2.4.7 Focus Visible |

---

### 4. Buttons and CTAs Low Contrast

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.3 Contrast (Minimum); 1.4.11 Non-text Contrast — Level AA |
| **Severity** | High |
| **Finding** | "Connect with an Expert" and other CTAs may use low-contrast backgrounds or text. Light gray buttons on white, pale blue on white do not register in glare. |
| **Impact** | Users scroll past CTAs, miss form submit buttons, or assume elements are decorative. Contact path may be missed. Task failure. |
| **Fix** | Ensure buttons have 4.5:1 contrast for text and 3:1 for UI components (1.4.11). Use strong borders, bold text, high-contrast backgrounds. |
| **WCAG Criterion** | 1.4.3 Contrast (Minimum); 1.4.11 Non-text Contrast |

---

### 5. Thin Font Weight Reduces Legibility in Glare

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.8 Visual Presentation (Level AAA); supports 1.4.3 |
| **Severity** | High |
| **Finding** | Body text, headings, and labels use font weight 300–400. Thin weights lose definition in glare. Letter edges vanish. |
| **Impact** | Text that might be readable indoors becomes illegible outdoors. Thin fonts compound contrast collapse. |
| **Fix** | Use font-weight: 400 (normal) minimum for body text; 500 (medium) for key content. Headings: 500–600. Avoid 300 or lighter. |
| **WCAG Criterion** | 1.4.8 Visual Presentation |

---

### 6. Form Labels and Placeholders

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.3 Contrast (Minimum) |
| **Severity** | Medium |
| **Finding** | Form labels and placeholders may use light gray. Placeholder-only labels are problematic. In glare, light gray labels vanish. |
| **Impact** | Users cannot read field labels. Form errors increase. Task completion (contacting company) at risk. |
| **Fix** | Labels must be dark (#333 or darker), visible, and meet 4.5:1. Avoid placeholder-only labeling. Ensure required indicators and error messages are high contrast. |
| **WCAG Criterion** | 1.4.3 Contrast (Minimum) |

---

### 7. Testimonials in Low Contrast + Italic

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.3 Contrast (Minimum); 1.4.6 Contrast (Enhanced) |
| **Severity** | Medium |
| **Finding** | Testimonials use italic text in light gray (#666–#777) on white. Contact page has five blocks above form. Italic distorts letter shapes; low contrast compounds barrier. |
| **Impact** | In glare, testimonials are completely invisible. Users scroll past. Content is lost. |
| **Fix** | Use regular or bold for testimonial text. Ensure contrast of at least 4.5:1 (AA) or 7:1 (AAA). Limit italic to 1–2 short lines if design requires it. |
| **WCAG Criterion** | 1.4.3 Contrast (Minimum); 1.4.6 Contrast (Enhanced) |

---

### 8. White Backgrounds Amplify Glare

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.3 Contrast (Minimum); environmental consideration |
| **Severity** | Medium |
| **Finding** | Large white areas reflect ambient light. Page becomes bright, washed-out field. Dark text on white survives; light gray on white does not. |
| **Impact** | Effective contrast of entire page is reduced. Users need elements that "pop" against glare. Light gray fails. |
| **Fix** | Darken text to ensure sufficient contrast even when white backgrounds reflect light. Consider slightly off-white backgrounds for large blocks to reduce glare amplification. |
| **WCAG Criterion** | 1.4.3 Contrast (Minimum) |

---

## Summary Table

| Issue | WCAG Ref | Severity | Priority |
|-------|----------|----------|----------|
| Body text contrast fails in glare | 1.4.3, 1.4.6 | Critical | P0 |
| Links without non-color cue | 1.4.1 | Critical | P0 |
| Faint focus indicators | 1.4.11, 2.4.7 | High | P0 |
| Buttons/CTAs low contrast | 1.4.3, 1.4.11 | High | P1 |
| Thin font weight | 1.4.8 | High | P1 |
| Form labels/placeholders | 1.4.3 | Medium | P2 |
| Testimonials low contrast + italic | 1.4.3, 1.4.6 | Medium | P2 |
| White backgrounds amplify glare | 1.4.3 | Medium | P2 |

---

## Recommended Remediation Order

1. **Increase body text contrast** — Darken to #595959 (AA) or #404040 (AAA). Design for glare; effective contrast collapses outdoors.
2. **Add non-color cues to links** — Underlines, bold, or icons. Ensure all links distinguishable without color. Critical for glare.
3. **Enhance focus indicators** — High-contrast focus rings (2px+, 3:1 minimum). Visible in bright light. Test in simulated glare.
4. **Enhance button/CTA contrast** — 4.5:1 for text; 3:1 for UI components per 1.4.11.
5. **Increase font weight** — Body text to 400 minimum; 500 for key content. Headings to 500–600.
6. **Audit form labels and placeholders** — Dark, visible, 4.5:1.
7. **Fix testimonials** — Regular/bold font; contrast 4.5:1 minimum.

---

## WCAG Criteria Referenced

- **1.4.3 Contrast (Minimum)** — Level AA: Text and images of text must have contrast ratio of at least 4.5:1 (normal) or 3:1 (large). In glare, effective ratio drops; design with margin.
- **1.4.6 Contrast (Enhanced)** — Level AAA: 7:1 for normal text; 4.5:1 for large. Preferred for glare survivability.
- **1.4.11 Non-text Contrast** — Level AA: UI components and graphical objects (including focus indicators) must have contrast of at least 3:1 against adjacent colors.
- **1.4.1 Use of Color** — Level A: Color must not be the only visual means of conveying information. Links need non-color cue.
- **2.4.7 Focus Visible** — Level AA: Any keyboard operable user interface has a mode of operation where the keyboard focus indicator is visible.
- **1.4.8 Visual Presentation** — Level AAA: Covers font weight and text presentation.

---

## Environmental Context

This report addresses **situational** contrast reduction—users with normal vision in high-glare environments. Key factors:

- **Screen brightness:** Assumed maxed. No further adjustment possible.
- **Effective contrast:** Glare reduces perceived contrast. 4.5:1 indoors may drop to 2:1 outdoors.
- **User strategies:** Cupping hands, tilting screen—temporary, exhausting. Site should not require them.
- **Real-world usage:** Outdoor cafés, bright offices, trains. Common scenarios. Not edge cases.

---

## References

- [WCAG 2.1 Success Criterion 1.4.3 Contrast (Minimum)](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
- [WCAG 2.1 Success Criterion 1.4.6 Contrast (Enhanced)](https://www.w3.org/WAI/WCAG21/Understanding/contrast-enhanced.html)
- [WCAG 2.1 Success Criterion 1.4.11 Non-text Contrast](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html)
- [WCAG 2.1 Success Criterion 1.4.1 Use of Color](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
- [WCAG 2.1 Success Criterion 2.4.7 Focus Visible](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
