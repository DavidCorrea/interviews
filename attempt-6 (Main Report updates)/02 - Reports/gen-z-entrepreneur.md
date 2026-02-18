# Accessibility Report: LaunchPad Lab Website
## Persona: Gen-Z Entrepreneur (Jordan, 23)

**Date:** February 18, 2026  
**Site:** https://launchpadlab.com/  
**Pages Reviewed:** Homepage, Services, Mobile App Development, Our Work, Contact, About Us  
**Method:** Full accessibility tree inspection, interactive element analysis, content structure review  

---

## Executive Summary

LaunchPad Lab's website demonstrates solid foundational accessibility practices — skip links, semantic HTML landmarks, labeled form fields, and ARIA tab patterns. However, the site has significant content accessibility issues, structural problems, and UX barriers that would impact users with cognitive disabilities (ADHD, processing disorders), low-vision users, keyboard-only users, and screen reader users. The most critical issue is the About Us page serving identical content to the homepage, and a carousel component with broken ARIA state text. The enterprise-heavy language and form design also create cognitive and emotional barriers for non-enterprise users.

**Overall Accessibility Score: 62/100**

---

## Issues by Category

### 1. Navigation & Structure

#### 1.1 About Us Page Serves Homepage Content
- **Description:** The About Us page (`/about/`) renders identical content to the homepage — same H1 ("AI Innovation. Digital Solutions. Results that Matter."), same hero paragraph, same services list, same case studies carousel, same contact form. There is no unique "About Us" content (team, history, mission, values).
- **Location:** About Us page (`/about/`)
- **Severity:** **High**
- **WCAG Criterion:** 2.4.4 Link Purpose, 2.4.2 Page Titled, 3.2.4 Consistent Identification
- **Impact:** Users navigating to "About Us" expect company information. Receiving duplicate homepage content is disorienting, breaks user expectations, and undermines trust. Screen reader users navigating by headings would find the same structure as the homepage with no differentiation.
- **Recommended Fix:** Create a dedicated About Us page with unique content: team bios, company history, founding story, mission/values, and office information.

#### 1.2 Unpredictable Navigation Behavior
- **Description:** During testing, clicking the LaunchPad Lab logo (which links to `/`) occasionally navigated to unexpected pages (e.g., a case study page) instead of the homepage, likely due to overlapping click targets or timing issues with dynamic content.
- **Location:** Site-wide header logo
- **Severity:** **Medium**
- **WCAG Criterion:** 3.2.3 Consistent Navigation, 3.2.4 Consistent Identification
- **Impact:** Users lose their sense of place in the site. Keyboard and assistive technology users who rely on predictable navigation are especially affected.
- **Recommended Fix:** Audit click target areas in the header. Ensure the logo link has a sufficiently large, non-overlapping hit area. Test navigation paths from all pages.

#### 1.3 No Mobile Navigation Pattern Detected
- **Description:** The accessibility tree shows seven top-level navigation items in a horizontal list. No hamburger menu button, mobile drawer, or responsive navigation toggle was detected.
- **Location:** Site-wide navigation bar
- **Severity:** **Medium**
- **WCAG Criterion:** 1.4.10 Reflow (responsive design)
- **Impact:** Seven navigation items likely overflow or cause horizontal scrolling on mobile screens. Users on small devices may miss navigation items or be unable to access them.
- **Recommended Fix:** Implement a responsive navigation pattern (hamburger menu) for viewports below a reasonable breakpoint. Ensure the toggle button is keyboard-accessible and properly labeled.

#### 1.4 Duplicate Footer Navigation
- **Description:** The footer contains a full navigation list that mirrors the header nav (Services, Technologies, Industries, Our Work, About Us, Insights) plus additional items (Careers, Client Testimonials). These footer links lack differentiation from header nav links.
- **Location:** Site-wide footer
- **Severity:** **Low**
- **Impact:** Not a critical issue, but screen reader users encounter the same navigation links twice per page. Adding `aria-label` to differentiate ("Main navigation" vs "Footer navigation") would help.
- **Recommended Fix:** Add `aria-label` attributes to the `<nav>` elements: "Main navigation" for the header and "Footer navigation" for the footer.

---

### 2. Content & Readability

#### 2.1 Dense, Enterprise-Focused Language
- **Description:** Page content is heavily weighted toward enterprise terminology: "digital transformation," "cross-functional teams," "operational efficiency," "modernize operations," "reduce costs and unlock growth." Paragraphs are long (3–5 sentences each) and read like marketing copy rather than clear communication.
- **Location:** Every page, particularly the homepage hero, Services page, and Mobile App Development page
- **Severity:** **Medium**
- **WCAG Criterion:** 3.1.5 Reading Level (AAA)
- **Impact:** Users with cognitive disabilities (ADHD, dyslexia, processing disorders) will struggle with dense text. Non-enterprise users (founders, startups, students) will feel excluded. The reading level is significantly above the recommended lower-secondary education level.
- **Recommended Fix:** Simplify language. Use shorter sentences. Break paragraphs into bullet points. Add plain-language alternatives. Consider persona-specific landing pages or a "For Startups" section.

#### 2.2 Repetitive Non-Descriptive "Learn More" Links
- **Description:** The Services page contains at least six "Learn More" links, all with identical visible text. The Mobile App Development page also has multiple "View Case Study" links with identical text.
- **Location:** Services page, Mobile App Development page, homepage
- **Severity:** **High**
- **WCAG Criterion:** 2.4.4 Link Purpose (In Context), 2.4.9 Link Purpose (Link Only) (AAA)
- **Impact:** Screen reader users navigating by links will hear "Learn More, Learn More, Learn More" with no differentiation. Sighted users skimming the page cannot distinguish link destinations without reading surrounding context.
- **Recommended Fix:** Use descriptive link text: "Learn more about AI Automation," "Learn more about Mobile Development," "View Kawasaki case study." If visual design requires short text, use `aria-label` to provide descriptive alternatives.

#### 2.3 Heading Hierarchy Issues
- **Description:** On the homepage, statistical labels ("Years in Business," "Projects," "Clients") are marked as h2 headings. The page has an excessive number of h2 headings (10+), making heading-based navigation unwieldy. Some sections also use heading levels inconsistently.
- **Location:** Homepage stats section, multiple pages
- **Severity:** **Medium**
- **WCAG Criterion:** 1.3.1 Info and Relationships, 2.4.6 Headings and Labels
- **Impact:** Screen reader users navigating by heading level will get an inaccurate picture of the page structure. Stat labels are not true section headings and inflate the heading count.
- **Recommended Fix:** Use appropriate non-heading elements for stat labels (e.g., `<dt>`/`<dd>` or `<strong>` within a paragraph). Reserve h2 for actual page sections. Audit heading hierarchy across all pages for logical nesting.

#### 2.4 Carousel ARIA Text is Broken
- **Description:** The case studies carousel on the homepage reports its state as "slide 5 to 7 of 3." This is mathematically impossible and confusing.
- **Location:** Homepage case studies carousel
- **Severity:** **High**
- **WCAG Criterion:** 4.1.2 Name, Role, Value
- **Impact:** Screen reader users will receive nonsensical state information. This erodes trust in the component and makes the carousel unusable for assistive technology users.
- **Recommended Fix:** Fix the carousel's live region or ARIA attributes to correctly report the current slide position (e.g., "slide 1 of 3").

---

### 3. Interactive Elements

#### 3.1 Carousel Navigation Lacks Arrow Controls
- **Description:** The homepage and contact page carousels only provide small dot indicators (buttons labeled "Carousel Page 1 (Current Slide)," "Carousel Page 2," etc.) for navigation. There are no previous/next arrow buttons.
- **Location:** Homepage case studies carousel, Contact page testimonials carousel
- **Severity:** **Medium**
- **WCAG Criterion:** 2.1.1 Keyboard, 2.5.5 Target Size (AAA)
- **Impact:** Dot indicators are typically very small (< 44x44 CSS pixels), failing touch target size guidelines. Keyboard users and motor-impaired users may struggle to activate small dot buttons. Lack of arrow controls means users must understand the dot metaphor.
- **Recommended Fix:** Add visible previous/next arrow buttons. Ensure all carousel controls meet minimum 44x44px target size. Support keyboard arrow key navigation within the carousel.

#### 3.2 Empty Alert Roles on Form Fields
- **Description:** Every form field on the site (First Name, Last Name, Company Email, Company, How Can We Help You?) is followed by an `alert` role element in the DOM, even before any user interaction or validation has occurred.
- **Location:** All pages with contact forms (Homepage, Services, Mobile App Dev, Contact, etc.)
- **Severity:** **Medium**
- **WCAG Criterion:** 4.1.3 Status Messages
- **Impact:** Screen readers may announce empty alerts or treat them as live regions, creating noise and confusion. Alert roles should only be populated when there is an actual error or status to communicate.
- **Recommended Fix:** Use `aria-live="polite"` regions instead of `role="alert"` for validation messages, or ensure alert elements are only injected into the DOM when validation fails — not pre-rendered as empty shells.

#### 3.3 Tab Panel Content Exposure
- **Description:** On the homepage, the tablist ("Operational Efficiency," "Modern Technology," etc.) exposes all tab panel content in the accessibility tree simultaneously, even for non-selected tabs. The tab descriptions ("Streamline processes...", "Modernize legacy systems...") appear as sibling text nodes to the tab elements rather than within their respective tabpanels.
- **Location:** Homepage "Ship Game-Changing Digital Products to Market Fast" section
- **Severity:** **Medium**
- **WCAG Criterion:** 4.1.2 Name, Role, Value
- **Impact:** Screen reader users may hear all tab content at once when navigating through the tablist, making it difficult to understand which description belongs to which tab. The ARIA tab pattern requires content to be within `tabpanel` elements that are shown/hidden appropriately.
- **Recommended Fix:** Ensure tab descriptions are contained within their respective `tabpanel` elements and that non-selected tabpanels are properly hidden with `aria-hidden="true"` or `hidden` attribute.

#### 3.4 reCAPTCHA Iframe Accessibility
- **Description:** The contact forms include an iframe (likely reCAPTCHA) that appears between form fields and the submit button. The iframe is not labeled.
- **Location:** All pages with contact forms
- **Severity:** **Medium**
- **WCAG Criterion:** 4.1.2 Name, Role, Value, 2.1.1 Keyboard
- **Impact:** Screen reader users will encounter an unlabeled iframe. reCAPTCHA can be a significant barrier for keyboard-only users and users of assistive technology. The audio challenge in reCAPTCHA is often difficult to complete.
- **Recommended Fix:** Add a descriptive `title` attribute to the iframe. Consider using reCAPTCHA v3 (invisible) or an alternative bot-prevention method that doesn't require user interaction.

---

### 4. Visual & Contrast

#### 4.1 No Dark Mode Support
- **Description:** The website does not offer a dark color scheme or respect the `prefers-color-scheme: dark` media query. The site uses light backgrounds throughout.
- **Location:** Site-wide
- **Severity:** **Medium**
- **WCAG Criterion:** 1.4.3 Contrast (Minimum), 1.4.6 Contrast (Enhanced) (AAA)
- **Impact:** Users who prefer dark mode (common among Gen-Z, users with light sensitivity, and users with certain visual impairments) experience increased eye strain. Many modern users browse in dark environments where light-themed sites cause discomfort.
- **Recommended Fix:** Implement a dark mode using `prefers-color-scheme: dark` media query. Ensure all color combinations in both themes meet WCAG AA contrast ratios (4.5:1 for text, 3:1 for large text and UI components).

#### 4.2 Empty Decorative Paragraph Elements
- **Description:** In the logo marquee/trust badges section, each logo image is followed by an empty `<p>` tag. These create empty nodes in the accessibility tree.
- **Location:** Homepage and About Us page logo marquee
- **Severity:** **Low**
- **WCAG Criterion:** 1.3.1 Info and Relationships
- **Impact:** Screen readers may announce empty paragraphs or create confusing pauses in reading flow. Sloppy markup reduces overall code quality.
- **Recommended Fix:** Remove empty `<p>` elements from the logo marquee, or if they serve a layout purpose, use `aria-hidden="true"` or CSS-only spacing.

---

### 5. Forms & Input

#### 5.1 "Company Email" Field Excludes Non-Corporate Users
- **Description:** The contact form uses the label "Company Email *" as a required field. Users without corporate email domains (founders, students, freelancers using Gmail/Outlook) may feel excluded or unsure if their submission will be taken seriously.
- **Location:** All contact forms site-wide
- **Severity:** **Medium**
- **WCAG Criterion:** 3.3.2 Labels or Instructions
- **Impact:** Creates a psychological barrier for non-enterprise users. Does not technically prevent form submission but signals that the company is not interested in individual inquiries. This is a significant inclusivity issue for the target persona.
- **Recommended Fix:** Change label to "Work Email *" or "Email *" to be more inclusive. If business email validation is needed, handle it server-side with a friendly message.

#### 5.2 "Company" Required Field for Pre-Revenue Users
- **Description:** The "Company *" field is required on all contact forms. Users who haven't incorporated a business, are in ideation phase, or are solo founders may not have a company name.
- **Location:** All contact forms site-wide
- **Severity:** **Low**
- **WCAG Criterion:** 3.3.2 Labels or Instructions
- **Impact:** May cause confusion or abandonment for early-stage founders. Increases friction in the conversion funnel.
- **Recommended Fix:** Make the Company field optional, or add helper text: "If you don't have a company yet, that's okay — just tell us about your project."

#### 5.3 Multiple Alert Roles Before Interaction
- **Description:** As noted in 3.2, form fields are surrounded by `alert` elements. Additionally, there are two extra `alert` elements at the bottom of the form (likely for overall form success/error messages) that are present in the DOM before submission.
- **Location:** All contact forms site-wide
- **Severity:** **Medium**
- **WCAG Criterion:** 4.1.3 Status Messages
- **Recommended Fix:** Dynamically inject alert messages only when validation fails or the form is submitted. Do not pre-render empty alert containers.

---

### 6. Page-Specific Issues

#### 6.1 Our Work Page — Overwhelming Volume of Case Studies
- **Description:** The Our Work page lists 50+ case studies in a single scrollable grid with minimal filtering (only an "Industries" dropdown). No search, no pagination, no secondary filters (by service type, company size, or technology).
- **Location:** Our Work page (`/work/`)
- **Severity:** **Medium**
- **Impact:** Cognitive overload for users trying to find relevant examples. Users with ADHD or attention difficulties will struggle to scan through 50+ items. The flat list provides no progressive disclosure.
- **Recommended Fix:** Add secondary filters (by service type, technology, company size). Implement pagination or "load more" functionality. Consider featuring 6-8 highlighted case studies with an option to view all.

#### 6.2 Unlabeled Iframes
- **Description:** Multiple `<iframe>` elements appear throughout the site without `title` attributes. At least one is for reCAPTCHA, one appears to be a video embed, and others are unidentified (possibly tracking/analytics).
- **Location:** Homepage, Services, Contact page
- **Severity:** **Medium**
- **WCAG Criterion:** 4.1.2 Name, Role, Value
- **Recommended Fix:** Add descriptive `title` attributes to all iframes (e.g., `title="reCAPTCHA verification"`, `title="Company overview video"`). Hide purely decorative or tracking iframes with `aria-hidden="true"`.

#### 6.3 Contact Page Testimonial Carousel — Limited Social Proof
- **Description:** The testimonials carousel on the Contact page shows one quote at a time with five dot-navigation buttons. The visible testimonial is from a VP at "Apex Leaders" — a company most users won't recognize. There's no way to filter or browse testimonials by industry or company type.
- **Location:** Contact page
- **Severity:** **Low**
- **Impact:** Users looking for social proof relevant to their situation (e.g., startup founders) cannot easily find it. The carousel format limits discoverability.
- **Recommended Fix:** Display 2-3 testimonials visually at once, or use a grid format. Add testimonials from diverse client types. Consider adding a dedicated testimonials page with filtering.

---

## Summary of Issues by Severity

| Severity | Count | Issues |
|----------|-------|--------|
| **High** | 3 | About Us page duplicate content, Repetitive "Learn More" links, Carousel broken ARIA text |
| **Medium** | 11 | Unpredictable navigation, No mobile nav pattern, Dense enterprise language, Heading hierarchy, Empty alert roles, Tab panel content exposure, reCAPTCHA iframe, No dark mode, "Company Email" label, Overwhelming case studies volume, Unlabeled iframes |
| **Low** | 4 | Duplicate footer navigation, Empty paragraph elements, Company required field, Testimonial carousel limitations |

---

## Positive Findings

The following accessibility practices were observed and should be maintained:

1. **Skip to Content link** — Present on all pages with correct `#primary` target.
2. **Semantic landmarks** — Proper use of `banner`, `navigation`, `contentinfo`, `complementary` roles.
3. **Form field labels** — All form inputs have associated text labels.
4. **Link destinations** — All navigation links have proper `href` attributes with meaningful URLs.
5. **Image alt text** — Logo images in the trust badges section have descriptive alt text (e.g., "Kawasaki Engines," "Harvard University").
6. **Phone number as tel: link** — The phone number in the footer and contact page uses `tel:` protocol for click-to-call.
7. **Multiple contact methods** — Email, phone, form, and LinkedIn are all available.
8. **Consistent page structure** — Navigation, hero, content sections, contact form, and footer follow a predictable layout across pages.

---

## Overall Assessment

LaunchPad Lab's website has a solid structural foundation but falls short on content accessibility, cognitive load management, and inclusive design for non-enterprise users. The three high-severity issues (About Us page duplication, non-descriptive repetitive links, and broken carousel ARIA) should be addressed immediately. The medium-severity issues around language complexity, form design, and missing dark mode represent significant opportunities to broaden the site's appeal and accessibility. Addressing these issues would not only improve WCAG compliance but also make the site more welcoming to a wider range of potential clients, including first-time founders, startups, and younger users.
