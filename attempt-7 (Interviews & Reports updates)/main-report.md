# Main Accessibility Report — LaunchPad Lab Website

## Summary

This report consolidates the findings from a structured accessibility and usability evaluation of [https://launchpadlab.com/](https://launchpadlab.com/). The evaluation was conducted through moderated interviews with personas representing real-world users with diverse needs and abilities. Each persona was asked to complete three core tasks on the website:

1. **Visit the website** and share first impressions
2. **Find what the company does**, particularly around AI and technology consulting
3. **Find how to contact** the company or request a consultation

The goal was to identify barriers that prevent users from successfully completing these tasks, with a focus on accessibility (visual, motor, cognitive) and content clarity for non-technical audiences.

---

## Personas, Interviews & Reports

| Persona | Description | Interview | Report |
|---------|-------------|-----------|--------|
| Margaret Chen | 54-year-old CEO of a logistics company. Non-technical. Wears progressive lenses (bifocals). Has mild wrist strain. Looking for an AI consulting partner. | [Interview](01%20-%20Interviews/margaret-chen-interview.md) | [Report](02%20-%20Reports/margaret-chen-report.md) |
| James Okafor | 38-year-old Senior Procurement Analyst. Legally blind. Uses VoiceOver (screen reader) and keyboard-only navigation. Evaluating technology consulting firms for his company. | [Interview](01%20-%20Interviews/james-okafor-interview.md) | [Report](02%20-%20Reports/james-okafor-report.md) |

---

## User Stories

The following user stories were created from the actionable items identified in this report. Each story includes acceptance criteria, developer notes with code examples, and examples from other sites.

| # | Story | Priority | Persona(s) | Link |
|---|-------|----------|------------|------|
| 1 | Replace Image-Based CAPTCHA with an Accessible Alternative | Critical | Margaret, James | [01-captcha-accessibility.md](03%20-%20User%20Stories/01-captcha-accessibility.md) |
| 10 | Add `main` Landmark to All Pages | Critical | James | [10-missing-main-landmark.md](03%20-%20User%20Stories/10-missing-main-landmark.md) |
| 11 | Provide Unique Accessible Names for All "Learn More" Links | Critical | James | [11-ambiguous-learn-more-links.md](03%20-%20User%20Stories/11-ambiguous-learn-more-links.md) |
| 2 | Increase Click Target Size on Service Card "Learn More" Links | High | Margaret | [02-service-card-click-targets.md](03%20-%20User%20Stories/02-service-card-click-targets.md) |
| 3 | Redesign Carousel Navigation with Accessible Controls | High | Margaret, James | [03-carousel-navigation-controls.md](03%20-%20User%20Stories/03-carousel-navigation-controls.md) |
| 4 | Add Missing Industry Categories to "Our Work" Filters | High | Margaret | [04-missing-industry-filters.md](03%20-%20User%20Stories/04-missing-industry-filters.md) |
| 12 | Add Descriptive `title` Attributes to All Iframes | High | James | [12-unlabeled-iframes.md](03%20-%20User%20Stories/12-unlabeled-iframes.md) |
| 5 | Provide Plain-Language Alternatives for Technical Jargon | Medium | Margaret | [05-technical-jargon-reduction.md](03%20-%20User%20Stories/05-technical-jargon-reduction.md) |
| 6 | Reframe AI Autonomy Messaging to Emphasize Human Oversight | Medium | Margaret | [06-ai-autonomy-framing.md](03%20-%20User%20Stories/06-ai-autonomy-framing.md) |
| 7 | Fix Grammatical Error in Services Dropdown Description | Medium | Margaret | [07-grammar-error-services-dropdown.md](03%20-%20User%20Stories/07-grammar-error-services-dropdown.md) |
| 13 | Add Unique `aria-label` to Duplicate Banner Landmarks | Medium | James | [13-duplicate-banner-landmarks.md](03%20-%20User%20Stories/13-duplicate-banner-landmarks.md) |
| 14 | Shorten Accordion Button Accessible Names | Medium | James | [14-accordion-accessible-names.md](03%20-%20User%20Stories/14-accordion-accessible-names.md) |
| 15 | Fix Heading Hierarchy (Stat Labels & Tab Panel Headings) | Medium | James | [15-heading-hierarchy-cleanup.md](03%20-%20User%20Stories/15-heading-hierarchy-cleanup.md) |
| 8 | Replace Vague Marketing Language with Specific, Outcome-Oriented Copy | Low | Margaret | [08-vague-marketing-language.md](03%20-%20User%20Stories/08-vague-marketing-language.md) |
| 9 | Clarify the "Technologies" Navigation Label for Non-Technical Users | Low | Margaret | [09-technologies-nav-label.md](03%20-%20User%20Stories/09-technologies-nav-label.md) |
| 16 | Provide Descriptive Labels for Ambiguous Links | Low | James | [16-ambiguous-connect-link.md](03%20-%20User%20Stories/16-ambiguous-connect-link.md) |
| 17 | Remove or Hide Empty Structural Elements from Accessibility Tree | Low | James | [17-empty-structural-elements.md](03%20-%20User%20Stories/17-empty-structural-elements.md) |
| 18 | Add `aria-required` to Required Form Fields | Low | James | [18-aria-required-form-fields.md](03%20-%20User%20Stories/18-aria-required-form-fields.md) |

---

## Consolidated Findings

The following items are drawn from all individual reports, deduplicated and grouped by theme. Each item includes a summary, the source(s) it originated from, and a priority level.

### 1. CAPTCHA Accessibility Barrier

| Attribute | Detail |
|-----------|--------|
| **Priority** | Critical |
| **Summary** | The contact form includes a CAPTCHA presented in an unlabeled iframe. For users with progressive lenses and wrist strain, the small image tiles are visually and physically challenging. For screen reader users, the iframe has no accessible name — VoiceOver announces only "frame" with no context — and may completely block form submission if the CAPTCHA requires visual interaction. This affects the primary conversion action on the site. Violates WCAG 1.1.1 (Non-text Content), 2.1.1 (Keyboard), and 4.1.2 (Name, Role, Value). |
| **Source** | [Margaret Chen Interview — Task 3](01%20-%20Interviews/margaret-chen-interview.md#task-3-finding-how-to-contact-them), [Margaret Chen Report — Visual & Motor Accessibility](02%20-%20Reports/margaret-chen-report.md#visual-accessibility-issues), [James Okafor Interview — Task 3](01%20-%20Interviews/james-okafor-interview.md#task-3-finding-how-to-contact-them), [James Okafor Report — Form Accessibility](02%20-%20Reports/james-okafor-report.md#form-accessibility-issues) |

### 2. Small Click Targets on Service Card "Learn More" Links

| Attribute | Detail |
|-----------|--------|
| **Priority** | High |
| **Summary** | The "Learn More" links on homepage service cards have small text and small click targets. Users with wrist discomfort reported difficulty clicking them, and users with progressive lenses found the text hard to read. These are primary CTAs that drive users deeper into the site's service offerings. |
| **Source** | [Margaret Chen Interview — Task 1](01%20-%20Interviews/margaret-chen-interview.md#task-1-first-impressions), [Margaret Chen Report — Motor Accessibility](02%20-%20Reports/margaret-chen-report.md#motor-accessibility-issues) |

### 3. Carousel Accessibility Issues (Navigation Controls & Status Text)

| Attribute | Detail |
|-----------|--------|
| **Priority** | High |
| **Summary** | The case study carousel has two distinct accessibility issues. First, navigation uses small circular dot indicators that are difficult targets for users with wrist discomfort and hard to see for users with visual impairments. Second, the carousel's status text announces nonsensical values to screen readers — e.g., "slide 5 to 7 of 3" on the homepage and off-by-one numbering on the contact page — making it impossible for screen reader users to understand their position. Violates WCAG 4.1.2 (Name, Role, Value) and WCAG 2.5.8 (Target Size). |
| **Source** | [Margaret Chen Interview — Task 1](01%20-%20Interviews/margaret-chen-interview.md#task-1-first-impressions), [Margaret Chen Report — Motor Accessibility](02%20-%20Reports/margaret-chen-report.md#motor-accessibility-issues), [James Okafor Interview — Task 1](01%20-%20Interviews/james-okafor-interview.md#task-1-first-impressions--accessibility-structure), [James Okafor Report — Interactive Widget Issues](02%20-%20Reports/james-okafor-report.md#interactive-widget-issues) |

### 4. Missing Industry Categories in "Our Work" Filters

| Attribute | Detail |
|-----------|--------|
| **Priority** | High |
| **Summary** | The "Our Work" page allows filtering case studies by industry, but the filter options exclude major B2B segments such as Logistics, Distribution, Supply Chain, and Manufacturing. Users in these industries cannot quickly find relevant case studies and must manually scan the entire list. This undermines the site's credibility for prospects outside the listed verticals. |
| **Source** | [Margaret Chen Interview — Task 2](01%20-%20Interviews/margaret-chen-interview.md#task-2-understanding-what-they-do), [Margaret Chen Report — Navigation & Information Architecture](02%20-%20Reports/margaret-chen-report.md#navigation--information-architecture-issues) |

### 5. Technical Jargon Without Plain-Language Explanations

| Attribute | Detail |
|-----------|--------|
| **Priority** | Medium |
| **Summary** | Multiple technical terms are used throughout the site without definitions or plain-language alternatives. Terms flagged include: "agentic AI," "sprint," "UAT," "stack," "UI/UX," "CSAT," "codification," "prompts," "data pipelines," and "full digital product lifecycle." Non-technical users experience confusion and reduced trust when encountering these terms. While individually they don't block task completion, their cumulative effect adds significant cognitive friction. |
| **Source** | [Margaret Chen Interview — Tasks 1 & 2](01%20-%20Interviews/margaret-chen-interview.md#task-1-first-impressions), [Margaret Chen Report — Content Clarity](02%20-%20Reports/margaret-chen-report.md#content-clarity-issues) |

### 6. "Autonomous AI Agents" Framing Creates Anxiety

| Attribute | Detail |
|-----------|--------|
| **Priority** | Medium |
| **Summary** | The AI Automation page describes "autonomous AI agents" that "act independently." For non-technical business executives, this framing raises concerns about AI making decisions without human oversight. While the description does mention "escalating when needed," the emphasis on autonomy over governance may deter risk-averse prospects from pursuing the service. |
| **Source** | [Margaret Chen Interview — Task 2](01%20-%20Interviews/margaret-chen-interview.md#task-2-understanding-what-they-do), [Margaret Chen Report — Content Clarity](02%20-%20Reports/margaret-chen-report.md#content-clarity-issues) |

### 7. Grammatical Error in Services Dropdown

| Attribute | Detail |
|-----------|--------|
| **Priority** | Medium |
| **Summary** | The Services dropdown menu contains the phrase "deliver more better and faster," which is grammatically incorrect. For detail-oriented executives, this undermines the professionalism of the site and creates doubt about the quality of the company's communication. |
| **Source** | [Margaret Chen Interview — Task 2](01%20-%20Interviews/margaret-chen-interview.md#task-2-understanding-what-they-do), [Margaret Chen Report — Content Clarity](02%20-%20Reports/margaret-chen-report.md#content-clarity-issues) |

### 8. Vague Marketing Language ("bespoke," "agile," "cross-functional")

| Attribute | Detail |
|-----------|--------|
| **Priority** | Low |
| **Summary** | Terms like "bespoke," "agile," and "cross-functional teams" are used in ways that sound like marketing-speak to non-technical users. While these terms don't prevent task completion, they add low-level friction and reduce the sense that the company is speaking directly to the user's needs rather than to an audience that already understands the terminology. |
| **Source** | [Margaret Chen Interview — Task 1](01%20-%20Interviews/margaret-chen-interview.md#task-1-first-impressions), [Margaret Chen Report — Content Clarity](02%20-%20Reports/margaret-chen-report.md#content-clarity-issues) |

### 9. "Technologies" Navigation Label Is Unclear

| Attribute | Detail |
|-----------|--------|
| **Priority** | Low |
| **Summary** | The "Technologies" item in the main navigation caused slight anxiety for a non-technical user, who was unsure whether clicking it would lead to content relevant to them or to a page full of technical specifications. While it did not prevent task completion, a more descriptive label or subtext could reduce hesitation. |
| **Source** | [Margaret Chen Interview — Task 1](01%20-%20Interviews/margaret-chen-interview.md#task-1-first-impressions), [Margaret Chen Report — Navigation & Information Architecture](02%20-%20Reports/margaret-chen-report.md#navigation--information-architecture-issues) |

### 10. Missing `main` Landmark on All Pages

| Attribute | Detail |
|-----------|--------|
| **Priority** | Critical |
| **Summary** | No `main` landmark is exposed in the accessibility tree on any page. The "Skip to content" link targets `#primary`, but that element does not have `role="main"` or use a `<main>` element. Screen reader users rely on the `main` landmark to jump directly to page content — without it, they must navigate linearly through the header and navigation on every page. Violates WCAG 1.3.1 (Info and Relationships). |
| **Source** | [James Okafor Interview — Task 1](01%20-%20Interviews/james-okafor-interview.md#task-1-first-impressions--accessibility-structure), [James Okafor Report — Landmark & Document Structure](02%20-%20Reports/james-okafor-report.md#landmark--document-structure-issues) |

### 11. Ambiguous Repeated "Learn More" Link Names for Screen Readers

| Attribute | Detail |
|-----------|--------|
| **Priority** | Critical |
| **Summary** | On the Services page and homepage, 8+ links are all labeled "Learn More" with no distinguishing accessible name or programmatic context. When screen reader users navigate by link list, they see 8 identical "Learn More" entries with no way to determine which service each one leads to. This makes link-list navigation — one of the most efficient screen reader techniques — completely useless. Violates WCAG 2.4.4 (Link Purpose in Context). This is distinct from the small click target issue (Item 2) — both affect the same elements but for different user groups. |
| **Source** | [James Okafor Interview — Task 2](01%20-%20Interviews/james-okafor-interview.md#task-2-understanding-what-they-do), [James Okafor Report — Link Accessibility](02%20-%20Reports/james-okafor-report.md#link-accessibility-issues) |

### 12. Unlabeled Iframes Throughout the Site

| Attribute | Detail |
|-----------|--------|
| **Priority** | High |
| **Summary** | Multiple iframes across the site (CAPTCHA widgets, embedded content) have no `title` attribute or accessible name. Screen readers announce them only as "frame" with no context about their content or purpose. Users cannot determine whether an iframe is relevant, interactive, or safe to skip. Violates WCAG 4.1.2 (Name, Role, Value). |
| **Source** | [James Okafor Interview — Tasks 1 & 3](01%20-%20Interviews/james-okafor-interview.md#task-1-first-impressions--accessibility-structure), [James Okafor Report — Interactive Widget Issues](02%20-%20Reports/james-okafor-report.md#interactive-widget-issues) |

### 13. Duplicate `banner` Landmarks Without Unique Labels

| Attribute | Detail |
|-----------|--------|
| **Priority** | Medium |
| **Summary** | Every page has two `banner` landmarks without unique `aria-label` attributes. When screen reader users navigate by landmarks, both appear as generic "banner" with no way to distinguish the site header from a secondary banner region. This creates confusion during landmark navigation. Violates WCAG 1.3.1 (Info and Relationships). |
| **Source** | [James Okafor Interview — Task 1](01%20-%20Interviews/james-okafor-interview.md#task-1-first-impressions--accessibility-structure), [James Okafor Report — Landmark & Document Structure](02%20-%20Reports/james-okafor-report.md#landmark--document-structure-issues) |

### 14. Accordion Buttons with Excessive Accessible Names

| Attribute | Detail |
|-----------|--------|
| **Priority** | Medium |
| **Summary** | Accordion-style buttons on the Services page include their entire expanded content as the accessible name. For example, the "Business" accordion button's name includes the heading, subtext, and full bullet-point list — announced in its entirety when a screen reader focuses the button. This is overwhelming and makes it difficult to understand what the button does. Violates WCAG 2.4.6 (Headings and Labels). |
| **Source** | [James Okafor Interview — Task 2](01%20-%20Interviews/james-okafor-interview.md#task-2-understanding-what-they-do), [James Okafor Report — Interactive Widget Issues](02%20-%20Reports/james-okafor-report.md#interactive-widget-issues) |

### 15. Heading Hierarchy Misuse (Stat Labels and Inactive Tab Headings)

| Attribute | Detail |
|-----------|--------|
| **Priority** | Medium |
| **Summary** | Two heading hierarchy issues were identified. First, metric labels ("Years in Business," "Projects," "Clients") are marked as h2 headings — these are stat labels, not content sections, and they clutter the heading outline. Second, h3 headings inside the "Problems We Solve" tablist remain in the accessibility tree even when their tab panel is not selected, inflating the heading list with off-screen content. Both issues make heading-based navigation less efficient for screen reader users. Violates WCAG 1.3.1 (Info and Relationships). |
| **Source** | [James Okafor Interview — Task 1](01%20-%20Interviews/james-okafor-interview.md#task-1-first-impressions--accessibility-structure), [James Okafor Report — Landmark & Document Structure](02%20-%20Reports/james-okafor-report.md#landmark--document-structure-issues) |

### 16. Ambiguous "Connect" Link on Contact Page

| Attribute | Detail |
|-----------|--------|
| **Priority** | Low |
| **Summary** | The LinkedIn link on the Contact page is labeled only "Connect" with no indication of where it leads. Screen reader users navigating by link list hear "Connect, link" with no context. It should be labeled "Connect with us on LinkedIn" or similar. Violates WCAG 2.4.4 (Link Purpose in Context). |
| **Source** | [James Okafor Interview — Task 3](01%20-%20Interviews/james-okafor-interview.md#task-3-finding-how-to-contact-them), [James Okafor Report — Link Accessibility](02%20-%20Reports/james-okafor-report.md#link-accessibility-issues) |

### 17. Empty Structural Elements Creating Navigation Noise

| Attribute | Detail |
|-----------|--------|
| **Priority** | Low |
| **Summary** | Multiple empty list items and paragraph elements exist in the DOM and are exposed in the accessibility tree. These create unnecessary stops during screen reader navigation, adding noise and cognitive load without providing any content. Violates WCAG 1.3.1 (Info and Relationships). |
| **Source** | [James Okafor Interview — Task 1](01%20-%20Interviews/james-okafor-interview.md#task-1-first-impressions--accessibility-structure), [James Okafor Report — Landmark & Document Structure](02%20-%20Reports/james-okafor-report.md#landmark--document-structure-issues) |

### 18. Missing `aria-required` on Required Form Fields

| Attribute | Detail |
|-----------|--------|
| **Priority** | Low |
| **Summary** | Required form fields convey their required state only through a visual asterisk character in the label text. While functional, best practice is to also use `aria-required="true"` so screen readers explicitly announce "required" independently of the visual indicator. This ensures programmatic exposure of the required state. Relates to WCAG 3.3.2 (Labels or Instructions). |
| **Source** | [James Okafor Interview — Task 3](01%20-%20Interviews/james-okafor-interview.md#task-3-finding-how-to-contact-them), [James Okafor Report — Form Accessibility](02%20-%20Reports/james-okafor-report.md#form-accessibility-issues) |

---

## Priority Summary

| Priority | Count | Items |
|----------|-------|-------|
| **Critical** | 3 | CAPTCHA Accessibility Barrier, Missing `main` Landmark, Ambiguous "Learn More" Link Names |
| **High** | 4 | Small Click Targets, Carousel Accessibility Issues, Missing Industry Filters, Unlabeled Iframes |
| **Medium** | 6 | Technical Jargon, AI Autonomy Framing, Grammar Error, Duplicate Banner Landmarks, Accordion Button Names, Heading Hierarchy Misuse |
| **Low** | 5 | Vague Marketing Language, "Technologies" Nav Label, Ambiguous "Connect" Link, Empty Structural Elements, Missing `aria-required` |

---

*This report was generated on February 18, 2026, based on moderated usability interviews. Findings should be validated with additional user profiles before finalizing development priorities.*
