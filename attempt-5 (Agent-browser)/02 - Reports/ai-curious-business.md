# Accessibility & Usability Report: AI-Curious Business Executive Persona

**Persona:** Margaret Sullivan — 57-year-old President of a mid-size insurance brokerage  
**Site Evaluated:** https://launchpadlab.com/  
**Date:** February 18, 2026  
**Evaluator:** Automated persona-driven assessment  
**Scope:** Homepage, Services, AI Automation, Industries, Insurance, Our Work, Case Studies, Contact, About Us  

---

## Executive Summary

LaunchPad Lab's website presents a professional, well-structured digital presence with strong credibility signals and a growing body of AI-related content. However, for AI-curious but non-technical business executives — a primary target audience for AI consulting services — the site presents significant usability barriers related to **unexplained jargon, disconnected content silos, unattributed claims, and a lack of guided pathways for AI-naive visitors.**

The site does many things well: it has a dedicated insurance industry page with concrete service descriptions, a compelling healthcare insurance AI case study, a clear engagement process (free workshop → proof of concept → deployment), and strong trust markers (13+ years, 240+ clients, Clutch ratings, recognizable logos).

The most critical issues are:
1. **AI jargon is pervasive and unexplained**, alienating the exact executives the AI services are designed to attract.
2. **AI content and industry content exist in separate silos** — there is no unified "AI for Insurance" narrative.
3. **Key statistics are unattributed**, undermining credibility with skeptical executives.
4. **The contact experience is generic** and does not differentiate enterprise-level inquiries.
5. **FAQ sections appear non-functional or difficult to expand**, hiding valuable educational content.

**Overall assessment:** The site would convert a tech-savvy buyer more effectively than an AI-curious executive. For the Margaret Sullivan persona, it requires 25+ minutes of cross-referencing multiple pages to assemble a coherent picture — a significant friction barrier for a comparison-shopping executive evaluating 3-4 firms.

---

## Issues

### Issue 1: Pervasive AI Jargon Without Inline Definitions

**Description:** Terms like "agentic AI," "autonomous digital workforce," "business logic codification," "repeatable prompts," "LLM," "RAG," "data pipelines," and "AI agents" appear throughout the AI Automation page and homepage without plain-language definitions. For an executive who is AI-curious but AI-illiterate, these terms are meaningless or anxiety-inducing.

**Location:** Homepage (hero section, services cards), AI Automation & Agentic AI page (throughout), Services page (section headings)

**Specific examples:**
- Homepage: "AI Automation & Agentic AI — Enabling an autonomous digital workforce"
- AI page: "Train digital agents to act independently—accessing data, following logic, and escalating when needed"
- AI page: "Convert human knowledge into repeatable prompts and workflows that scale across your org"
- AI page: "Structured data pipelines that power real-time decisions"

**Impact on persona:** Margaret cannot determine whether the described services are relevant to her business because she cannot understand what they mean. She reads carefully but encounters a wall of jargon that makes her feel excluded — the exact opposite of what an AI consulting firm should convey. This is the single largest barrier to conversion for non-technical executives.

**Suggested fix:** Add inline parenthetical definitions or tooltip-style explanations for every AI-specific term on first use. Example: "Agentic AI (software agents that can handle specific business tasks automatically, like processing claims or answering customer questions, with human oversight when needed)." Consider adding a "What is AI? A Business Leader's Guide" page linked from the AI Automation section.

**Priority:** **HIGH**

---

### Issue 2: AI Content and Industry Content Are Siloed

**Description:** The AI Automation page discusses AI capabilities broadly but never mentions insurance or financial services specifically. The Insurance industry page describes insurance-relevant services (quote-to-bind, claims, compliance) but barely mentions AI. A business executive looking for "AI for my insurance company" must visit both pages and mentally combine them — a significant cognitive burden.

**Location:** AI Automation & Agentic AI page, Insurance Industry page

**Impact on persona:** Margaret came to the site looking for a company that can help her implement AI in her insurance brokerage. She found relevant AI capabilities on one page and insurance expertise on another, but no page that brings them together. This forced her to assemble the narrative herself across 6+ pages over 25 minutes. A competitor with a single "AI for Insurance" page would immediately gain an advantage.

**Suggested fix:** Create a dedicated "AI for Insurance" page (or section within the Insurance page) that maps AI capabilities to insurance-specific use cases. Example content: "Here are 5 ways AI can transform your brokerage: 1) Automated claims intake that reduces processing from 3 days to 2 hours. 2) AI-powered underwriting recommendations. 3) Intelligent policyholder self-service. 4) Compliance documentation automation. 5) Predictive analytics for risk assessment."

**Priority:** **HIGH**

---

### Issue 3: Unattributed Statistics Undermine Credibility

**Description:** The AI Automation page displays prominent statistics — "60%+ reduction in repetitive manual work," "3x faster response across service and support channels," "6 weeks to deploy a working AI solution" — without attributing them to specific clients, case studies, or methodologies. The Insurance page shows "140% increase in online conversions," "5,000+ insurance agents supported," and "$2M in projected profit" similarly without clear attribution to named companies.

**Location:** AI Automation page (stats section), Insurance Industry page (stats section), Services page (speed metrics)

**Impact on persona:** Margaret is a skeptical, experienced executive who has seen tech fads come and go. Unattributed statistics feel like marketing claims rather than evidence. She specifically looks for "proof that AI has delivered measurable results for companies like hers." Without knowing where the 60% reduction came from, she cannot evaluate whether it's relevant to her business or whether it's aspirational marketing.

**Suggested fix:** Link each statistic to a specific case study or client. Example: "60%+ reduction in repetitive manual work (based on Bullhorn case study)" with a hyperlink to the full case study. For statistics that represent averages or projections, state the methodology: "Based on results across 15 AI automation engagements in 2024-2025."

**Priority:** **HIGH**

---

### Issue 4: FAQ Sections Appear Non-Functional or Hard to Expand

**Description:** Multiple pages (AI Automation, Services, Industries, Insurance) feature FAQ sections with highly relevant questions (e.g., "What is agentic AI?", "Do I need to change my tech stack?", "What's different about your AI services?"). However, these FAQ items appeared as collapsed group elements that could not be easily expanded during the browsing session. The questions themselves suggest the site anticipated the persona's exact concerns, but the answers were inaccessible.

**Location:** AI Automation page (FAQ section), Services page (FAQ section), Industries page (FAQ section), Insurance page (FAQ section)

**Impact on persona:** Margaret would have found enormous value in answers to "What is agentic AI?" and "Do I need to change my tech stack?" — these address her top concerns directly. If she couldn't expand these sections, the site wasted its best opportunity to educate and reassure her. Even if they do expand with a click, the collapsed-by-default state means a reader who is scrolling through might not realize they're interactive.

**Suggested fix:** Ensure FAQ accordion elements are fully accessible and clearly interactive (visible expand/collapse icons). Consider displaying the first 1-2 FAQ items in an expanded state by default to signal interactivity and immediately provide value. Test with keyboard navigation and screen readers to ensure accessibility.

**Priority:** **HIGH**

---

### Issue 5: Generic Contact Form Doesn't Serve Enterprise Inquiries

**Description:** The contact form across all pages (Contact page, footer forms on every page) is a generic 5-field form: First Name, Last Name, Company Email, Company, and "How Can We Help You?" There is no way to indicate the nature or seriousness of the inquiry, the person's role, the desired service, or preferred contact method. Every page's form is identical.

**Location:** Contact page, all page footers with embedded contact forms

**Impact on persona:** Margaret is a company president making a potentially six-figure investment decision. Being presented with the same generic form as someone asking about a small website project is deflating. She expects the contact experience to reflect the seriousness of an enterprise engagement. There's no way to schedule a call directly, no option to specify her role (CEO/President vs. marketing coordinator), and no way to indicate she's specifically interested in AI services.

**Suggested fix:** Add optional fields for: Role/Title, Company Size, Specific Service Interest (dropdown: AI Automation, Web Development, Mobile, Salesforce, etc.), and Preferred Contact Method (call, email, video). Consider adding a "Schedule a Call" button with calendar integration (Calendly or similar) for executive-level visitors. On the AI pages specifically, use the existing "Book an AI Automation Assessment" CTA more prominently and link it to a dedicated scheduling flow.

**Priority:** **MEDIUM**

---

### Issue 6: Heavy Salesforce/Agentforce Coupling Creates Confusion

**Description:** The AI Automation page heavily features Salesforce's "Agentforce" product — including an "Agentforce Quick Start Program," links to Agentforce webinars, and Agentforce-specific blog posts. This creates the impression that LaunchPad Lab's AI offering is primarily (or exclusively) a Salesforce implementation service rather than a broader AI consulting practice.

**Location:** AI Automation page (Agentforce Quick Start section, related content section), Homepage (Salesforce Partner badge in footer)

**Impact on persona:** Margaret uses Salesforce for her CRM, so this isn't entirely irrelevant. But she doesn't know whether her AI needs are Salesforce-specific. If she needs to automate document processing (like the healthcare insurance case study), that may not involve Salesforce at all. The heavy Agentforce focus makes her wonder: "Is this just a Salesforce shop, or can they help me with AI more broadly?" This ambiguity creates hesitation.

**Suggested fix:** Clearly delineate between Salesforce-specific AI offerings (Agentforce) and platform-agnostic AI capabilities. Add a brief section: "Our AI solutions work with your existing technology stack, whether you use Salesforce, custom systems, or other platforms." Show case studies that use non-Salesforce technology (the healthcare insurance case study uses OpenAI API, MS SQL Server — highlight this diversity).

**Priority:** **MEDIUM**

---

### Issue 7: Case Studies Use Anonymous Company Names

**Description:** Several case studies use anonymized company names: "Healthcare Insurance Platform," "Financial Services Firm," "Actuarial Firm," "Biotech Organization," "Wealth Management Firm." While understandable for confidentiality reasons, this reduces the trust-building value of case studies for skeptical executives.

**Location:** Our Work page, Insurance Industry page (case study references)

**Impact on persona:** Margaret values trust signals — recognizable names, logos, and testimonials from executives at her level. Anonymous case studies feel less credible than named ones. When she reads about a "Healthcare Insurance Platform" reducing claim review from 3-4 days to 24 hours, she can't verify the claim or assess whether that company is comparable to hers. The anonymity reduces the persuasive power of otherwise excellent case studies.

**Suggested fix:** Where possible, obtain client permission to use company names. For cases requiring anonymity, provide more context: industry sub-segment, company size, geography, and the executive title of the sponsor. Example: "A mid-size healthcare insurance technology company (500 employees, Midwest region) reduced claim review turnaround from 3-4 days to under 24 hours." Consider adding video testimonials from willing clients.

**Priority:** **MEDIUM**

---

### Issue 8: No Pricing Guidance Anywhere on the Site

**Description:** There is no pricing information, cost ranges, or even pricing philosophy described anywhere on the site. No "starting at" figures, no "typical engagement ranges," no "factors that influence pricing" content.

**Location:** Site-wide (absent from all pages)

**Impact on persona:** Margaret's board has approved investment in "digital modernization" but she needs to understand the order of magnitude before pursuing a conversation. Is this a $50,000 engagement or a $500,000 engagement? She can't make a recommendation to her board without some sense of the financial commitment. The complete absence of pricing guidance forces her into an awkward position: she must start a sales conversation just to understand if the company is in her budget range.

**Suggested fix:** Add a pricing philosophy page or section. It doesn't need to list exact prices, but could say: "Typical AI automation engagements range from $X to $Y depending on scope and complexity. Our free AI Opportunity Workshop helps us scope the right engagement for your budget and goals." This sets expectations without committing to specific pricing.

**Priority:** **MEDIUM**

---

### Issue 9: Testimonials Lack Executive-Level Insurance/Financial Voices

**Description:** The testimonials on the Contact page are from a Vice President of Apex Leaders and from Amplify Credit Union. While positive, none come from insurance industry executives, C-suite leaders, or company presidents. There are no testimonials from people at Margaret's decision-making level in her industry.

**Location:** Contact page (testimonial carousel)

**Impact on persona:** Margaret specifically looks for testimonials from "people at her level (executives, founders)" and in her industry. A VP of a sports leadership company, while positive, doesn't build the specific confidence she needs. She needs to see that other company presidents or insurance executives have had a good experience.

**Suggested fix:** Actively solicit testimonials from C-suite clients in insurance, financial services, and professional services. Feature these prominently on the Contact page and the Insurance industry page. Include the speaker's title, company type, and a specific outcome: "Margaret-like executive at a 200-person brokerage saw 40% reduction in claims processing time."

**Priority:** **MEDIUM**

---

### Issue 10: Inconsistent "Years in Business" Statistic

**Description:** The homepage displays "12+ Years in Business" while the About Us page displays "13+ Years in Business." The company was founded in 2012, making the correct figure 13+ years as of 2026. This inconsistency, while minor, can erode trust with detail-oriented executives.

**Location:** Homepage (statistics section), About Us page (statistics section)

**Impact on persona:** Margaret reads carefully and notices details. An inconsistency in a basic fact like years in business might make her wonder about the accuracy of other claims on the site.

**Suggested fix:** Audit all instances of the "years in business" stat across the site and make them consistent. Consider using a dynamic calculation based on the founding year to prevent future drift.

**Priority:** **LOW**

---

### Issue 11: "ChatGPT" Name-Drop on About Page Feels Casual

**Description:** The About page's "On the Cutting Edge" section says: "From AI like ChatGPT to Salesforce products like Agentforce, we're on the cutting edge to bring you into the future." Name-dropping ChatGPT as an example of AI expertise is like a construction company saying "we use hammers" — it demonstrates awareness of a popular consumer tool, not deep expertise.

**Location:** About Us page ("On the Cutting Edge" section)

**Impact on persona:** Margaret has heard of ChatGPT but doesn't consider it a professional tool. Referencing it in the context of enterprise AI services feels slightly unserious and may actually undermine the company's positioning as an expert AI consulting firm. She'd rather hear about proprietary frameworks, methodologies, or enterprise-grade AI capabilities.

**Suggested fix:** Replace the ChatGPT reference with a description of actual AI capabilities: "From custom AI document processing to enterprise-scale automation with Salesforce Agentforce, we bring cutting-edge AI solutions that deliver measurable business outcomes." Focus on what the company builds, not consumer AI brands.

**Priority:** **LOW**

---

### Issue 12: Every Page Has the Same Contact Form in the Footer

**Description:** Every page on the site includes an identical contact form in the footer section with the same heading ("Let's Build Something Great" or "Ready to Build Something Great?") and the same five fields. While having a form available is convenient, the repetition without contextual adaptation creates a missed opportunity.

**Location:** Footer of every page visited (Homepage, Services, AI Automation, Industries, Insurance, Our Work, Contact, About)

**Impact on persona:** When Margaret arrives at the Insurance page form, it says "Let's Redefine Your Insurance Experience — Book a Discovery Call to Explore Digital Transformation for Your Organization." This is well-tailored. But most other pages use generic text. The AI Automation page says "Ready to Unlock ROI with AI? — Book an AI Automation Workshop Today!" which is better. The inconsistency suggests some pages have been optimized while others haven't.

**Suggested fix:** Ensure every page's contact form CTA is contextually relevant to the page content. The AI page's CTA is already good; replicate this approach for all pages. Consider pre-filling a hidden field with the page source so the sales team knows which page drove the inquiry.

**Priority:** **LOW**

---

### Issue 13: No "AI Readiness Assessment" or Self-Service Educational Content

**Description:** For an AI-curious but AI-illiterate executive, there is no self-guided educational path. No "AI Readiness Assessment" quiz, no "Is AI Right for Your Business?" checklist, no downloadable guide titled "AI for Business Leaders: What You Need to Know." The site assumes visitors will navigate to specific service pages and read marketing copy.

**Location:** Site-wide (absent)

**Impact on persona:** Margaret doesn't know what she doesn't know. She'd benefit enormously from a 5-question self-assessment ("Do your teams spend more than 20 hours/week on manual data entry? → AI automation could save you X hours") that helps her self-qualify and builds confidence that the company understands her starting point. Without this, she must rely entirely on sales conversations to understand whether AI is right for her.

**Suggested fix:** Create an interactive "AI Readiness Assessment" or downloadable "AI for Business Leaders" guide prominently linked from the homepage and AI Automation page. This serves as both an educational tool and a lead generation mechanism. The existing "Discovery Space Navigator" partially fills this role but is positioned as a paid engagement tool, not a self-service educational resource.

**Priority:** **MEDIUM**

---

### Issue 14: Carousel Navigation on Homepage Case Studies Limits Discoverability

**Description:** The homepage case studies section uses a carousel (slider) that shows only 3 case studies at a time with small dot-navigation buttons. The carousel is labeled "slide 5 to 7 of 3" in the accessibility tree, which is confusing and potentially a bug.

**Location:** Homepage (case studies carousel section)

**Impact on persona:** Margaret reads deliberately and may not realize the dots are navigable. She may only see 3 case studies and assume that's all there is. The "slide 5 to 7 of 3" label is nonsensical to screen reader users and suggests an accessibility bug. The carousel format inherently reduces content visibility compared to a scrollable list.

**Suggested fix:** Consider replacing the carousel with a static grid or scrollable list showing all featured case studies. If keeping the carousel, fix the accessibility label to accurately reflect slide position (e.g., "slide 1 of 3"), add left/right arrow navigation buttons that are clearly visible, and ensure the total number of case studies is communicated.

**Priority:** **LOW**

---

## Summary Table

| # | Issue | Location | Impact Level | Priority |
|---|-------|----------|-------------|----------|
| 1 | AI jargon without inline definitions | Homepage, AI Automation page, Services page | Blocks comprehension for target audience | **HIGH** |
| 2 | AI and insurance content are siloed | AI Automation page, Insurance page | Forces cross-referencing across 6+ pages | **HIGH** |
| 3 | Unattributed statistics | AI Automation page, Insurance page, Services page | Undermines credibility with skeptical executives | **HIGH** |
| 4 | FAQ sections hard to expand / non-functional | AI Automation, Services, Industries, Insurance pages | Hides educational content the persona needs most | **HIGH** |
| 5 | Generic contact form for all inquiry types | Contact page, all page footers | Doesn't serve enterprise-level inquiries | **MEDIUM** |
| 6 | Heavy Salesforce/Agentforce coupling | AI Automation page, Homepage footer | Creates confusion about breadth of AI services | **MEDIUM** |
| 7 | Anonymous case study company names | Our Work page, Insurance page | Reduces trust-building value of evidence | **MEDIUM** |
| 8 | No pricing guidance anywhere | Site-wide | Blocks budget conversations with boards | **MEDIUM** |
| 9 | No executive-level insurance testimonials | Contact page | Missing peer validation for decision-makers | **MEDIUM** |
| 10 | Inconsistent "years in business" stat | Homepage vs. About Us | Erodes trust with detail-oriented readers | **LOW** |
| 11 | ChatGPT name-drop feels casual | About Us page | Undermines expert positioning | **LOW** |
| 12 | Same contact form on every page footer | All pages | Missed contextual conversion opportunities | **LOW** |
| 13 | No AI readiness self-assessment tool | Site-wide (absent) | No self-guided path for AI-naive visitors | **MEDIUM** |
| 14 | Carousel limits case study discoverability + a11y bug | Homepage | Reduces content visibility; confusing screen reader label | **LOW** |
