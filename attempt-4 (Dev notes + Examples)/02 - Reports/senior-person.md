# Accessibility Audit Report — Senior / Non-Tech-Savvy User Persona

**Persona:** Eleanor Morrison, 74, retired school administrator with age-related vision decline, reduced processing speed, unfamiliar with modern web patterns  
**Website:** https://launchpadlab.com/  
**Audit Date:** February 16, 2026  
**Evaluator Approach:** Manual heuristic evaluation from the perspective of a non-tech-savvy older adult using default browser settings, a mouse, no assistive technology, and no browser extensions.

---

## Executive Summary

LaunchPad Lab's website presents significant usability and accessibility barriers for older, non-tech-savvy users. The site relies heavily on marketing jargon instead of plain language, uses complex interactive UI patterns (mega dropdown menus, auto-scrolling carousels, scroll-triggered animations), and buries critical contact information below lengthy content and forms. While standard navigation labels like "Contact" and "About Us" are present in the top bar, the overall experience is overwhelming, jargon-laden, and structurally hostile to users who read methodically and expect conventional web layouts.

**Issues Found:** 18  
**Critical:** 4 | **Major:** 8 | **Minor:** 6

---

## Issue 1: Hero Section Uses Jargon Instead of Plain Language

**Page:** Homepage (`/`)  
**Element:** Hero heading — "AI Innovation. Digital Solutions. Results that Matter." and supporting paragraph mentioning "tailored consulting and product development services," "modernize operations, reduce costs, and unlock growth"  
**WCAG Criterion:** 3.1.5 Reading Level (AAA), and general usability best practice for cognitive accessibility  
**Severity:** Major

**Description:** The hero section, which is the first content a user encounters, uses abstract marketing language that does not plainly communicate what the company does. Terms like "AI Innovation," "digital solutions," and "tailored consulting" require domain expertise to interpret. Eleanor read the entire hero section twice and could not determine in simple terms what the company offers.

**Impact on This User:** Eleanor cannot achieve her first goal (understand what the company does) from the most prominent content on the page. She must scroll through large amounts of additional jargon-heavy content to piece together a basic understanding. This wastes her time and erodes her confidence in the site.

**Recommended Fix:** Add a plain-language summary immediately below or replacing the marketing headline. Example: "We are a Chicago-based company that designs and builds websites, mobile apps, and business software." Keep the marketing language if desired, but lead with clarity.

---

## Issue 2: Primary CTA Label "Connect with an Expert" Is Unconventional

**Page:** Homepage (`/`), Services page (`/services`)  
**Element:** Primary call-to-action button in hero section — `<a>Connect with an Expert</a>`  
**WCAG Criterion:** 3.2.4 Consistent Identification (AA), 2.4.6 Headings and Labels (AA)  
**Severity:** Major

**Description:** The main CTA button on the homepage and services page uses the label "Connect with an Expert" rather than a conventional label like "Contact Us." This marketing-oriented phrasing is inconsistent with user expectations. Eleanor hesitated at this button, unsure if it would take her to a contact page, a sales funnel, or a chat with a consultant. The label does not match the function (navigating to a contact form).

**Impact on This User:** Eleanor distrusts labels she doesn't immediately understand. She did not click this button because the wording felt like a sales commitment rather than a simple request for contact information. This directly prevents her from achieving her second goal (finding contact information) via the most prominent path the site offers.

**Recommended Fix:** Use a conventional label such as "Contact Us" for the primary CTA, or at minimum provide a secondary, clearly labeled "Contact Us" link of equal prominence. If "Connect with an Expert" is retained for marketing purposes, pair it with clarifying text (e.g., "Have a question? Contact us directly").

---

## Issue 3: Auto-Scrolling Logo Carousel Is Disorienting

**Page:** Homepage (`/`), About page (`/about`)  
**Element:** Client logo scroller (`.logos__scroller`) with CSS `animation: scroll` set to `linear infinite`  
**WCAG Criterion:** 2.2.2 Pause, Stop, Hide (A)  
**Severity:** Critical

**Description:** The client logo sections on the homepage and about page feature continuously auto-scrolling carousels that animate indefinitely. There is no visible pause, stop, or hide mechanism available to the user. The code does check `prefers-reduced-motion`, but Eleanor uses default browser settings and would not have this preference enabled, so the animation always runs.

The animation uses `will-change: transform` and `animation: scroll var(--_logo-scroll-duration, 20s) linear infinite`, meaning logos scroll perpetually across the viewport with no user control.

**Impact on This User:** The constant motion is distracting and disorienting. Eleanor tried to read the company logos but could not because they move continuously. This is a direct WCAG 2.2.2 Level A failure — auto-updating content that starts automatically, lasts more than 5 seconds, and has no mechanism to pause, stop, or hide it.

**Recommended Fix:** Add a visible pause/play button to the logo carousel. Alternatively, display the logos in a static grid layout. If animation is retained, ensure it pauses on hover/focus and provide a visible control to stop it. Also consider honoring `prefers-reduced-motion` by default, but do not rely on it as the sole mechanism since non-tech-savvy users will not have it configured.

---

## Issue 4: Mega Dropdown Navigation Menus Are Overwhelming and Fragile

**Page:** All pages (global navigation)  
**Element:** Max Mega Menu plugin — `#mega-menu-menu-1` with `data-event="hover_intent"`, specifically the Services and Industries dropdowns  
**WCAG Criterion:** 2.4.3 Focus Order (A), 2.4.7 Focus Visible (AA), 3.2.1 On Focus (A) — general usability for cognitive accessibility  
**Severity:** Major

**Description:** The Services and Industries navigation items trigger large mega-dropdown panels on hover intent. These panels contain 6–9 sub-items with icons, descriptive text, and CTA buttons. The panels:

- Appear and disappear based on mouse hover, with a 300ms hover-intent timeout (`data-hover-intent-timeout="300"`)
- Contain dense information (icons, labels, descriptions, and promotional CTAs)
- Disappear entirely if the mouse moves outside the dropdown boundary
- Present 6+ choices simultaneously in a layout that resembles a page unto itself

**Impact on This User:** Eleanor found the dropdowns overwhelming and fragile. She accidentally dismissed them by moving her mouse, and the density of information (AI Automation, Web App Development, Mobile App Development, Salesforce Development, Product Strategy & Design, Managed Services & Support — each with icons and subtitles) was too much to process in a transient popup. She could not comfortably browse the navigation without triggering unwanted panel appearances/disappearances.

**Recommended Fix:** Consider a simpler dropdown with just text labels (no icons, no promotional blocks, no CTAs within the dropdown). Ensure the dropdown remains visible long enough for slow mouse users to navigate. Add a click-to-open option as an alternative to hover. On the breakpoint collapse (1069px), ensure the mobile menu is clearly labeled and intuitive.

---

## Issue 5: Hamburger Menu on Tablet/Narrow Screens

**Page:** All pages (global navigation)  
**Element:** `#burgerBtn` div and `.mega-menu-toggle` with breakpoint at 1069px (`data-breakpoint="1069"`)  
**WCAG Criterion:** 3.2.3 Consistent Navigation (AA), general cognitive accessibility  
**Severity:** Major

**Description:** The navigation collapses into a hamburger menu (animated three-line toggle button) at screen widths below 1069px. This is a relatively high breakpoint — many laptops, especially older ones with lower resolutions, and all tablets will trigger this collapse. The hamburger button is an animated icon (`mega-toggle-animated-slider`) with an `aria-label="Toggle Menu"` but no visible text label.

**Impact on This User:** Eleanor does not recognize hamburger menus as navigation. If she accesses the site on a tablet, a smaller laptop, or with any window that is not maximized on a large screen, she would see no navigation at all — just a small icon with three lines. She would not know to click it. This would prevent her from finding the "Contact," "About Us," or any other page. The `aria-label` is helpful for screen reader users, but Eleanor does not use a screen reader.

**Recommended Fix:** Add a visible text label "Menu" next to the hamburger icon. Consider raising the breakpoint threshold so that the full navigation is visible on more devices, or use a simplified single-row navigation that doesn't require a mega dropdown pattern. Ensure the collapsed menu state is clearly identifiable with the word "Menu" visible.

---

## Issue 6: Scroll-Triggered Animations (AOS) Delay Content Visibility

**Page:** Homepage (`/`), all pages using `data-aos` attributes  
**Element:** Multiple elements with `data-aos="fade-up" data-aos-duration="200"` to `data-aos-duration="1000"`, including the hero text block and all service cards  
**WCAG Criterion:** 2.3.3 Animation from Interactions (AAA), general cognitive accessibility  
**Severity:** Major

**Description:** The site uses the AOS (Animate on Scroll) library to animate content into view as the user scrolls. Elements start invisible and fade/slide up when they enter the viewport. The hero text block has a 1000ms animation duration, and service cards each have 200ms durations.

**Impact on This User:** Eleanor reads methodically from top to bottom. When she scrolls to a new section, the content is not immediately visible — it fades in from below. This creates the impression that content is still loading or appearing unpredictably. She reported feeling disoriented and unsure whether she was "missing something." For a user with reduced processing speed, having content animate into position rather than being statically present adds unnecessary cognitive load.

**Recommended Fix:** Remove or significantly reduce scroll-triggered animations, or at minimum ensure they respect `prefers-reduced-motion`. Better yet, default to no animation and only enable it for users who have not set a reduced motion preference. For this user type, static content is always preferable to animated content.

---

## Issue 7: Contact Information Buried Below Form and Testimonials

**Page:** Contact page (`/contact`)  
**Element:** "Let's Connect" section containing email (contact@launchpadlab.com), phone ((312) 888-9651), and LinkedIn link — positioned below the contact form and five client testimonials  
**WCAG Criterion:** 2.4.6 Headings and Labels (AA), general usability best practice  
**Severity:** Critical

**Description:** The Contact page is structured as follows:
1. Heading: "Ready to Build Something Great?"
2. Contact form (First Name, Last Name, Company Email, Company, How Can We Help You?, reCAPTCHA, Submit)
3. Five client testimonial quotes
4. **"Let's Connect" section with email, phone, and LinkedIn** (below the fold)

The direct contact information (phone number and email) that Eleanor explicitly needs is buried at the bottom of the page, after a form she cannot meaningfully complete and testimonials she did not request. The phone number and email are not visible without significant scrolling.

**Impact on This User:** Eleanor strongly prefers phone and email over web forms. She had to scroll past the entire form and five testimonials to find (312) 888-9651 and contact@launchpadlab.com. She nearly abandoned the page before discovering this information. A user with less patience would have left without finding any direct contact method.

**Recommended Fix:** Place the phone number and email address prominently at the top of the Contact page, above or alongside the form. At minimum, add a visible "Prefer to call? (312) 888-9651" line directly below the page heading. The form should be presented as one option for contact, not the only apparent option.

---

## Issue 8: Contact Form Assumes Business Context

**Page:** Contact page (`/contact`), Services page (`/services`) embedded form  
**Element:** Ninja Forms contact form — fields: "Company Email" (required), "Company" (required)  
**WCAG Criterion:** 3.3.2 Labels or Instructions (A) — general usability  
**Severity:** Major

**Description:** The contact form requires "Company Email" and "Company" as mandatory fields. The label "Company Email" implies that a personal email address is not acceptable. The "Company" field is required, which excludes individuals, retirees, volunteers, or anyone not representing a business.

**Impact on This User:** Eleanor is retired and does not have a company email or a company name. These required fields create a barrier that prevents her from submitting the form even if she wanted to. The label "Company Email" made her feel the form was not intended for her, reinforcing the impression that the site caters only to corporate professionals.

**Recommended Fix:** Change "Company Email" to "Email" or "Email Address." Make the "Company" field optional, or add helper text: "If applicable." This removes barriers for individuals, small organization representatives, volunteers, or retirees.

---

## Issue 9: Contact Form Requires JavaScript

**Page:** Contact page (`/contact`), Services page (`/services`)  
**Element:** Ninja Forms — displays "Notice: JavaScript is required for this content" when JS is unavailable  
**WCAG Criterion:** 4.1.1 Parsing (A) — deprecated but relevant; Conformance Requirement 5 (Non-Interference)  
**Severity:** Minor

**Description:** The contact form is rendered entirely via JavaScript (Ninja Forms plugin). If JavaScript fails to load or is blocked, the user sees only the message "Notice: JavaScript is required for this content." There is no fallback contact method displayed in place of the form.

**Impact on This User:** While Eleanor likely has JavaScript enabled by default, older browsers, corporate firewalls, or loading errors could prevent the form from rendering. In such cases, she would see only the notice with no alternative way to reach the company — the phone number and email are further down the page. This is a minor risk but a real one for non-technical users who cannot troubleshoot JavaScript issues.

**Recommended Fix:** Add a fallback `<noscript>` block that displays the email address (contact@launchpadlab.com) and phone number ((312) 888-9651) when JavaScript is unavailable.

---

## Issue 10: Excessive Jargon Throughout All Pages

**Page:** Homepage (`/`), Services (`/services`), About (`/about`)  
**Element:** Body copy, headings, CTAs  
**WCAG Criterion:** 3.1.5 Reading Level (AAA), general cognitive accessibility best practice  
**Severity:** Major

**Description:** The following jargon terms appear throughout the site without explanation or plain-language alternatives:

| Term | Where Used |
|---|---|
| "Agentic AI" | Homepage services section, Services page |
| "Bespoke" | Homepage service cards ("Bespoke, redefining experiences") |
| "Cross-functional teams" | Homepage, Services page, About page (appears 5+ times) |
| "Digital product lifecycle" | Homepage, Services page nav dropdown |
| "Agile sprints" | Services page FAQ |
| "ROI" | Homepage ("Driving ROI with AI"), Services page |
| "CSAT" | Homepage ("boosts CSAT") |
| "UX/UI" | Services page, About page |
| "Discovery call" | Services page CTA ("Book a Discovery Call") |
| "Speed to market" | Homepage, Services page |
| "Nearshore" | Services page FAQ |
| "Heroku" | Services page FAQ |
| "Flow" | Services page FAQ (Salesforce Flow) |
| "Experience Cloud" | Services page FAQ |
| "Headless commerce" | Services page related blog posts |
| "Replatform" | Services page FAQ |

**Impact on This User:** Eleanor cannot parse this language. Each unfamiliar term forces her to stop, re-read, and either guess the meaning or give up on the sentence. The cumulative effect of encountering dozens of unexplained jargon terms is that she feels excluded and distrusts the site's transparency.

**Recommended Fix:** Use plain language for all user-facing content. Where technical terms are necessary, provide brief inline explanations or link to a glossary. Example: Instead of "Agentic AI — Enabling an autonomous digital workforce," write "AI Automation — We build software that handles repetitive tasks so your team can focus on higher-value work."

---

## Issue 11: Excessive Page Length on Homepage

**Page:** Homepage (`/`)  
**Element:** Full page — estimated 8,000+ pixels in height with 12+ distinct content sections  
**WCAG Criterion:** 2.4.1 Bypass Blocks (A), general cognitive accessibility  
**Severity:** Major

**Description:** The homepage contains an extremely long, single-page layout with the following sections in order: Hero, Logo Carousel, "Your Strategic AI Partner," "Driving ROI with AI" (6 service cards), "Problems We Solve" (6 items), Statistics, "Our Signature Approach" (process diagram), "Put AI to Work" CTA, "Our Latest Case Studies" (carousel), second Logo Carousel, "Connect with an Expert" CTA, and Footer.

While there is a "Skip to content" link (`<a class="skip-link screen-reader-text" href="#primary">`), it is visually hidden and only available to screen reader users.

**Impact on This User:** Eleanor reads top-to-bottom and does not skim or jump around. The extreme length of the homepage caused her to lose her place multiple times. She forgot what she had read by the time she reached the bottom. The sheer volume of content and CTAs was overwhelming. The skip link is invisible to her because she is not a screen reader user.

**Recommended Fix:** Reduce the number of content sections on the homepage, or provide a visible table of contents / anchor navigation so users can jump to specific sections. Consider breaking the homepage into a concise overview with clear links to dedicated subpages. Make the "Skip to content" link visible on keyboard focus for all users, not just screen reader users.

---

## Issue 12: Carousel/Slider for Case Studies and Testimonials

**Page:** Homepage (`/`) — case studies section; Contact page (`/contact`) — testimonials  
**Element:** Tiny Slider (`tns`) instances — `.single-item-slider`, `.outcome-slider`, `.cards-slider`  
**WCAG Criterion:** 2.2.2 Pause, Stop, Hide (A), 1.3.2 Meaningful Sequence (A)  
**Severity:** Major

**Description:** The site uses the Tiny Slider library for multiple carousel instances: case studies on the homepage, testimonials on the contact page, and timeline/image galleries on other pages. These carousels present one item at a time and require users to discover and use navigation controls (arrows or dots) to view additional content.

**Impact on This User:** Eleanor does not intuitively understand carousels. She does not know how many items are hidden, whether she has seen all the content, or how to navigate between slides. She expressed concern about "missing something" behind the slides. For a user who reads linearly, carousels break the expected content flow by hiding information behind an interactive control she may not notice or know how to use.

**Recommended Fix:** Replace carousels with stacked content (show all items vertically) or provide a clear "View All" link that takes users to a page with all items displayed. If carousels are retained, add visible indicators of total slide count (e.g., "1 of 5"), ensure navigation controls are large and clearly labeled, and provide a "View All" alternative.

---

## Issue 13: "Insights" Navigation Label Instead of "Blog"

**Page:** All pages (global navigation)  
**Element:** Navigation item — `<a class="mega-menu-link" href="https://launchpadlab.com/blog/">Insights</a>`  
**WCAG Criterion:** 2.4.6 Headings and Labels (AA), 3.2.4 Consistent Identification (AA)  
**Severity:** Minor

**Description:** The navigation uses the label "Insights" for what is essentially the company blog (the URL is `/blog/`). The page title in the browser tab reads "Web Design & Development Blog." The disconnect between the navigation label ("Insights") and the actual content (a blog) creates unnecessary confusion.

**Impact on This User:** Eleanor does not recognize "Insights" as a blog. She expects conventional labels. This minor inconsistency adds to the overall feeling that the site uses unnecessarily fancy language when plain terms would suffice.

**Recommended Fix:** Rename the navigation item to "Blog" or "Blog & Insights" to match user expectations and the actual page URL.

---

## Issue 14: "Book a Discovery Call" CTA Uses Marketing Jargon

**Page:** Services page (`/services`)  
**Element:** CTA button — "Book a Discovery Call"  
**WCAG Criterion:** 2.4.6 Headings and Labels (AA)  
**Severity:** Minor

**Description:** The Services page features a CTA labeled "Book a Discovery Call" within a section about a "Discovery Space Navigator." The term "Discovery Call" is sales industry jargon that means an initial consultation, but to a non-business user, the meaning is unclear.

**Impact on This User:** Eleanor doesn't know what a "discovery call" is. She would not click this button because she does not understand what she would be signing up for. She wants to "call" or "email" — not "book a discovery call."

**Recommended Fix:** Use plain language: "Schedule a Free Consultation" or "Talk to Us About Your Needs." If "discovery call" is important to internal branding, add clarifying text: "Book a Discovery Call — a free, no-obligation conversation to discuss your needs."

---

## Issue 15: Small Default Font Size for Preset "Small" Text

**Page:** All pages  
**Element:** CSS custom property `--wp--preset--font-size--small: 13px`  
**WCAG Criterion:** 1.4.4 Resize Text (AA), general readability best practice  
**Severity:** Minor

**Description:** The WordPress theme sets a "small" font size preset of 13px. While the main body copy may be larger, any elements using this preset size (labels, captions, fine print, navigation sub-items) would be difficult for Eleanor to read with her reading glasses. Additionally, the mega menu sub-items and footer text appear to use relatively small type.

**Impact on This User:** Eleanor has age-related vision decline and uses reading glasses. Text at 13px is at the lower limit of comfortable readability. She uses default browser settings and does not zoom or increase font size via browser controls.

**Recommended Fix:** Set a minimum font size of 16px for all body copy and interactive elements. Ensure navigation labels, form labels, and footer text are at least 14px. Avoid using the 13px "small" preset for any content that users need to read.

---

## Issue 16: Footer Phone Number Link Has Malformed HTML

**Page:** All pages (global footer)  
**Element:** `<a href="tel:312-888-9651"">(312) 888-9651</a>` — note the double quote at the end of the `href` attribute  
**WCAG Criterion:** 4.1.1 Parsing (A) — deprecated in WCAG 2.2 but still relevant for robustness  
**Severity:** Minor

**Description:** The phone number link in the footer has a malformed `href` attribute with a trailing double-quote: `href="tel:312-888-9651""`. While most browsers will parse this correctly and the link will still function, it is technically invalid HTML that could cause issues in edge cases or older browsers.

**Impact on This User:** Likely no direct impact since modern browsers handle this gracefully, but it indicates a lack of quality assurance in the template and could cause issues for users on older or non-standard browsers.

**Recommended Fix:** Remove the trailing double-quote: `<a href="tel:312-888-9651">(312) 888-9651</a>`.

---

## Issue 17: Multiple Competing CTAs Create Choice Overload

**Page:** Homepage (`/`), Services page (`/services`)  
**Element:** Multiple CTA buttons throughout: "Connect with an Expert," "Learn More" (x6), "View Services," "View Industries," "View Case Study" (x3+), "Book a Discovery Call"  
**WCAG Criterion:** General cognitive accessibility best practice (COGA supplement to WCAG)  
**Severity:** Minor

**Description:** The homepage alone contains approximately 15+ clickable CTAs of varying labels. Each service card has its own "Learn More" button, the hero has "Connect with an Expert," the mega dropdown has "View Services" and "View Industries," the case studies section has multiple "View Case Study" links, and the services page adds "Book a Discovery Call" and "Learn More" for each service.

**Impact on This User:** Eleanor is overwhelmed by the number of choices. She does not skim — she reads each option and tries to decide if it's the right one. Having 15+ CTAs competing for attention makes her less likely to click any of them. She experiences decision fatigue, which contributes to her overall frustration with the site.

**Recommended Fix:** Reduce the number of visible CTAs per page. Prioritize one primary action per section. Use consistent labeling (don't mix "Learn More," "View," "Explore," and "Connect" for similar actions). Consider a single prominent CTA in the hero with a clearly labeled secondary CTA for contact.

---

## Issue 18: "Ready to Build Something Great?" — Non-Descriptive Page Heading on Contact Page

**Page:** Contact page (`/contact`)  
**Element:** Page heading — `<h1>` or equivalent: "Ready to Build Something Great?"  
**WCAG Criterion:** 2.4.2 Page Titled (A), 2.4.6 Headings and Labels (AA)  
**Severity:** Minor

**Description:** The Contact page heading is "Ready to Build Something Great?" rather than a descriptive heading like "Contact Us" or "Get in Touch." The page `<title>` is "Contact Us | LaunchPad Lab" (which is good), but the visible on-page heading uses a marketing question instead of a clear label.

**Impact on This User:** When Eleanor navigated to the Contact page, her first impression was confusion — the heading sounded like a project kickoff invitation, not a contact page. She expected to see "Contact Us" as the main heading with contact details immediately visible below it.

**Recommended Fix:** Use "Contact Us" as the visible page heading, consistent with the `<title>` tag and the navigation label. The marketing question can be retained as a subheading if desired.

---

## Summary Table

| # | Issue | Page(s) | WCAG Criterion | Severity |
|---|---|---|---|---|
| 1 | Hero jargon instead of plain language | Homepage | 3.1.5 (AAA) | Major |
| 2 | "Connect with an Expert" CTA label | Homepage, Services | 3.2.4, 2.4.6 (AA) | Major |
| 3 | Auto-scrolling logo carousel — no pause control | Homepage, About | 2.2.2 (A) | Critical |
| 4 | Mega dropdown menus overwhelming and fragile | All pages (nav) | 2.4.3, 3.2.1 (A) | Major |
| 5 | Hamburger menu with no text label at ≤1069px | All pages (nav) | 3.2.3 (AA) | Major |
| 6 | Scroll-triggered AOS animations delay content | Homepage, all | 2.3.3 (AAA) | Major |
| 7 | Contact info buried below form and testimonials | Contact | 2.4.6 (AA) | Critical |
| 8 | Contact form requires "Company Email" and "Company" | Contact, Services | 3.3.2 (A) | Major |
| 9 | Contact form requires JavaScript — no fallback | Contact, Services | Non-Interference | Minor |
| 10 | Excessive jargon without plain-language alternatives | Homepage, Services, About | 3.1.5 (AAA) | Major |
| 11 | Excessive homepage length — no visible skip/TOC | Homepage | 2.4.1 (A) | Major |
| 12 | Carousel/slider hides content behind controls | Homepage, Contact | 2.2.2, 1.3.2 (A) | Major |
| 13 | "Insights" nav label instead of "Blog" | All pages (nav) | 2.4.6 (AA) | Minor |
| 14 | "Book a Discovery Call" jargon CTA | Services | 2.4.6 (AA) | Minor |
| 15 | Small font size preset (13px) | All pages | 1.4.4 (AA) | Minor |
| 16 | Footer phone link has malformed HTML | All pages (footer) | 4.1.1 (A) | Minor |
| 17 | Multiple competing CTAs cause choice overload | Homepage, Services | COGA best practice | Minor |
| 18 | Non-descriptive heading on Contact page | Contact | 2.4.2, 2.4.6 (A/AA) | Minor |

---

## Priority Recommendations

### Immediate (Critical)
1. **Move phone number and email to the top of the Contact page** — above the form, in large, clear text.
2. **Add a visible pause/stop button to the logo carousel** or replace it with a static grid.

### Short-Term (Major)
3. **Add plain-language descriptions** to the hero section and service cards alongside or replacing jargon.
4. **Add a visible "Menu" text label** to the hamburger toggle button.
5. **Simplify mega dropdown menus** — reduce density, add click-to-open option.
6. **Reduce or remove scroll-triggered animations** — default to static content.
7. **Make "Company" field optional** and rename "Company Email" to "Email."
8. **Shorten the homepage** or add visible section navigation.

### Long-Term (Minor)
9. Rename "Insights" to "Blog" in navigation.
10. Add plain-language alternative for "Book a Discovery Call."
11. Increase minimum font size to 16px.
12. Fix the malformed `href` in the footer phone link.
13. Reduce the total number of CTAs per page.
14. Use "Contact Us" as the visible Contact page heading.
