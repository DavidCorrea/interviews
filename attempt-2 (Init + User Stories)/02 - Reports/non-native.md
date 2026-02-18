# Technical Report: Non-Native English Speaker Accessibility

**Website:** https://launchpadlab.com/  
**Persona:** Maria Santos (Non-Native English Speaker, B1/B2 CEFR)  
**Test Date:** February 16, 2025  
**Test Task:** Find what the company does and how to contact them

---

## Executive Summary

LaunchPad Lab's website presents significant language barriers for users with intermediate English proficiency (B1/B2 level). The primary issues center on **jargon and unfamiliar terminology**, **idioms and figurative language**, **unexplained acronyms**, **complex sentence structures**, and **abstract rather than concrete language**. While standard navigation labels (About, Services, Contact) and some visual structure provide orientation, the content is written for native English speakers familiar with American business and tech culture. Users like Maria Santos may struggle to complete basic tasks—understanding what the company does and finding contact information—without frequent lookups, re-reading, or assistance.

**Key findings:**
- Jargon throughout: "bespoke," "agentic," "seamless handoff," "discovery process," "operational efficiency"
- Idioms that don't translate well: "harness the power," "move the needle," "hit the ground running"
- Acronyms used without expansion: ROI, MVP, UAT
- Long, multi-clause sentences in testimonials and service descriptions
- Contact page prioritizes testimonials over contact details
- No plain-language summary or simplified content option

---

## Accessibility Issues

### Critical

#### 1. Jargon and Unusual Words Without Definitions

| Field | Detail |
|-------|--------|
| **Description** | Terms such as "bespoke," "agentic," "seamless handoff," "discovery process," "operational efficiency," "codification," "cross-functional," and "proof of concept" appear without definition or plain-language alternatives. A B1/B2 reader would need to look these up or guess. |
| **Location** | Homepage, About page, Services pages, AI/Agentic AI content, Contact page testimonials |
| **Impact** | Non-native speakers cannot understand core service descriptions. Blocks comprehension of what the company does and whether their services are relevant. |
| **Recommended Fix** | Replace jargon with plain-language equivalents on first use, or provide inline definitions. Examples: "bespoke" → "custom-made"; "agentic AI" → "AI that works independently to complete tasks"; "discovery process" → "we talk with you to understand your needs before building." Consider a glossary for key terms. |
| **WCAG** | **3.1.3 Unusual Words (Level AAA)** — A mechanism is available for identifying specific definitions of words or phrases used in an unusual or restricted way. |

---

#### 2. Idioms and Figurative Language

| Field | Detail |
|-------|--------|
| **Description** | Phrases like "harness the power," "move the needle," "hit the ground running," "low-hanging fruit," and "ever-ready presence" rely on figurative or idiomatic meaning. These do not translate well and are confusing for non-native speakers who may interpret them literally. |
| **Location** | Marketing copy, service descriptions, testimonials |
| **Impact** | Idioms create comprehension barriers. Translation tools often produce garbled or misleading output for idiomatic expressions. Users may misinterpret or skip content entirely. |
| **Recommended Fix** | Replace idioms with literal, direct equivalents. "Harness the power of AI" → "Use AI" or "Work with AI." "Move the needle" → "Make a real difference" or "Improve results." "Hit the ground running" → "Start quickly and effectively." |
| **WCAG** | **3.1.3 Unusual Words (Level AAA)** — Idioms fall under "unusual" usage. **3.1.5 Reading Level (Level AAA)** — Idioms increase reading difficulty. |

---

#### 3. Acronyms Not Expanded on First Use

| Field | Detail |
|-------|--------|
| **Description** | Acronyms such as ROI, MVP, UAT, AI (in some contexts), and UX appear without expansion. Non-native speakers may not know that ROI = Return on Investment, MVP = Minimum Viable Product, or UAT = User Acceptance Testing. |
| **Location** | Service descriptions, blog content, testimonials |
| **Impact** | Acronyms create instant barriers. Users must guess, look up, or skip. Reduces confidence and comprehension. |
| **Recommended Fix** | Expand all acronyms on first use: "ROI (Return on Investment)," "MVP (Minimum Viable Product)," "UAT (User Acceptance Testing)." Use the full form first, then acronym in parentheses for subsequent uses. |
| **WCAG** | **3.1.4 Abbreviations (Level AAA)** — A mechanism for identifying the expanded form or meaning of abbreviations is available. |

---

#### 4. No Plain-Language Summary of Company Purpose

| Field | Detail |
|-------|--------|
| **Description** | The homepage and key pages do not provide a simple, 1–2 sentence summary of what LaunchPad Lab does. Users must infer from "AI-Centric Digital Product Design & Development" and similar abstract phrasing. |
| **Location** | Homepage, About page, Services page |
| **Impact** | Non-native speakers cannot quickly answer "What does this company do?" without parsing jargon and abstract language. Increases task abandonment. |
| **Recommended Fix** | Add a prominent plain-language summary at the top of the homepage and About page: "We build websites and mobile apps for businesses. We help you use AI and technology to grow. We are based in Chicago." Consider a "Read in simple English" toggle or supplemental summary. |
| **WCAG** | **3.1.5 Reading Level (Level AAA)** — When text requires reading ability more advanced than the lower secondary education level, supplemental content or a version that does not require advanced reading ability is available. |

---

#### 5. Contact Information Obscured by Testimonials

| Field | Detail |
|-------|--------|
| **Description** | The Contact page features multiple long testimonials before or alongside contact details. Testimonials use complex language ("discovery process," "selective choice of questioning," "tumultuous journey of entrepreneurship") and occupy prominent space. Phone, email, and form may be below the fold. |
| **Location** | Contact page (https://launchpadlab.com/contact) |
| **Impact** | Users seeking contact information must scroll past jargon-heavy content. Increases frustration and task completion time. Users who prefer to call or email may not find direct contact details. |
| **Recommended Fix** | Reorder Contact page: (1) Clear "Contact Us" heading, (2) Phone, email, address prominently displayed, (3) Contact form, (4) Testimonials moved to bottom or separate page. Ensure phone and email are visible without scrolling. |
| **WCAG** | **2.4.6 Headings and Labels (Level AA)** — Headings describe topic/purpose. **2.1 Operable** — Multiple ways to complete tasks (form, phone, email). |

---

### High

#### 6. Complex Sentence Structures

| Field | Detail |
|-------|--------|
| **Description** | Long sentences (20+ words) with multiple clauses, passive voice, or nested qualifiers appear in testimonials and service descriptions. Example: "Their attention to detail in the discovery process, and their selective choice of questioning is what really stood out to me. The information they were able to gather from each business unit provided insights that have evolved beyond just our website and have moved on to shaping many aspects of our overall marketing strategy." |
| **Location** | Contact page testimonials, About page, Services descriptions |
| **Impact** | Non-native speakers must re-read multiple times. Increases cognitive load and comprehension failure. Long sentences are harder to parse in a second language. |
| **Recommended Fix** | Break long sentences into 2–3 shorter sentences (15–20 words or fewer). Use active voice. One idea per sentence. Example: "They asked good questions. They learned about our business. This helped us improve our website and marketing." |
| **WCAG** | **3.1.5 Reading Level (Level AAA)** — Supplemental content or simplified version when text requires advanced reading ability. |

---

#### 7. Abstract Language Instead of Concrete Examples

| Field | Detail |
|-------|--------|
| **Description** | Phrases like "drive operational efficiency," "unlock growth," "strategic partner," "digital transformation," and "tailored consulting" are abstract. They do not clearly describe concrete actions or outcomes. |
| **Location** | Homepage, About page, Services pages |
| **Impact** | Non-native speakers rely on concrete, literal content. Abstract claims require inference and cultural familiarity. "We help you work faster and save money" is clearer than "We drive operational efficiency." |
| **Recommended Fix** | Replace abstract claims with concrete equivalents. "Drive operational efficiency" → "Help you work faster and reduce costs." "Unlock growth" → "Help your business grow." Include specific examples: "We built an app for X company that reduced their processing time by 50%." |
| **WCAG** | **3.1.5 Reading Level (Level AAA)** — Supplemental content for advanced reading level. |

---

#### 8. Testimonials Use Jargon and Complex Language

| Field | Detail |
|-------|--------|
| **Description** | Client testimonials on the Contact page use terms like "discovery process," "selective choice of questioning," "business unit," "marketing strategy," "mainstay," "ever-ready presence," "tumultuous journey of entrepreneurship." These are not edited for plain language. |
| **Location** | Contact page |
| **Impact** | Testimonials block users from reaching contact details and add no value for users who cannot understand them. Creates negative impression and frustration. |
| **Recommended Fix** | Edit testimonials for plain language where possible, or provide shorter, simplified summaries. Move testimonials to a dedicated "Reviews" or "Testimonials" page. On Contact page, prioritize contact information only. |
| **WCAG** | **3.1.3 Unusual Words (Level AAA)** — Definitions for unusual terms. **3.1.5 Reading Level (Level AAA)** — Simplified version where needed. |

---

### Medium

#### 9. Inconsistent Terminology Across Pages

| Field | Detail |
|-------|--------|
| **Description** | If navigation or content uses varying labels for the same concept (e.g., "Contact" on one page, "Get in Touch" or "Reach Out" on another), non-native speakers must map these to the same meaning. Inconsistent terminology increases cognitive load. |
| **Location** | Navigation, CTAs, page headers |
| **Impact** | Users may not recognize that "Get in Touch" and "Contact" are the same. Reduces confidence and wayfinding. |
| **Recommended Fix** | Use consistent, standard labels site-wide: "Contact," "About," "Services," "Work." Avoid creative alternatives (e.g., "Let's Connect," "Reach Out") unless clearly equivalent and used consistently. |
| **WCAG** | **3.2.4 Consistent Identification (Level AA)** — Components with the same functionality are identified consistently. |

---

#### 10. No Glossary or "Simple Summary" Option

| Field | Detail |
|-------|--------|
| **Description** | The site does not provide a glossary for business/tech terms (AI, ROI, MVP, UAT, Salesforce, proof of concept, etc.) or a "Read in simple English" option for key pages. |
| **Location** | Site-wide |
| **Impact** | Users must use external tools (dictionary, Google Translate) to understand content. Translation of jargon and idioms often fails. No in-site support for comprehension. |
| **Recommended Fix** | Add a glossary page linking key terms to definitions. Consider a "Simple summary" toggle or short plain-language summary at the top of key pages (About, Services, Contact). |
| **WCAG** | **3.1.3 Unusual Words (Level AAA)** — Mechanism for definitions. **3.1.5 Reading Level (Level AAA)** — Supplemental content for advanced reading level. |

---

#### 11. Contact Form Labels and Instructions

| Field | Detail |
|-------|--------|
| **Description** | If the contact form uses labels like "Project brief," "Contact email," or "Tell us about your initiative" without plain-language alternatives, non-native speakers may struggle. Error messages must also be simple and actionable. |
| **Location** | Contact page form |
| **Impact** | Users may abandon the form if labels are unclear. "Project brief" may not be understood. "Please complete all mandatory fields" is harder than "Please fill in the required fields." |
| **Recommended Fix** | Use plain-language labels: "Your email address," "Tell us about your project," "Your phone number." Mark required fields clearly. Use simple error messages: "Please enter your email" not "Invalid input format for contact field." |
| **WCAG** | **3.3.2 Labels or Instructions (Level A)** — Labels or instructions provided. **3.3.3 Error Suggestion (Level AA)** — Suggestions for correction. |

---

### Low

#### 12. Culturally Specific References

| Field | Detail |
|-------|--------|
| **Description** | References to "Silicon Valley," American business practices, or region-specific expressions may not resonate with international audiences. |
| **Location** | About page, blog, marketing copy |
| **Impact** | Non-native speakers from outside the US may not understand context. Reduces relatability. |
| **Recommended Fix** | Explain or avoid culturally specific references. If "Chicago-based" or "US-based" is relevant, state it plainly. Avoid assuming familiarity with American business culture. |
| **WCAG** | **3.1.5 Reading Level (Level AAA)** — Supplemental content for advanced reading level. |

---

#### 13. No Multilingual Option for Key Pages

| Field | Detail |
|-------|--------|
| **Description** | Key pages (About, Services, Contact) are not available in other languages (e.g., Spanish, Portuguese) despite serving international clients. |
| **Location** | Site-wide |
| **Impact** | Non-native English speakers have no alternative. Increases barrier for international prospects. |
| **Recommended Fix** | If the site serves international audiences, consider offering key pages in Spanish, Portuguese, or other relevant languages. At minimum, ensure English content is as plain and accessible as possible. |
| **WCAG** | **3.1.2 Language of Parts (Level AA)** — Language of each passage can be programmatically determined. Multilingual content supports diverse audiences. |

---

## WCAG References (Especially 3.1.x)

| Guideline | Level | Relevance |
|-----------|-------|-----------|
| **3.1.1 Language of Page** | A | Ensure page language is set (e.g., `lang="en"`). |
| **3.1.2 Language of Parts** | AA | If content in other languages exists, mark it correctly. |
| **3.1.3 Unusual Words** | AAA | Provide mechanism for definitions of jargon, idioms, unusual terms. |
| **3.1.4 Abbreviations** | AAA | Expand acronyms (ROI, MVP, UAT) on first use or provide mechanism. |
| **3.1.5 Reading Level** | AAA | When text exceeds lower secondary level, provide supplemental or simplified content. |
| **2.4.6 Headings and Labels** | AA | Use clear, descriptive headings. |
| **3.2.4 Consistent Identification** | AA | Use consistent labels across pages. |
| **3.3.2 Labels or Instructions** | A | Clear form labels and instructions. |

*Note: 3.1.3, 3.1.4, and 3.1.5 are Level AAA but are highly relevant for non-native speakers and international audiences.*

---

## Priority Recommendations

### Phase 1 (Critical — Address First)

1. **Replace or define jargon** — Use plain-language equivalents for "bespoke," "agentic," "seamless handoff," "discovery process," "operational efficiency." Add inline definitions or glossary.
2. **Replace idioms with literal language** — "Harness the power" → "Use"; "move the needle" → "make a real difference." Audit all marketing copy for idiomatic expressions.
3. **Expand acronyms on first use** — ROI (Return on Investment), MVP (Minimum Viable Product), UAT (User Acceptance Testing). Use full form first, then acronym.
4. **Add plain-language summary** — One to two sentences at top of homepage and About: "We build websites and mobile apps for businesses. We help you use AI. We are in Chicago."
5. **Reorganize Contact page** — Put phone, email, address, and form first. Move testimonials to bottom or separate page.

### Phase 2 (High — Next)

6. **Simplify sentence structure** — Break long sentences into 2–3 shorter ones. Use active voice. Aim for 15–20 words per sentence.
7. **Use concrete over abstract language** — "Drive operational efficiency" → "Help you work faster and save money." Add specific examples.
8. **Edit or relocate testimonials** — Simplify testimonial language or move to dedicated page. Ensure Contact page prioritizes contact information.

### Phase 3 (Medium — Follow-Up)

9. **Standardize terminology** — Use "Contact," "About," "Services" consistently. Avoid "Get in Touch," "Reach Out" unless used site-wide.
10. **Add glossary or "Simple summary" option** — Glossary for key terms. Consider "Read in simple English" toggle for key pages.
11. **Improve form labels and error messages** — Plain-language labels. Simple, actionable error messages.

### Phase 4 (Low — Ongoing)

12. **Review culturally specific references** — Explain or avoid US-specific business culture references.
13. **Consider multilingual option** — If serving international audiences, offer key pages in Spanish, Portuguese, or other languages.

---

*This report is based on accessibility testing performed from the perspective of the non-native English speaker persona (Maria Santos, B1/B2 CEFR) and aligns with WCAG 2.1 guidelines, with emphasis on Guideline 3.1 (Readable). Implementation should be validated with user testing involving intermediate English speakers.*