# Accessibility Technical Report: Motor Impairment (Keyboard User)

**Persona:** Sam Chen (Motor Impairment, Essential Tremor)  
**Website:** https://launchpadlab.com/  
**Date:** February 16, 2025  
**Testing Focus:** Keyboard operability, focus visibility, target size, skip links, tab order, and hover-independent access for users with motor impairment.

---

## Executive Summary

The site is keyboard-operable: all interactive elements can be reached and activated via Tab, Enter, and Space. However, multiple barriers create significant strain and risk for users with motor impairment: no skip link, invisible or faint focus indicators, small click targets (under 44×44px), excessive tab sequences (20+ tabs to main content, 40+ to contact form), and potential hover-dependent interactions. Severity ranges from Medium to Critical. WCAG 2.1 Level AA criteria for keyboard access (2.1.1), focus visible (2.4.7), and bypass blocks (2.4.1) are not fully met. Level AAA target size (2.5.5) and pointer gestures (2.5.8) are also implicated.

---

## Issues Identified

### 1. No Skip Link (Bypass Blocks)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.1 Bypass Blocks — Level A |
| **Severity** | Critical |
| **Finding** | No "Skip to main content," "Skip to navigation," or equivalent skip link. First focusable element is likely the logo or first nav item. User must tab through entire header (logo, nav items, CTA) before reaching main content. |
| **Impact** | 20+ tab stops required to reach main content. 40+ to reach contact form. Users with motor impairment fatigue from excessive tabbing. Cognitive and physical effort increases; abandonment risk rises. |
| **Fix** | Add visible "Skip to main content" link as first focusable element. Ensure it receives focus on Tab from page load. On activation, move focus to main content landmark. Optionally add "Skip to contact form" on Contact page. |
| **WCAG Criterion** | 2.4.1 Bypass Blocks |

---

### 2. Missing or Faint Focus Indicators

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.7 Focus Visible — Level AA |
| **Severity** | Critical |
| **Finding** | Focus indicators are missing, faint, or low contrast. Default browser focus ring may be overridden. Observed: thin (1px) outline, light gray color, insufficient contrast against background. Affects nav links, CTAs, service box links, form inputs, submit button, footer links. |
| **Impact** | Keyboard users cannot determine current focus position. "Tabbing blind" leads to wrong activations, lost place, and frustration. Users with motor impairment rely entirely on focus visibility for orientation. |
| **Fix** | Ensure all focusable elements have visible focus indicator: minimum 2px solid outline, 3:1 contrast against adjacent colors. Do not remove outline:focus. Use :focus-visible for custom styling. Test with keyboard only; verify visibility on every interactive element. |
| **WCAG Criterion** | 2.4.7 Focus Visible |

---

### 3. Insufficient Target Size

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.5.5 Target Size (Level AAA) |
| **Severity** | High |
| **Finding** | Multiple interactive elements have clickable/focusable areas under 44×44 CSS pixels: "Learn More" links in service boxes, "View project" links in case studies, arrow icons (carousel/slider controls), secondary CTAs, possibly nav links and footer links. Submit button may be borderline (~40px). |
| **Impact** | Users with limited fine motor control misclick, activate wrong elements, or require multiple attempts. Small targets cause frustration and abandonment. Pointer users (trackball, joystick) especially affected. |
| **Fix** | Ensure all interactive elements have minimum 44×44px touch target. Add padding to links; increase button dimensions. Provide 8px+ spacing between adjacent targets to prevent misactivation. Use min-height/min-width or padding to expand hit area. |
| **WCAG Criterion** | 2.5.5 Target Size |

---

### 4. Excessive Tab Stops to Reach Main Content

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.1 Bypass Blocks, 2.4.3 Focus Order |
| **Severity** | High |
| **Finding** | Approximately 20–23 tab stops from page load to main content (hero/services). Approximately 40+ tab stops to reach contact form from homepage. No skip link to reduce count. Tab order includes logo, nav items, CTA, possibly client logos, before main content. |
| **Impact** | Users with motor impairment fatigue from repetitive tabbing. Long sequences increase error rates and abandonment. Physical effort (repeated key presses) compounds with tremor and limited dexterity. |
| **Fix** | Implement skip link (see Issue 1). Reduce focusable decorative elements (e.g., client logos as links—consider if necessary). Ensure tab order follows logical reading order. Group related interactive elements. |
| **WCAG Criterion** | 2.4.1 Bypass Blocks, 2.4.3 Focus Order |

---

### 5. Hover-Dependent Interactions

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.1.1 Keyboard, 2.5.8 Target Size (Minimum) — Level AA (pointer gestures) |
| **Severity** | Medium–High |
| **Finding** | Navigation may include dropdowns or submenus that open only on hover. Service boxes, carousels, or other components may reveal content on hover. Users with motor impairment cannot reliably trigger hover states. |
| **Impact** | Content or functionality hidden behind hover is inaccessible. Users cannot access dropdown menus, tooltips, or hover-revealed content. All functionality must be available via keyboard (focus + Enter/Space). |
| **Fix** | Ensure all dropdowns, menus, and interactive content open on focus and/or keyboard activation (Enter, Space). Do not rely on hover alone. Provide visible keyboard affordance (e.g., "Press Enter to expand"). Test all interactive components with keyboard only. |
| **WCAG Criterion** | 2.1.1 Keyboard, 2.5.8 Target Size (Minimum) |

---

### 6. Contact Page: Testimonials Above Form

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.1 Bypass Blocks, 2.4.3 Focus Order |
| **Severity** | Medium |
| **Finding** | Contact page displays five testimonial blocks above the contact form. User must tab through testimonial links/content before reaching form fields. Increases tab count and delays task completion. |
| **Impact** | Additional tab stops before form. User fatigue increases. Task completion delayed. Consider placing form above testimonials or providing skip-to-form link. |
| **Fix** | Reorder content: place contact form above testimonials. Or add "Skip to contact form" link at top of Contact page. Reduces tab count and improves efficiency. |
| **WCAG Criterion** | 2.4.1 Bypass Blocks |

---

### 7. Form Accessibility

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.7 Focus Visible, 2.5.5 Target Size, 3.3.2 Labels or Instructions |
| **Severity** | Medium |
| **Finding** | Form fields (name, email, company, dropdown, message) are keyboard-reachable. Labels appear present. Focus indicator on inputs may be faint. Submit button target size borderline (~40px). Required field indication unclear. |
| **Impact** | Users can complete form but may lose place due to faint focus. Submit button may be difficult to activate with pointer. Error handling and focus management on validation failure not verified. |
| **Fix** | Strengthen focus indicators on all form controls. Ensure submit button is at least 44×44px. Associate labels with inputs via for/id. Indicate required fields clearly. On validation error, move focus to error message and ensure it is announced. |
| **WCAG Criterion** | 2.4.7 Focus Visible, 2.5.5 Target Size, 3.3.2 Labels or Instructions |

---

## Summary Table

| Issue | WCAG | Severity | Priority |
|-------|------|----------|----------|
| No skip link | 2.4.1 | Critical | P0 |
| Missing/faint focus indicators | 2.4.7 | Critical | P0 |
| Insufficient target size | 2.5.5 | High | P0 |
| Excessive tab stops | 2.4.1, 2.4.3 | High | P0 |
| Hover-dependent interactions | 2.1.1, 2.5.8 | Medium–High | P1 |
| Testimonials above form | 2.4.1 | Medium | P1 |
| Form accessibility | 2.4.7, 2.5.5, 3.3.2 | Medium | P1 |

---

## Recommended Remediation Order

1. **Add skip link** — "Skip to main content" as first focusable element. Reduces tab count from 20+ to 1–2. Critical for users with motor impairment.
2. **Strengthen focus indicators** — 2px solid outline, 3:1 contrast minimum on all interactive elements. Do not remove or override default focus styles without replacement.
3. **Enlarge touch targets** — All interactive elements to 44×44px minimum. Nav links, "Learn More," "View project," arrow icons, secondary CTAs, submit button.
4. **Verify keyboard-only access** — Test all dropdowns, menus, carousels with keyboard. Ensure focus + Enter/Space activates; no hover-only interactions.
5. **Reorder Contact page** — Place form above testimonials, or add skip-to-form link.
6. **Improve form** — Submit button 44×44px. Clear required indicators. Error focus management.
7. **Audit tab order** — Ensure logical sequence. Reduce focusable decorative elements where possible.

---

## WCAG References

- [2.1.1 Keyboard](https://www.w3.org/WAI/WCAG21/Understanding/keyboard.html) — All functionality available via keyboard
- [2.4.1 Bypass Blocks](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html) — Skip links
- [2.4.3 Focus Order](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html) — Logical tab order
- [2.4.7 Focus Visible](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html) — Visible focus indicator
- [2.5.5 Target Size](https://www.w3.org/WAI/WCAG21/Understanding/target-size.html) — 44×44px minimum (Level AAA)
- [2.5.8 Target Size (Minimum)](https://www.w3.org/WAI/WCAG21/Understanding/target-size-minimum.html) — Pointer gestures (Level AA)

---

*Report based on keyboard-only testing as Sam Chen (motor impairment persona). Task: Find what LaunchPad Lab does and how to contact them. Completed with significant friction. Rating: 2/5.*
