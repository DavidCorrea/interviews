# Interview: James Okafor — Screen Reader User

## Date: February 18, 2026

## Website: https://launchpadlab.com/

## Assistive Technology: VoiceOver (macOS) + Keyboard-only navigation

---

### Task 1: First Impressions & Accessibility Structure

#### Initial Landing

I landed on the LaunchPad Lab homepage and immediately did what I always do — checked the page structure. The page title announced as "AI-Centric Digital Product Design & Development | LaunchPad Lab," which is descriptive and tells me right away what this company is about. Good start.

#### Skip Navigation

The very first thing my screen reader announced was a "Skip to content" link pointing to `#primary`. That's promising — it means somebody thought about keyboard users. I pressed Tab and it was the first focusable element, which is exactly where it should be. I activated it, though I cannot confirm whether focus was actually moved to a `main` content area, because — and this is a significant issue — there is **no `main` landmark** exposed in the accessibility tree anywhere on this page.

#### Landmarks

I checked for landmarks, and here's what I found:

- **`banner`**: Two separate `banner` landmarks are present. The first wraps the site header and navigation. The second wraps the hero section with the h1 heading. Having two `banner` landmarks without distinct `aria-label` values is confusing. When I use my screen reader's landmark navigation (VO+U, then selecting landmarks), I hear "banner" twice with no way to distinguish them. Best practice says a page should have one `banner`, or if multiple exist, they must have unique accessible names. This is a **WCAG 1.3.1 (Info and Relationships)** concern.
- **`navigation`**: Present, nested inside the first banner. It contains a list of links: Services, Technologies, Industries, Our Work, About Us, Insights, Contact. All links have clear, descriptive accessible names. This is done well.
- **`contentinfo`** (footer): Present. Contains company description, duplicate navigation links, contact info, social media links, and legal links. Properly structured.
- **`main`**: **Missing entirely.** This is a significant landmark omission. As a screen reader user, I rely on the `main` landmark to jump directly to page content. Without it, I have to tab through the entire header and navigation every time, or hope the "Skip to content" link actually works. The target `#primary` may exist in the DOM but is not exposed as a `main` landmark role in the accessibility tree. This violates **WCAG 1.3.1 (Info and Relationships)** and is a major barrier to efficient navigation.

#### Heading Hierarchy

I navigated by headings (VO+Command+H) and here's the full heading structure I encountered:

| Level | Text | Notes |
|-------|------|-------|
| h1 | "AI Innovation. Digital Solutions. Results that Matter." | Good — single h1 for the page |
| h2 | "AI-Powered Digital Solutions for the Modern Enterprise" | Logical section heading |
| h2 | "Make AI Your Competitive Advantage" | Logical section heading |
| h3 | "AI Automation & Agentic AI" | Under h2, good hierarchy |
| h3 | "Web Application Development" | Under h2, good hierarchy |
| h3 | "Mobile Application Development" | Under h2, good hierarchy |
| h3 | "Salesforce Development" | Under h2, good hierarchy |
| h3 | "Product Strategy & Design" | Under h2, good hierarchy |
| h3 | "Managed Services & Support" | Under h2, good hierarchy |
| h2 | "Ship Game-Changing Digital Products to Market Fast" | Logical section heading |
| h3 | "Operational Efficiency" | Inside tab control |
| h3 | "Modern Technology" | Inside tab control |
| h3 | "Customer Engagement" | Inside tab control |
| h3 | "Scalable Solutions" | Inside tab control |
| h3 | "Expansive Resources" | Inside tab control |
| h3 | "Speed to Market" | Inside tab control |
| h2 | "Years in Business" | **Issue** — this is a stat label, not a section heading |
| h2 | "Projects" | **Issue** — stat label inflated to h2 |
| h2 | "Clients" | **Issue** — stat label inflated to h2 |
| h2 | "Accelerate Digital Product Speed to Market" | Logical section heading |
| h3 | "Discover" | Good sub-heading |
| h4 | "Research & Define" | Good sub-heading |
| h3 | "Deliver" | Good sub-heading |
| h4 | "Development" | Good sub-heading |
| h4 | "QA Testing" | Good sub-heading |
| h3 | "Release" | Good sub-heading |
| h4 | "Deploy" | Good sub-heading |
| h4 | "Ongoing Support" | Good sub-heading |
| h2 | "Transform how your business operates with custom AI solutions" | Logical section heading |
| h2 | "We Help Shape Our Clients' Digital Future" | Logical section heading |
| h3 | "Spurring Enterprise Innovation" | Good |
| h3 | "360-Customer View in Salesforce" | Good |
| h3 | "Sales Discovery Portal for Automotive Companies" | Good |
| h2 | "You Might Also be Interested In" | Good |
| h3 | "The Business Value of Building Applications and Portals" | Good |
| h3 | "Download Our Guide: Building Your Competitive Advantage With Salesforce" | Good |
| h3 | "How Automated Intelligence Is Reshaping the Way Businesses Scale" | Good |
| h2 | "Let's Build Something Great." | Contact form section |
| h2 | "Contact Us" | Footer |
| h2 | "Let's Get Social" | Footer |

**Heading Issues:**
- "Years in Business," "Projects," and "Clients" are marked as h2 headings, but they are metric labels (12+, 730+, 240+ respectively). When I navigate by headings, I land on "Years in Business" expecting a major content section, only to find it's a stat. This clutters the heading outline and makes it harder for me to find actual content sections. **WCAG 1.3.1 (Info and Relationships)** — heading levels should reflect document structure, not visual styling.
- Headings are nested inside `tab` elements in the tablist. While this functions, it means my headings list includes all six tab labels (Operational Efficiency, Modern Technology, etc.), even when those tabs aren't selected. This inflates the headings list.

#### Focus Order

I tabbed through the interactive elements in order. The focus sequence I encountered was:

1. Skip to content link
2. LaunchPad Lab logo (home link)
3. Services, Technologies, Industries, Our Work, About Us, Insights, Contact (nav links)
4. "Connect with an Expert" link (hero CTA)
5. Service card links (AI Automation, Web App Development, etc.)
6. Tab controls (Operational Efficiency, Modern Technology, etc.)
7. "Learn More" standalone link
8. Case study links (Millennium Trust Company, Prosci, CDK Global)
9. Carousel page buttons
10. Blog post links
11. Form fields (First Name, Last Name, Company Email, Company, How Can We Help You)
12. Submit button
13. Footer links

The focus order is logical and follows the visual reading order from top to bottom. No focus traps were encountered. This is done well.

#### Client Logos

The client logo section includes images for Kawasaki Engines, 1-800-GOT-JUNK?, Harvard University, Prosci, Whirlpool, Northwestern University, CDK Global, Ann & Robert H. Lurie Children's Hospital of Chicago, Indiana University, Select Home Warranty, MD Anderson Cancer Center, and Bullhorn. **All logos have descriptive alt text**, which is excellent. Each logo is inside a list item with an empty paragraph element, which is slightly odd but not a functional issue.

#### Tablist Component

There is a `tablist` labeled "Ship Game-Changing Digital Products to Market Fast" with six tabs. The first tab "Operational Efficiency" is marked as `[selected]`. Each tab has an associated `tabpanel`. The ARIA roles (`tablist`, `tab`, `tabpanel`) appear correctly applied. The tabs were reachable via keyboard. This component appears well-implemented from an ARIA perspective.

#### Carousel

The case studies section uses a carousel with three slides and three page buttons labeled "Carousel Page 1 (Current Slide)," "Carousel Page 2," and "Carousel Page 3." The buttons update their labels when activated, which is good. However, the carousel status text reads **"slide 5 to 7 of 3"**, which is nonsensical. A screen reader user hearing this would be confused — it says slides 5 to 7 out of 3 total, which is mathematically impossible. This is a **WCAG 4.1.2 (Name, Role, Value)** violation — the programmatic state information is incorrect and misleading.

There are no previous/next buttons exposed in the accessibility tree for the carousel, only the page dots. This means I can navigate between slides, but the lack of explicit previous/next controls could be a minor usability concern. The carousel does not appear to auto-rotate, which is good for accessibility.

#### Iframes

There is an unlabeled `iframe` in the middle of the page (likely a video or embedded widget) and another in the footer. Neither has an accessible name or `title` attribute exposed. **WCAG 4.1.2 (Name, Role, Value)** — all iframes should have a descriptive `title` so screen reader users know what content they contain.

---

### Task 2: Understanding What They Do

#### Navigating to Services via Dropdown

From the homepage, I activated the "Services" link in the navigation. Rather than immediately navigating to a new page, the link revealed a dropdown submenu. The `link` element changed to `[expanded]` state, which is good — my screen reader announced the expanded state. Inside the dropdown, I found two columns of service links:

- AI Automation
- Web App Development
- Mobile App Development
- Salesforce Development
- Product Strategy & Design
- Managed Services & Support

There was also a "View Services" link with a paragraph describing the services overview. I activated "View Services" to navigate to the full Services page.

**Dropdown Accessibility Notes:** The dropdown menu opened on click (not hover), which is keyboard-friendly. The submenu items were reachable via Tab. However, I could not confirm whether Escape closes the dropdown without navigating away — standard pattern for accessible menus. The dropdown uses nested lists rather than a `menu`/`menuitem` ARIA pattern, which is acceptable for navigation but less semantically rich.

#### Services Page Structure

The Services page loaded with the title "AI-Centered Digital Product Development." The heading hierarchy was well-structured:

- **h1:** "AI-Centered Digital Product Development" — single, descriptive h1
- **h2:** "Supporting AI-Driven Digital Product Development" — clear section heading
- **h3 (×6):** Individual service headings (AI Automation & Agentic AI, Web Application Development, Mobile Application Development, Salesforce Development, Digital Product Strategy & Design, Managed Services & Support) — proper nesting under h2
- **h2:** "Advance with Modern Tech Solutions"
- **h3 (×3):** Business, IT, Users — describing who benefits
- **h2:** "Discovery Space Navigator"
- **h2:** "Build Digital Products that Deliver Outcomes"
- **h3 (×6):** Individual case study headings for Kawasaki, Whirlpool, Harvard, MD Anderson, Inspira Financial, Bullhorn
- **h2:** "Let's Build Something Great." (contact form)
- **h2:** "You Might Also Be Interested In"
- **h3 (×3):** Blog post headings
- **h2:** "Frequently Asked Questions"

This heading hierarchy is significantly better than the homepage — it's clean, logical, and makes it easy for me to navigate by headings to find exactly what I need.

#### Understanding Their Services

Through the headings and paragraph content, I was able to clearly understand what LaunchPad Lab offers:

1. **AI Automation & Agentic AI** — "Leverage AI automation capabilities and tooling to streamline operations, reduce costs, drive customer satisfaction, and enhance decision-making capabilities—faster and at scale."
2. **Web Application Development** — "Build an intuitive, user-friendly digital product that helps your team become more efficient, boost adoption, and differentiate your organization from the competition."
3. **Mobile Application Development** — "Deliver a world-class, mobile experience for your apps and websites, shipping to market in 50% less time than other software development consultancies."
4. **Salesforce Development** — "Combine the power of software application development with Salesforce products to create a one-of-a-kind, digital solution."
5. **Digital Product Strategy & Design** — "Bring your vision to life with a clear, human-centric product strategy and design."
6. **Managed Services & Support** — "Extend capabilities with our cross-functional team to ensure seamless execution and measurable results."

The content was accessible and descriptive. I could understand their value proposition without needing to see any visual elements.

#### "Learn More" Link Problem

A critical accessibility issue on this page: there are **at least 8 links all labeled "Learn More"** with no additional distinguishing context. When I navigate by links (VO+U, then selecting links list), my screen reader shows:

- Learn More
- Learn More
- Learn More
- Learn More
- Learn More
- Learn More
- Learn More
- Learn More

I have no idea which "Learn More" goes to which service without reading the surrounding content. This is a **WCAG 2.4.4 (Link Purpose in Context)** violation. Even with context, some of these links would be ambiguous. A much better approach would be "Learn more about AI Automation," "Learn more about Web App Development," etc. — or using `aria-label` or `aria-labelledby` to give each link a unique accessible name.

#### Accordion Buttons with Excessive Names

The "Advance with Modern Tech Solutions" section has three accordion-style buttons for Business, IT, and Users. The button accessible names include their *entire content*, making them extremely long. For example, the Business button's accessible name is: "Business Business Speed to market brings features to customers quicker. Enjoy a nimble response to mitigate risks or issues that could impact the experience. Future-proof your business with digital product development support." — this is announced in its entirety when I focus the button. It's overwhelming and makes it hard to understand what the button does. **WCAG 2.4.6 (Headings and Labels)** — labels should be descriptive but concise.

#### FAQ Section

The FAQ section uses `group` role elements for each question. The questions are:
- How much does it cost to build a custom software solution?
- Does LaunchPad Lab sell or license a specific type of software?
- How long does it take to build a digital product?
- Can I engage LaunchPad Lab for just product strategy and design?
- How does your team support core Salesforce implementation?
- What's different about your AI services?
- Do you modernize existing portals or applications?
- How do your managed IT services work post-launch?
- Can you work with our internal IT or product team?
- How do you ensure accessibility in digital product development?
- How does LaunchPad Lab handle security and compliance?
- Does your team deliver work fully remote?
- Is your team US-based?

I found it ironic that one of their FAQs asks "How do you ensure accessibility in digital product development?" — given some of the accessibility issues I'm documenting in this very interview.

#### Case Studies with Distinct Link Names

The case study section on the Services page uses descriptive link names: "View Case Study" for each — these are repeated but slightly more descriptive than bare "Learn More." The case study headings themselves are descriptive and unique, which helps provide context.

---

### Task 3: Finding How to Contact Them

#### Navigating to Contact Page

From the Services page, I activated the "Contact" link in the main navigation. The page loaded with the h1 heading "Ready to Build Something Great?" and a helpful paragraph: "Complete the form below to tell us about your project. We will get in touch with you as soon as possible."

#### Contact Page Landmarks

The same landmark issues persist:
- **Two `banner` landmarks** without unique labels
- **No `main` landmark**
- **`contentinfo`** present (footer)
- **`navigation`** present (header nav)

#### Contact Form Assessment

The contact form contains five text fields:

| Field | Accessible Name | Type | Required |
|-------|----------------|------|----------|
| First Name * | "First Name *" | textbox | Yes (indicated by *) |
| Last Name * | "Last Name *" | textbox | Yes |
| Company Email * | "Company Email *" | textbox | Yes |
| Company * | "Company *" | textbox | Yes |
| How Can We Help You? * | "How Can We Help You? *" | textbox | Yes |

**Positive:** Every field has a proper accessible label. My screen reader announced "First Name, required, text field" (or equivalent) when I tabbed to each one. The labels include the asterisk indicating required fields, which is announced. This is well-done.

**Concern:** The required state is conveyed only through the asterisk character in the label text. While this is common, best practice would be to also use the `aria-required="true"` attribute so the screen reader explicitly announces "required" independently of the visual asterisk. Without checking the HTML source, I cannot confirm whether `aria-required` is set, but the labels are at minimum functional.

Each text field is followed by an `alert` role element (likely for validation error messages). These are currently empty, which is fine — they should populate when validation errors occur.

#### Filling Out the Form

I successfully filled out all five fields using keyboard navigation:

1. Tabbed to "First Name" field — typed "James"
2. Tabbed to "Last Name" field — typed "Okafor"
3. Tabbed to "Company Email" field — typed "james.okafor@example.com"
4. Tabbed to "Company" field — typed "Accessibility Consulting Inc"
5. Tabbed to "How Can We Help You?" field — typed my message

All fields accepted input without issues. Tab order through the form fields was logical and sequential.

#### The CAPTCHA Barrier

After the last text field and before the Submit button, there is an **`iframe`** element with **no accessible name, no title, and no label**. Based on its position in the form (between the last field and Submit), this is almost certainly a CAPTCHA widget (likely Google reCAPTCHA).

This is a **critical accessibility barrier** for several reasons:

1. **Unlabeled iframe** — The iframe has no `title` attribute, so my screen reader just announces "frame" with no context about what it contains or what I need to do. **WCAG 4.1.2 (Name, Role, Value).**
2. **CAPTCHA accessibility** — Visual CAPTCHAs are inherently inaccessible to blind users. While reCAPTCHA v3 can work invisibly, and reCAPTCHA v2 offers an audio alternative, the iframe's contents are not accessible to my screen reader from the parent page context. **WCAG 1.1.1 (Non-text Content)** — if this is a visual CAPTCHA, there must be an accessible alternative.
3. **Potential form submission blocker** — If the CAPTCHA requires visual interaction I cannot perform, I would be completely unable to submit this form, which is the primary conversion mechanism on this page. This would be a **WCAG 2.1.1 (Keyboard)** failure if the CAPTCHA cannot be completed via keyboard.

When I tabbed from the message field toward the Submit button, I did pass through the iframe area. I could not determine from the accessibility tree alone whether there was an interactive element inside the iframe (like a checkbox) since iframe content is not directly exposed in the parent page's accessibility tree.

#### Submit Button

The Submit button has a clear accessible name: "Submit." It was reachable via Tab. I did not activate it since I did not want to actually submit a test form, but its presence and labeling are correct.

#### Alternative Contact Methods

Below the form, the Contact page provides alternative ways to reach out, under the h2 "Let's Connect":

- **Email**: `contact@launchpadlab.com` (properly linked with `mailto:`)
- **Call**: `(312) 888-9651` (properly linked with `tel:`)
- **LinkedIn**: A link labeled simply "Connect" pointing to their LinkedIn company page

The email and phone links are excellent — they use proper protocols (`mailto:` and `tel:`) so I can activate them directly from my screen reader. However, the LinkedIn link's accessible name is just "Connect," which is ambiguous. A screen reader user navigating by links would hear "Connect, link" with no context about what they're connecting to. It should be labeled something like "Connect with us on LinkedIn." **WCAG 2.4.4 (Link Purpose in Context).**

#### Testimonials Carousel

The Contact page also includes a testimonials carousel with 5 slides. The carousel buttons are labeled "Carousel Page 1 (Current Slide)," "Carousel Page 2," etc. I activated "Carousel Page 2" and the content updated — a new testimonial appeared, the status text changed from "slide 2 of 5" to "slide 3 of 5," and the button labels updated to reflect the new current slide. This carousel is keyboard-operable and provides state feedback, which is good.

However, I notice the numbering seems offset — clicking "Carousel Page 2" showed "slide 3 of 5" instead of "slide 2 of 5." This off-by-one discrepancy in the status text is confusing, similar to the homepage carousel issue.

#### Footer Contact Information

The footer (`contentinfo`) also provides contact information under the heading "Contact Us":
- Physical address: 2045 W Grand Ave Ste B PMB 37406, Chicago, Illinois 60612
- Phone: (312) 888-9651 (linked with `tel:`)

And under "Let's Get Social":
- Facebook (linked)
- Instagram (linked)
- LinkedIn (linked)

All footer links have clear, descriptive accessible names. The social media links are properly labeled with the platform name rather than generic "social media icon" text.

---

### Accessibility Violations Summary

| # | Issue | WCAG SC | Severity | Page(s) |
|---|-------|---------|----------|---------|
| 1 | **Missing `main` landmark** — No `main` landmark exposed in the accessibility tree. Screen reader users cannot jump directly to main content via landmark navigation. | 1.3.1 Info and Relationships | High | All pages |
| 2 | **Duplicate `banner` landmarks without unique labels** — Two `banner` landmarks on every page with no `aria-label` to distinguish them. Screen reader landmark navigation announces "banner" twice with no context. | 1.3.1 Info and Relationships | Medium | All pages |
| 3 | **Ambiguous repeated "Learn More" links** — Multiple links with identical accessible name "Learn More" with no programmatic context to distinguish them. Screen reader link lists show 8+ identical entries. | 2.4.4 Link Purpose (In Context) | High | Homepage, Services |
| 4 | **Unlabeled iframes** — Multiple iframes (CAPTCHA, embedded widgets) have no `title` attribute or accessible name. Screen reader announces "frame" with no context. | 4.1.2 Name, Role, Value | High | All pages |
| 5 | **CAPTCHA accessibility barrier** — An iframe-based CAPTCHA sits between form fields and Submit button. If it requires visual interaction, blind users cannot complete the form. | 1.1.1 Non-text Content | Critical | Homepage (embedded form), Services (embedded form), Contact |
| 6 | **Misleading carousel status text** — Homepage carousel announces "slide 5 to 7 of 3" which is nonsensical. Contact page carousel has off-by-one numbering. | 4.1.2 Name, Role, Value | Medium | Homepage, Contact |
| 7 | **Stat labels as h2 headings** — "Years in Business," "Projects," and "Clients" are marked as h2 but are metric labels, cluttering the heading outline for screen reader users. | 1.3.1 Info and Relationships | Low | Homepage |
| 8 | **Ambiguous "Connect" link** — Link labeled "Connect" on the Contact page provides no context about the destination (LinkedIn). | 2.4.4 Link Purpose (In Context) | Low | Contact |
| 9 | **Accordion buttons with excessive accessible names** — Buttons include entire paragraph content in their accessible names, making them extremely long and overwhelming. | 2.4.6 Headings and Labels | Medium | Services |
| 10 | **Empty list items and paragraphs** — Multiple list items contain only empty paragraph elements, creating unnecessary stops during navigation. | 1.3.1 Info and Relationships | Low | Homepage |
| 11 | **Headings nested inside tab elements** — h3 headings inside tab controls pollute the heading hierarchy, appearing in heading navigation even when their tabs aren't selected. | 1.3.1 Info and Relationships | Low | Homepage |
| 12 | **Multiple empty `alert` role elements** — Empty `alert` elements in forms may cause screen reader noise if they briefly receive content during validation. | 4.1.3 Status Messages | Low | All pages (forms) |

---

### Overall Experience Summary

As a legally blind user who depends entirely on VoiceOver and keyboard navigation, my overall experience on launchpadlab.com was **mixed — functional but with meaningful barriers**.

**What Works Well:**
- The site has a clear, mostly logical heading hierarchy that let me understand the page structure quickly. The single h1 per page and organized h2/h3 sections made headings-based navigation effective.
- Navigation links are clearly labeled with descriptive text (Services, Technologies, Industries, etc.) — no mystery meat navigation.
- The form fields on the contact page are properly labeled. I could fill out every text field without guessing what was expected.
- Client logos and most images have descriptive alt text.
- The phone number and email use `tel:` and `mailto:` links respectively, allowing direct activation.
- A "Skip to content" link is present as the first focusable element.
- The tab focus order follows a logical sequence from top to bottom across all pages.
- The navigation dropdown opened on click (not hover-only), making it keyboard accessible.
- Social media links in the footer are labeled with platform names.

**What Needs Improvement:**
- The absence of a `main` landmark is my biggest structural concern. Landmark navigation is one of the most efficient ways for screen reader users to orient themselves on a page, and missing `main` forces me to navigate linearly through the header every time.
- The duplicate unlabeled `banner` landmarks compound the landmark navigation problem.
- The repeated "Learn More" links are a frustrating pattern I encounter on many sites. When I pull up my links list, I see 8 identical entries with no way to distinguish them. This forces me to navigate contextually, which is slower and more cognitively demanding.
- The CAPTCHA iframe is potentially the most serious barrier. If I cannot complete the CAPTCHA, I cannot submit the contact form — the primary conversion action on the site. While alternative contact methods exist (email, phone), the form is positioned as the primary CTA, and blocking screen reader users from it is a significant equity issue.
- The carousel status text errors ("slide 5 to 7 of 3") suggest the carousel widget was not thoroughly tested with assistive technology.

**Bottom Line:**
I was able to navigate the site, understand what LaunchPad Lab does, and locate the contact form. The content is well-written and the heading structure mostly supports efficient navigation. However, the missing `main` landmark, CAPTCHA barrier, and ambiguous link names represent real obstacles. I would likely resort to calling (312) 888-9651 or emailing contact@launchpadlab.com rather than struggling with the contact form's CAPTCHA. For a company that lists accessibility in their FAQ ("How do you ensure accessibility in digital product development?"), there is clear room for improvement on their own site.
