# ADHD Persona: Technical Accessibility Report

**Website:** https://launchpadlab.com/  
**Persona:** Jordan Rivera (ADHD, Combined Type)  
**Date:** February 16, 2025  
**Testing Focus:** Finding what the company does; finding contact information

---

## Executive Summary

Users with ADHD experience cognitive overload, impatience, and difficulty sustaining focus. LaunchPad Lab's site presents multiple barriers: excessive choices, dense content, buried contact information, and no mechanisms to bypass repetitive or non-essential content. While core information (value proposition, contact CTA) is present, the path to completion is cluttered and cognitively demanding.

---

## Issues Found

### 1. No Skip Links

**WCAG Reference:** 2.4.1 Bypass Blocks (Level A)

**Description:** No "Skip to main content" or "Skip to contact" link is present. Users must scroll through the entire homepage—hero, logos, service boxes, statistics, badges, testimonials—to reach desired content.

**Severity:** High

**Impact on ADHD Users:** Sustained scrolling increases cognitive load and fatigue. Users lose focus before reaching their goal. Many will abandon or forget their original intent.

**Recommended Fix:** Add a visible or focusable "Skip to main content" link at the top of every page. Consider "Skip to contact form" on the Contact page. Ensure skip links are keyboard-accessible and visible on focus.

---

### 2. Testimonials Blocking Contact Form

**WCAG Reference:** 2.4.3 Focus Order (Level A); 2.4.6 Headings and Labels (Level AA)

**Description:** The Contact page displays five to six long client testimonials above the contact form. Users must scroll past substantial content to reach the primary action.

**Severity:** High

**Impact on ADHD Users:** Delays completion of the primary task. Testimonials compete for attention and distract from the goal. Users may overscroll, lose place, or abandon before reaching the form.

**Recommended Fix:** Move testimonials below the form, or provide a "Skip to form" link. Alternatively, collapse testimonials behind an expandable section. Ensure the form is reachable within one or two scrolls.

---

### 3. Excessive Choices and Cognitive Overload

**WCAG Reference:** 2.4.10 Section Headings (Level AAA); 2.4.6 Headings and Labels (Level AA)

**Description:** Homepage presents six service boxes, seven-plus award badges, multiple nav items, and several CTAs ("Connect with an Expert," "Learn More," etc.) with no clear hierarchy or "start here" guidance.

**Severity:** High

**Impact on ADHD Users:** Decision paralysis. Too many choices lead to freezing or impulsive clicking without comprehension. Users cannot efficiently extract the single answer: "What do you do?"

**Recommended Fix:** Reduce visible choices per viewport. Use clear visual hierarchy—one primary CTA, secondary options de-emphasized. Add a concise "What we do" summary at the top. Consider progressive disclosure for service details.

---

### 4. Dense Text and Jargon

**WCAG Reference:** 3.1.5 Reading Level (Level AAA); 2.4.6 Headings and Labels (Level AA)

**Description:** Long paragraphs (4+ lines), business jargon ("agentic AI," "bespoke solutions," "cross-functional"), and lack of bullet points or short summaries make content difficult to scan.

**Severity:** Medium

**Impact on ADHD Users:** Walls of text trigger skip behavior. Jargon causes tune-out. Users process bullets and numbers; paragraphs are often ignored. Key information may be missed.

**Recommended Fix:** Use bullet points, short paragraphs (2–3 sentences max), and plain language. Add one-line summaries for each service. Replace jargon with accessible alternatives or provide brief definitions.

---

### 5. Ambiguous CTA Labels

**WCAG Reference:** 2.4.6 Headings and Labels (Level AA); 2.4.4 Link Purpose (In Context) (Level A)

**Description:** Primary CTA is "Connect with an Expert" rather than "Contact." Users must infer that this leads to contact. Multiple similar CTAs ("Get Started," "Learn More") create ambiguity about which action leads to a human response.

**Severity:** Medium

**Impact on ADHD Users:** Impulsive clicking without certainty. Users may click the wrong CTA and land on a page that doesn't meet their goal. Increases backtracking and frustration.

**Recommended Fix:** Use clear, predictable labels: "Contact" or "Contact Us" for the contact path. Ensure CTA hierarchy is obvious—primary action (contact) vs. secondary (learn more).

---

### 6. Contact Information Not Easily Discoverable

**WCAG Reference:** 2.4.5 Multiple Ways (Level AA); 2.4.1 Bypass Blocks (Level A)

**Description:** Phone number and direct email are not prominently displayed in the header or above the fold. Contact requires navigating to a page and scrolling past testimonials to reach the form.

**Severity:** High

**Impact on ADHD Users:** Users who prefer calling or emailing cannot find alternatives quickly. Form-only contact increases friction. Users may abandon or resort to external search.

**Recommended Fix:** Display phone number and/or email in the header or footer, visible without scrolling. Provide a direct contact link in the primary navigation. Ensure contact is reachable in one click from any page.

---

### 7. Animations and Motion

**WCAG Reference:** 2.3.3 Animation from Interactions (Level AAA); 2.2.2 Pause, Stop, Hide (Level A)

**Description:** Scroll-triggered effects, hover animations, and potentially auto-playing elements can distract users and hijack attention.

**Severity:** Medium

**Impact on ADHD Users:** Motion draws attention away from static content. Users focus on movement instead of text and CTAs. Increases cognitive load and reduces task completion.

**Recommended Fix:** Provide a "Reduce motion" preference or respect `prefers-reduced-motion` media query. Avoid auto-playing carousels. Ensure animations can be paused or disabled. Use subtle, non-distracting transitions.

---

### 8. Form Length and Required Fields

**WCAG Reference:** 3.3.2 Labels or Instructions (Level A); 3.3.1 Error Identification (Level A)

**Description:** Contact form has five fields (name, email, company, dropdown, message). Required fields may feel excessive. Validation and error messaging clarity unknown.

**Severity:** Medium

**Impact on ADHD Users:** Each field is a hurdle. Long forms trigger avoidance. Users may skip required fields or abandon. Prefer fewer fields or alternative contact methods (phone, email).

**Recommended Fix:** Minimize required fields. Consider name, email, and message only. Make company and dropdown optional. Ensure clear labels and helpful error messages. Provide visible phone/email as alternative.

---

### 9. Light Gray Text and Low Contrast

**WCAG Reference:** 1.4.3 Contrast (Minimum) (Level AA)

**Description:** Known issue: light gray text (#666–#777) may fail contrast requirements against white backgrounds.

**Severity:** Medium (if contrast fails)

**Impact on ADHD Users:** Low-contrast text requires more effort to read. Combined with dense content, increases fatigue. Users may skip low-contrast elements entirely.

**Recommended Fix:** Ensure text meets WCAG AA contrast ratio (4.5:1 for normal text, 3:1 for large text). Avoid #666–#777 on white; use darker grays or black.

---

### 10. Faint or Missing Focus Indicators

**WCAG Reference:** 2.4.7 Focus Visible (Level AA)

**Description:** Known issue: focus indicators may be faint or missing on interactive elements.

**Severity:** High (for keyboard users)

**Impact on ADHD Users:** Users who tab through the page lose their place if focus is not visible. Increases disorientation and frustration. May lead to repeated tabbing or abandonment.

**Recommended Fix:** Ensure all interactive elements have a visible focus indicator (e.g., 2px outline, high-contrast border). Do not remove focus outlines with `outline: none` without providing a visible alternative.

---

## Summary Table

| Issue                         | Severity | WCAG Level | Impact on ADHD Users        |
|------------------------------|----------|------------|-----------------------------|
| No skip links                 | High     | A          | Exhaustion, abandonment     |
| Testimonials blocking form    | High     | A/AA       | Delay, distraction, exit    |
| Excessive choices             | High     | AA/AAA     | Decision paralysis          |
| Dense text / jargon           | Medium   | AA/AAA     | Skip behavior, tune-out     |
| Ambiguous CTAs                | Medium   | A/AA       | Wrong clicks, backtracking  |
| Contact info buried           | High     | A/AA       | Abandonment, external search|
| Animations / motion           | Medium   | A/AAA      | Attention hijacking         |
| Form length                   | Medium   | A          | Avoidance, abandonment      |
| Low contrast                  | Medium   | AA         | Fatigue, skip behavior      |
| Missing focus indicators      | High     | AA         | Disorientation, frustration |

---

## Recommended Priorities

1. **Immediate:** Add skip links; move or collapse testimonials above contact form; surface phone/email in header or footer.
2. **Short-term:** Reduce homepage choices; clarify CTA labels; improve focus indicators; fix contrast.
3. **Ongoing:** Respect `prefers-reduced-motion`; shorten forms; use plain language and scannable structure.

---

## Conclusion

LaunchPad Lab's site is information-rich but cognitively demanding. For users with ADHD, the primary barriers are **too many choices**, **buried contact information**, **no bypass mechanisms**, and **content that competes for attention**. Addressing these issues would significantly improve task completion and reduce frustration for Jordan and users with similar cognitive profiles.
