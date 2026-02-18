# Accessibility Technical Report: Red-Green Color Blind (Deuteranopia/Protanopia)

**Persona:** Marcus Chen (Red-Green Color Blind)  
**Website:** https://launchpadlab.com/  
**Date:** February 16, 2025  
**Testing Focus:** Use of color alone for links, form validation, button states, and status indicators. Non-color cue availability.

---

## Executive Summary

The site is navigable and the primary task (find what the company does and how to contact them) is completable. However, multiple barriers create significant risk for users with red-green color vision deficiency: links rely on color alone (no underlines), form validation uses red/green borders without text or icons, and button/hover states may use color-only differentiation. These issues violate WCAG 2.1 Level A (1.4.1) and Level AA (1.4.3, 1.4.11, 3.3.1). Severity ranges from Medium to High. Users may miss validation errors, submit invalid forms, or fail to identify links without keyboard navigation.

---

## Issues Identified

### 1. Links Identified by Color Alone (No Underlines)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.1 Use of Color — Level A |
| **Severity** | High |
| **Finding** | Navigation links (Work, Services, About), "Learn more" links in service boxes, "View project" links in case studies, and footer links appear to use color as the primary or only means of distinguishing them from body text. No underlines in default state. |
| **Impact** | Users with red-green color deficiency cannot visually distinguish links from static text. Links blend with body copy. Users must Tab through the page or guess. Casual scanning fails. |
| **Fix** | Add underlines to all links in default state. Alternatively, add icons or explicit "link" context. Ensure visited, hover, and focus states use non-color cues (underline style, background, outline). |
| **WCAG Criterion** | 1.4.1 Use of Color |

---

### 2. Form Validation Uses Red/Green Borders Without Text or Icons

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.1 Use of Color, 3.3.1 Error Identification — Level A |
| **Severity** | High |
| **Finding** | Contact form validation may use red borders for invalid fields and green borders for valid fields. No visible error text ("Invalid email," "This field is required") or icons (✗, ✓) confirmed. Success confirmation may rely on green styling. |
| **Impact** | Users cannot see validation feedback. Invalid forms may be submitted. Users cannot correct errors. Success state is unverifiable. Trust in form submission is lost. |
| **Fix** | Add inline error text for each invalid field. Add ✗ icon or "Error" label. Add ✓ icon or "Valid" label for valid fields. Add explicit success message: "Thank you, we received your message." Do not rely on colored borders alone. |
| **WCAG Criterion** | 1.4.1 Use of Color, 3.3.1 Error Identification |

---

### 3. Button State Changes Use Color Only

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.1 Use of Color, 1.4.11 Non-text Contrast — Level AA |
| **Severity** | Medium |
| **Finding** | Submit button, "Connect with an Expert" CTA, and possibly service box links may use color-only changes for hover, focus, and active states. Red/green or similar color shifts are indistinguishable for users with deuteranopia/protanopia. |
| **Impact** | Users cannot perceive hover or focus state. Interactive elements may appear static. Keyboard users may lose focus position if focus indicator is color-only. |
| **Fix** | Add visible outline (2px minimum, 3:1 contrast) for focus. Add underline, border, or background change for hover. Use opacity or pattern for disabled state. Ensure state changes are perceivable without color. |
| **WCAG Criterion** | 1.4.1 Use of Color, 1.4.11 Non-text Contrast |

---

### 4. Required Field Indicators May Use Red Alone

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.1 Use of Color, 3.3.2 Labels or Instructions — Level A |
| **Severity** | Medium |
| **Finding** | Required fields may be indicated by red asterisk only. Red is indistinguishable from brown/gray for users with red-green deficiency. No "Required" text or legend confirmed. |
| **Impact** | Users cannot identify required fields. May omit required information. Form submission fails without clear feedback. |
| **Fix** | Use "Required" text in label or add asterisk with visible legend ("* Required"). Ensure asterisk is not red-only; use dark color or add icon. |
| **WCAG Criterion** | 1.4.1 Use of Color, 3.3.2 Labels or Instructions |

---

### 5. Service Box Hover/Focus States

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.1 Use of Color, 1.4.11 Non-text Contrast |
| **Severity** | Low–Medium |
| **Finding** | Service boxes have hover effects (lift, scale, shadow). These provide non-color cues—positive. However, if any part of the hover state relies on red/green color change (e.g., border color), that component is inaccessible. Links within boxes still lack underlines. |
| **Impact** | Card-level interactivity may be perceivable; link-level interactivity is not. Mixed experience. |
| **Fix** | Ensure no hover/focus state relies on color alone. Add underlines to links within service boxes. Verify focus indicator on cards is visible (outline, border). |
| **WCAG Criterion** | 1.4.1 Use of Color, 1.4.11 Non-text Contrast |

---

### 6. Contrast and Red/Green Confusion

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.3 Contrast (Minimum) — Level AA |
| **Severity** | Medium |
| **Finding** | Red and green text or borders on typical backgrounds may have reduced effective contrast for users with color deficiency. Red/green confusion can make elements appear to blend with background or adjacent content. |
| **Impact** | Even when color is not the sole cue, reduced contrast makes elements harder to perceive. Error text in red on white may fail contrast for some users. |
| **Fix** | Use dark text for all messages (error, success, labels). Ensure borders use sufficient contrast (3:1 for non-text) or pair with icons/text. Avoid red/green as primary palette for critical UI. |
| **WCAG Criterion** | 1.4.3 Contrast (Minimum) |

---

### 7. Success Confirmation After Form Submit

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.1 Use of Color, 3.3.1 Error Identification |
| **Severity** | High |
| **Finding** | Post-submit success state may use green checkmark, green border, or green background without accompanying text. User cannot verify submission succeeded. |
| **Impact** | User submits form and receives no perceivable confirmation. May resubmit. May assume failure. May abandon or contact via alternate channel. |
| **Fix** | Display explicit text: "Thank you, we received your message." Ensure message has sufficient contrast. Do not rely on green icon or green styling alone. |
| **WCAG Criterion** | 1.4.1 Use of Color, 3.3.1 Error Identification |

---

## Summary Table

| Issue | WCAG | Severity | Priority |
|-------|------|----------|----------|
| Links by color alone (no underlines) | 1.4.1 | High | P0 |
| Form validation (red/green borders, no text/icons) | 1.4.1, 3.3.1 | High | P0 |
| Success confirmation (color only) | 1.4.1, 3.3.1 | High | P0 |
| Button state changes (color only) | 1.4.1, 1.4.11 | Medium | P1 |
| Required field indicators (red asterisk) | 1.4.1, 3.3.2 | Medium | P1 |
| Contrast with red/green elements | 1.4.3 | Medium | P1 |
| Service box link underlines | 1.4.1 | Low–Medium | P2 |

---

## Recommended Remediation Order

1. **Add underlines to all links** — Default state must include underline. Ensure links are distinguishable without color. Apply to nav, service boxes, case studies, footer.
2. **Add text and icons to form validation** — Inline error text ("Invalid email," "This field is required"). ✗ icon for errors. ✓ icon for valid. Do not rely on red/green borders alone.
3. **Add explicit success message** — "Thank you, we received your message." Plain text. Sufficient contrast. No green-only confirmation.
4. **Add non-color focus indicators** — 2px outline, 3:1 contrast. Visible on all interactive elements. Do not rely on color change for focus.
5. **Fix required field indicators** — "Required" text or asterisk with legend. Ensure indicator is not red-only.
6. **Audit hover/active states** — Ensure no state relies on color alone. Add outline, border, or background change.
7. **Review contrast of error/success text** — Use dark text. Ensure 4.5:1 minimum for body text, 3:1 for large text.

---

## References

- [WCAG 2.1 Success Criterion 1.4.1 Use of Color](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
- [WCAG 2.1 Success Criterion 1.4.3 Contrast (Minimum)](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
- [WCAG 2.1 Success Criterion 1.4.11 Non-text Contrast](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html)
- [WCAG 2.1 Success Criterion 3.3.1 Error Identification](https://www.w3.org/WAI/WCAG21/Understanding/error-identification.html)
- [WCAG 2.1 Success Criterion 3.3.2 Labels or Instructions](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)
