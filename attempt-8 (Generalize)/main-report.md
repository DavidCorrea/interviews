# Main Report: LaunchPad Lab Accessibility & Usability Audit

**Website:** https://launchpadlab.com/  
**Date:** February 18, 2026  
**Method:** Persona-driven usability interviews using browser automation

---

## Summary

This report documents the findings of a usability audit conducted on the LaunchPad Lab website. The audit used a persona-driven interview methodology where a simulated user — representing a specific target audience — navigated the website to complete defined goals: visit the site, find out what the company does, and find how to contact them.

The persona was crafted to represent a real-world user segment that may visit the site, with specific characteristics, behaviors, and limitations that influence how they perceive and interact with the website. The interviewee browsed the site using real browser automation (not screenshots or inspections) to ensure feedback was grounded in authentic experience.

---

## Personas

| Persona | Description | Interview | Report |
|---------|-------------|-----------|--------|
| [Jayden Rivera](00%20-%20Personas/gen-z-app-founder.md) | 22-year-old Gen-Z solo founder with an AI app idea. Tech-savvy skimmer who needs a dev agency but is allergic to corporate messaging. | [Interview](01%20-%20Interviews/jayden-rivera-interview.md) | [Report](02%20-%20Reports/jayden-rivera-report.md) |

---

## User Stories

| # | Story | Priority | Link |
|---|-------|----------|------|
| 1 | [Startup-Inclusive Homepage Messaging](03%20-%20User%20Stories/01-startup-inclusive-messaging.md) | High | [Issue 1](02%20-%20Reports/jayden-rivera-report.md#issue-1-enterprise-centric-messaging-alienates-startup-founders), [Issue 10](02%20-%20Reports/jayden-rivera-report.md#issue-10-no-startupmvp-specific-content) |
| 2 | [Consumer Case Studies on Homepage](03%20-%20User%20Stories/02-consumer-case-studies-homepage.md) | High | [Issue 2](02%20-%20Reports/jayden-rivera-report.md#issue-2-consumer-portfolio-buried-under-enterprise-case-studies) |
| 3 | [Balanced Technology Identity](03%20-%20User%20Stories/03-balanced-technology-identity.md) | Medium | [Issue 3](02%20-%20Reports/jayden-rivera-report.md#issue-3-overemphasis-on-salesforce-identity) |
| 4 | [Inclusive Contact Form Fields](03%20-%20User%20Stories/04-inclusive-contact-form.md) | Medium | [Issue 4](02%20-%20Reports/jayden-rivera-report.md#issue-4-company-email-field-creates-barrier-for-solo-founders) |
| 5 | [Pricing Transparency](03%20-%20User%20Stories/05-pricing-transparency.md) | Medium | [Issue 5](02%20-%20Reports/jayden-rivera-report.md#issue-5-no-pricing-transparency) |
| 6 | [Modern Tech Stack Visibility](03%20-%20User%20Stories/06-modern-tech-stack-visibility.md) | Medium | [Issue 6](02%20-%20Reports/jayden-rivera-report.md#issue-6-technology-stack-listing-feels-dated) |
| 7 | [Differentiated Hero Copy](03%20-%20User%20Stories/07-differentiated-hero-copy.md) | Low | [Issue 7](02%20-%20Reports/jayden-rivera-report.md#issue-7-homepage-hero-copy-is-generic) |
| 8 | [Grammar Fix on Services Page](03%20-%20User%20Stories/08-grammar-fix-services.md) | Low | [Issue 8](02%20-%20Reports/jayden-rivera-report.md#issue-8-grammar-error-on-services-page) |
| 9 | [Frictionless CAPTCHA](03%20-%20User%20Stories/09-frictionless-captcha.md) | Low | [Issue 9](02%20-%20Reports/jayden-rivera-report.md#issue-9-captcha-on-contact-form) |

---

## Consolidated Findings

The following items emerged from the usability interviews and reports. Duplicate and related items have been grouped.

### 1. Enterprise-Centric Messaging Alienates Non-Enterprise Users

**Priority:** High  
**Summary:** The website's copy overwhelmingly targets enterprise audiences with phrases like "Modern Enterprise," "Digital Transformation," and "Operational Efficiency." Users who are not enterprise buyers (startup founders, small business owners, individual entrepreneurs) feel excluded or assume the agency doesn't work with their segment — even though the portfolio suggests otherwise.

**Sources:**
- [Interview: Homepage Hero](01%20-%20Interviews/jayden-rivera-interview.md#hero-section) — *"This is already giving enterprise energy"*
- [Interview: AI Partner Section](01%20-%20Interviews/jayden-rivera-interview.md#strategic-ai-partner-section) — *"'Modern Enterprise.' That's their target customer. They said the quiet part loud."*
- [Report: Issue 1](02%20-%20Reports/jayden-rivera-report.md#issue-1-enterprise-centric-messaging-alienates-startup-founders)
- [Report: Issue 10](02%20-%20Reports/jayden-rivera-report.md#issue-10-no-startupmvp-specific-content)

---

### 2. Consumer/Startup Case Studies Are Not Surfaced

**Priority:** High  
**Summary:** The homepage exclusively showcases enterprise case studies (Millennium Trust, Prosci, CDK Global). Impressive consumer-scale work — Breadcrumb (10M views), NextLot ($2B+), Omaha Zoo (25M users) — is buried deep in the portfolio page and requires significant scrolling to discover. First impressions are shaped by the homepage carousel, which misrepresents the breadth of the agency's experience.

**Sources:**
- [Interview: Homepage Case Studies](01%20-%20Interviews/jayden-rivera-interview.md#homepage-case-studies-carousel) — *"Cool results but again, very enterprise"*
- [Interview: Consumer Portfolio](01%20-%20Interviews/jayden-rivera-interview.md#consumerstartup-case-studies) — *"Those are the case studies I wish were on the homepage"*
- [Report: Issue 2](02%20-%20Reports/jayden-rivera-report.md#issue-2-consumer-portfolio-buried-under-enterprise-case-studies)

---

### 3. Salesforce Branding Overrepresentation

**Priority:** Medium  
**Summary:** Salesforce is prominently featured across the entire site — footer badge, dedicated service pages, Agentforce mentions on the AI page, and Clutch badges. For users who don't need Salesforce, this creates the impression that the agency is primarily a Salesforce consultancy, which narrows perceived relevance.

**Sources:**
- [Interview: Services Cards](01%20-%20Interviews/jayden-rivera-interview.md#driving-roi-with-ai) — *"I personally couldn't care less about Salesforce"*
- [Interview: Salesforce Ecosystem](01%20-%20Interviews/jayden-rivera-interview.md#salesforce-ecosystem) — *"They're DEEP in the Salesforce ecosystem"*
- [Interview: Overall Negative](01%20-%20Interviews/jayden-rivera-interview.md#what-didnt-work) — *"Salesforce is EVERYWHERE... 40% of their identity"*
- [Report: Issue 3](02%20-%20Reports/jayden-rivera-report.md#issue-3-overemphasis-on-salesforce-identity)

---

### 4. Contact Form "Company Email" Label Is Exclusionary

**Priority:** Medium  
**Summary:** The contact form uses the label "Company Email" rather than "Email," which signals to solo founders, freelancers, and individuals that the form isn't intended for them. This creates unnecessary friction at a critical conversion point.

**Sources:**
- [Interview: Homepage Footer](01%20-%20Interviews/jayden-rivera-interview.md#homepage-footer--form) — *"That's a little intimidating for a solo founder"*
- [Report: Issue 4](02%20-%20Reports/jayden-rivera-report.md#issue-4-company-email-field-creates-barrier-for-solo-founders)

---

### 5. No Pricing Information or Budget Expectations

**Priority:** Medium  
**Summary:** The entire site lacks any pricing indicators — no ranges, tiers, or starting-at figures. Users cannot self-qualify, which may deter budget-conscious prospects from reaching out. The free AI Opportunity Workshop partially addresses this but doesn't substitute for pricing context.

**Sources:**
- [Interview: Overall Negative](01%20-%20Interviews/jayden-rivera-interview.md#what-didnt-work) — *"No pricing transparency whatsoever"*
- [Report: Issue 5](02%20-%20Reports/jayden-rivera-report.md#issue-5-no-pricing-transparency)

---

### 6. Listed Tech Stack Doesn't Reflect Modern Startup Ecosystem

**Priority:** Medium  
**Summary:** The Technologies page features Ruby on Rails, ReactJS, and Ionic. While solid, these don't reflect the frameworks and platforms that startup founders and modern developers expect (Next.js, TypeScript, Tailwind, Vercel, Supabase). The agency claims to be tech-agnostic, but the listed stack creates a perception gap.

**Sources:**
- [Interview: Frameworks](01%20-%20Interviews/jayden-rivera-interview.md#frameworks--languages) — *"No mention of Next.js, TypeScript-first"*
- [Report: Issue 6](02%20-%20Reports/jayden-rivera-report.md#issue-6-technology-stack-listing-feels-dated)

---

### 7. Generic Homepage Hero Copy

**Priority:** Low  
**Summary:** "AI Innovation. Digital Solutions. Results that Matter." is perceived as generic and undifferentiated. Specifically, "Results that Matter" could appear on any agency site. The headline misses an opportunity to lead with concrete differentiators (6-week launches, 730+ projects, consumer AI expertise).

**Sources:**
- [Interview: Homepage Hero](01%20-%20Interviews/jayden-rivera-interview.md#hero-section) — *"'Results that Matter' is the kind of thing every single agency says"*
- [Report: Issue 7](02%20-%20Reports/jayden-rivera-report.md#issue-7-homepage-hero-copy-is-generic)

---

### 8. Grammar Error on Services Page

**Priority:** Low  
**Summary:** The Services page tagline reads "deliver more better and faster," which is grammatically incorrect and undermines professionalism.

**Sources:**
- [Interview: Services Page](01%20-%20Interviews/jayden-rivera-interview.md#the-services-page) — *"the grammar on 'deliver more better and faster' is a little awkward"*
- [Report: Issue 8](02%20-%20Reports/jayden-rivera-report.md#issue-8-grammar-error-on-services-page)

---

### 9. CAPTCHA Adds Contact Form Friction

**Priority:** Low  
**Summary:** The contact form includes a visible CAPTCHA iframe. While necessary for spam prevention, visible CAPTCHAs add friction and are a known accessibility barrier. Modern alternatives (reCAPTCHA v3, honeypot fields) achieve the same goal with less user-facing friction.

**Sources:**
- [Interview: Homepage Footer](01%20-%20Interviews/jayden-rivera-interview.md#homepage-footer--form)
- [Report: Issue 9](02%20-%20Reports/jayden-rivera-report.md#issue-9-captcha-on-contact-form)
