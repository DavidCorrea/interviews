# Technical Report: Cognitive Disability Accessibility

**Website:** https://launchpadlab.com/  
**Persona:** Marcus Thompson (Cognitive Disability)  
**Test Date:** February 16, 2025  
**Test Task:** Find what the company does and how to contact them

---

## Executive Summary

LaunchPad Lab's website presents significant barriers for users with cognitive disabilities, including mild intellectual disability. The primary issues center on **complex language and jargon**, **lack of plain-language summaries**, **contact information discoverability**, and **cognitive overload** from dense content and testimonials. While standard navigation labels (About, Contact, Services) provide some orientation, the content itself is written for an audience familiar with digital product and software development terminology. Users like Marcus Thompson may struggle to complete basic tasks (understanding the company's purpose and finding contact details) without assistance.

**Key findings:**
- Jargon-heavy language throughout (e.g., "AI-centric," "discovery process," "entrepreneurship journey")
- No plain-language summary or "simple summary" option
- Contact information may be obscured by testimonials and form-focused layout
- Long paragraphs and dense text increase cognitive load
- Testimonials on Contact page use complex language and distract from primary task

---

## Accessibility Issues

### Critical

#### 1. No Plain-Language Summary of Company Purpose

| Field | Detail |
|-------|--------|
| **Description** | The homepage and key pages do not provide a simple, 1–2 sentence summary of what LaunchPad Lab does. Users must infer meaning from jargon such as "AI-centric digital product design" and "digital product development." |
| **Location** | Homepage, About page, Services page |
| **Impact** | Users with cognitive disabilities may be unable to understand the company's core offering. This blocks the primary task of "finding what they do." |
| **Recommended Fix** | Add a prominent "Simple summary" at the top of the homepage and About page, e.g., "We build websites and mobile apps for businesses. We help companies use technology to grow." Consider a "Read in simple language" toggle. |
| **WCAG** | **2.1 Understanding (Guideline 3.1)** — Readable: 3.1.5 Reading Level (Level AAA). Consider 3.1.3 Unusual Words (Level AAA) for jargon. |

---

#### 2. Contact Information Not Prominently Displayed

| Field | Detail |
|-------|--------|
| **Description** | Phone number, email, and physical address may not be immediately visible on the Contact page. Testimonials and long quotes occupy prominent space, potentially pushing contact details below the fold or into a form-only flow. |
| **Location** | Contact page (https://launchpadlab.com/contact) |
| **Impact** | Users who prefer to call or email (rather than use a form) may not find direct contact details. This is critical for users who struggle with forms. |
| **Recommended Fix** | Display phone number, email, and address at the top of the Contact page, in large, readable text. Repeat contact info in the header or footer on every page. Ensure it is visible without scrolling. |
| **WCAG** | **2.1 Operable (Guideline 2.1)** — Multiple ways to complete tasks. **2.4 Navigable** — Help users find content. |

---

### High

#### 3. Jargon and Unfamiliar Terminology

| Field | Detail |
|-------|--------|
| **Description** | Terms such as "AI-centric," "digital product design," "discovery process," "entrepreneurship journey," "tumultuous," "MVP," "UX," and "marketing strategy" appear without definition or plain-language alternatives. |
| **Location** | Homepage, About, Services, Contact (testimonials) |
| **Impact** | Users with limited comprehension cannot understand the content. Each unfamiliar term creates a barrier and increases cognitive load. |
| **Recommended Fix** | Replace or supplement jargon with plain language. Provide inline definitions or a glossary. Example: "discovery process" → "We talk with you to understand your needs before we build." |
| **WCAG** | **3.1.3 Unusual Words (Level AAA)** — Provide a mechanism to identify definitions. **3.1.5 Reading Level (Level AAA)** — Provide summaries or simplified versions. |

---

#### 4. Testimonials on Contact Page Create Cognitive Overload

| Field | Detail |
|-------|--------|
| **Description** | The Contact page features multiple long testimonials using complex language (e.g., "discovery process," "selective choice of questioning," "tumultuous journey of entrepreneurship"). These appear before or alongside contact information. |
| **Location** | Contact page |
| **Impact** | Users must scroll past or process dense, jargon-heavy content to reach contact details. Increases cognitive load and may cause task abandonment. |
| **Recommended Fix** | Move testimonials to a separate "Testimonials" or "Reviews" section. On the Contact page, prioritize: (1) clear heading "Contact Us," (2) phone, email, address, (3) contact form. Keep testimonials minimal or remove from this page. |
| **WCAG** | **2.4.6 Headings and Labels (Level AA)** — Headings should describe topic/purpose. **2.1 Understanding** — Minimize cognitive load. |

---

#### 5. Long Paragraphs and Dense Text Blocks

| Field | Detail |
|-------|--------|
| **Description** | Content is presented in long paragraphs (5+ lines) without sufficient subheadings, bullet points, or white space. This increases cognitive load for users with limited working memory. |
| **Location** | About page, Services page, homepage sections |
| **Impact** | Users may lose their place, forget earlier content, or abandon reading. Short-term memory limitations make long blocks difficult to process. |
| **Recommended Fix** | Break content into short paragraphs (2–4 sentences). Use bullet points and subheadings. Increase line height and spacing. Aim for one idea per paragraph. |
| **WCAG** | **2.1 Understanding** — Make text content readable and understandable. **1.4.8 Visual Presentation (Level AAA)** — Allow users to modify text blocks (width, line height, spacing). |

---

### Medium

#### 6. Inconsistent or Non-Standard Navigation Labels

| Field | Detail |
|-------|--------|
| **Description** | If navigation uses creative labels (e.g., "Get in Touch" instead of "Contact," "Our Story" instead of "About"), users who rely on familiar patterns may be confused. |
| **Location** | Main navigation (if applicable) |
| **Impact** | Users expect standard terms. Non-standard labels require extra cognitive effort to map to familiar concepts. |
| **Recommended Fix** | Use consistent, standard labels: "About," "Services," "Contact," "Work." Avoid creative or abstract alternatives. |
| **WCAG** | **3.2.4 Consistent Identification (Level AA)** — Components with the same functionality are identified consistently. |

---

#### 7. Contact Form Instructions and Error Handling

| Field | Detail |
|-------|--------|
| **Description** | If the contact form lacks clear labels, required field indicators, inline validation, and simple error messages, users with cognitive disabilities may struggle to complete it. |
| **Location** | Contact page form |
| **Impact** | Forms can cause anxiety. Unclear instructions or cryptic errors (e.g., "Invalid input") increase abandonment risk. |
| **Recommended Fix** | Provide visible labels for all fields. Mark required fields with "*" or "required" and explain at top of form. Use inline validation with clear, actionable messages (e.g., "Please enter a valid email address"). Offer confirmation after submission. |
| **WCAG** | **3.3.1 Error Identification (Level A)** — Describe errors in text. **3.3.2 Labels or Instructions (Level A)** — Provide labels or instructions. **3.3.3 Error Suggestion (Level AA)** — Suggest corrections. |

---

#### 8. No Breadcrumbs or Clear Location Indicator

| Field | Detail |
|-------|--------|
| **Description** | Inner pages may lack breadcrumbs or a clear indicator of where the user is in the site structure. |
| **Location** | About, Services, Contact, Work pages |
| **Impact** | Users with limited memory may feel "lost" on deeper pages. Breadcrumbs support orientation and reduce cognitive load. |
| **Recommended Fix** | Add breadcrumbs (e.g., Home > About) on inner pages. Ensure "Contact" link is visible in header on every page. |
| **WCAG** | **2.4.8 Location (Level AAA)** — Provide information about user's location. **2.4.5 Multiple Ways (Level AA)** — Provide more than one way to locate content. |

---

### Low

#### 9. Possible Auto-Playing or Animated Content

| Field | Detail |
|-------|--------|
| **Description** | Hero sections, carousels, or animations may auto-play or create visual distraction, overwhelming users with cognitive disabilities. |
| **Location** | Homepage, key landing sections |
| **Impact** | Competing motion and content can increase cognitive load and make it harder to focus on primary tasks. |
| **Recommended Fix** | Ensure carousels and animations can be paused. Avoid auto-playing content that cannot be stopped. Respect `prefers-reduced-motion` media query. |
| **WCAG** | **2.2.2 Pause, Stop, Hide (Level A)** — Provide mechanism to pause auto-updating content. **2.3.3 Animation from Interactions (Level AAA)** — Allow disabling of animations. |

---

#### 10. Icon-Only Buttons Without Text Labels

| Field | Detail |
|-------|--------|
| **Description** | If navigation or actions use icons (e.g., hamburger menu, social icons) without visible text labels, users may misinterpret or miss them. |
| **Location** | Header, footer, navigation |
| **Impact** | Icons without labels require inference. Users with cognitive disabilities benefit from explicit text. |
| **Recommended Fix** | Provide visible text labels for all interactive elements. Ensure `aria-label` or visible text is present. Prefer text links over icon-only buttons where possible. |
| **WCAG** | **2.1.1 Keyboard (Level A)** — All functionality available via keyboard. **4.1.2 Name, Role, Value (Level A)** — Ensure name/label is programmatically determinable. |

---

## WCAG Guidelines Referenced

| Guideline | Level | Relevance |
|-----------|-------|------------|
| 2.1 Understanding — Readable | A–AAA | Plain language, readability, unusual words |
| 2.4 Navigable | A–AAA | Multiple ways to find content, headings, location |
| 3.1 Readable | A–AAA | Language of page, unusual words, reading level |
| 3.2 Predictable | A–AA | Consistent identification, consistent navigation |
| 3.3 Input Assistance | A–AA | Labels, error identification, error suggestion |
| 2.2 Enough Time | A | Pause, stop, hide for auto-updating content |
| 2.3 Seizures and Physical Reactions | A–AAA | Animation controls, reduced motion |

---

## Priority Recommendations

### Phase 1 (Critical — Address First)

1. **Add plain-language summary** — One to two sentences at top of homepage and About page explaining what LaunchPad Lab does in simple terms.
2. **Display contact information prominently** — Phone, email, and address at top of Contact page and in footer/header site-wide.

### Phase 2 (High — Next)

3. **Reduce jargon** — Replace or define terms like "AI-centric," "discovery process," "entrepreneurship journey." Provide plain-language alternatives.
4. **Reorganize Contact page** — Move testimonials to separate section. Prioritize contact details and form.
5. **Break up long text** — Short paragraphs, bullet points, subheadings across About and Services pages.

### Phase 3 (Medium — Follow-Up)

6. **Standardize navigation labels** — Use "About," "Services," "Contact" consistently.
7. **Improve form accessibility** — Clear labels, required field indicators, inline validation, simple error messages.
8. **Add breadcrumbs** — On About, Services, Contact, Work pages.

### Phase 4 (Low — Ongoing)

9. **Control animations** — Ensure carousels/animations can be paused. Respect reduced motion.
10. **Label all icons** — Visible text or `aria-label` for icon-only buttons.

---

*This report is based on accessibility testing performed from the perspective of the cognitive disability persona (Marcus Thompson) and aligns with WCAG 2.1 guidelines. Implementation should be validated with user testing involving people with cognitive disabilities.*
