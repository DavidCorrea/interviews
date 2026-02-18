# Accessibility Report: Skeptical User (Trust & Credibility Audit)

**Persona**: Derek Walsh, 45, Procurement Manager  
**Condition**: Skepticism — evaluates website credibility, trust signals, and professionalism before engaging  
**Date**: February 16, 2026  
**Website Tested**: https://launchpadlab.com/  
**Pages Evaluated**: Homepage (/), Contact (/contact/), About (/about/)  

---

## Executive Summary

LaunchPad Lab's website is professionally designed and provides many of the trust signals a skeptical procurement professional would seek: recognizable client logos, attributed testimonials, case studies with measurable outcomes, and a visible leadership team. However, several trust-undermining issues were identified, including vague marketing copy, inconsistent data across pages, missing image alt text, a JavaScript-dependent contact form with no fallback, and minor HTML quality errors. These issues, while not individually critical, compound to erode the impression of meticulous quality that a skeptical user expects from a premium digital product firm.

---

## Issues Found

### Issue 1: Vague, Unsubstantiated Service Descriptions

**Page**: Homepage (/)  
**Element**: Service cards section — "Driving ROI with AI" / "Make AI Your Competitive Advantage"  
**Specific Content**: Card subtitles: "Enabling an autonomous digital workforce," "Bespoke, redefining experiences," "Meeting users where they are," "Solving business problems," "Agile, cross-functional expertise," "Operating as an extension of your team"  

**WCAG Criteria**: Not a direct WCAG violation but relates to WCAG 3.1.5 (Reading Level) and general usability heuristic of using clear, meaningful language  
**Severity**: Major  

**Description**: The service card descriptions use marketing buzzwords instead of concrete, informative language. A skeptical user evaluating vendor credibility needs to understand what services are actually provided. "Solving business problems" under Salesforce Development is so generic it could describe any company in any industry. "Bespoke, redefining experiences" for Web Application Development is aspirational copy, not a service description. These vague descriptions fail to communicate what the company actually does and undermine trust.

**Recommended Fix**: Replace vague taglines with concrete descriptions. For example: "Web Application Development" → "Custom web applications built with React, Ruby on Rails, and Node.js for enterprises needing scalable internal tools and customer-facing platforms." Each service should communicate the technology, the deliverable, and the target customer.

**Impact on This User**: A skeptical procurement manager interprets vague language as a sign that the vendor is hiding something or doesn't have a clear value proposition. Vague descriptions increase the likelihood of the user leaving the site.

---

### Issue 2: Inconsistent Statistics Between Pages

**Page**: Homepage (/) vs. About (/about/)  
**Element**: Stats/metrics sections  
**Specific Content**: Homepage says "12+ Years in Business" while About page says "13+ Years in Business"  

**WCAG Criteria**: WCAG 3.1.6 (Pronunciation) — tangentially; more directly a violation of information accuracy and consistency principles  
**Severity**: Minor  

**Description**: The "Years in Business" statistic differs between the homepage and the about page. The homepage reads "12+" while the about page reads "13+." While this may be a content update that was applied to one page and not the other, to a skeptical user it signals careless content management. If a company cannot keep its own key metrics consistent across two pages, it raises questions about their attention to detail on client work.

**Recommended Fix**: Audit all pages for statistics and ensure they are consistent. Consider using a single content source (e.g., a WordPress custom field or shortcode) for key metrics so they update globally.

**Impact on This User**: Inconsistent data directly undermines credibility. A procurement manager trained to evaluate vendors will notice discrepancies and interpret them as either dishonesty or sloppiness — both red flags.

---

### Issue 3: Contact Form Requires JavaScript With No Fallback

**Page**: Contact (/contact/)  
**Element**: `<div id="nf-form-13-cont">` — Ninja Forms contact form  
**Specific Content**: `<noscript class="ninja-forms-noscript-message">Notice: JavaScript is required for this content.</noscript>`  

**WCAG Criteria**: WCAG 4.1.2 (Name, Role, Value) — form must be operable; WCAG 2.1.1 (Keyboard) — form content is inaccessible without JS; relates to progressive enhancement principle  
**Severity**: Major  

**Description**: The primary contact form on the /contact page is rendered entirely via JavaScript (Ninja Forms). If JavaScript fails to load, is blocked by a corporate firewall, or is disabled for security reasons, the user sees only the message "Notice: JavaScript is required for this content." There is no HTML fallback form, no mailto link within the form area, and no alternative method presented in the form's location. While alternative contact info (email, phone) exists lower on the page, the form area itself provides no graceful degradation.

**Recommended Fix**: Add a progressive enhancement fallback — at minimum, include within the `<noscript>` block a plain HTML form that submits to the server, or provide a clear link to the email address and phone number so users without JavaScript have immediate recourse.

**Impact on This User**: A skeptical user encountering a broken or non-loading form may interpret it as a sign of poor engineering quality. If they use corporate browsers with strict JavaScript policies, they may be completely unable to submit the form and may not notice the email/phone cards further down the page.

---

### Issue 4: Missing or Empty Alt Text on Substantive Images

**Page**: About (/about/), Homepage (/)  
**Element**: Multiple `<img>` elements  
**Specific Content**:
- About page team photos: `<img src="...scott.jpg" alt=""/>`, `<img src="...ryan.jpg" alt=""/>`, etc. (all 15 team member photos)
- About page main image: `<img src="...LaunchPad-Lab-Final-Selects-10.jpg" alt="" class="main-image" />`
- About page award badges: `<img src="...clutch1000.webp" alt="" />`, `<img src="...2022-Top-Developers-Clutch.png" alt="" />`, `<img src="...launchpad-lab-2022-best-places-to-work-chicago.png" alt="" />`, `<img src="...launchpadlab-b2b-companies-on-clutch-2022.png" alt="" />`, `<img src="...launchpadlab-top-1000-companies-on-clutch-2020.png" alt="" />`
- Homepage tab section images: `<img src="...Operational-Efficiency-2.png" alt="" class="tab-image" />` (all 6 tab images)
- Homepage inline callout: `<img src="...AI-Automation.svg" alt="">`
- Service card icons: `<img src="...authentic-white.png" alt="" />` and similar across all 6 cards
- Footer social media icons: `<img src="...facebook.svg" alt="">`, `<img src="...instagram.svg" alt="">`, `<img src="...linkedin.svg" alt="">`

**WCAG Criteria**: WCAG 1.1.1 (Non-text Content) — Level A  
**Severity**: Critical  

**Description**: Numerous images that convey meaningful information have empty `alt` attributes. The most egregious are:
1. **Team member photos** on the About page — all 15 leadership photos have `alt=""`. These images are within links to LinkedIn profiles and accompany names/titles. A user who cannot see the images (or a user evaluating professionalism) misses the visual credibility of seeing real people.
2. **Award badges** — several Clutch awards and Best Places to Work badges lack alt text. For a skeptical user, these are key trust signals; making them invisible to screen readers or degraded experiences undermines the credibility the awards are meant to provide.
3. **Social media icons** in the footer have empty alt text. While the adjacent text ("Facebook", "Instagram", "LinkedIn") provides some context, the images themselves are not marked as decorative via `role="presentation"` — they simply have empty alt attributes.

Some empty alt texts are appropriate (purely decorative icons, SVG arrows), but substantive images like team photos and award badges must have descriptive alt text.

**Recommended Fix**:
- Team photos: `alt="Scott Weisman, Co-Founder and CEO of LaunchPad Lab"`
- Award badges: `alt="Clutch Top 1000 Companies Global Badge 2021"` (use the award name and year)
- Tab images: `alt="Illustration of operational efficiency improvements through digital products"` or similar
- Social icons: Either add `alt="Facebook"` or mark as decorative with `role="presentation"` if the text label is sufficient
- Main about image: Add a meaningful description like `alt="LaunchPad Lab team collaborating at a whiteboard"`

**Impact on This User**: While Derek Walsh is not a screen reader user, empty alt text on award badges means these trust signals are invisible in degraded browsing contexts (images blocked, slow connections). More importantly, a skeptical user evaluating a digital product firm's own website quality would note this as a lack of attention to detail — the kind of error a firm selling web development services should not have on their own site.

---

### Issue 5: HTML Error in Footer Phone Link

**Page**: Contact (/contact/), all pages (footer is global)  
**Element**: Footer phone link  
**Specific Content**: `<a href="tel:312-888-9651"">(312) 888-9651</a>` — note the extra double-quote after the href value  

**WCAG Criteria**: WCAG 4.1.1 (Parsing) — Level A  
**Severity**: Minor  

**Description**: The footer phone number link has a malformed `href` attribute with an extra quotation mark: `href="tel:312-888-9651""`. While most browsers will handle this gracefully (parsing will stop at the first closing quote), it is an HTML validation error. For a skeptical user evaluating a web development firm, discovering HTML errors on the firm's own site is a credibility concern.

**Recommended Fix**: Remove the extra quotation mark: `<a href="tel:312-888-9651">(312) 888-9651</a>`

**Impact on This User**: A procurement manager evaluating a development firm expects the firm's own website to be flawless. An HTML error, even a minor one, suggests quality control gaps and undermines the firm's "we build high-quality digital products" positioning.

---

### Issue 6: Infinite Auto-Scrolling Logo Carousel Without Pause Control

**Page**: Homepage (/)  
**Element**: `.logos__scroller` / `.logos__list` — client logo carousel  
**Specific Content**: The "Trusted by Hundreds of Innovative Businesses" logo banner auto-scrolls infinitely using CSS animation  

**WCAG Criteria**: WCAG 2.2.2 (Pause, Stop, Hide) — Level A  
**Severity**: Major  

**Description**: The client logo carousel uses an infinite CSS animation (`animation: scroll var(--_logo-scroll-duration, 20s) linear infinite`) to scroll logos continuously. There is no visible pause, stop, or hide control for users. The code does check for `prefers-reduced-motion: reduce` and will skip the animation if the user has that OS setting enabled, which is positive. However, there is no on-page control to pause the animation, and most users (including a skeptical procurement manager) will not have the reduced-motion preference enabled.

For a trust-focused user, auto-scrolling logos create a specific problem: you cannot study them at your own pace. If a user wants to carefully read each client logo (and a skeptical user definitely would), the constant motion makes it difficult to verify the full list of clients. The animation speed is set dynamically based on the number of logos, but with 12 logos the scroll is relatively fast.

**Recommended Fix**: 
1. Add a visible pause button to the carousel
2. Pause the animation on hover/focus so users can study individual logos
3. Consider displaying logos in a static grid layout instead, which provides better usability for trust evaluation

**Impact on This User**: A skeptical user wants to carefully examine every client logo as a trust signal. An auto-scrolling carousel that cannot be paused forces the user to chase moving content, reducing the effectiveness of the trust signal and creating frustration.

---

### Issue 7: No Visible Pricing, Engagement Model, or Scoping Information

**Page**: All pages  
**Element**: Entire site — absence of content  

**WCAG Criteria**: Not a direct WCAG violation; relates to WCAG 3.1.5 (Reading Level) and the broader principle of providing sufficient information for users to make informed decisions  
**Severity**: Major  

**Description**: The entire website contains no information about pricing ranges, engagement models (fixed-bid vs. time-and-materials), typical project timelines, or how the scoping/estimation process works. For a skeptical procurement manager, the absence of any commercial framing is a barrier to trust. It forces the user to submit a contact form without knowing whether the company is even in their budget range, which feels like a sales funnel rather than a transparent business relationship.

**Recommended Fix**: Add a "How We Work" or "Engagement Models" page that describes typical engagement structures, approximate timelines, and — if appropriate — starting price ranges or "projects typically range from $X-$Y." Even qualitative information (e.g., "We typically work with mid-market companies on 3-6 month engagements") would help a skeptical user gauge fit.

**Impact on This User**: A procurement manager who has been burned by vendors will not fill out a contact form without some sense of commercial fit. The complete absence of pricing or engagement model information makes the site feel like a lead-generation funnel, which reduces trust and increases the likelihood of the user leaving without making contact.

---

### Issue 8: "AI" Keyword Saturation Without Substantiation

**Page**: Homepage (/), all pages  
**Element**: Page titles, hero sections, service descriptions, meta descriptions  
**Specific Content**: Title: "AI-Centric Digital Product Design & Development"; Meta: "builds mission-critical digital solutions with AI at the center of all we do"; Hero: "AI Innovation. Digital Solutions. Results that Matter."; Section headers: "Your Strategic AI Partner," "AI-Powered Digital Solutions," "Driving ROI with AI," "Make AI Your Competitive Advantage," "Put AI to Work"  

**WCAG Criteria**: WCAG 3.1.5 (Reading Level) — tangentially; primarily a usability and trust concern  
**Severity**: Minor  

**Description**: The word "AI" appears in nearly every major heading and section of the homepage. The site title, meta description, hero headline, and at least five section headers all reference AI. For a company founded in 2012, this heavy AI positioning appears to be a recent marketing pivot. A skeptical user may question whether the AI expertise is genuine or whether the company has simply relabeled existing services with AI buzzwords. The site does not provide evidence of AI-specific capabilities — no AI case studies with technical depth, no AI certifications (e.g., AWS AI Practitioner, Google Cloud AI), and no examples of AI models built or deployed.

**Recommended Fix**: 
1. Create dedicated AI case studies showing specific AI/ML models, tools, or automations built for clients
2. Add team certifications or credentials specific to AI
3. Reduce AI keyword saturation and balance with evidence. Let the case studies speak for the capability rather than repeating the claim in every heading
4. Consider an "AI Capabilities" page with technical depth

**Impact on This User**: A skeptical procurement manager interprets keyword saturation without evidence as a red flag. It suggests trend-chasing rather than genuine expertise. If the company has real AI capabilities, the site needs to prove it with specifics rather than repeating the claim.

---

### Issue 9: Tab Panel Images Lack Meaningful Alt Text

**Page**: Homepage (/)  
**Element**: `.tabs-wrapper` — "Problems We Solve" tabbed interface  
**Specific Content**: Six tab panels each contain an `<img>` with `alt=""` (empty alt text): Operational Efficiency, Modern Technology, Customer Engagement, Scalable Solutions, Expansive Resources, Speed to Market  

**WCAG Criteria**: WCAG 1.1.1 (Non-text Content) — Level A  
**Severity**: Minor  

**Description**: The tabbed interface in the "Ship Game-Changing Digital Products to Market Fast" section includes images for each tab panel. These images appear to be illustrative graphics related to each problem area. All six images have empty alt attributes. While the tab buttons have text labels and preview descriptions, the images provide visual context that reinforces the content. Treating them all as decorative may be acceptable if they are purely illustrative, but if they contain text, charts, or meaningful visual data, they need alt text.

**Recommended Fix**: If images are decorative, add `role="presentation"` for clarity. If they contain meaningful visual information, add descriptive alt text such as `alt="Illustration showing streamlined workflow for operational efficiency"`.

**Impact on This User**: A skeptical user evaluating the site's professionalism may view consistently empty alt text as a pattern of neglect, especially from a firm that sells digital product development services.

---

### Issue 10: Social Media Icons in Footer Lack Accessible Names

**Page**: All pages (global footer)  
**Element**: Footer social media links  
**Specific Content**:
```html
<a href="https://www.facebook.com/LaunchPadLab" target="_blank" rel="noopener"><img src="...facebook.svg" alt=""> Facebook</a>
<a href="https://www.instagram.com/launchpadlab/" target="_blank" rel="noopener"><img src="...instagram.svg" alt=""> Instagram</a>
<a href="https://www.linkedin.com/company/launchpad-lab" target="_blank" rel="noopener"><img src="...linkedin.svg" alt=""> LinkedIn</a>
```

**WCAG Criteria**: WCAG 1.1.1 (Non-text Content) — Level A; WCAG 2.4.4 (Link Purpose) — Level A  
**Severity**: Minor  

**Description**: The social media links in the footer contain icons with empty alt attributes. Because the link text ("Facebook", "Instagram", "LinkedIn") is visible alongside the icon, the accessible name of the link is technically available. However, the empty alt on the icon means screen readers will attempt to announce the image (some may announce the filename). The links also open in new windows (`target="_blank"`) without indicating this to the user.

**Recommended Fix**: 
1. Either add `alt="Facebook icon"` or mark icons as decorative with `role="presentation"`  
2. Add an indication that links open in a new window, e.g., `aria-label="Facebook (opens in new window)"` or visible text "(opens in new tab)"

**Impact on This User**: Minor for a skeptical user who can see the page, but the lack of new-window indicators is a transparency issue — a skeptical user doesn't like being redirected without warning.

---

### Issue 11: About Page Team Photos All Have Empty Alt Text

**Page**: About (/about/)  
**Element**: `.clickable-image-and-text-gid-wrapper` — Leadership Team section  
**Specific Content**: All 15 team member `<img>` tags have `alt=""`:
- `<img src="...scott.jpg" alt=""/>` (Scott Weisman, Co-Founder & CEO)
- `<img src="...ryan.jpg" alt=""/>` (Ryan Francis, Partner)
- `<img src="...brendan.jpg" alt=""/>` (Brendan Hennessy, Co-Founder & CTO)
- (and 12 more team members)

**WCAG Criteria**: WCAG 1.1.1 (Non-text Content) — Level A  
**Severity**: Major  

**Description**: The leadership team section is a critical trust-building component for a skeptical user. Seeing real people with real photos significantly increases credibility. However, all 15 team member photos have empty alt attributes. These images are not decorative — they are within linked elements (each team member links to their LinkedIn profile) and directly support the credibility of the team section. Empty alt text means:
1. Screen readers skip the images entirely
2. If images fail to load, no fallback text appears
3. The trust value of "showing real people" is lost for any user in a degraded experience

**Recommended Fix**: Each image should have a descriptive alt attribute: `alt="Photo of Scott Weisman, Co-Founder and CEO"`. This ensures the trust signal is communicated regardless of whether the image renders.

**Impact on This User**: Team photos are one of the strongest trust signals for a skeptical user. If they fail to load (corporate proxy, slow connection, content blocker), the empty alt text means the user sees nothing — no names, no context, no credibility. The section becomes a wall of broken image icons with no explanation.

---

### Issue 12: Dev Environment URL Leaking in Production

**Page**: Contact (/contact/)  
**Element**: CTA section icon image  
**Specific Content**: `<img src="https://dev-launchpadlab.pantheonsite.io/wp-content/uploads/2022/06/launch-black.svg" alt="">`  

**WCAG Criteria**: Not a direct WCAG violation; relates to site professionalism and trust  
**Severity**: Minor  

**Description**: The "Reach Out" section on the contact page contains an image that loads from a development/staging URL (`dev-launchpadlab.pantheonsite.io`) rather than the production domain. This suggests the content was created or edited in a development environment and the asset URL was not updated when promoted to production. While the image may still load (Pantheon likely serves it), exposing a development URL on a production site is unprofessional and signals a QA gap.

**Recommended Fix**: Update the image source to use the production domain: `https://launchpadlab.com/wp-content/uploads/2022/06/launch-black.svg`

**Impact on This User**: A technically literate procurement manager may inspect page source or notice mixed-domain asset loading. Development URLs in production suggest inadequate deployment processes — a red flag for a company that sells software development services.

---

## Summary Table

| # | Issue | Page | WCAG | Severity | Category |
|---|-------|------|------|----------|----------|
| 1 | Vague service descriptions | Homepage | 3.1.5 | Major | Trust/Content |
| 2 | Inconsistent statistics across pages | Homepage, About | — | Minor | Trust/Content |
| 3 | JS-dependent contact form, no fallback | Contact | 4.1.2, 2.1.1 | Major | Functionality |
| 4 | Empty alt text on substantive images | All pages | 1.1.1 (A) | Critical | Accessibility |
| 5 | HTML error in footer phone link | All pages | 4.1.1 (A) | Minor | Code Quality |
| 6 | Auto-scrolling logo carousel, no pause | Homepage | 2.2.2 (A) | Major | Accessibility |
| 7 | No pricing/engagement model info | All pages | 3.1.5 | Major | Trust/Content |
| 8 | AI keyword saturation without evidence | Homepage | 3.1.5 | Minor | Trust/Content |
| 9 | Tab panel images lack alt text | Homepage | 1.1.1 (A) | Minor | Accessibility |
| 10 | Social icons lack accessible names | All pages | 1.1.1 (A), 2.4.4 | Minor | Accessibility |
| 11 | Team photos all have empty alt text | About | 1.1.1 (A) | Major | Accessibility/Trust |
| 12 | Dev environment URL in production | Contact | — | Minor | Code Quality/Trust |

---

## Trust Verdict

**Would this user engage?** Cautiously yes — but only because external trust signals (client logos, Clutch reviews, LinkedIn-verified leadership) overcome the site's quality issues. The site earns enough credibility through third-party validation and specific case study metrics to justify an initial email inquiry, but the vague marketing copy, inconsistent statistics, and code quality issues would prevent this user from filling out the contact form with high confidence. A skeptical procurement manager would reach out via email (contact@launchpadlab.com) or phone ((312) 888-9651) rather than the JavaScript-dependent form, and would conduct additional due diligence through Clutch reviews and LinkedIn before any meaningful engagement.
