# Accessibility Technical Report: Voice Control User

**Persona:** Marcus Webb (ALS, Voice Control / Dragon NaturallySpeaking)  
**Website:** https://launchpadlab.com/  
**Date:** February 16, 2025  
**Testing Focus:** Voice-only navigation—link labels, button labels, accessible names, icon-only controls, and Label in Name compliance for users who rely on voice commands.

---

## Executive Summary

The site is navigable by voice and the primary task (find what the company does and how to contact them) is completable. However, multiple barriers create significant friction for voice control users: six or more identical "Learn More" links that cannot be distinguished by voice, icon-only buttons (hamburger menu, carousel arrows, social icons) with no speakable labels, and potential accessible name mismatches. Users must rely on the "Show numbers" fallback to distinguish links and activate icon-only controls. Severity ranges from Medium to Critical. WCAG 2.1 Level A criteria 2.5.3, 2.4.4, 1.1.1, 4.1.2, and 2.1.1 are not fully met.

---

## Issues Identified

### 1. Identical "Learn More" Links (Link Purpose / Label in Name)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.4 Link Purpose (In Context) — Level A, 2.5.3 Label in Name — Level A |
| **Severity** | High |
| **Finding** | Six or more links with identical text "Learn more" in the services section and possibly case studies. Voice command "Click Learn More" either activates the wrong link or prompts "Which one?" User cannot distinguish links by speaking the visible label. |
| **Impact** | Voice control users cannot target a specific service or case study. Must use "Show numbers" fallback to overlay numbers and say "Click Learn More 3"—a workaround that indicates design failure. Violates 2.4.4 and makes 2.5.3 impossible (label cannot be unique if six elements share it). |
| **Fix** | Provide unique, descriptive link text: "Learn more about AI Strategy," "Learn more about Product Development," "Learn more about Web Apps," "View [Project Name] case study," etc. Each link must have a label that uniquely identifies its destination. |
| **WCAG Criterion** | 2.4.4 Link Purpose (In Context), 2.5.3 Label in Name |

---

### 2. Icon-Only Buttons Without Accessible Names

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.1.1 Non-text Content — Level A, 4.1.2 Name, Role, Value — Level A |
| **Severity** | High |
| **Finding** | Hamburger menu, carousel arrows (next/previous), and social media icons (LinkedIn, Twitter, etc.) are icon-only controls. No visible text. No speakable label. Voice command "Click Next" or "Click LinkedIn" fails—user has nothing to say that targets these elements. |
| **Impact** | Voice control users cannot activate icon-only controls by name. Must use "Show numbers" fallback to overlay numbers and guess which number corresponds to the desired control. Icon-only buttons are dead ends for voice navigation. |
| **Fix** | Add `aria-label` to every icon-only control: `aria-label="Open navigation menu"`, `aria-label="Next slide"`, `aria-label="Previous slide"`, `aria-label="LinkedIn"`, `aria-label="Twitter"`. Ensure labels match what users would naturally say. Alternatively, provide visually hidden text. |
| **WCAG Criterion** | 1.1.1 Non-text Content, 4.1.2 Name, Role, Value |

---

### 3. Accessible Name Mismatch (Label in Name)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.5.3 Label in Name — Level A |
| **Severity** | Medium to High |
| **Finding** | Interactive elements may have accessible names (aria-label, aria-labelledby) that do not match visible text. Example: button displays "Submit" but has `aria-label="Send form"`. User says "Click Submit"—command may fail because accessible name is "Send form." |
| **Impact** | Voice control matches user speech to accessible name. Mismatches cause failed commands. User must discover correct label by trial and error. Violates 2.5.3: "For user interface components with labels that include text or images of text, the name contains the text of that label." |
| **Fix** | Ensure accessible name includes the visible text. If button shows "Submit," aria-label should be "Submit" or "Submit form"—not "Send form." Audit all interactive elements with custom aria-labels. Verify that visible text is a substring of or matches the accessible name. |
| **WCAG Criterion** | 2.5.3 Label in Name |

---

### 4. "Show Numbers" Fallback Required

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.4 Link Purpose, 4.1.2 Name, Role, Value |
| **Severity** | Medium (indicates underlying failures) |
| **Finding** | User must invoke "Show numbers" to overlay numbers on interactive elements when labels are duplicated or missing. Required to distinguish "Learn More" links and to activate icon-only buttons. |
| **Impact** | "Show numbers" is a workaround, not a solution. Needing it indicates the site has failed to provide unique, descriptive labels. Users should be able to speak "Click Learn more about AI Strategy" without overlaying numbers. Document as barrier. |
| **Fix** | Address root causes: unique link labels (Issue 1), labeled icon-only buttons (Issue 2). Once fixed, "Show numbers" should not be necessary for core tasks. |
| **WCAG Criterion** | 2.4.4, 4.1.2 |

---

### 5. Hover-Dependent Content (Keyboard / Voice)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.1.1 Keyboard — Level A |
| **Severity** | Medium (if present) |
| **Finding** | Voice control users cannot trigger hover. Dropdown menus, tooltips, or content that reveals only on hover are inaccessible. Navigation dropdowns (Work, Services, About) may require hover to reveal submenus. |
| **Impact** | If dropdowns or tooltips require hover, voice users cannot access them. All functionality must be available via focus and click/Enter. Violates 2.1.1 when hover-only content contains essential information or functionality. |
| **Fix** | Ensure all interactive content is reachable via focus. Dropdowns must open on focus or click, not hover only. Tooltips must be reachable via keyboard/voice. No hover-only interactions. |
| **WCAG Criterion** | 2.1.1 Keyboard |

---

### 6. Contact Form Submit Button (Label in Name)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.5.3 Label in Name, 4.1.2 Name, Role, Value |
| **Severity** | Medium |
| **Finding** | Contact form submit button may have accessible name that does not match visible text. If button shows "Submit" but has `aria-label="Send form"` or similar, "Click Submit" may fail. |
| **Impact** | User cannot complete contact task if submit button is unactivatable by voice. Must verify accessible name matches visible text. |
| **Fix** | Audit submit button. Ensure accessible name includes visible text. If visible text is "Submit," aria-label should be "Submit" or "Submit form." Remove or align any mismatched aria-labels. |
| **WCAG Criterion** | 2.5.3 Label in Name, 4.1.2 Name, Role, Value |

---

## Summary Table

| Issue | WCAG Ref | Severity | Priority |
|-------|----------|----------|----------|
| Identical "Learn More" links | 2.4.4, 2.5.3 | High | P0 |
| Icon-only buttons unlabeled | 1.1.1, 4.1.2 | High | P0 |
| Accessible name mismatch | 2.5.3 | High | P0 |
| "Show numbers" fallback required | 2.4.4, 4.1.2 | Medium | P1 |
| Hover-dependent content | 2.1.1 | Medium | P1 |
| Submit button label mismatch | 2.5.3, 4.1.2 | Medium | P1 |

---

## Recommended Remediation Order

1. **Fix identical links** — Unique link text for each "Learn more": "Learn more about [Service Name]," "View [Project Name] case study." Ensures "Click Learn more about AI Strategy" works unambiguously.
2. **Label icon-only buttons** — `aria-label` on hamburger menu, carousel arrows, social icons. Every interactive element must have a speakable name. "Click Next slide," "Click LinkedIn" must work.
3. **Audit accessible names** — Verify all interactive elements: accessible name must include or match visible text. Fix mismatches (e.g., "Submit" visible vs. "Send form" in aria-label). WCAG 2.5.3 compliance.
4. **Verify hover independence** — Ensure dropdowns, tooltips, and carousel controls work via focus and click. No hover-only interactions.
5. **Verify contact form** — Submit button accessible name matches visible text. All form fields have labels that match accessible names.

---

## WCAG Criteria Referenced

- **2.5.3 Label in Name (A):** For UI components with labels, the accessible name contains the text of that label. Critical for voice control—user speaks visible text; system must match.
- **2.4.4 Link Purpose (A):** Link purpose determinable from link text or context. Identical "Learn more" links fail—purpose cannot be determined.
- **1.1.1 Non-text Content (A):** Text alternatives for non-text content. Icon-only buttons need accessible names.
- **4.1.2 Name, Role, Value (A):** All UI components have accessible name and role. Icon-only controls without names fail.
- **2.1.1 Keyboard (A):** All functionality available via keyboard. Hover-only content fails—voice cannot trigger hover.

---

## References

- [WCAG 2.1 Success Criterion 2.5.3 Label in Name](https://www.w3.org/WAI/WCAG21/Understanding/label-in-name.html)
- [WCAG 2.1 Success Criterion 2.4.4 Link Purpose (In Context)](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
- [WCAG 2.1 Success Criterion 1.1.1 Non-text Content](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)
- [WCAG 2.1 Success Criterion 4.1.2 Name, Role, Value](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
- [WCAG 2.1 Success Criterion 2.1.1 Keyboard](https://www.w3.org/WAI/WCAG21/Understanding/keyboard.html)
