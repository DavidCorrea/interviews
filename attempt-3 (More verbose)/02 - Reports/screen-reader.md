# Accessibility Technical Report: Screen Reader User (Blind User)

**Persona:** David Okonkwo (Blind, NVDA/VoiceOver)  
**Website:** https://launchpadlab.com/  
**Date:** February 16, 2025  
**Testing Focus:** Screen reader accessibility—headings, landmarks, links, buttons, forms, skip links, and programmatic structure for blind keyboard users.

---

## Executive Summary

The site is navigable and the primary task (find what the company does and how to contact them) is completable with a screen reader. However, multiple barriers create significant friction: no skip links, chaotic heading hierarchy (duplicate H2s, statistics incorrectly marked as headings), six or more identical "Learn more" links, icon-only buttons without accessible names, and a contact form that may be in an iframe and potentially unreachable. Severity ranges from Medium to Critical. WCAG 2.1 Level A and AA criteria are not fully met.

---

## Issues Identified

### 1. No Skip Link (Bypass Blocks)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.1 Bypass Blocks — Level A |
| **Severity** | High |
| **Finding** | No "Skip to main content" or equivalent link present as the first focusable element. Users must Tab through the entire header (logo, nav links, CTA) before reaching main content on every page load. |
| **Impact** | Repetitive, time-consuming navigation. Keyboard and screen reader users experience fatigue. Violates Level A. |
| **Fix** | Add a skip link as the first focusable element: `<a href="#main-content" class="skip-link">Skip to main content</a>`. Ensure target `id="main-content"` exists on `<main>`. Style to be visible on focus. |
| **WCAG Criterion** | 2.4.1 Bypass Blocks |

---

### 2. Identical "Learn More" Links (Link Purpose)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.4 Link Purpose (In Context) — Level A |
| **Severity** | High |
| **Finding** | Six or more links with identical text "Learn more" in the services section and case studies. Links list (Insert+F7) announces "Learn more" repeatedly with no way to distinguish which service or case study each link refers to. |
| **Impact** | Screen reader users cannot use the links list to navigate. Must read sequentially to determine link purpose. Violates 2.4.4. |
| **Fix** | Provide unique, descriptive link text: "Learn more about AI Automation," "Learn more about Web Apps," "View Acme Corp case study," etc. Link purpose must be determinable from link text alone or from link text plus programmatic context. |
| **WCAG Criterion** | 2.4.4 Link Purpose (In Context) |

---

### 3. Statistics Incorrectly Marked as Headings (Info and Relationships)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.3.1 Info and Relationships — Level A, 2.4.6 Headings and Labels — Level AA |
| **Severity** | High |
| **Finding** | Statistics ("12+ Years in Business," "730+ Projects," "4.8 Rating") are marked as H2 headings. These are decorative/informational numbers, not section headings. Duplicate H2s per section further pollute the heading hierarchy. |
| **Impact** | Heading navigation (H key) becomes chaotic. Users cannot build a mental map of page structure. Screen reader users get lost. |
| **Fix** | Remove heading tags from statistics. Use a single H2 for the section (e.g., "Our Track Record") and mark stats as `<p>` or `<div>`. Ensure logical H1→H2→H3 hierarchy with no skips. Eliminate duplicate H2s. |
| **WCAG Criterion** | 1.3.1 Info and Relationships, 2.4.6 Headings and Labels |

---

### 4. Icon-Only Buttons Without Accessible Names

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.1.1 Non-text Content — Level A, 4.1.2 Name, Role, Value — Level A |
| **Severity** | High |
| **Finding** | Hamburger menu, carousel arrows, and social media icons are icon-only controls. They announce as "button" or "link" with no accessible name. No `aria-label`, `aria-labelledby`, or visible text. |
| **Impact** | Screen reader users cannot determine purpose. Icon-only buttons are dead ends. Users cannot activate the correct control. |
| **Fix** | Add `aria-label` to every icon-only control: `aria-label="Open navigation menu"`, `aria-label="Next slide"`, `aria-label="Previous slide"`, `aria-label="LinkedIn"`, etc. Alternatively, provide visually hidden text. |
| **WCAG Criterion** | 1.1.1 Non-text Content, 4.1.2 Name, Role, Value |

---

### 5. Contact Form in Iframe—Potentially Unreachable

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 4.1.2 Name, Role, Value — Level A, 2.1.1 Keyboard — Level A |
| **Severity** | Critical (if confirmed) |
| **Finding** | Contact form may be embedded in an iframe (e.g., HubSpot). Iframe may lack descriptive `title`. Form may not be reachable via Tab or forms mode. Dynamically loaded forms may not announce. |
| **Impact** | Screen reader users may be unable to reach or complete the contact form. Task failure for "how to contact them." |
| **Fix** | Ensure iframe has `title="Contact form"` or similar. Verify form is in tab order and reachable. Ensure all form fields have associated `<label>` elements. If form loads dynamically, ensure it is announced and focusable. Test with NVDA and VoiceOver. |
| **WCAG Criterion** | 4.1.2 Name, Role, Value, 2.1.1 Keyboard |

---

### 6. Duplicate Headings and Poor Heading Hierarchy

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.6 Headings and Labels — Level AA |
| **Severity** | Medium |
| **Finding** | Multiple H2s with identical or non-descriptive text. Possible skips in hierarchy (H2 to H4). Headings do not accurately describe section content. |
| **Impact** | Heading navigation is confusing. Users cannot efficiently jump to desired sections. |
| **Fix** | Use one H1 per page. Ensure H2→H3→H4 hierarchy with no skips. Each heading must uniquely describe its section. Avoid duplicate heading text. |
| **WCAG Criterion** | 2.4.6 Headings and Labels |

---

### 7. Testimonials Above Contact Form

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.1 Bypass Blocks (interpreted), 2.4.6 Headings and Labels |
| **Severity** | Medium |
| **Finding** | Contact page places five long testimonials above the contact form. Users must scroll or read through all testimonials before reaching the form. No "Skip to contact form" link. |
| **Impact** | Extra navigation burden. Users seeking to contact must bypass large block of content. |
| **Fix** | Move contact form above testimonials, or add "Skip to contact form" link at top of Contact page. Ensure form is first focusable content in main region. |
| **WCAG Criterion** | 2.4.1 Bypass Blocks |

---

## Summary Table

| Issue | WCAG Ref | Severity | Priority |
|-------|----------|----------|----------|
| No skip link | 2.4.1 | High | P0 |
| Identical "Learn more" links | 2.4.4 | High | P0 |
| Statistics as headings | 1.3.1, 2.4.6 | High | P0 |
| Icon-only buttons unlabeled | 1.1.1, 4.1.2 | High | P0 |
| Iframe form unreachable | 4.1.2, 2.1.1 | Critical | P0 |
| Duplicate/poor heading hierarchy | 2.4.6 | Medium | P1 |
| Testimonials above form | 2.4.1 | Medium | P1 |

---

## Recommended Remediation Order

1. **Add skip link** — "Skip to main content" as first focusable element. Target `<main id="main-content">`. Visible on focus.
2. **Fix identical links** — Unique link text for each "Learn more": "Learn more about [Service Name]," "View [Project Name] case study."
3. **Fix heading hierarchy** — Remove H2 from statistics. Use single section heading. Eliminate duplicate H2s. Ensure logical H1→H2→H3.
4. **Label icon-only buttons** — `aria-label` on hamburger menu, carousel arrows, social icons. Every interactive element must have accessible name.
5. **Verify contact form accessibility** — If in iframe: add `title`. Ensure form is reachable via Tab and forms mode. All fields must have `<label>`. Test with NVDA and VoiceOver.
6. **Reorder Contact page** — Form above testimonials, or add "Skip to contact form" link.

---

## WCAG Criteria Referenced

- **2.4.1 Bypass Blocks (A):** Mechanism to bypass repeated blocks (e.g., skip link).
- **2.4.4 Link Purpose (A):** Link purpose determinable from link text or context.
- **2.4.6 Headings and Labels (AA):** Headings and labels describe topic or purpose.
- **1.1.1 Non-text Content (A):** Text alternatives for non-text content.
- **1.3.1 Info and Relationships (A):** Structure and relationships programmatically determinable.
- **4.1.2 Name, Role, Value (A):** All UI components have accessible name and role.
- **2.1.1 Keyboard (A):** All functionality available via keyboard.

---

## References

- [WCAG 2.1 Success Criterion 2.4.1 Bypass Blocks](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
- [WCAG 2.1 Success Criterion 2.4.4 Link Purpose (In Context)](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
- [WCAG 2.1 Success Criterion 2.4.6 Headings and Labels](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)
- [WCAG 2.1 Success Criterion 1.1.1 Non-text Content](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)
- [WCAG 2.1 Success Criterion 1.3.1 Info and Relationships](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)
- [WCAG 2.1 Success Criterion 4.1.2 Name, Role, Value](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
- [WCAG 2.1 Success Criterion 2.1.1 Keyboard](https://www.w3.org/WAI/WCAG21/Understanding/keyboard.html)
