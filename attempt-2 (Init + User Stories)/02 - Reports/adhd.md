# ADHD Accessibility Technical Report: LaunchPad Lab

**Website:** https://launchpadlab.com/  
**Persona:** Jordan Rivera (ADHD, Combined Type)  
**Report Date:** February 16, 2025  
**Testing Method:** Persona-based accessibility evaluation

---

## Executive Summary

LaunchPad Lab's website presents significant usability barriers for users with ADHD. The persona (Jordan Rivera) successfully completed the core tasks—finding what the company does and how to contact them—but experienced notable cognitive overload, frustration, and inefficiency. Key findings include:

- **Contact information is buried** and requires navigation to a separate page plus scrolling past testimonials
- **Visual clutter** (logo carousels, multiple CTAs, award badges) competes for attention and creates decision paralysis
- **No skip links** or quick navigation to key sections (main content, contact)
- **Lengthy paragraphs and jargon** make content difficult to scan
- **Testimonials precede the contact form** on the Contact page, delaying access to primary actions
- **Motion and animations** may not respect `prefers-reduced-motion`, causing distraction

The site would benefit from structural changes that reduce cognitive load, surface primary information prominently, and support users who need to complete tasks quickly.

---

## Accessibility Issues

### Critical

#### C1. Contact Information Not Visible in Header or Above the Fold

| Field | Details |
|-------|---------|
| **Description** | Phone number and email are not displayed in the header or immediately visible on the homepage. Users must navigate to the Contact page and scroll to find contact details. |
| **Location** | Homepage header, Contact page (above the fold) |
| **Impact on Persona** | Jordan expects to find contact info within 30 seconds. Having to click through to Contact and scroll past testimonials creates frustration and increases abandonment risk. Users with ADHD may give up before reaching the goal. |
| **Recommended Fix** | Add phone number and/or email to the header so they are always visible. Alternatively, add a prominent contact block in the homepage footer or above the fold. Ensure contact info is visible without scrolling on the Contact page. |
| **WCAG** | None directly; relates to UX best practice for users with cognitive disabilities (WCAG 2.1 Understanding: Cognitive Accessibility - Findable). |

---

#### C2. Contact Form Preceded by Testimonials on Contact Page

| Field | Details |
|-------|---------|
| **Description** | The Contact page displays a large testimonials section before the contact form. Users must scroll past multiple long quotes to reach the form or contact details. |
| **Location** | https://launchpadlab.com/contact/ |
| **Impact on Persona** | Jordan's attention is pulled by testimonials. Long-form content before the primary action increases cognitive load and the likelihood of abandonment. Users who want to contact quickly may scroll past the form or leave. |
| **Recommended Fix** | Move the contact form and/or contact details (phone, email) to the top of the Contact page. Place testimonials below the form or on a separate section. Consider a "Contact" or "Get in Touch" heading as the first visible content. |
| **WCAG** | None directly; relates to 2.4.4 Link Purpose (In Context) and general cognitive accessibility principles. |

---

### High

#### H1. No Skip Links

| Field | Details |
|-------|---------|
| **Description** | No "Skip to main content" or "Skip to contact" links are present at the top of the page. Users must scroll through all content to reach key sections. |
| **Location** | All pages (homepage, About, Contact, Services, Work) |
| **Impact on Persona** | Jordan prefers jumping directly to sections. Long pages require excessive scrolling, increasing cognitive load and the risk of losing place or abandoning. Skip links would allow quick navigation to Contact or main content. |
| **Recommended Fix** | Add a "Skip to main content" link as the first focusable element. Consider adding "Skip to contact" or "Skip to footer" on long pages. Ensure links are visible on keyboard focus (not hidden). |
| **WCAG** | **2.4.1 Bypass Blocks (Level A)** — A mechanism must be available to bypass blocks of content that are repeated on multiple pages. |

---

#### H2. Multiple Competing CTAs Per Viewport

| Field | Details |
|-------|---------|
| **Description** | Multiple call-to-action buttons (e.g., "Learn More," "Get Started," "See Our Work") appear in the same viewport with no clear primary hierarchy. |
| **Location** | Homepage, Services page |
| **Impact on Persona** | Jordan experiences decision paralysis when faced with 5+ similar choices. Without a clear primary action, users may hesitate, click impulsively, or avoid choosing. |
| **Recommended Fix** | Limit to 1–2 primary CTAs per viewport. Use visual hierarchy (size, color, placement) to make the primary action (e.g., "Contact Us") dominant. Move secondary actions to subpages or less prominent positions. |
| **WCAG** | None directly; relates to cognitive accessibility (WCAG 2.1 Understanding: Cognitive Accessibility - Clear Purpose). |

---

#### H3. Dense Paragraphs and Lack of Scannable Structure

| Field | Details |
|-------|---------|
| **Description** | Some sections use paragraphs of 4+ lines without bullet points or short summaries. Jargon terms (e.g., "agentic AI," "bespoke") appear without plain-language alternatives. |
| **Location** | Homepage, About, Services, Contact (testimonials) |
| **Impact on Persona** | Jordan skips paragraphs over 3–4 lines. Dense text blocks feel like walls. Jargon requires extra processing. Content is not effectively communicated to users who scan. |
| **Recommended Fix** | Break paragraphs into 2–3 sentences maximum. Use bullet points for lists of features, benefits, or process steps. Add short TL;DR summaries at the top of dense sections. Replace or explain jargon with plain language. |
| **WCAG** | **3.1.5 Reading Level (Level AAA)** — When text requires reading ability more advanced than lower secondary education, provide a simplified version. **2.1 Understanding: Cognitive Accessibility** — Use clear, simple language. |

---

### Medium

#### M1. Excessive Visual Clutter (Logo Carousels, Award Badges)

| Field | Details |
|-------|---------|
| **Description** | Homepage displays many client logos and 7+ award badges in a single view. These elements compete for attention with the primary value proposition. |
| **Location** | Homepage |
| **Impact on Persona** | Jordan's attention is pulled by logos and badges. Visual noise increases cognitive load and makes it harder to focus on "What does this company do?" |
| **Recommended Fix** | Reduce logo carousel to 4–6 visible logos at a time, or move to a dedicated Clients page. Display 2–3 key awards; move the rest to an Awards/Recognition page. Increase white space between sections. |
| **WCAG** | None directly; relates to cognitive accessibility (Reduce Distractions). |

---

#### M2. Motion and Animations May Not Respect prefers-reduced-motion

| Field | Details |
|-------|---------|
| **Description** | The site uses animations, scroll effects, and possibly auto-playing carousels. It is unclear whether animations are disabled or reduced when the user has `prefers-reduced-motion: reduce` set in their system. |
| **Location** | Homepage, Services, possibly other pages |
| **Impact on Persona** | Jordan is sensitive to motion. Animations and scroll effects can hijack attention and make it harder to focus on static content. Users with ADHD may find motion distracting or uncomfortable. |
| **Recommended Fix** | Implement `@media (prefers-reduced-motion: reduce)` to disable or minimize animations, transitions, and scroll effects. Ensure carousels do not auto-play, or provide manual controls and a pause option. |
| **WCAG** | **2.3.3 Animation from Interactions (Level AAA)** — Motion from interactions can be disabled. **2.2.2 Pause, Stop, Hide (Level A)** — For auto-updating content, provide a mechanism to pause, stop, or hide. |

---

#### M3. Contact Form Complexity

| Field | Details |
|-------|---------|
| **Description** | The contact form includes multiple fields (name, email, company, dropdown, message). Required fields may feel excessive for users who want to reach out quickly. |
| **Location** | https://launchpadlab.com/contact/ |
| **Impact on Persona** | Jordan prefers fewer fields. Each additional field increases the likelihood of abandonment. Forms with many required fields feel like obstacles. |
| **Recommended Fix** | Reduce required fields to 3–5 (e.g., name, email, message). Make company and dropdown optional or move to a second step. Ensure phone and email are prominent as alternatives to the form. |
| **WCAG** | None directly; relates to cognitive accessibility (Minimize Cognitive Load). |

---

#### M4. No Single Clear Value Proposition Above the Fold

| Field | Details |
|-------|---------|
| **Description** | The homepage does not present a single, prominent headline that immediately answers "What does this company do?" in plain language. |
| **Location** | Homepage hero section |
| **Impact on Persona** | Jordan wants to answer "What do you do?" within 15 seconds. Without a clear value proposition, users must scroll or click to find the answer, increasing cognitive load and time on task. |
| **Recommended Fix** | Add a prominent H1 at the top: e.g., "We build custom AI software and digital products for businesses." Keep it to one sentence. Use plain language. |
| **WCAG** | None directly; relates to cognitive accessibility (Clear Purpose). |

---

### Low

#### L1. No Breadcrumbs on Inner Pages

| Field | Details |
|-------|---------|
| **Description** | Inner pages (About, Services, Contact, Work) do not display breadcrumbs to help users understand their location in the site hierarchy. |
| **Location** | About, Services, Contact, Work pages |
| **Impact on Persona** | Jordan may lose track of location when navigating. Breadcrumbs help reorient after distraction or tab switching. |
| **Recommended Fix** | Add breadcrumbs (e.g., Home > Contact) on inner pages. Ensure they are keyboard accessible and semantically correct. |
| **WCAG** | None directly; supports 2.4.8 Location (Level AAA). |

---

#### L2. No Progress Indicator for Long Pages

| Field | Details |
|-------|---------|
| **Description** | Long pages (e.g., homepage) do not indicate how much content remains or which section the user is viewing. |
| **Location** | Homepage |
| **Impact on Persona** | Jordan may feel overwhelmed by long pages without knowing how far they are from the end. A progress indicator or sticky table of contents could reduce anxiety. |
| **Recommended Fix** | Consider a scroll progress indicator or sticky table of contents linking to main sections (Services, Case Studies, Contact). |
| **WCAG** | None directly; supports cognitive accessibility. |

---

## WCAG Guidelines Referenced

| Guideline | Level | Relevance |
|-----------|-------|-----------|
| 2.4.1 Bypass Blocks | A | Skip links required |
| 2.2.2 Pause, Stop, Hide | A | Auto-playing content should be pausable |
| 2.3.3 Animation from Interactions | AAA | Motion should be reducible |
| 3.1.5 Reading Level | AAA | Plain language for complex content |
| 2.4.8 Location | AAA | Breadcrumbs support orientation |

---

## Priority Recommendations

### Priority 1 (Critical — Address First)

1. **Surface contact info in header** — Add phone and/or email to the header so they are always visible. Alternatively, ensure contact info is above the fold on the Contact page.
2. **Restructure Contact page** — Move contact form and contact details to the top. Place testimonials below the form.

### Priority 2 (High — Address Soon)

3. **Add skip links** — Implement "Skip to main content" and optionally "Skip to contact" as the first focusable elements.
4. **Reduce CTAs per viewport** — Limit to 1–2 primary CTAs per viewport. Make "Contact Us" the dominant action.
5. **Improve scannability** — Shorten paragraphs, add bullet points, use plain language. Add a clear value proposition at the top of the homepage.

### Priority 3 (Medium — Address in Next Iteration)

6. **Reduce visual clutter** — Consolidate logos and awards. Increase white space.
7. **Respect prefers-reduced-motion** — Disable or minimize animations when the user has reduced motion enabled.
8. **Simplify contact form** — Reduce required fields. Offer phone and email prominently.

### Priority 4 (Low — Nice to Have)

9. **Add breadcrumbs** — On inner pages for orientation.
10. **Add progress indicator** — For long pages (homepage).

---

## Conclusion

LaunchPad Lab's website presents significant barriers for users with ADHD. The most critical issues are the burial of contact information and the placement of testimonials before the contact form. Implementing the Priority 1 and 2 recommendations would substantially improve the experience for Jordan and similar users, enabling them to complete core tasks (find what the company does, contact them) quickly and with minimal cognitive load.
