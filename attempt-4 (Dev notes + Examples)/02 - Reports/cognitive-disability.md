# Accessibility Report: Cognitive Disability Persona

**Persona:** Sam Rivera — 28-year-old with cognitive disability affecting reading comprehension, memory, and complex decision-making  
**Website:** https://launchpadlab.com/  
**Date:** February 16, 2026  
**Pages Evaluated:** Homepage, Contact, About, Services

---

## Summary

The LaunchPad Lab website presents significant barriers for users with cognitive disabilities. The primary issues are pervasive use of jargon and complex language without plain-language alternatives, a JavaScript-dependent contact form with no fallback, inconsistent calls-to-action, and unlabeled interactive controls. While the site has a consistent navigation structure and footer across pages, the content itself is largely inaccessible to users who need plain language and simple, predictable interactions.

**Goals Achieved:**
- Find what LaunchPad Lab does: **Partially** — could not find a plain-language explanation
- Find how to contact them: **Partially** — form was inaccessible; phone/email found in footer

---

## Issues

### Issue 1: Pervasive Use of Jargon and Complex Language Without Plain-Language Alternatives

**Pages Affected:** All pages (Homepage, About, Services, Contact)  
**Severity:** Critical  
**WCAG Criteria:**
- 3.1.5 Reading Level (AAA) — Content requires reading ability more advanced than the lower secondary education level, with no simplified version available
- 3.1.3 Unusual Words (AAA) — Specialized terminology used without definitions or explanations

**Description:**  
Across the entire site, content relies heavily on industry jargon, marketing buzzwords, and technical terminology without providing plain-language alternatives, definitions, or glossary explanations. Specific examples include:

| Page | Text | Problematic Terms |
|------|------|-------------------|
| Homepage (H1) | "AI Innovation. Digital Solutions. Results that Matter." | "AI Innovation," "Digital Solutions" — abstract, undefined |
| Homepage (hero paragraph) | "...harness the power of AI through tailored consulting and product development services...modernize operations, reduce costs, and unlock growth." | "harness," "tailored consulting," "product development services," "modernize operations," "unlock growth" |
| Homepage (section heading) | "AI-Powered Digital Solutions for the Modern Enterprise" | "Modern Enterprise" — unclear audience |
| Homepage (body text) | "...combine deep expertise in product design and development with cutting-edge AI consulting to solve critical business challenges." | "deep expertise," "cutting-edge," "AI consulting," "critical business challenges" |
| Homepage (service card) | "AI Automation & Agentic AI — Enabling an autonomous digital workforce" | "Agentic AI," "autonomous digital workforce" |
| Homepage (service card) | "Web Application Development — Bespoke, redefining experiences" | "Bespoke" |
| Homepage (service card) | "Product Strategy & Design — Agile, cross-functional expertise" | "Agile," "cross-functional" |
| Homepage (tab label) | "Scalable Solutions," "Expansive Resources" | Abstract business jargon |
| Nav mega menu | "Our cross-functional teams have the skills and experience to support the full digital product lifecycle, using proven methods to deliver more better and faster with AI at the core." | "cross-functional teams," "full digital product lifecycle," "proven methods" |
| Services page | "Discovery Space Navigator" (tool name) | Opaque branding that doesn't convey purpose |
| About page | "Holistic Capability," "On the Cutting Edge" | Marketing slogans without explanation |
| About page | Job titles: "Principal Software Architect II," "Co Founder & CTO" | Unexplained technical titles |

**Recommended Fix:**
- Provide a plain-language summary at the top of each page (e.g., "We are a company that builds websites, phone apps, and computer tools for businesses")
- Add a glossary or inline definitions for technical terms on first use
- Use short sentences (under 20 words) and common vocabulary wherever possible
- Supplement marketing language with concrete, everyday descriptions
- Consider offering a "Simple Language" toggle or alternative version of key pages

**Impact on User:**  
Sam could not determine what the company does in terms he could explain to others. The jargon created a feeling of exclusion and confusion, likely causing site abandonment.

---

### Issue 2: Contact Form Requires JavaScript with No Fallback

**Pages Affected:** Contact page (`/contact`), Homepage (bottom section), About page (bottom section), Services page (bottom section)  
**Element:** Embedded form (Ninja Forms plugin)  
**Severity:** Critical  
**WCAG Criteria:**
- 4.1.1 Parsing (A) — Content must be accessible regardless of technology constraints
- 1.3.1 Info and Relationships (A) — Form structure is entirely absent without JavaScript
- 3.3.2 Labels or Instructions (A) — No form labels visible to provide guidance
- WCAG General — Progressive enhancement / graceful degradation

**Description:**  
The primary contact form on the contact page (and repeated on the homepage, about page, and services page) is rendered entirely by JavaScript (Ninja Forms plugin). When JavaScript is unavailable, blocked, or fails to load, the form is replaced with only the text: **"Notice: JavaScript is required for this content."**

This message is not actionable — it does not explain what JavaScript is, how to enable it, or provide an alternative contact method in its place. The form has zero labels, zero inputs, and zero structure visible in the non-JS state. Sam, who uses a simple browser configuration, may encounter this as a blank section or a confusing error message.

**Recommended Fix:**
- Provide a `<noscript>` fallback that includes the company email (contact@launchpadlab.com), phone number ((312) 888-9651), and mailing address directly within the form area
- Alternatively, provide a static HTML form that works without JavaScript
- At minimum, replace the generic JavaScript notice with a human-readable message: "If this form isn't loading, you can reach us by phone at (312) 888-9651 or email at contact@launchpadlab.com"

**Impact on User:**  
Sam's primary goal of contacting the company was blocked by the form's failure to render. He was only able to find contact details by scrolling to the very bottom of the page. Many users with cognitive disabilities would not persist to find the footer contact information.

---

### Issue 3: Hamburger Menu Icon Has No Visible Text Label

**Pages Affected:** All pages (mobile/responsive viewport)  
**Element:** `<button aria-label="Toggle Menu" class="mega-toggle-animated mega-toggle-animated-slider">`  
**Severity:** Major  
**WCAG Criteria:**
- 3.3.2 Labels or Instructions (A) — Visible label is absent
- 1.3.1 Info and Relationships (A) — The button's purpose is communicated only through `aria-label`, not visible text

**Description:**  
On mobile viewports (below 1069px breakpoint), the main navigation collapses into a hamburger icon button (`<div id="burgerBtn">` / toggle button). The button has an `aria-label="Toggle Menu"` which is helpful for screen readers, but there is no visible text label such as "Menu" displayed alongside or beneath the icon. The icon consists of animated `<span>` elements forming three horizontal bars — a convention that is not universally understood, especially by users with cognitive disabilities.

Additionally, `<div id="burgerBtn">` appears to be a separate visual element from the actual `<button>` with the aria-label, which may cause confusion about which element is interactive.

**Recommended Fix:**
- Add a visible text label "Menu" adjacent to or below the hamburger icon
- Ensure the clickable/tappable area encompasses both the icon and the label
- Consider keeping the full navigation visible at all viewport sizes, or providing a simplified navigation alternative

**Impact on User:**  
Sam may not recognize the hamburger icon as a menu control. Without a visible "Menu" label, he could be unable to access the site's navigation on mobile devices, effectively locking him out of the site's structure.

---

### Issue 4: Inconsistent Calls-to-Action Across Pages

**Pages Affected:** Homepage, Contact, About, Services  
**Severity:** Major  
**WCAG Criteria:**
- 3.2.4 Consistent Identification (AA) — Components with the same functionality are not identified consistently

**Description:**  
The calls-to-action (CTAs) that lead to contacting the company use different phrasing on each page and even within the same page:

| Location | CTA Text |
|----------|----------|
| Homepage hero | "Connect with an Expert" |
| Homepage bottom | "Let's Build Something Great." |
| Homepage bottom (sub-text) | "Get in touch with one of our experts today!" |
| Homepage heading | "Reach Out" |
| Contact page heading | "Ready to Build Something Great?" |
| Contact page sub-heading | "Partner with us to develop technology to grow your business." |
| Contact page bottom section | "Let's Connect" |
| About page bottom | "Ready to Build Something Great?" |
| About page sub-heading | "Partner with us to develop technology to grow your business." |
| Services page bottom | "Let's Build Something Great." |
| Footer | "Let's Get Social" (ambiguous — refers to social media, not contact) |

Users with cognitive disabilities rely on consistent terminology to understand that different links or buttons lead to the same outcome. When phrases change ("Reach Out" vs. "Connect with an Expert" vs. "Let's Build Something Great"), Sam cannot be sure they all lead to the contact form.

**Recommended Fix:**
- Standardize CTA text to one or two clear phrases (e.g., "Contact Us" and "Call Us") and use them consistently across all pages
- Avoid creative/marketing-driven CTA language when the function is identical
- Ensure each CTA clearly communicates the outcome (e.g., "Contact Us — Fill out a form or call us")

**Impact on User:**  
Sam felt uncertain about whether each CTA would take him to the same place. The inconsistency caused confusion and hesitation, slowing down task completion and increasing cognitive load.

---

### Issue 5: Complex Mega Menu Dropdowns with Dense Content

**Pages Affected:** All pages (global navigation)  
**Element:** `#mega-menu-wrap-menu-1` (Max Mega Menu)  
**Severity:** Major  
**WCAG Criteria:**
- 3.2.3 Consistent Navigation (AA) — Navigation presentation is consistent but overly complex
- 2.4.8 Location (AAA) — Users with cognitive disabilities may lose track of their position in the mega menu
- 3.1.5 Reading Level (AAA) — Dropdown descriptions use complex language

**Description:**  
The "Services" and "Industries" navigation items expand into large mega menu dropdowns containing:
- 6 service sub-items with icons and text labels
- A paragraph description using complex jargon ("cross-functional teams," "full digital product lifecycle")
- An "Explore all Services" link plus a "View Services" link (two links for the same purpose)
- 9 industry sub-items with icons and text labels
- A paragraph description with complex language

The mega menu triggered on hover intent (with a 300ms timeout and 100ms interval), which can be unpredictable. There are also duplicate entry points — "Explore all Services" and "View Services" appear to go to the same destination but use different wording.

The grammar error in the Services dropdown description ("deliver more better and faster") adds further confusion for a user already struggling with the language.

**Recommended Fix:**
- Simplify dropdown content to just the link items — remove paragraph descriptions from the dropdowns
- Eliminate duplicate links ("Explore all Services" vs. "View Services" — pick one)
- Fix the grammar error ("deliver more better" → "deliver better and faster")
- Provide a simpler navigation alternative or reduce the number of items per dropdown
- Ensure dropdowns work on click (not just hover) for predictability

**Impact on User:**  
The mega menu overwhelmed Sam with too many options, complex descriptions, and duplicate links. He struggled to parse the dropdown content and was unsure which link to click.

---

### Issue 6: Duplicate "Learn More" Links on Service Cards

**Pages Affected:** Homepage  
**Element:** Service cards in the "Make AI Your Competitive Advantage" section  
**Severity:** Major  
**WCAG Criteria:**
- 2.4.4 Link Purpose (In Context) (A) — Multiple links with identical text ("Learn More") point to different destinations without sufficient context
- 2.4.9 Link Purpose (Link Only) (AAA) — "Learn More" is ambiguous out of context

**Description:**  
In the services section on the homepage, each of the six service cards contains two "Learn More" links. The visible text for all 12 links is identical: "Learn More." For a user with cognitive disability:
- It is unclear whether the two "Learn More" links on the same card go to the same page or different pages
- All 12 links look identical, making it impossible to distinguish which service each link corresponds to without reading the card context

The links do not have distinguishing `aria-label` attributes to clarify their destinations.

**Recommended Fix:**
- Remove duplicate links — each card should have only one link
- Use descriptive link text instead of generic "Learn More" (e.g., "Learn about Web App Development," "Learn about AI Automation")
- If "Learn More" must be used, add `aria-label` attributes with the full context (e.g., `aria-label="Learn more about AI Automation"`)

**Impact on User:**  
Sam was confused by the duplicate links and could not tell them apart. He hesitated to click because he wasn't sure what he'd get.

---

### Issue 7: Fade-Up Animations on Scroll

**Pages Affected:** Homepage (7 elements use `data-aos="fade-up"`)  
**Severity:** Minor  
**WCAG Criteria:**
- 2.3.3 Animation from Interactions (AAA) — Motion animation triggered by interaction (scrolling) can be disorienting
- 2.2.2 Pause, Stop, Hide (A) — No mechanism to pause or disable animations

**Description:**  
Seven elements on the homepage use AOS (Animate On Scroll) with a `fade-up` animation effect. Content appears by sliding upward and fading in as the user scrolls down. There is no user control to disable these animations, and the site does not respect the `prefers-reduced-motion` media query.

For users with cognitive disabilities, content that appears dynamically can be disorienting — it may feel like the page is still loading, or the user may think they've missed content that hasn't animated in yet.

**Recommended Fix:**
- Respect the `prefers-reduced-motion: reduce` CSS media query to disable animations for users who have set this preference in their OS
- Provide a visible toggle to turn off animations
- Reduce or eliminate non-essential animations, especially on key content sections

**Impact on User:**  
Sam found the fade-in animations disorienting and was unsure if the page was fully loaded. This added unnecessary cognitive load.

---

### Issue 8: Social Media Icons in Footer Have Empty Alt Text

**Pages Affected:** All pages (global footer)  
**Elements:** Facebook, Instagram, and LinkedIn icon images  
**Severity:** Minor  
**WCAG Criteria:**
- 1.1.1 Non-text Content (A) — Images used as part of links should have meaningful alt text describing the link destination

**Description:**  
The footer social media links contain icon images (`<img>`) with empty `alt=""` attributes:
```html
<a href="https://www.facebook.com/LaunchPadLab"><img src="...facebook.svg" alt=""> Facebook</a>
<a href="https://www.instagram.com/launchpadlab/"><img src="...instagram.svg" alt=""> Instagram</a>
<a href="https://www.linkedin.com/company/launchpad-lab"><img src="...linkedin.svg" alt=""> LinkedIn</a>
```

While the visible text "Facebook," "Instagram," and "LinkedIn" is present next to each icon (which is a positive finding), the empty `alt` attributes on the images are technically correct since the text provides the label. However, the icons are presented as decorative without `aria-hidden="true"`, which may cause screen readers to announce them as unlabeled images.

**Note:** This is a minor issue because the visible text labels *are* present, which actually works well for Sam. The social links are one of the better-labeled elements on the site.

**Recommended Fix:**
- Add `aria-hidden="true"` and `role="presentation"` to the decorative icon images, or
- Provide meaningful alt text (e.g., `alt="Facebook icon"`)

**Impact on User:**  
Minimal impact for Sam specifically, since visible text labels are present. This is primarily a screen reader concern.

---

### Issue 9: "Notice: JavaScript is required for this content" — Unhelpful Error Message

**Pages Affected:** Contact page, Homepage (form section), About page (form section), Services page (form section)  
**Severity:** Major  
**WCAG Criteria:**
- 3.3.1 Error Identification (A) — The error is not described in a way the user can understand
- 3.3.3 Error Suggestion (AA) — No suggestion is provided for how to resolve the issue

**Description:**  
When the Ninja Forms contact form fails to load (due to JavaScript being unavailable, blocked by browser settings, or failing to execute), the only message displayed is: **"Notice: JavaScript is required for this content."**

This message:
- Uses technical language ("JavaScript") that a user with cognitive disability will not understand
- Does not explain what action to take
- Does not provide an alternative way to contact the company
- Appears in multiple locations across the site (homepage, contact, about, services pages)

**Recommended Fix:**
- Replace the technical notice with a user-friendly message: "Having trouble seeing the form? You can reach us by phone at (312) 888-9651 or email at contact@launchpadlab.com"
- Provide direct contact information immediately adjacent to or inside the `<noscript>` block
- Include a link to the contact page with the phone/email details

**Impact on User:**  
Sam did not know what JavaScript is and could not act on this message. He was blocked from using the contact form and had to search the page to find alternative contact methods.

---

### Issue 10: No Plain-Language Summary or "What We Do" Section

**Pages Affected:** All pages  
**Severity:** Major  
**WCAG Criteria:**
- 3.1.5 Reading Level (AAA) — Content is not available in a simplified form
- 2.4.6 Headings and Labels (AA) — Headings use marketing language instead of descriptive labels

**Description:**  
Despite having an extensive homepage, about page, and services page, the site never provides a clear, simple, one-sentence explanation of what LaunchPad Lab does in everyday language. The closest attempt is the meta description (not visible on the page): "LaunchPad Lab is a digital product development consultancy that builds mission-critical digital solutions with AI at the center of all we do."

Even this sentence uses "consultancy," "mission-critical," and "digital solutions" — terms that are not accessible to users with lower reading comprehension.

A plain-language equivalent might be: "LaunchPad Lab is a company in Chicago that builds websites, phone apps, and computer tools for businesses. We also help businesses use AI (artificial intelligence) to work faster and save money."

**Recommended Fix:**
- Add a prominent, plain-language summary near the top of the homepage (above the fold)
- Use a maximum 8th-grade reading level for this summary
- Include concrete examples of what they build (e.g., "websites," "phone apps," "business tools")
- Consider adding a "What We Do in Simple Terms" section or page

**Impact on User:**  
Sam's primary goal — understanding what the company does — was not achievable through the content provided. He would need to rely on a helper or leave the site entirely.

---

### Issue 11: Grammar Error in Navigation Dropdown

**Pages Affected:** All pages (global navigation, Services dropdown)  
**Element:** Description text in the Services mega menu dropdown  
**Severity:** Minor  
**WCAG Criteria:**
- 3.1.5 Reading Level (AAA) — Grammar errors increase the difficulty of comprehension

**Description:**  
The Services dropdown contains the text: "Our cross-functional teams have the skills and experience to support the full digital product lifecycle, using proven methods to **deliver more better** and faster with AI at the core."

"Deliver more better" is grammatically incorrect and adds confusion for a user who is already struggling to parse complex language. The user may think they are misreading the sentence and re-read it multiple times.

**Recommended Fix:**
- Correct to "deliver better and faster" or "deliver more, better, and faster" (if "more" is intentional as a separate item)
- Simplify the entire sentence

**Impact on User:**  
Sam re-read this sentence multiple times trying to understand it, adding to his frustration and cognitive fatigue.

---

### Issue 12: Heading Hierarchy Issues

**Pages Affected:** Homepage  
**Severity:** Minor  
**WCAG Criteria:**
- 1.3.1 Info and Relationships (A) — Heading levels should form a logical outline
- 2.4.6 Headings and Labels (AA) — Headings should be descriptive

**Description:**  
On the homepage, the heading hierarchy has inconsistencies:
- H2 headings are used for statistics ("Years in Business," "Projects," "Clients") which are not section headings — they are data points styled as headings for visual emphasis
- This breaks the logical document outline and makes it harder for users who rely on headings to scan content

Additionally, many headings use marketing language rather than descriptive labels (e.g., "Ship Game-Changing Digital Products to Market Fast" vs. "What Problems We Solve").

**Recommended Fix:**
- Use appropriate heading levels that form a logical outline
- Do not use heading tags for statistical numbers — use styled `<p>` or `<div>` elements instead
- Use descriptive, plain-language headings that tell the user what the section contains

**Impact on User:**  
Sam found it harder to scan and understand the page structure due to headings that serve a visual purpose rather than a structural one.

---

## Summary Table

| # | Issue | Severity | WCAG | Page(s) |
|---|-------|----------|------|---------|
| 1 | Pervasive jargon/complex language | Critical | 3.1.5, 3.1.3 (AAA) | All |
| 2 | Contact form requires JavaScript, no fallback | Critical | 4.1.1, 1.3.1, 3.3.2 (A) | Contact, Home, About, Services |
| 3 | Hamburger menu has no visible text label | Major | 3.3.2, 1.3.1 (A) | All (mobile) |
| 4 | Inconsistent CTA text across pages | Major | 3.2.4 (AA) | All |
| 5 | Complex mega menu with dense content | Major | 3.2.3 (AA), 3.1.5 (AAA) | All |
| 6 | Duplicate "Learn More" links | Major | 2.4.4 (A), 2.4.9 (AAA) | Homepage |
| 7 | Scroll-triggered fade animations with no disable | Minor | 2.3.3 (AAA), 2.2.2 (A) | Homepage |
| 8 | Social media icons have empty alt text | Minor | 1.1.1 (A) | All (footer) |
| 9 | Unhelpful "JavaScript required" error message | Major | 3.3.1 (A), 3.3.3 (AA) | Contact, Home, About, Services |
| 10 | No plain-language summary of services | Major | 3.1.5 (AAA), 2.4.6 (AA) | All |
| 11 | Grammar error in nav dropdown | Minor | 3.1.5 (AAA) | All (nav) |
| 12 | Heading hierarchy issues | Minor | 1.3.1 (A), 2.4.6 (AA) | Homepage |

---

## Recommendations Priority

### Immediate (Critical)
1. Add a plain-language description of the company on the homepage
2. Provide a `<noscript>` fallback for the contact form with email/phone information
3. Replace or supplement jargon with plain-language alternatives on key pages

### Short-Term (Major)
4. Add visible "Menu" label to the hamburger button
5. Standardize CTA text across all pages
6. Simplify mega menu dropdown content and remove duplicates
7. De-duplicate "Learn More" links and add descriptive text
8. Replace the JavaScript error notice with a helpful, plain-language message with contact alternatives

### Long-Term (Minor)
9. Respect `prefers-reduced-motion` for all animations
10. Fix heading hierarchy to use semantic, descriptive headings
11. Correct the grammar error in the Services dropdown
12. Add `aria-hidden="true"` to decorative icon images
