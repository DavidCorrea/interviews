# Accessibility Report: ADHD (Cognitive/Attention) Evaluation

**Website:** https://launchpadlab.com/  
**Evaluator Persona:** Jordan Chen — 34-year-old marketing professional with ADHD (combined type)  
**Date:** February 2026  
**Pages Evaluated:** Homepage (`/`), Contact (`/contact`), Services (`/services`), About (`/about`)  

---

## Executive Summary

The LaunchPad Lab website presents several accessibility barriers for users with ADHD and other cognitive/attention-related conditions. While the site has some strengths—a clear headline, well-structured service cards, and a visible "Contact" link in the navigation—it is undermined by persistent motion distractions, an extremely long homepage with competing sections, dense mega-menu navigation, a JavaScript-dependent contact form with no fallback, and an intrusive popup that breaks user focus. These issues combine to create an experience where cognitive load rapidly exceeds what users with attention difficulties can manage, increasing the risk of task abandonment.

---

## Issues Found

### Issue 1: Continuously Scrolling Logo Ticker with No Pause Control

**Page:** Homepage (`/`)  
**Element:** Logo ticker/marquee beneath the hero section (displays client logos: Kawasaki, Harvard, Whirlpool, Northwestern, etc.)  
**WCAG Criteria:** [2.2.2 Pause, Stop, Hide (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)  
**Severity:** Major  

**Description:**  
The client logo section uses a continuously scrolling/auto-advancing animation that plays indefinitely. There is no visible mechanism to pause, stop, or hide this motion. The logos scroll horizontally in an infinite loop.

**Impact on this user:**  
Continuous peripheral motion is one of the strongest attention-hijacking stimuli for users with ADHD. Jordan's eyes were repeatedly drawn to the moving logos, pulling focus away from the actual page content. This distraction occurred every time the logo ticker was in the viewport and could not be mitigated by the user.

**Recommended Fix:**  
- Add a visible pause/stop button for the logo ticker.  
- Alternatively, display logos in a static grid layout.  
- Ensure the animation respects the `prefers-reduced-motion: reduce` media query by halting all motion when the user has this OS-level setting enabled.  
- Consider removing auto-scroll entirely; a static logo grid conveys the same credibility without the distraction cost.

---

### Issue 2: Scroll-Triggered Animations (AOS) Create Persistent Motion on Scroll

**Page:** Homepage (`/`), Services (`/services`), About (`/about`)  
**Element:** Multiple sections using `data-aos="fade-up"` (7 instances on the homepage)  
**WCAG Criteria:** [2.3.3 Animation from Interactions (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/animation-from-interactions.html), [1.4.10 Reflow (indirectly)](https://www.w3.org/WAI/WCAG21/Understanding/reflow.html)  
**Severity:** Major  

**Description:**  
The site uses the AOS (Animate on Scroll) library to trigger fade-up entrance animations as users scroll. At least 7 elements on the homepage animate in this way. While the HTML includes 2 references to `prefers-reduced-motion`, it is unclear whether all AOS animations are fully suppressed when this setting is active.

**Impact on this user:**  
Each scroll action triggers new motion, fragmenting Jordan's attention. Instead of smoothly reading content top-to-bottom, each section "appearing" created a new visual event that his brain registered as a stimulus requiring attention. The cumulative effect of 7+ animations across a single long page significantly increased cognitive load.

**Recommended Fix:**  
- Verify that `prefers-reduced-motion: reduce` fully disables all AOS animations (not just reduces duration).  
- Add a user-facing toggle for "Reduce animations" that persists across pages.  
- Consider removing entrance animations entirely, or limiting them to a single hero animation.  
- If animations are retained, ensure they fire only once (not on every scroll into view).

---

### Issue 3: Excessively Long Homepage with Too Many Competing Sections

**Page:** Homepage (`/`)  
**Element:** Full page — 11 `<section>` elements, 84 images, approximately 10-11 distinct content blocks  
**WCAG Criteria:** [3.2.3 Consistent Navigation (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/consistent-navigation.html), [2.4.6 Headings and Labels (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html) (contextually applicable)  
**Severity:** Major  

**Description:**  
The homepage contains 11 distinct sections: Hero, Logo Ticker, Value Proposition, Services (6 cards), Problems We Solve (6 boxes), Statistics, Approach/Process, AI Call-to-Action, Case Studies, Blog/Related Content, and a Contact Form. Each section introduces a new visual design, new headings, and new content to process. There is no clear endpoint or "you've found what you need" signal.

**Impact on this user:**  
Jordan's working memory was overwhelmed by the volume of sections. By the midpoint of the page, he had forgotten the content at the top. The lack of a clear content hierarchy (everything felt equally prominent) meant there was no obvious "primary task" the page was guiding him toward. For a user with limited sustained attention, this resulted in surface-level skimming at best and complete disengagement at worst.

**Recommended Fix:**  
- Reduce the homepage to 4–5 focused sections maximum.  
- Establish a clear visual hierarchy: one primary message, one primary CTA, and supporting content that clearly defers to the main message.  
- Use a "progressive disclosure" pattern—show key info upfront and let users click to expand or navigate to detail pages.  
- Consider adding a sticky "Contact" CTA or anchor link so the user always has a clear next step visible.

---

### Issue 4: Contact Form Requires JavaScript with No Fallback

**Page:** Contact (`/contact`), Homepage (`/`) footer section, About (`/about`) footer section  
**Element:** Ninja Forms contact form (`nf-form-title-13`)  
**WCAG Criteria:** [4.1.2 Name, Role, Value (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html) (indirectly), [1.3.1 Info and Relationships (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)  
**Severity:** Critical  

**Description:**  
The contact form is rendered entirely via JavaScript (Ninja Forms). When JavaScript is blocked, disabled, or fails to load, the user sees only the text: **"Notice: JavaScript is required for this content."** No email address, phone number, or alternative contact method is displayed in the immediate vicinity of the empty form area.

**Impact on this user:**  
Jordan uses browser extensions that can interfere with JavaScript execution (Reader View, distraction blockers, script blockers). When the form failed to render, his primary path to contacting LaunchPad Lab was completely blocked. The fallback message ("JavaScript is required") provides no actionable alternative. The actual contact information (email, phone) exists further down the page, but a user who encounters a blank form may assume the page is broken and leave.

**Recommended Fix:**  
- Add a `<noscript>` block immediately where the form should appear, containing the email address (`contact@launchpadlab.com`), phone number (`(312) 888-9651`), and a note that the form requires JavaScript.  
- Consider providing a static HTML form as a fallback.  
- At minimum, place visible contact info (email, phone) *adjacent to* the form container, not only in a separate section below.

---

### Issue 5: Mega-Menu Dropdowns Present Excessive Options Simultaneously

**Page:** All pages (global navigation)  
**Element:** Mega-menu dropdowns for "Services" (6 items + description + CTA) and "Industries" (9 items in 3 columns + description + CTA)  
**WCAG Criteria:** [3.2.1 On Focus (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/on-focus.html), [2.4.8 Location (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/location.html)  
**Severity:** Moderate  

**Description:**  
Hovering over "Services" or "Industries" in the main navigation triggers a mega-menu dropdown that displays all sub-items simultaneously in a multi-column grid layout. The Services mega-menu shows 6 service links, a paragraph description, and a "View Services" button. The Industries mega-menu shows 9 industry links in 3 columns, a paragraph description, and a "View Industries" button.

**Impact on this user:**  
The sudden appearance of 6–9 options in a grid, plus descriptive text, overloaded Jordan's decision-making capacity. With ADHD, choosing from a large set of simultaneously presented options is significantly harder than scanning a simple list. Jordan had to consciously slow down and process each column individually, and reported forgetting the first column's contents by the time he reached the third.

**Recommended Fix:**  
- Simplify mega-menu dropdowns to show only link labels without description paragraphs.  
- Consider a single-column dropdown or a progressive disclosure pattern (hover to expand categories).  
- Ensure the mega-menu can be navigated via keyboard with clear focus indicators.  
- Limit the number of simultaneously visible items to 5–7 (within typical working memory capacity).

---

### Issue 6: Bloom (Elegant Themes) Popup Interrupts User Flow

**Page:** Homepage (`/`) — triggers after a delay or scroll threshold  
**Element:** Bloom email opt-in popup (`et_bloom` class)  
**WCAG Criteria:** [2.2.4 Interruptions (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/interruptions.html), [3.2.5 Change on Request (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/change-on-request.html)  
**Severity:** Major  

**Description:**  
The site uses the Bloom plugin (by Elegant Themes) to display a popup overlay. This popup appears to be triggered by a timed delay or scroll-depth threshold. It appears unpredictably during the user's browsing session, overlaying the content they are currently reading.

**Impact on this user:**  
The popup completely derailed Jordan's reading flow. When it appeared, he lost his place on the page, had to locate and activate the close button, and then needed to re-orient himself to where he was before the interruption. For users with ADHD, recovering from unexpected interruptions is disproportionately difficult—context-switching has a much higher cognitive cost. This single popup added significant frustration and contributed to near-abandonment of the site.

**Recommended Fix:**  
- Remove timed/scroll-triggered popups entirely, or delay them significantly (e.g., 3+ minutes of active engagement).  
- Never interrupt users who are actively scrolling or reading.  
- If a popup must exist, ensure it respects `prefers-reduced-motion` and appears only once per session.  
- Provide a clearly visible, large close button (not a small "X" in a corner).  
- Consider replacing the popup with a non-intrusive inline banner or sticky bar.

---

### Issue 7: Carousel/Slider Content Hides Information Behind Interaction

**Page:** Homepage (`/`), Contact (`/contact`)  
**Element:** Multiple carousels using tiny-slider library (case studies on homepage; testimonials on contact page — 5 quotes in a slider)  
**WCAG Criteria:** [1.3.2 Meaningful Sequence (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/meaningful-sequence.html), [2.4.7 Focus Visible (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)  
**Severity:** Moderate  

**Description:**  
The site uses the tiny-slider library to create multiple carousels. On the contact page, 5 client testimonials are displayed in a single-item carousel with dot navigation at the bottom. On the homepage, case studies are presented in a slider format. The carousel configuration shows `autoplay: false` (good), but navigation relies on small dot indicators or mouse-drag interaction.

**Impact on this user:**  
Jordan read the first testimonial and initially did not realize there were more slides. The dot navigation at the bottom was not immediately obvious. By the time he noticed the dots, he had already mentally moved on. Carousels require users to (1) realize more content exists, (2) figure out the interaction mechanism, and (3) remember previous slides—all of which tax working memory. For users with ADHD, this pattern results in most carousel content being missed entirely.

**Recommended Fix:**  
- Replace carousels with vertically stacked content (show all testimonials/case studies in a scrollable list).  
- If carousels must be used, add visible "Previous/Next" arrow buttons (not just dots).  
- Show a clear indicator like "1 of 5" to signal hidden content.  
- Ensure carousel controls are keyboard-accessible with visible focus indicators.

---

### Issue 8: Dense Paragraph Text in Key Informational Sections

**Page:** Homepage (`/`), Services (`/services`), About (`/about`)  
**Element:** Multiple sections, including: "AI-Powered Digital Solutions for the Modern Enterprise" (homepage), "We Help Unleash Your Digital Potential" (about page), service description paragraphs  
**WCAG Criteria:** [3.1.5 Reading Level (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/reading-level.html), [1.4.8 Visual Presentation (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/visual-presentation.html)  
**Severity:** Moderate  

**Description:**  
Several sections that communicate essential information about LaunchPad Lab's identity and services rely on multi-sentence paragraphs of corporate language. For example, the homepage paragraph: *"At LaunchPad Lab, we combine deep expertise in product design and development with cutting-edge AI consulting to solve critical business challenges. We've helped hundreds of businesses across all industries solve complex problems that go beyond just ROI."* These paragraphs use abstract, marketing-heavy language without concrete specifics.

**Impact on this user:**  
Jordan skimmed these paragraphs without absorbing meaningful information. The abstract, jargon-heavy language ("cross-functional teams," "cutting-edge AI consulting," "solve critical business challenges") blends together for someone who is scanning quickly. The key details—what exactly the company does, for whom, and how—were buried in prose that required sustained focus to parse.

**Recommended Fix:**  
- Break paragraphs into bullet points where possible.  
- Lead with the most concrete, specific information (e.g., "We build web and mobile apps for enterprise clients").  
- Limit paragraphs to 2–3 sentences maximum.  
- Use bold text to highlight key phrases within paragraphs.  
- Replace abstract language with specific, concrete descriptions.

---

### Issue 9: Heading Hierarchy Used for Styling Rather Than Structure

**Page:** Homepage (`/`)  
**Element:** Statistics section — `<h2>` tags used for "Years in Business," "Projects," and "Clients" (these are labels for numeric statistics, not section headings)  
**WCAG Criteria:** [1.3.1 Info and Relationships (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html), [2.4.6 Headings and Labels (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)  
**Severity:** Minor  

**Description:**  
The statistics section on the homepage uses `<h2>` heading elements for labels like "Years in Business," "Projects," and "Clients." These are descriptive labels for numeric values (12+, 730+, 240+), not section headings. Using heading tags for non-heading content creates a misleading document structure.

**Impact on this user:**  
When Jordan scans headings (which is his primary navigation strategy), encountering "Projects" as an h2 heading is confusing—it doesn't signal a new content section, it's just a stat label. This pollutes the heading hierarchy and makes it harder to use headings as navigation landmarks.

**Recommended Fix:**  
- Use `<p>`, `<span>`, or `<dt>`/`<dd>` elements for statistic labels instead of `<h2>`.  
- Reserve heading elements strictly for content section titles.  
- Ensure heading levels follow a logical hierarchy (h1 → h2 → h3) without skipping levels for visual purposes.

---

### Issue 10: Duplicate Heading Text on Contact Page

**Page:** Contact (`/contact`)  
**Element:** `<h1>` and `<h2>` both read "Ready to Build Something Great?"  
**WCAG Criteria:** [2.4.6 Headings and Labels (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)  
**Severity:** Minor  

**Description:**  
The contact page has both an `<h1>` and an `<h2>` element with the identical text: "Ready to Build Something Great?" This creates confusion in the document structure—the h1 appears to be a decorative/hero heading, while the h2 appears above the form section. Both convey the same information.

**Impact on this user:**  
When scanning headings to orient on the page, encountering the same heading twice provides no new information and creates momentary confusion about whether the user has scrolled in a loop or if there are two different sections with the same name.

**Recommended Fix:**  
- Differentiate the headings. For example, keep the h1 as the page title and change the h2 to something actionable like "Tell Us About Your Project" or "Get in Touch."  
- Ensure each heading on a page communicates unique, descriptive information.

---

### Issue 11: Wistia Video Embed Lacks Descriptive Context

**Page:** Homepage (`/`)  
**Element:** Wistia iframe embed (`wistia.net/embed/iframe/0wko1dsuhk`)  
**WCAG Criteria:** [1.1.1 Non-text Content (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html), [2.4.6 Headings and Labels (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)  
**Severity:** Minor  

**Description:**  
A Wistia video is embedded on the homepage within an iframe. While the iframe has a `title` attribute ("LaunchPad Lab: Our Approach to Building Digital Products Video"), there is no visible text near the embed that tells users what the video is about, how long it is, or why they should watch it.

**Impact on this user:**  
Jordan skipped the video entirely because there was no visible context about what it contained. Users with ADHD need a clear value proposition before committing attention to a video—something like "Watch: Our 2-Minute Approach Overview." Without this, the video is perceived as an unknown time commitment and is ignored.

**Recommended Fix:**  
- Add a visible heading or caption near the video describing its content and duration (e.g., "Watch: How We Build Digital Products (2 min)").  
- Ensure the iframe `title` attribute is descriptive (currently adequate).  
- Consider providing a text transcript or summary as an alternative for users who prefer reading.

---

### Issue 12: Minimal Visible Focus Indicators for Keyboard/Sequential Navigation

**Page:** All pages  
**Element:** Global styles — only 1 `:focus` reference found in CSS  
**WCAG Criteria:** [2.4.7 Focus Visible (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)  
**Severity:** Moderate  

**Description:**  
Analysis of the site's CSS reveals only a single `:focus` style reference. While browsers provide default focus outlines, many modern CSS resets (including those used by WordPress themes) remove these defaults. Without explicit focus styles, interactive elements (links, buttons, form fields) may not show visible focus indicators when navigated via keyboard.

**Impact on this user:**  
While Jordan primarily uses a mouse, users with ADHD often lose track of where they are on a page. Visible focus indicators serve as an anchor point—they show "you are here." Without clear focus styles, users who tab through the page (or who lose their place and use keyboard navigation to re-orient) have no visual feedback about which element is active.

**Recommended Fix:**  
- Add explicit `:focus-visible` styles to all interactive elements (links, buttons, form controls).  
- Use a high-contrast focus indicator (e.g., a 2px solid outline in a contrasting color).  
- Do not use `outline: none` without providing an alternative focus style.  
- Test the entire site using keyboard-only navigation to verify focus visibility.

---

### Issue 13: No Site-Level Accessibility Preferences (Reduced Motion, Dark Mode)

**Page:** All pages  
**Element:** Site-wide  
**WCAG Criteria:** [1.4.8 Visual Presentation (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/visual-presentation.html), [2.3.3 Animation from Interactions (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/animation-from-interactions.html)  
**Severity:** Minor  

**Description:**  
The site does not provide any user-facing controls for accessibility preferences such as reduced motion, high contrast, or dark mode. While there are 2 references to `prefers-reduced-motion` in the code (suggesting some OS-level support), there is no on-site toggle for users who haven't configured OS settings.

**Impact on this user:**  
Jordan prefers dark mode and reduced motion. While he may have OS-level settings configured, many users with ADHD who would benefit from reduced motion are unaware of the OS setting. A visible on-site toggle would directly empower these users. Additionally, the lack of dark mode means the bright white backgrounds create additional visual stimulation that some ADHD users find fatiguing.

**Recommended Fix:**  
- Add a site-wide accessibility preferences panel (accessible from the header or footer) with options for:  
  - Reduced motion (disables all animations)  
  - Dark mode / high contrast mode  
- Store preferences in localStorage so they persist across visits.  
- Ensure all animations (AOS, logo ticker, carousels) respect both the OS-level `prefers-reduced-motion` media query and the on-site toggle.

---

### Issue 14: Multiple Identical "Learn More" Link Texts

**Page:** Homepage (`/`), Services (`/services`)  
**Element:** Service cards — each card has a "Learn More" link, all with identical link text  
**WCAG Criteria:** [2.4.4 Link Purpose (In Context) (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html), [2.4.9 Link Purpose (Link Only) (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-link-only.html)  
**Severity:** Minor  

**Description:**  
The six service cards on the homepage each contain a "Learn More" link. All six links use identical text ("Learn More") with no programmatic differentiation. While the visual context (card headings) may make the destination clear visually, the link text alone does not distinguish between destinations.

**Impact on this user:**  
When Jordan scans links quickly (a common ADHD navigation pattern), six identical "Learn More" links blur together. It's not clear which he's already clicked or which leads where without re-reading the card heading each time. This adds unnecessary cognitive overhead.

**Recommended Fix:**  
- Use descriptive link text such as "Learn More About AI Automation" or "Explore Web App Development."  
- Alternatively, use `aria-label` or `aria-labelledby` to associate each "Learn More" link with its card heading for assistive technology users.  
- Consider making the entire card clickable (with the heading as the accessible name) instead of relying on a small "Learn More" link.

---

## Summary Table

| # | Issue | WCAG | Severity | Page(s) |
|---|-------|------|----------|---------|
| 1 | Continuously scrolling logo ticker | 2.2.2 (A) | Major | Homepage |
| 2 | Scroll-triggered AOS animations | 2.3.3 (AAA) | Major | Homepage, Services, About |
| 3 | Excessively long homepage | 3.2.3 (AA) | Major | Homepage |
| 4 | Contact form requires JavaScript, no fallback | 4.1.2 (A), 1.3.1 (A) | Critical | Contact, Homepage, About |
| 5 | Mega-menu presents too many options | 3.2.1 (A) | Moderate | All pages (nav) |
| 6 | Bloom popup interrupts user flow | 2.2.4 (AAA) | Major | Homepage |
| 7 | Carousel hides content behind interaction | 1.3.2 (A) | Moderate | Homepage, Contact |
| 8 | Dense paragraph text in key sections | 3.1.5 (AAA) | Moderate | Homepage, Services, About |
| 9 | Headings used for styling (stats labels) | 1.3.1 (A), 2.4.6 (AA) | Minor | Homepage |
| 10 | Duplicate heading text on contact page | 2.4.6 (AA) | Minor | Contact |
| 11 | Video embed lacks visible context | 1.1.1 (A) | Minor | Homepage |
| 12 | Minimal visible focus indicators | 2.4.7 (AA) | Moderate | All pages |
| 13 | No site-level accessibility preferences | 1.4.8 (AAA) | Minor | All pages |
| 14 | Multiple identical "Learn More" links | 2.4.4 (A) | Minor | Homepage, Services |

**Critical:** 1 | **Major:** 4 | **Moderate:** 4 | **Minor:** 5  
**Total Issues:** 14
