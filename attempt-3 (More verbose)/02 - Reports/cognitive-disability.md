# Accessibility Report: Cognitive Disability Persona

**Persona:** Jordan (cognitive disability)  
**Website:** https://launchpadlab.com/  
**Test Date:** February 16, 2025  
**Tester:** AI subagent embodying cognitive disability persona

---

## Executive Summary

The Launchpad Lab website presents significant cognitive accessibility barriers. Users with cognitive disabilities (processing speed, working memory limitations) struggle to understand what the company does and to locate contact information. Jargon-heavy language, excessive choices, and unclear labels create confusion and overwhelm. Core tasks are completable but require disproportionate effort.

---

## Issues Identified

### 1. Unusual Words (Jargon) Without Explanations

**WCAG Criterion:** 3.1.3 Unusual Words (Level AAA)  
**Severity:** High  
**Location:** Homepage hero, Services section, testimonials, About page

**Description:** The site uses industry and abstract terms without definitions: "AI-centric," "digital product design," "development firm," "agentic AI," "bespoke," "cross-functional," "discovery process," "digital transformation." Users who process language slowly or concretely cannot infer meaning.

**Fix:** Provide a glossary or expand the first use of each term. Add a plain-language summary at the top of the homepage (e.g., "We build websites and apps for businesses").

**Impact:** Users may abandon the site before understanding the company's purpose.

---

### 2. Reading Level Exceeds Lower Secondary Education

**WCAG Criterion:** 3.1.5 Reading Level (Level AAA)  
**Severity:** High  
**Location:** Hero, service descriptions, testimonials, About page

**Description:** Sentences are long and dense. Testimonials use phrases like "selective choice of questioning," "business units," "marketing strategy," "tumultuous journey of entrepreneurship." Abstract and compound ideas increase cognitive load.

**Fix:** Rewrite key content in short sentences (under 15 words). One idea per sentence. Replace jargon with plain language.

**Impact:** Users with limited working memory cannot retain or process information.

---

### 3. Headings and Labels Do Not Describe Topic or Purpose

**WCAG Criterion:** 2.4.6 Headings and Labels (Level AA)  
**Severity:** Medium  
**Location:** Navigation ("Connect with an Expert"), service box titles, dropdown labels

**Description:** "Connect with an Expert" does not indicate it leads to contact. Service titles ("AI Automation," "Agentic AI") do not explain what the service entails in plain terms. Contact form dropdown may lack a clear label.

**Fix:** Use descriptive labels: "Contact Us" or "Get in Touch" in the nav. Ensure form controls have visible, programmatic labels that state purpose.

**Impact:** Users cannot predict outcomes of actions or locate contact path efficiently.

---

### 4. Too Many Choices at a Decision Point

**WCAG Criterion:** 2.4.6 (interpreted for cognitive load), 2.2.1 Timing Adjustable (related)  
**Severity:** Medium  
**Location:** Homepage Services section (6 boxes), navigation (4+ items), footer links

**Description:** Six service boxes presented simultaneously cause analysis paralysis. Users with working memory limitations (3–5 items) cannot process all options. No progressive disclosure or grouping.

**Fix:** Group services into 2–3 categories. Use accordions or "Learn more" links to reduce initial choices. Limit visible options to 3–5 at any decision point.

**Impact:** Users freeze, pick randomly, or abandon the task.

---

### 5. Contact Path Not Obvious

**WCAG Criterion:** 2.4.6 Headings and Labels, 2.4.4 Link Purpose (In Context)  
**Severity:** High  
**Location:** Navigation, footer, Contact page

**Description:** No explicit "Contact" link in primary navigation. "Connect with an Expert" is ambiguous. Contact form is placed below five long testimonials, requiring extensive scrolling. Users must infer that "Connect with an Expert" = contact.

**Fix:** Add "Contact" to main navigation. Move contact form above testimonials on Contact page, or provide a prominent "Skip to form" link.

**Impact:** Users cannot complete the goal of finding how to contact the company without trial and error.

---

### 6. Form Labels and Required Fields Unclear

**WCAG Criterion:** 3.3.2 Labels or Instructions (Level A), 3.3.1 Error Identification  
**Severity:** Medium  
**Location:** Contact form

**Description:** Form has name, email, company, dropdown, message. Required fields may not be clearly marked. Dropdown purpose may be unclear. No visible indication of which fields are optional vs. required before submission.

**Fix:** Mark required fields with "(required)" or asterisk with legend. Ensure dropdown has a clear label (e.g., "How did you hear about us?" or "Project type"). Provide instructions at top of form.

**Impact:** Users may submit incomplete forms, make errors, or abandon the form.

---

### 7. Long Page Without Skip Links or Landmarks

**WCAG Criterion:** 2.4.1 Bypass Blocks (Level A), 1.3.1 Info and Relationships  
**Severity:** Medium  
**Location:** Homepage, Contact page

**Description:** Homepage is very long with multiple sections. No "Skip to main content" or "Skip to contact form" link. Landmarks (main, nav, etc.) may exist but users who rely on headings to orient may still feel lost. Contact page forces scroll through testimonials before form.

**Fix:** Add skip links. Ensure landmarks are present and correctly used. On Contact page, add "Skip to contact form" link at top.

**Impact:** Users lose their place, re-read content, and experience fatigue.

---

### 8. Inconsistent or Abstract CTA Language

**WCAG Criterion:** 2.4.4 Link Purpose (In Context)  
**Severity:** Medium  
**Location:** "Connect with an Expert" and similar CTAs

**Description:** CTAs use marketing language ("Connect with an Expert," "Let's Go!") instead of action-oriented labels ("Contact Us," "Submit"). Users cannot predict what will happen when they click.

**Fix:** Use explicit action labels: "Contact Us," "Send Message," "Submit Form."

**Impact:** Users hesitate or avoid clicking due to uncertainty.

---

## Recommendations Summary

| Issue | WCAG Ref | Severity | Priority |
|-------|----------|----------|----------|
| Jargon without explanations | 3.1.3 | High | P0 |
| Reading level too high | 3.1.5 | High | P0 |
| Unclear headings/labels | 2.4.6 | Medium | P1 |
| Too many choices | 2.4.6 / cognitive | Medium | P1 |
| Contact path not obvious | 2.4.6, 2.4.4 | High | P0 |
| Form labels/required unclear | 3.3.2 | Medium | P1 |
| Long page, no skip links | 2.4.1 | Medium | P1 |
| Abstract CTA language | 2.4.4 | Medium | P2 |

---

## Conclusion

The site is technically navigable but cognitively demanding. Users with cognitive disabilities can complete core tasks (find what the company does, find contact) only with significant effort. Addressing jargon, reducing choices, clarifying labels, and surfacing the contact path would substantially improve accessibility for this population.
