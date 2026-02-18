# Accessibility & Usability Report: AI-Curious Business Leader Persona

**Persona:** Patricia Langford — 52-year-old VP of Operations, regional logistics company (400 employees)  
**Evaluation Date:** February 18, 2026  
**Site:** https://launchpadlab.com/  
**Navigation Method:** Mouse-only, desktop browser  
**Assistive Context:** Reading glasses user; relies on clear visual hierarchy and adequate text sizing  

---

## Executive Summary

LaunchPad Lab's website presents a professional appearance with strong content in areas like case studies and AI service descriptions. However, the browsing session revealed **significant navigation reliability issues**, **missing contact accessibility**, and **content gaps that alienate non-tech-sector prospects**. The most critical finding is that the primary navigation behaves unpredictably — dropdown menus and page navigation conflict with each other, causing the user to land on unexpected pages. For a company that builds digital products, this undermines credibility. Additionally, the absence of a dedicated contact page, no visible email address, and heavy Salesforce-specific branding limit accessibility for a broad business audience.

**Overall Assessment:** The site has strong foundational content but suffers from navigation reliability, information architecture gaps, and content accessibility issues that create real barriers for methodical, non-technical business decision-makers.

---

## Issues by Category

### 1. Navigation & Wayfinding

#### 1.1 Dropdown Navigation Conflicts with Page Navigation
- **Description:** Top-level navigation items with sub-menus ("Services," "Industries") exhibit unpredictable behavior. Clicking "Services" simultaneously opens a dropdown menu and navigates to a sub-page (Mobile App Development) rather than a Services overview. A second click on "Services" navigated to the "Our Work" (Case Studies) page instead. Clicking "Industries" opened a dropdown but did not navigate at all.
- **Location:** Global navigation bar, all pages
- **Severity:** **High**
- **Impact:** Users cannot reliably navigate to intended pages. A methodical user clicking through the menu will arrive at unexpected destinations, creating confusion and eroding trust.
- **Recommendation:** Separate the dropdown trigger from the page link. Use a chevron/arrow icon as the dropdown trigger and make the text link navigate to the parent page. Alternatively, ensure clicking the parent link always navigates to an overview page and use hover (or a separate button) for the dropdown. Test across multiple click sequences to ensure consistent behavior.

#### 1.2 No Dedicated Contact Page
- **Description:** The "Contact" link in the main navigation (href: `/contact/`) loads the homepage rather than a standalone contact page. The intent appears to be scrolling to the contact form at the bottom of the homepage, but when navigating from other pages, users see the top of the homepage with no indication they have reached a contact section.
- **Location:** "Contact" link in global navigation
- **Severity:** **High**
- **Impact:** Users seeking contact information are redirected without reaching a dedicated contact experience. Critical contact details (phone, address) are only in the footer and require scrolling to discover.
- **Recommendation:** Create a dedicated `/contact/` page with phone number, email address, physical address, a map, and the contact form. This page should also appear when the nav "Contact" link is clicked.

#### 1.3 No Breadcrumb Navigation
- **Description:** There are no breadcrumbs on any page to indicate the user's position within the site hierarchy. Sub-pages (e.g., AI Automation under Services, Bullhorn under Our Work) do not show navigational context.
- **Location:** All interior pages
- **Severity:** **Medium**
- **Impact:** Users lose orientation, especially after experiencing the navigation issues described above. Without breadcrumbs, there is no way to confirm which section of the site you are in.
- **Recommendation:** Add breadcrumb navigation to all interior pages (e.g., Home > Services > AI Automation & Agentic AI).

#### 1.4 Services Menu Has No Overview Landing Page
- **Description:** There is no general "Services" overview page that summarizes all offerings. The "Services" link in navigation either opens a dropdown or navigates to a random sub-service page. The "View Services" link within the dropdown does appear to exist but the parent link behavior overrides it.
- **Location:** Services section of navigation
- **Severity:** **Medium**
- **Impact:** Users who want a high-level understanding of all services before drilling into specifics cannot access an overview page through normal navigation.
- **Recommendation:** Ensure `/services/` loads a dedicated overview page that lists all services with brief descriptions and links to detail pages.

---

### 2. Contact & Communication Accessibility

#### 2.1 No Email Address Displayed Anywhere
- **Description:** There is no general email address (e.g., info@, hello@, sales@) visible on any page of the site — not in the footer, not on the About page, not in the contact form area. The only contact methods are a phone number in the footer and contact forms.
- **Location:** Site-wide (footer, About page, Contact section)
- **Severity:** **High**
- **Impact:** Business decision-makers who prefer email as an initial contact method are forced into form submissions or phone calls. Forms feel impersonal and uncertain ("Will anyone read this?"). This creates a barrier for cautious prospects who want to ask a specific question before committing to a call.
- **Recommendation:** Display a general contact email address in the footer and on the contact section. Consider adding a direct email for the sales/business development team.

#### 2.2 Phone Number Only in Footer
- **Description:** The phone number (312) 888-9651 appears only in the site footer, below all page content. It is not featured in the header, on a contact page, or in any prominent position.
- **Location:** Footer, all pages
- **Severity:** **Medium**
- **Impact:** Users must scroll to the very bottom of every page to find the phone number. On content-heavy pages (like the Bullhorn case study), this requires significant scrolling.
- **Recommendation:** Include the phone number in the header or in a sticky contact bar. Also feature it prominently on a dedicated contact page.

#### 2.3 Repetitive Contact Form on Every Page
- **Description:** An identical contact form (First Name, Last Name, Company Email, Company, How Can We Help You?) appears at the bottom of every page visited — homepage, AI Automation, Bullhorn case study, About Us, Industries.
- **Location:** Bottom of all pages
- **Severity:** **Low**
- **Impact:** While having a form available is not inherently bad, the repetition across every single page feels excessive and pushy. It contributes to a sense that the site is more interested in capturing leads than providing information. The forms also include multiple empty `alert` elements that could cause issues for screen reader users.
- **Recommendation:** Consider showing the full form on key conversion pages (homepage, contact page, services pages) and using a simpler CTA (e.g., "Get in Touch" button linking to the contact page) on content pages like case studies and blog posts.

---

### 3. Content & Readability

#### 3.1 Buzzword-Heavy Language Reduces Clarity
- **Description:** Multiple sections use marketing buzzwords without concrete explanation. Examples: "Game-Changing Digital Products," "autonomous digital workforce," "bespoke, redefining experiences," "ship to market fast," "agentic AI." The term "Agentic AI" in particular is used extensively without a plain-language definition on the main services cards.
- **Location:** Homepage services cards, AI Automation page, section headings throughout
- **Severity:** **Medium**
- **Impact:** Non-technical business decision-makers — the very audience the site aims to attract — may find the language off-putting or unclear. Buzzwords without substance erode trust for skeptical evaluators. The FAQ section on the AI Automation page does have a "What is agentic AI?" question, but it is collapsed by default and easy to miss.
- **Recommendation:** Provide plain-language explanations alongside or instead of jargon in primary content areas. Use the detailed, specific language found in the Bullhorn case study as a model for the rest of the site. Consider adding a brief parenthetical or tooltip for terms like "Agentic AI."

#### 3.2 Inconsistent Statistics Across Pages
- **Description:** The homepage states "12+ Years in Business." The About page states "13+ Years in Business." Both pages list "730+ Projects" and "240+ Clients," so the year discrepancy appears to be an oversight.
- **Location:** Homepage statistics section, About Us statistics section
- **Severity:** **Medium**
- **Impact:** For detail-oriented evaluators, inconsistencies in basic facts undermine credibility. If a vendor cannot keep their own statistics consistent, it raises questions about their attention to detail in client work.
- **Recommendation:** Audit all statistics across the site and ensure consistency. Consider using a dynamic approach (e.g., calculating years from founding date) to prevent future drift.

#### 3.3 Salesforce Dependency Unclear in AI Services
- **Description:** The AI Automation page heavily features Salesforce Agentforce branding. The "Agentforce Quick Start Program," "Watch the Talk" webinar, and related content all reference Salesforce. It is not clear whether AI automation services are available to companies that do not use Salesforce.
- **Location:** AI Automation page (/services/ai-automation-agentforce/)
- **Severity:** **High**
- **Impact:** Prospects who do not use Salesforce may self-select out, assuming the services are not relevant to them. This represents lost business opportunities. The URL itself contains "agentforce," reinforcing the Salesforce-specific impression.
- **Recommendation:** Clearly delineate Salesforce-specific AI services from platform-agnostic AI capabilities. Consider creating separate sections or pages: one for Agentforce/Salesforce AI and one for general AI automation and consulting. Add a statement addressing non-Salesforce environments.

#### 3.4 No Logistics/Supply Chain/Manufacturing Industry Representation
- **Description:** The Industries page lists nine industries: Financial Services, Private Equity, Healthcare, Professional Services, Insurance, Technology, Legal, Knowledge/Education, and Social Impact. There is no mention of logistics, supply chain, manufacturing, transportation, or operations-heavy industries. The hero text mentions "manufacturing" once in passing but there is no dedicated page.
- **Location:** Industries page, Industries navigation dropdown
- **Severity:** **Medium**
- **Impact:** Prospects from underrepresented industries (logistics, manufacturing, retail, etc.) see no evidence that LaunchPad Lab understands their domain. The site claims to be "industry-agnostic" but the industry pages contradict this by only representing a subset of sectors. This creates a disconnect between messaging and content.
- **Recommendation:** Either expand industry pages to include operations-heavy sectors (manufacturing, logistics, supply chain) or restructure the Industries section around business challenges (e.g., "Operations Optimization," "Compliance & Regulatory") rather than vertical names. Highlight any relevant case studies from adjacent industries.

---

### 4. Interactive Elements & Components

#### 4.1 Carousel Counter Displays Incorrect Text
- **Description:** The case studies carousel on the homepage and About page displays the text "slide 5 to 7 of 3." This counter is nonsensical — it claims to show slides 5-7 out of a total of 3.
- **Location:** Homepage case studies carousel, About page carousel
- **Severity:** **Medium**
- **Impact:** While likely hidden visually, this text is exposed in the accessibility tree and would be read by screen readers, creating confusion. It also indicates a logic error in the carousel component.
- **Recommendation:** Fix the carousel counter logic to accurately reflect the current slide position and total count (e.g., "slide 1 of 3"). Ensure the counter is properly updated when carousel pagination buttons are clicked.

#### 4.2 Multiple Empty Alert Elements on Contact Forms
- **Description:** Each contact form contains multiple `alert` role elements that appear to be empty — likely used for client-side validation messages. There is one `alert` after each form field and two additional ones after the submit button.
- **Location:** Contact forms on all pages
- **Severity:** **Medium**
- **Impact:** Screen readers may announce empty alert regions, creating noise and confusion. When validation errors do appear, the multiple alert elements could result in a flood of announcements.
- **Recommendation:** Use `aria-live` regions more judiciously. Consider a single validation summary area or apply `alert` roles only when error content is present. Ensure validation messages are clear and specific.

#### 4.3 Tab Panels Appear Empty in Accessibility Tree
- **Description:** The "Problems We Solve" tabbed interface on the homepage has tab panels for each category (Operational Efficiency, Modern Technology, Customer Engagement, etc.), but the panel content nodes appear empty in the accessibility tree.
- **Location:** Homepage "Ship Game-Changing Digital Products to Market Fast" section
- **Severity:** **Medium**
- **Impact:** Users navigating with assistive technology may find tab panels that appear to contain no content. Even for sighted users, the tab content was generic and offered little detail.
- **Recommendation:** Ensure tab panel content is properly associated with its tab and rendered in the accessibility tree. Add meaningful, detailed content to each tab panel.

#### 4.4 Unlabeled Iframes
- **Description:** Multiple `iframe` elements appear throughout the site without descriptive titles or labels. These appear on the homepage (possibly a video embed), About page (video), and within contact forms (likely reCAPTCHA).
- **Location:** Homepage, About page, all contact forms
- **Severity:** **Medium**
- **Impact:** Screen reader users encounter iframes without context about what they contain. This makes it difficult to decide whether to interact with them.
- **Recommendation:** Add descriptive `title` attributes to all iframes (e.g., `title="Company overview video"`, `title="reCAPTCHA verification"`).

#### 4.5 FAQ Sections Collapsed by Default with Minimal Discoverability
- **Description:** FAQ sections on the AI Automation page and Industries page are rendered as collapsed `group` elements. The questions are visible but answers require interaction to reveal. There is no visual cue (beyond the question text) indicating these are expandable.
- **Location:** AI Automation page, Industries page
- **Severity:** **Low**
- **Impact:** Users scanning pages quickly may miss valuable information in FAQ sections. The collapsed state reduces content discoverability, especially for users who are evaluating the company and would benefit from seeing answers to common questions.
- **Recommendation:** Consider showing the first 1-2 FAQ answers expanded by default. Ensure expand/collapse controls have clear visual indicators (e.g., +/- icons or chevrons) and proper ARIA attributes.

---

### 5. Information Architecture

#### 5.1 Case Study Page Lacks Filtering by Service Type
- **Description:** The "Our Work" page lists 40+ case studies with only an "Industries" filter. There is no way to filter by service type (e.g., AI, Salesforce, Mobile) or by problem solved.
- **Location:** /work/ page
- **Severity:** **Medium**
- **Impact:** A prospect interested specifically in AI case studies must scan through dozens of case studies to identify relevant ones. This is time-consuming for methodical evaluators who want targeted evidence.
- **Recommendation:** Add filtering options for service type, technology, and/or problem category in addition to the existing industry filter. Consider a search function.

#### 5.2 Leadership Team Lacks Direct Contact Information
- **Description:** The About page lists 15 leadership team members with their names, titles, and LinkedIn profile links. No email addresses or direct phone numbers are provided for any team member.
- **Location:** About page, "Meet Our Leadership Team" section
- **Severity:** **Low**
- **Impact:** Business prospects who want to reach a specific person (e.g., VP of Client Growth, Business Development Manager) cannot do so directly. They must use LinkedIn, fill out the generic form, or call the main number.
- **Recommendation:** Consider adding email addresses for customer-facing team members (e.g., Head of Sales, Business Development Manager) or at minimum a direct "Schedule a Call" link for sales contacts.

#### 5.3 PDF Downloads Without Warning
- **Description:** The "Download Overview" link on the AI Automation page links directly to a PDF file (Agentforce-Quickstart-Program-2.0-6-weeks.pdf) without indicating the file type or size.
- **Location:** AI Automation page
- **Severity:** **Low**
- **Impact:** Users clicking the link may be surprised by a PDF download rather than a web page. This can be disorienting, especially for users on slower connections or those who prefer to stay within the browser.
- **Recommendation:** Add file type and size indicators next to download links (e.g., "Download Overview (PDF, 2.4 MB)"). Consider offering a web-based preview alongside the PDF option.

---

### 6. Visual & Structural Accessibility

#### 6.1 Empty List Items and Paragraphs in Client Logo Sections
- **Description:** Client logo list items and Clutch award badge list items contain empty `paragraph` elements. Some badge items appear to be missing images entirely, leaving blank spaces in the layout.
- **Location:** Homepage client logos section, About page awards section
- **Severity:** **Low**
- **Impact:** Empty elements add noise to the accessibility tree. Missing images create visual gaps that may confuse sighted users or suggest broken content.
- **Recommendation:** Remove empty paragraph elements from list items. Ensure all badge/logo items either have properly loaded images or are excluded from the rendered output.

#### 6.2 Heading Hierarchy Issues
- **Description:** Statistics like "Years in Business," "Projects," and "Clients" are marked as `h2` headings. On the AI Automation page, stat descriptions like "reduction in repetitive manual work" and "faster response across service and support channels" are also `h2` headings. These are not true section headings but decorative stat labels.
- **Location:** Homepage, About page, AI Automation page statistics sections
- **Severity:** **Low**
- **Impact:** Improper heading hierarchy confuses screen reader users who navigate by headings. Using `h2` for decorative statistics inflates the heading count and reduces the utility of heading navigation.
- **Recommendation:** Use semantically appropriate elements for statistics (e.g., `<p>` with `aria-label` or `<dl>` definition lists) rather than heading tags. Reserve heading tags for actual section titles.

#### 6.3 Carousel Pagination Lacks Descriptive Labels
- **Description:** Carousel pagination buttons are labeled "Carousel Page 1 (Current Slide)," "Carousel Page 2," and "Carousel Page 3." While functional, these labels do not describe what content each slide contains.
- **Location:** Homepage and About page carousels
- **Severity:** **Low**
- **Impact:** Users navigating by buttons or using screen readers cannot determine which case study is on which slide without cycling through them.
- **Recommendation:** Add more descriptive labels to carousel pagination (e.g., "Slide 1: Millennium Trust Company case study"). Consider adding slide titles to pagination indicators.

---

## Summary of Issues by Severity

| Severity | Count | Key Issues |
|----------|-------|------------|
| **High** | 4 | Dropdown navigation conflicts, no dedicated contact page, no email address, Salesforce dependency unclear |
| **Medium** | 10 | No breadcrumbs, no services overview page, buzzword-heavy language, inconsistent statistics, carousel counter error, empty alerts on forms, empty tab panels, unlabeled iframes, no case study filtering by service, missing industry representation |
| **Low** | 6 | Repetitive contact forms, collapsed FAQs, no team contact info, PDF download without warning, empty list elements, heading hierarchy, carousel pagination labels |

## Overall Accessibility Score

**5.5 / 10**

The site presents well visually and contains genuinely valuable content (particularly the detailed case studies and the AI service descriptions). However, the navigation reliability issues are a fundamental barrier — a user who cannot predict where clicking a menu item will take them will lose trust quickly. The absence of basic contact accessibility (no email, no dedicated contact page, phone buried in footer) creates unnecessary friction for business decision-makers. The content gaps (no logistics/manufacturing representation, unclear Salesforce dependencies) further limit the site's effectiveness for a significant segment of potential prospects.

**Strengths:**
- Professional visual design and branding
- Detailed, credible case studies (Bullhorn in particular)
- Clear service descriptions on the AI Automation page
- Consistent footer with contact info on every page
- Strong client roster builds credibility
- Free AI Opportunity Workshop is an accessible entry point

**Priority Fixes:**
1. Fix navigation dropdown/link conflict behavior (High)
2. Create a dedicated contact page with email, phone, and address (High)
3. Add a visible email address site-wide (High)
4. Clarify Salesforce-agnostic vs. Salesforce-specific AI services (High)
5. Add breadcrumb navigation to all interior pages (Medium)
6. Fix carousel counter text ("slide 5 to 7 of 3") (Medium)
7. Audit and standardize statistics across all pages (Medium)
8. Expand industry representation or restructure around business challenges (Medium)
