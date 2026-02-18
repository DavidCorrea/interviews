# Technical Report: Screen Reader User Accessibility Assessment

**Website:** https://launchpadlab.com/  
**Persona:** David Okonkwo (Blind Screen Reader User — NVDA/VoiceOver)  
**Assessment Date:** February 16, 2025  
**Testing Method:** Persona-based evaluation (heading navigation, landmark navigation, link/button labels, form accessibility, alt text)

---

## Executive Summary

LaunchPad Lab's website is partially accessible to blind screen reader users. The persona (David Okonkwo) successfully completed the task of finding what the company does and how to contact them, but reported significant frustration due to confusing heading structure, unlabeled or generic links, a contact form that could not be located or accessed via keyboard, and unclear ARIA landmarks. The site benefits from a functional skip link, descriptive page titles, and reachable contact information (email, phone). However, structural and labeling issues—duplicate H2 headings, statistics incorrectly marked as headings, multiple "Learn More" links without context, and an inaccessible or missing contact form—create substantial barriers for efficient screen reader navigation.

**Key findings:**
- Duplicate H2 headings throughout (e.g., section label + subtitle both as H2)
- Statistics ("12+ Years in Business," "730+ Projects," "240+ Clients") incorrectly marked as H2
- Six or more "Learn More" links with no distinguishing context (WCAG 2.4.4 failure)
- Contact form referenced in content but not keyboard accessible or not exposed to screen readers
- Unclear or missing landmark structure (main, nav, contentinfo)
- Generic "Connect" link for LinkedIn without destination context
- Skip link present and functional (positive)

---

## Specific Accessibility Issues

### Critical

#### C1. Contact Form Not Keyboard Accessible or Not Exposed
| Field | Detail |
|-------|--------|
| **Description** | The Contact page states "Complete the form below" but no form fields (inputs, textareas, submit button) are reachable via Tab or announced by screen readers. The form may be in an iframe, loaded dynamically without focus management, or not keyboard accessible. |
| **Location** | https://launchpadlab.com/contact/ |
| **Impact** | Users who prefer or require the contact form cannot use it. Screen reader users cannot complete the primary contact CTA. This blocks a key user flow. |
| **Recommended Fix** | Ensure the contact form is in the main DOM (not hidden or inaccessible). If in an iframe (e.g., HubSpot), ensure the iframe has a descriptive `title` and that form fields are focusable and properly labeled. If loaded dynamically, move focus to the form when it appears. Ensure all fields have associated `<label>` elements and that the submit button is reachable via Tab. |
| **WCAG** | **2.1.1 Keyboard** (Level A) — All functionality operable via keyboard; **4.1.2 Name, Role, Value** (Level A) — UI components have programmatically determinable name and role |

---

#### C2. Multiple "Learn More" Links Without Context
| Field | Detail |
|-------|--------|
| **Description** | Six or more links on the homepage and other pages use the identical text "Learn More" with no additional context. Each link refers to a different service (AI Automation, Web Development, Mobile Development, etc.), but the link text alone does not convey purpose. |
| **Location** | Homepage (services section), Services page, possibly other pages |
| **Impact** | Screen reader users cannot distinguish links when using the links list (Insert+F7 in NVDA). Each "Learn More" sounds identical. Users must tab to each link and read surrounding context—inefficient and frustrating. |
| **Recommended Fix** | Use unique, descriptive link text: "Learn more about AI Automation & Agentic AI," "Learn more about Web Application Development," etc. Alternatively, use `aria-label` to provide context: `<a href="..." aria-label="Learn more about AI Automation & Agentic AI">Learn More</a>`. Ensure link purpose is determinable from link text alone or with programmatic context. |
| **WCAG** | **2.4.4 Link Purpose (In Context)** (Level A) — The purpose of each link can be determined from the link text alone or from the link text together with its programmatically determined link context |

---

### High

#### H1. Duplicate H2 Headings for Same Section
| Field | Detail |
|-------|--------|
| **Description** | Almost every major section has two consecutive H2 headings—e.g., "Problems We Solve" followed by "Ship Game-Changing Digital Products to Market Fast," or "Reach Out" followed by "Let's Build Something Great." The second heading functions as a subtitle visually but is marked as a heading, doubling the heading count. |
| **Location** | Homepage, About page, Services page, Contact page |
| **Impact** | Heading navigation (H key) becomes inefficient. Users hear redundant information. Mental model of page structure is confused. Screen reader users expect one heading per section. |
| **Recommended Fix** | Use one H2 per section. Make the subtitle regular text (e.g., `<p>`) or an H3 only if it introduces a distinct subsection. Example: H2 "Our Services" with subtitle as `<p class="subtitle">AI-Powered solutions...</p>`. |
| **WCAG** | **2.4.6 Headings and Labels** (Level AA) — Headings describe topic or purpose; **1.3.1 Info and Relationships** (Level A) — Structure can be programmatically determined |

---

#### H2. Statistics Incorrectly Marked as Headings
| Field | Detail |
|-------|--------|
| **Description** | "12+ Years in Business," "730+ Projects," and "240+ Clients" are marked as H2 headings. These are statistics/data points, not section headings. They do not introduce content sections. |
| **Location** | Homepage (statistics section) |
| **Impact** | Heading navigation announces "Heading level 2, Years in Business" etc., which misleads users about page structure. Users expect headings to denote sections, not data values. |
| **Recommended Fix** | Use `<div>`, `<span>`, or a definition list (`<dl>`) for statistics. Do not use heading elements. If a section needs a heading, use one H2 such as "Our Track Record" and keep the stats as non-heading content. |
| **WCAG** | **2.4.6 Headings and Labels** (Level AA); **1.3.1 Info and Relationships** (Level A) |

---

#### H3. Unclear or Missing Landmark Structure
| Field | Detail |
|-------|--------|
| **Description** | Landmark navigation (D key in NVDA) does not clearly announce banner, navigation, main, and contentinfo regions. Semantic HTML5 elements (`<main>`, `<nav>`, `<header>`, `<footer>`) or equivalent ARIA roles may be missing or improperly used. |
| **Location** | All pages |
| **Impact** | Screen reader users cannot jump directly to main content or navigation using landmark shortcuts. They must tab or read sequentially, which is slower and more frustrating. |
| **Recommended Fix** | Use semantic HTML5: `<header>`, `<nav>`, `<main>`, `<footer>`. Ensure `<main>` wraps the primary content. If multiple `<nav>` elements exist, use `aria-label` to distinguish (e.g., `aria-label="Main navigation"`, `aria-label="Footer links"`). Verify with D key that landmarks are announced. |
| **WCAG** | **2.4.1 Bypass Blocks** (Level A) — Mechanism to bypass repeated blocks; **1.3.1 Info and Relationships** (Level A) |

---

#### H4. Generic "Connect" Link for LinkedIn
| Field | Detail |
|-------|--------|
| **Description** | The LinkedIn link is announced as "Connect" with no indication of destination. Users cannot determine that it links to LaunchPad Lab's LinkedIn page. |
| **Location** | Contact page (and possibly footer) |
| **Impact** | Link purpose is not determinable from link text alone. "Connect" could mean many things. |
| **Recommended Fix** | Use descriptive link text: "Connect with LaunchPad Lab on LinkedIn" or "LaunchPad Lab on LinkedIn." Alternatively, use `aria-label="Connect with LaunchPad Lab on LinkedIn"` if visible text must remain short. |
| **WCAG** | **2.4.4 Link Purpose (In Context)** (Level A); **4.1.2 Name, Role, Value** (Level A) |

---

### Medium

#### M1. Icon-Only Buttons May Lack Accessible Names
| Field | Detail |
|-------|--------|
| **Description** | Icon-only buttons (e.g., hamburger menu, carousel arrows, social icons) may not have `aria-label` or visible text. Screen reader users may hear "button" with no purpose. |
| **Location** | Navigation (mobile menu toggle), carousels, social/share buttons |
| **Impact** | Users cannot determine button purpose. Critical for hamburger menu—users must be able to open navigation. |
| **Recommended Fix** | Add `aria-label` to all icon-only buttons: "Open menu," "Close menu," "Next slide," "Previous slide," "Share on LinkedIn." Ensure every focusable control has an accessible name. |
| **WCAG** | **4.1.2 Name, Role, Value** (Level A); **2.1.1 Keyboard** (Level A) |

---

#### M2. Images May Have Missing or Generic Alt Text
| Field | Detail |
|-------|--------|
| **Description** | Award badges, case study screenshots, and decorative icons may have missing, filename-based, or generic alt text (e.g., "Prosci Interface Screenshot" instead of a description of what is shown). Decorative images may not be hidden (`alt=""` or `aria-hidden="true"`). |
| **Location** | Homepage (client logos, case studies, award badges), Services page, About page |
| **Impact** | Informative images without proper alt text convey no meaning. Decorative images that are not hidden add noise. Filename-based alt text is useless. |
| **Recommended Fix** | Informative images: Provide alt text that conveys the same information (e.g., "2025 Clutch Top Salesforce Company award badge for United States"). Decorative images: Use `alt=""` or `aria-hidden="true"`. Logo images: Use "LaunchPad Lab logo" or "LaunchPad Lab home" if linked. |
| **WCAG** | **1.1.1 Non-text Content** (Level A) — All non-text content has a text alternative |

---

#### M3. Repeated H1/H2 Text on Contact Page
| Field | Detail |
|-------|--------|
| **Description** | The Contact page H1 is "Ready to Build Something Great?" and an H2 repeats the same text. Screen reader users hear the same phrase twice, which sounds like an error or duplicate content. |
| **Location** | https://launchpadlab.com/contact/ |
| **Impact** | Confusion. Users may think the page loaded incorrectly or that content is duplicated. |
| **Recommended Fix** | Use one heading for the main contact message. If a subtitle is needed, use regular text or a single H2 with different wording. |
| **WCAG** | **2.4.6 Headings and Labels** (Level AA) |

---

### Low

#### L1. No Accessibility Statement
| Field | Detail |
|-------|--------|
| **Description** | No accessibility statement or policy is linked. Users cannot easily report accessibility issues or understand the site's commitment to accessibility. |
| **Location** | Footer, site-wide |
| **Impact** | Minor. Users with accessibility needs may want to know the site's stance and how to report problems. |
| **Recommended Fix** | Add an accessibility statement page. Link from footer. Include contact information for accessibility feedback. |
| **WCAG** | Best practice; supports **2.4.1 Bypass Blocks** and user trust |

---

## WCAG Guidelines Referenced

| Guideline | Level | Relevance |
|-----------|-------|-----------|
| **1.1.1 Non-text Content** | A | Image alt text |
| **1.3.1 Info and Relationships** | A | Heading structure, landmarks |
| **2.1.1 Keyboard** | A | Form accessibility, all functionality keyboard operable |
| **2.4.1 Bypass Blocks** | A | Skip link, landmarks |
| **2.4.4 Link Purpose (In Context)** | A | "Learn More," "Connect" links |
| **2.4.6 Headings and Labels** | AA | Duplicate headings, statistics as headings |
| **4.1.2 Name, Role, Value** | A | Form fields, buttons, links—accessible names |

---

## Priority Recommendations

### P0 (Immediate)
1. **Fix contact form accessibility** — Ensure the form is keyboard accessible, all fields are focusable and labeled, and the form is exposed to screen readers. If in an iframe, verify iframe title and form accessibility.
2. **Make "Learn More" links unique** — Add context to each link (e.g., "Learn more about AI Automation") or use `aria-label` so link purpose is determinable.

### P1 (High)
3. **Reduce duplicate H2 headings** — Use one H2 per section; make subtitles regular text.
4. **Remove headings from statistics** — Use non-heading elements for "12+ Years," "730+ Projects," "240+ Clients."
5. **Implement clear landmarks** — Add `<main>`, `<nav>`, `<header>`, `<footer>`. Label multiple navs with `aria-label`.
6. **Fix "Connect" link** — Use "Connect with LaunchPad Lab on LinkedIn" or equivalent.

### P2 (Medium)
7. **Audit icon-only buttons** — Ensure hamburger menu, carousel arrows, and social icons have `aria-label`.
8. **Audit image alt text** — Fix award badges, case study screenshots, decorative images.
9. **Fix Contact page heading duplication** — Remove repeated H1/H2 text.

### P3 (Low)
10. **Add accessibility statement** — Link from footer with contact for accessibility feedback.

---

*This report is based on persona-driven evaluation (David Okonkwo, blind screen reader user) and content/structure analysis of https://launchpadlab.com/. Testing was simulated by examining DOM structure, ARIA, and semantic HTML as reported in prior assessments. Verification with live screen reader testing (NVDA, JAWS, or VoiceOver) is recommended.*
