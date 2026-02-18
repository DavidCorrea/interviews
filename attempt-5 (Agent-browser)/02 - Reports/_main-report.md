# Main Accessibility Report: LaunchPad Lab Website

**Website:** https://launchpadlab.com/  
**Date:** February 18, 2026  
**Personas Evaluated:** ADHD (Jamie Rivera), Dyslexia (Sam Chen), Non-Native English Speaker (Yuki Tanaka), Non-Technical Business Executive (Richard Okonkwo), Gen Z First-Time Founder (Zara Mitchell), AI-Curious Business Executive (Margaret Sullivan)  
**Pages Covered:** Homepage, Services, Our Work, About Us, Industries, Insurance, AI Automation, Contact

---

## Methodology

Four distinct personas — each representing a different accessibility dimension — independently browsed the LaunchPad Lab website using automated browser tools. Each persona attempted to accomplish two goals: (1) understand what LaunchPad Lab does, and (2) find how to contact them. Their experiences were documented as first-person interviews and translated into structured technical reports. This main report consolidates all findings, removes duplicates, groups related issues, and assigns consolidated priorities.

---

## Consolidated Issues

### 1. Dense Text Blocks & Complex Sentence Structures

**Priority:** High  
**Reported by:** ADHD, Dyslexic, Non-Native  
**Location:** All pages — hero sections, service descriptions, about copy, process sections

**Summary:** The site relies heavily on multi-sentence paragraphs (3-5 lines) with complex, multi-clause structures. Body paragraphs contain no internal formatting — no bold keywords, no bullet points, no visual anchors. Examples include the homepage hero paragraph (~40 words, 2 dense sentences), the "AI-Powered Digital Solutions" section, and service descriptions on the Services page.

- **ADHD impact:** Paragraphs are skipped entirely because there are no visual anchors to grab attention.
- **Dyslexia impact:** Dense blocks cause letters to appear to shift and merge; multi-clause sentences overload working memory, requiring multiple re-reads.
- **Non-native impact:** Complex sentence structures with nested clauses and passive voice require multiple readings and mental translation.

**Recommendations:**
- Limit paragraphs to 2-3 sentences maximum
- Use bullet points and numbered lists to break up information
- Bold key phrases within paragraphs to create visual anchors
- Target 15-20 words per sentence, active voice, Subject-Verb-Object order
- Increase `margin-bottom` between paragraphs for visual separation

---

### 2. Pervasive Jargon, Unexplained Acronyms & Technical Language

**Priority:** High  
**Reported by:** ADHD, Dyslexic, Non-Native, Big Company Owner  
**Location:** All pages — especially Services, Homepage, Industries

**Summary:** The site uses extensive technical terminology without definitions or context. Key offenders include:
- **Acronyms:** ROI, CSAT, UAT, UI/UX, CRM, MVP, CI/CD — used without expansion
- **Industry terms:** Agile, Sprint, cross-functional, bespoke, agentic AI, product discovery, headless commerce
- **Idioms/Metaphors:** "Harness the power of AI," "Ship game-changing products," "Cutting-edge," "Forging a partnership," "Unleash your digital potential," "Move the needle"
- **"Digital product" framing:** Used as the primary descriptor sitewide, but non-technical users think in terms of "software," "system," or "application"

- **ADHD impact:** Jargon requires extra cognitive processing; ADHD users skip it and miss key information.
- **Dyslexia impact:** Unfamiliar words are easily misread (e.g., "Agentic" → "Genetic"); complex vocabulary adds cognitive load.
- **Non-native impact:** Idioms are among the hardest elements for non-native speakers; acronyms are incomprehensible without expansion.
- **Business owner impact:** Terms like "Sprint releases," "UAT validation," and "cross-functional" are completely meaningless to non-technical executives.

**Recommendations:**
- Replace jargon with plain-language equivalents sitewide ("custom" not "bespoke," "teams with different skills" not "cross-functional")
- Expand all acronyms on first use (e.g., "Return on Investment (ROI)")
- Replace idioms with literal language ("Use AI effectively" not "Harness the power of AI")
- Use "software," "application," and "system" alongside "digital product"
- Add a glossary page or tooltip definitions for technical terms
- Target 8th-grade reading level using tools like Hemingway Editor

---

### 3. AI-First Messaging Obscures Core Value Proposition

**Priority:** High  
**Reported by:** Big Company Owner  
**Location:** Homepage — Hero section (H1 heading)

**Summary:** The primary headline "AI Innovation. Digital Solutions. Results that Matter." leads with AI, which is irrelevant to many prospective clients who need custom software for operational problems (inventory management, workflow automation, internal tools). "Digital Solutions" is too vague to confirm the company builds custom software applications.

**Recommendations:**
- Add a secondary headline plainly stating the core offering: "We build custom software for businesses — web applications, internal tools, and operational platforms"
- Position AI as a secondary capability, not the lead message
- Consider A/B testing headlines for technical vs. non-technical audiences

---

### 4. No Dedicated Contact Page & Missing Post-Submission Expectations

**Priority:** High  
**Reported by:** Dyslexic, Non-Native, Big Company Owner  
**Location:** /contact/ URL, all embedded contact forms

**Summary:** The "Contact" navigation link does not lead to a focused, dedicated contact page. Instead, users encounter the same content as other pages and must scroll to find the form. Additionally, the form says "We will get in touch with you as soon as possible" without specifying response time, response format, what the first conversation covers, or what the prospect should prepare.

**Recommendations:**
- Create a dedicated `/contact/` page with only: the form, phone number, email, address, and clear next-step expectations
- Add post-submission expectations: "Step 1: We review your message within 4 business hours. Step 2: A team member calls or emails to schedule a free 30-minute discovery call."
- Consider adding a Calendly/scheduling link for immediate booking
- Provide guidance for the open-ended "How Can We Help You?" field

---

### 5. Typography Issues: Text Size, Spacing, All-Caps, Serif Fonts

**Priority:** High  
**Reported by:** Dyslexic  
**Location:** All pages — body text, section labels, hero headings

**Summary:** Multiple typography issues compound reading difficulty:
- Body text appears to be ~16px with standard line-height — at the lower end of comfortable reading for dyslexic users
- Section labels ("TRUSTED BY HUNDREDS OF INNOVATIVE BUSINESSES," "WHAT WE DO," etc.) use ALL-CAPS, which removes ascender/descender cues critical for dyslexic word recognition
- Hero headlines use serif/italic font styles that add visual noise and make similar letters harder to distinguish
- Navigation links use all-caps with tight spacing

**Recommendations:**
- Increase body text to 18px minimum
- Set line-height to at least 1.8 (ideally 2.0)
- Add letter-spacing of 0.05em–0.12em
- Replace all-caps text with sentence case or title case
- Use clean sans-serif fonts for all text (recommended: Open Sans, Atkinson Hyperlegible, Verdana)
- Avoid italic styles for headings; use font-weight for emphasis
- Consider offering a text size adjustment widget

---

### 6. Overwhelming Our Work Page (40+ Items, No Hierarchy)

**Priority:** High  
**Reported by:** ADHD  
**Location:** /work/

**Summary:** The Our Work page displays 40+ case study cards in a flat grid with no visual hierarchy, no featured items, and no summary section. The only organizational tool is a "Select Industries" filter dropdown. Users are confronted with a wall of uniformly-sized cards, triggering "paralysis of choice."

**Recommendations:**
- Add a "Featured Work" section at the top with 3-5 curated case studies
- Group case studies by industry or service type with clear section headings
- Show fewer items by default with "Load More" or pagination
- Add brief summary tags to each card for quick relevance assessment
- Use visual category buttons instead of a dropdown filter

---

### 7. Auto-Playing Carousels & Limited Content Discoverability

**Priority:** High  
**Reported by:** ADHD, Big Company Owner  
**Location:** Homepage (case studies), About page (case studies), Contact page (testimonials)

**Summary:** Multiple pages feature carousels that auto-advance slides. Only 3 items are visible at a time with small dot pagination buttons. Users may not realize additional content exists.

- **ADHD impact:** Auto-playing content involuntarily draws attention, breaks concentration, and causes the user to lose their place.
- **Business owner impact:** If visible case studies aren't relevant, the user may conclude the company lacks relevant experience without discovering more options.

**Recommendations:**
- Disable auto-play on all carousels by default
- Add clear, large Previous/Next arrow buttons
- Add visible text like "Showing 1-3 of 9 case studies"
- Consider replacing carousels with static grids of 6-9 items
- Add a visible pause/play button if auto-play is retained

---

### 8. Missing Industry Coverage

**Priority:** High  
**Reported by:** Big Company Owner  
**Location:** /industries/

**Summary:** The Industries page lists only 9 industries (Financial Services, Private Equity, Healthcare, etc.) with no mention of manufacturing, distribution, logistics, supply chain, or food/beverage — despite existing case studies for companies like Kawasaki and American Truck Business Services. The body copy claims "industry-agnostic" but the narrow list contradicts this.

**Recommendations:**
- Expand the Industries list to include Manufacturing, Logistics/Distribution, and Supply Chain
- Add a fallback message: "Don't see your industry? We've built solutions across 50+ industries" with a CTA
- Consider organizing by problem type rather than industry vertical

---

### 9. Marketing Fluff & Vague Service Descriptions

**Priority:** Medium  
**Reported by:** Non-Native, Big Company Owner  
**Location:** Homepage services cards, Services page, hero sections

**Summary:** Service taglines use aspirational marketing language that provides no concrete information:
- Web App Development: "Bespoke, redefining experiences"
- Mobile App Development: "Meeting users where they are"
- Product Strategy & Design: "Agile, cross-functional expertise"
Marketing superlatives like "high-impact," "world-class," "award-winning," "mission-critical," and "cutting-edge" appear throughout without supporting evidence.

**Recommendations:**
- Replace taglines with concrete benefit statements ("Custom web-based software for your business operations")
- Replace superlatives with specific, verifiable claims (name awards, cite metrics)
- Focus on outcomes that resonate with decision-makers

---

### 10. Repetitive Content Across Pages

**Priority:** Medium  
**Reported by:** ADHD, Non-Native  
**Location:** All pages

**Summary:** The same content blocks appear on nearly every page: identical contact forms, identical stats (12+ years, 730+ projects, 240+ clients), and similar case study carousels. The Contact and Services pages may display the same content as the homepage, creating confusion about whether navigation actually worked.

**Recommendations:**
- Limit full contact forms to the Contact page and Homepage
- On other pages, use a simpler CTA block linking to the Contact page
- Ensure each page has distinctive content that clearly differentiates it
- Add page titles or breadcrumbs so users always know where they are

---

### 11. Long Pages Without Section Navigation

**Priority:** Medium  
**Reported by:** ADHD, Dyslexic  
**Location:** Homepage, Services page, About page

**Summary:** Pages contain 10+ distinct content sections requiring extensive scrolling. Users lose context as they scroll and may forget what they saw at the top or what they were originally looking for.

**Recommendations:**
- Add a sticky table of contents or section jump links for long pages
- Add a "back to top" floating button
- Prioritize content — not everything needs to be on one page
- Consider breaking the About page into smaller sub-pages

---

### 12. Confusing or Ambiguous Navigation Labels

**Priority:** Medium  
**Reported by:** ADHD, Dyslexic, Non-Native, Big Company Owner  
**Location:** Main navigation bar (all pages)

**Summary:** Several navigation issues compound:
- No visible active state indicating the current page
- "Insights" is ambiguous for non-native speakers (should be "Blog" or "Articles")
- "Technologies" is irrelevant to non-technical decision-makers
- "Services" vs. "Technologies" vs. "Industries" are conceptually similar and confusing
- No icons or visual differentiation between nav items

**Recommendations:**
- Add a visible active state to the current page's nav item (underline, bold, or color)
- Rename "Insights" to "Blog" or "Articles"
- Rename or deprioritize "Technologies" (move to footer or rename "How We Build")
- Add brief descriptive subtitles on hover or in a mega-menu
- Consider adding icons next to navigation labels

---

### 13. Insufficient Visual Content to Supplement Text

**Priority:** Medium  
**Reported by:** Dyslexic, Non-Native  
**Location:** Homepage, Services page, Industries page

**Summary:** Core informational content is almost entirely text-based. There are no infographics, diagrams, or illustrations explaining what the company does or how their process works. The "Discover → Deliver → Release" process is text-only with no visual flow.

**Recommendations:**
- Add explanatory illustrations or icons alongside service descriptions
- Create a visual process diagram for the Discover → Deliver → Release workflow
- Add short explainer videos for key service areas
- Use before/after diagrams or infographics to explain service value
- Consider providing text-to-speech functionality

---

### 14. Hero Text Contrast Over Background Images

**Priority:** Medium  
**Reported by:** Dyslexic, Big Company Owner  
**Location:** Homepage hero, About page hero, Services page hero

**Summary:** Hero sections use white text overlaid on photographic backgrounds with a semi-transparent dark overlay. The variable brightness of the photograph means contrast is inconsistent across the text area, reducing readability in lighter spots.

**Recommendations:**
- Increase opacity of the dark overlay for consistent contrast
- Add a solid semi-transparent background behind the text block specifically
- Ensure minimum contrast ratio of 7:1 (WCAG AAA) across the entire text area
- Test with a contrast analyzer across the full text area, not just the darkest point

---

### 15. No Pricing or Engagement Cost Guidance

**Priority:** Medium  
**Reported by:** Big Company Owner  
**Location:** Sitewide — absent from all pages

**Summary:** There is no pricing information, cost ranges, typical project budgets, or budget expectations anywhere on the website. Prospects have no way to self-qualify before reaching out.

**Recommendations:**
- Add a FAQ entry addressing pricing: "Custom software projects typically range from $X to $Y, depending on complexity, timeline, and scope"
- Include directional guidance to help prospects self-qualify
- Even a statement like "Most projects start at $50K+" builds trust through transparency

---

### 16. Contact Form UX Issues (Guidance, reCAPTCHA, Duplication)

**Priority:** Medium  
**Reported by:** ADHD, Big Company Owner  
**Location:** All contact forms across the site

**Summary:** Three issues compound:
1. The "How Can We Help You?" field provides no guidance on expected input, creating decision paralysis for ADHD users and uncertainty for non-native speakers
2. The reCAPTCHA "I'm not a robot" checkbox adds friction at the critical conversion moment
3. The Contact page itself has duplicate forms (one at the top, one embedded at the bottom)

**Recommendations:**
- Add placeholder text or examples ("Tell us briefly about your project and timeline")
- Consider a dropdown for project type or inquiry category
- Use invisible reCAPTCHA (v3) instead of the checkbox version
- Remove the duplicate form on the Contact page

---

### 17. Creative/Metaphorical Product Names Add Cognitive Load

**Priority:** Medium  
**Reported by:** Non-Native, Big Company Owner  
**Location:** Services page, Industries page

**Summary:** "Discovery Space Navigator" and "Mission Control" use space-themed metaphors that extend the LaunchPad brand. While creative for native speakers, these names obscure the actual function. "Discovery Space Navigator" sounds like a space exploration tool, not a business consulting process.

**Recommendations:**
- Add plain-language subtitles: "Discovery Space Navigator — Our process for identifying your best product opportunities"
- Rename "Mission Control" to something descriptive: "AI Analysis Platform" or "Project Analyzer"
- Or rename entirely: "Get Your Custom Roadmap" or "Your Free Project Blueprint"

---

### 18. FAQ Sections Collapsed by Default

**Priority:** Medium  
**Reported by:** Big Company Owner  
**Location:** Services page, Industries page — bottom sections

**Summary:** FAQ sections contain highly relevant questions ("How much does it cost?", "How long does it take?", "How fast will we see results?") but all answers are collapsed by default. Users scanning quickly may see the questions but not click to expand, missing some of the most valuable content on the site.

**Recommendations:**
- Expand the first 2-3 most important FAQs by default (especially cost and timeline)
- Surface key FAQ answers in a dedicated "What to Expect" section higher on the page
- Add a visual indicator that items are expandable

---

### 19. Interactive Tab Section as Distraction Trap

**Priority:** Medium  
**Reported by:** ADHD  
**Location:** Homepage — "Ship Game-Changing Digital Products to Market Fast" section

**Summary:** A tabbed interface with 6 tabs provides novelty-seeking ADHD users with a "dopamine trap" — clicking through tabs provides small rewards that pull the user away from their original goal without delivering substantive information.

**Recommendations:**
- Display all 6 items in a static grid/list format instead of tabs
- If using tabs, ensure content is substantive enough to justify the interaction
- Avoid pairing tabs with visually rich imagery that competes for attention

---

### 20. Similar-Looking Words in Close Proximity

**Priority:** Medium  
**Reported by:** Dyslexic  
**Location:** Homepage tabs, process section, About page

**Summary:** Several words on the site are visually similar and confuse dyslexic readers: "modernize" vs. "monetize," "Expansive" vs. "Expensive," "develop" vs. "deliver" vs. "deploy," "AI-Centered" vs. "AI-Censored."

**Recommendations:**
- Avoid placing visually similar words near each other
- Increase letter-spacing to make individual letters more distinguishable
- Bold or style key differentiating words
- Consider alternative word choices where confusion risk is high

---

### 21. No Search Functionality

**Priority:** Low  
**Reported by:** ADHD, Big Company Owner  
**Location:** Sitewide

**Summary:** The website has no search bar or search functionality. Users must manually browse through pages to find specific information.

**Recommendations:**
- Add a search feature accessible from the navigation bar
- Ensure search results are ranked by relevance and clearly formatted

---

### 22. Clutch Award Badges Too Small to Read

**Priority:** Low  
**Reported by:** ADHD  
**Location:** About page — below "We Help Unleash Your Digital Potential"

**Summary:** A row of 7-8 Clutch badges are displayed at ~80-100px wide. The text within badges is nearly illegible at that size, turning a potential trust signal into visual clutter.

**Recommendations:**
- Increase badge sizes so text is legible
- Add text labels below each badge
- Limit to 3-4 most impressive awards

---

### 23. Video Embed Without Preview Information

**Priority:** Low  
**Reported by:** ADHD  
**Location:** About page — "Solve complex problems" section

**Summary:** An embedded video has no visible title, duration, or description. Users have no information about what the video covers before committing to watch.

**Recommendations:**
- Add a visible title/heading for the video
- Display the video duration
- Add a 1-sentence description of video content

---

### 24. No Accessibility Customization Options

**Priority:** Low  
**Reported by:** Dyslexic  
**Location:** Sitewide

**Summary:** The site offers no user-facing accessibility controls (text size, contrast, line-spacing, dyslexia-friendly font, reading mode).

**Recommendations:**
- Add an accessibility widget with text size, line-height, letter-spacing, contrast, and font toggles
- Or integrate a solution like UserWay or a custom accessibility panel
- Ensure CSS custom properties support runtime theming

---

### 25. No Multilingual Support

**Priority:** Low  
**Reported by:** Non-Native  
**Location:** Sitewide

**Summary:** No language selection, no multilingual content, and no acknowledgment of international visitors — despite featuring global client metrics.

**Recommendations:**
- Consider adding a Google Translate widget for key pages
- Ensure English text follows plain language guidelines for better automated translation
- Note that the team can accommodate international clients

---

### 26. Informal Tone / Cultural Mismatch

**Priority:** Low  
**Reported by:** Non-Native  
**Location:** CTAs, footer, various headings

**Summary:** Casual phrases like "Let's Build Something Great" and "Let's Get Social" may feel unprofessional to users from cultures where corporate communication is more formal (e.g., Japanese business culture).

**Recommendations:**
- Balance casual CTAs with substantive, professional content nearby
- Consider offering more formal alternatives for key conversion CTAs

---

### 27. Contact Form Excludes Non-Corporate Users

**Priority:** High  
**Reported by:** Gen Z  
**Location:** All contact forms sitewide

**Summary:** The contact form requires "Company Email" and "Company" as mandatory fields. These assume the user works at an established company with a corporate email domain. A young founder with a startup idea has neither — these fields create a psychological barrier signaling the form wasn't designed for individuals, freelancers, or early-stage founders.

**Recommendations:**
- Rename "Company Email" to "Email"
- Make "Company" optional, or rename to "Company / Project Name (optional)"
- Add a "What stage is your project?" dropdown (e.g., "Just an idea," "Early stage," "Growing business," "Enterprise") to make all stages feel welcome

---

### 28. No Live Chat, Calendly, or Low-Barrier Contact Option

**Priority:** High  
**Reported by:** Gen Z  
**Location:** Sitewide — no chat widget present

**Summary:** The only contact methods are a static form (with reCAPTCHA), email, phone, and LinkedIn. There is no live chat widget, no Calendly scheduling link, and no "book a quick call" option. Gen Z users expect instant, low-friction communication — a form that says "we'll get back to you" provides no timeline and feels like shouting into the void.

**Recommendations:**
- Add a Calendly or Cal.com embed for "Book a Free 15-Minute Intro Call"
- Consider adding a chat widget (Intercom, Drift, or similar) for instant engagement
- At minimum, add a clear expected response time to the form

---

### 29. Enterprise-Only Social Proof (Case Studies & Client Logos)

**Priority:** High  
**Reported by:** Gen Z  
**Location:** Homepage carousel, Our Work page, client logo bar

**Summary:** The homepage case study carousel features only large corporations (Millennium Trust, Prosci, CDK Global). The client logo bar shows Kawasaki, Harvard, Whirlpool, Northwestern, etc. Startup-adjacent case studies (Tiny House Listings, Breadcrumb, AlgoFast) exist but are buried deep on the Our Work page. No startup logos appear in the trust bar.

**Recommendations:**
- Feature at least one startup/small-company case study in the homepage carousel
- Include logos from smaller/startup clients alongside enterprise logos
- Add a "Startups" filter to the Our Work page
- If startup work is under NDA, add text like "...and 50+ startups and growing companies"

---

### 30. No Startup/Audience-Segmented Navigation Path

**Priority:** High  
**Reported by:** Gen Z  
**Location:** Sitewide navigation

**Summary:** The navigation includes Services, Technologies, Industries, Our Work, About Us, Insights, and Contact — all generic. There is no audience-based navigation (e.g., "For Startups," "For Enterprise") and no content specifically addressing startup founders or small teams. Without a clear path for their user type, startup founders must self-navigate through enterprise-oriented content.

**Recommendations:**
- Add a "For Startups" or "Work With Us" page addressing the startup audience
- Add audience-based sub-navigation under Services (e.g., "Startup MVP Development")
- Include startup-specific messaging in the Industries section

---

### 31. Discovery Space Navigator Is Buried

**Priority:** Medium  
**Reported by:** Gen Z  
**Location:** Services page — mid-page section

**Summary:** The "Discovery Space Navigator" offering ("Your 3-Step Blueprint for What to Build" — prototype in 4 weeks, launch in 6 weeks) is the most startup-friendly content on the entire site. However, it's buried deep within the Services page and not referenced on the homepage, About page, or Contact page. Early-stage founders — the exact audience it serves — are the least likely to scroll that far.

**Recommendations:**
- Feature the Discovery Space Navigator prominently on the homepage
- Create a standalone CTA on the Contact page: "Not sure where to start? Try our Discovery Space Navigator"
- Use this as a low-barrier entry point for early-stage founders

---

### 32. Team Page Lacks Personality and Human Connection

**Priority:** Medium  
**Reported by:** Gen Z  
**Location:** About Us page — "Meet Our Leadership Team" section

**Summary:** The leadership team section displays circular headshots with names, formal titles (VP, President, Principal Software Architect II), and LinkedIn links. There are no bios, personal descriptions, fun facts, or humanizing content. The section reads like an org chart.

**Recommendations:**
- Add 1-2 sentence bios with a personal touch (interests, passion projects)
- Mix candid photos with professional ones
- Use approachable title descriptions alongside formal ones ("leads our design team" not just "VP of Design")

---

### 33. Neglected Social Media Presence (Instagram)

**Priority:** Medium  
**Reported by:** Gen Z  
**Location:** Instagram (@launchpadlab), linked from footer

**Summary:** The Instagram account has 463 posts but only ~250 followers. The last post was from December 2025 — nearly two months of inactivity. Content is primarily award announcements and holiday graphics with minimal engagement. For Gen Z, an inactive social account signals a company that is out of touch or in decline.

**Recommendations:**
- Invest in regular, engaging Instagram content (behind-the-scenes, project showcases, team personality, founder tips)
- Or remove the Instagram link to avoid the negative signal
- Aim for authentic, human content over corporate award announcements

---

### 34. No TikTok or Twitter/X Social Presence

**Priority:** Low  
**Reported by:** Gen Z  
**Location:** Footer — "Let's Get Social" section (all pages)

**Summary:** Social media links include Facebook, Instagram, and LinkedIn. There is no TikTok or Twitter/X. Facebook is largely irrelevant to Gen Z; TikTok and Twitter/X are primary discovery platforms for this demographic.

**Recommendations:**
- Add TikTok for short-form content (team day-in-the-life, "how we built this" shorts)
- Add Twitter/X for tech community engagement
- Consider deprioritizing the Facebook link

---

### 35. AI Content and Industry Content Are Siloed

**Priority:** High  
**Reported by:** AI-Curious Business  
**Location:** AI Automation page, Insurance Industry page, Industries page

**Summary:** The AI Automation page discusses AI capabilities broadly but never mentions specific industries like insurance or financial services. The Insurance industry page describes insurance-relevant services (quote-to-bind, claims, compliance) but barely mentions AI. An executive looking for "AI for my insurance company" must visit both pages and mentally combine them — a significant cognitive burden requiring 25+ minutes of cross-referencing across 6+ pages.

**Recommendations:**
- Create dedicated "AI for [Industry]" pages or sections that map AI capabilities to industry-specific use cases
- Example: "5 ways AI can transform your brokerage: 1) Automated claims intake 2) AI-powered underwriting recommendations 3) Intelligent policyholder self-service 4) Compliance documentation automation 5) Predictive risk assessment"
- At minimum, cross-link AI and industry pages with contextual callouts

---

### 36. Unattributed Statistics Undermine Credibility

**Priority:** High  
**Reported by:** AI-Curious Business  
**Location:** AI Automation page (stats section), Insurance page (stats section), Services page

**Summary:** Prominent statistics like "60%+ reduction in repetitive manual work," "3x faster response across service channels," "140% increase in online conversions," and "$2M in projected profit" appear without attributing them to specific clients, case studies, or methodologies. For skeptical, experienced executives, unattributed stats feel like marketing claims rather than evidence.

**Recommendations:**
- Link each statistic to a specific case study or client ("60%+ reduction in manual work — based on Bullhorn engagement")
- For averages/projections, state methodology ("Based on results across 15 AI automation engagements in 2024-2025")
- Add hyperlinks from stats to full case studies

---

### 37. Salesforce/Agentforce Coupling Creates AI Scope Confusion

**Priority:** Medium  
**Reported by:** AI-Curious Business  
**Location:** AI Automation page (Agentforce Quick Start section, related content), Homepage footer

**Summary:** The AI Automation page heavily features Salesforce's "Agentforce" product — including a Quick Start Program, webinar links, and blog posts. This creates the impression that the AI offering is primarily or exclusively a Salesforce implementation service, when the company actually offers platform-agnostic AI consulting (e.g., the healthcare insurance case study uses OpenAI API and MS SQL Server).

**Recommendations:**
- Clearly delineate Salesforce-specific AI offerings from platform-agnostic capabilities
- Add a statement: "Our AI solutions work with your existing technology stack, whether you use Salesforce, custom systems, or other platforms"
- Highlight the technology diversity shown in case studies

---

### 38. Anonymous Case Study Company Names Reduce Trust

**Priority:** Medium  
**Reported by:** AI-Curious Business  
**Location:** Our Work page, Insurance page (case study references)

**Summary:** Several case studies use anonymized company names: "Healthcare Insurance Platform," "Financial Services Firm," "Actuarial Firm," "Wealth Management Firm." While understandable for confidentiality, this reduces trust-building value for skeptical executives who want to verify claims and assess comparability.

**Recommendations:**
- Where possible, obtain client permission to use company names
- For anonymous cases, add context: industry sub-segment, company size, geography, and sponsor's executive title
- Consider adding video testimonials from willing clients

---

### 39. Missing Executive/Industry-Specific Testimonials

**Priority:** Medium  
**Reported by:** AI-Curious Business  
**Location:** Contact page (testimonial carousel)

**Summary:** Testimonials on the Contact page come from a VP at Apex Leaders and from Amplify Credit Union. None come from insurance industry executives, C-suite leaders, or company presidents. AI-curious executives specifically look for peer validation from people at their decision-making level in their industry.

**Recommendations:**
- Actively solicit testimonials from C-suite clients in insurance, financial services, and professional services
- Feature these on the Contact page and relevant industry pages
- Include speaker's title, company type, and a specific outcome metric

---

### 40. No AI Readiness Assessment or Self-Service Educational Path

**Priority:** Medium  
**Reported by:** AI-Curious Business  
**Location:** Sitewide (absent)

**Summary:** For AI-curious but AI-illiterate executives, there is no self-guided educational path — no "AI Readiness Assessment" quiz, no "Is AI Right for Your Business?" checklist, no downloadable guide for business leaders. The site assumes visitors will navigate service pages and read marketing copy, but AI-naive visitors don't know what they don't know.

**Recommendations:**
- Create an interactive "AI Readiness Assessment" (5-question self-assessment that maps answers to recommendations)
- Create a downloadable "AI for Business Leaders" guide
- Link prominently from homepage and AI Automation page
- Serves dual purpose: educational tool + lead generation mechanism

---

### 41. Inconsistent Statistics Across Pages

**Priority:** Low  
**Reported by:** AI-Curious Business  
**Location:** Homepage ("12+ Years in Business") vs. About Us page ("13+ Years in Business")

**Summary:** The homepage displays "12+ Years" while the About page says "13+ Years" (company founded in 2012, correct figure is 13+ as of 2026). A minor inconsistency, but detail-oriented executives who notice it may question the accuracy of other claims.

**Recommendations:**
- Audit all instances of the "years in business" stat and make them consistent
- Use a dynamic calculation based on founding year to prevent future drift

---

### 42. ChatGPT Name-Drop Undermines Expert Positioning

**Priority:** Low  
**Reported by:** AI-Curious Business  
**Location:** About Us page — "On the Cutting Edge" section

**Summary:** The About page says: "From AI like ChatGPT to Salesforce products like Agentforce, we're on the cutting edge." Name-dropping a consumer AI brand as an example of expertise feels like a construction company saying "we use hammers." It demonstrates awareness of a popular tool, not deep expertise. Skeptical executives may find it slightly unserious for an enterprise AI consulting firm.

**Recommendations:**
- Replace the ChatGPT reference with descriptions of actual AI capabilities: "From custom AI document processing to enterprise-scale automation, we bring cutting-edge AI solutions that deliver measurable business outcomes"
- Focus on what the company builds, not consumer AI brands

---

## Priority Summary

| Priority | Count | Issue Numbers |
|----------|-------|---------------|
| **High** | 14 | 1, 2, 3, 4, 5, 6, 7, 8, 27, 28, 29, 30, 35, 36 |
| **Medium** | 20 | 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 31, 32, 33, 37, 38, 39, 40 |
| **Low** | 9 | 21, 22, 23, 24, 25, 26, 34, 41, 42 |

---

## Cross-Persona Impact Matrix

| Issue | ADHD | Dyslexic | Non-Native | Biz Owner | Gen Z | AI-Curious |
|-------|------|----------|------------|-----------|-------|------------|
| 1. Dense Text | X | X | X | | X | X |
| 2. Jargon & Acronyms | X | X | X | X | X | X |
| 3. AI-First Messaging | | | | X | X | |
| 4. Contact Page Issues | | X | X | X | X | X |
| 5. Typography | | X | | | | |
| 6. Overwhelming Work Page | X | | | | | |
| 7. Auto-Playing Carousels | X | | | X | | X |
| 8. Missing Industries | | | | X | | |
| 9. Marketing Fluff | | | X | X | X | X |
| 10. Repetitive Content | X | | X | | | X |
| 11. Long Pages | X | X | | | | |
| 12. Navigation Labels | X | X | X | X | X | |
| 13. Visual Content Gaps | | X | X | | | |
| 14. Hero Contrast | | X | | X | | |
| 15. No Pricing | | | | X | X | X |
| 16. Contact Form UX | X | | | X | X | X |
| 17. Creative Product Names | | | X | X | | |
| 18. Collapsed FAQs | | | | X | X | X |
| 19. Tab Distraction | X | | | | | |
| 20. Similar-Looking Words | | X | | | | |
| 21. No Search | X | | | X | | |
| 22. Small Badges | X | | | | | |
| 23. Video No Preview | X | | | | | |
| 24. No Accessibility Options | | X | | | | |
| 25. No Multilingual | | | X | | | |
| 26. Informal Tone | | | X | | | |
| 27. Form Excludes Non-Corp | | | | | X | |
| 28. No Chat/Calendly | | | | | X | |
| 29. Enterprise-Only Proof | | | | | X | |
| 30. No Startup Nav Path | | | | | X | |
| 31. DSN Buried | | | | | X | |
| 32. Team Lacks Personality | | | | | X | |
| 33. Neglected Instagram | | | | | X | |
| 34. No TikTok/Twitter | | | | | X | |
| 35. AI/Industry Siloed | | | | | | X |
| 36. Unattributed Stats | | | | | | X |
| 37. Salesforce Coupling | | | | | | X |
| 38. Anonymous Case Studies | | | | | | X |
| 39. Missing Exec Testimonials | | | | | | X |
| 40. No AI Readiness Tool | | | | | | X |
| 41. Inconsistent Stats | | | | | | X |
| 42. ChatGPT Name-Drop | | | | | | X |

---

## Top 8 Highest-Impact Recommendations

These changes would yield the greatest improvement across the most personas:

1. **Plain Language Overhaul** (addresses issues 1, 2, 9, 17, 20, 42): Rewrite all site copy using plain language guidelines — short sentences, no jargon, expanded acronyms, bullet points, bold keywords, inline definitions for AI terms. This single effort addresses the #1 issue for 5 of 6 personas.

2. **Inclusive Contact Experience** (addresses issues 4, 15, 16, 27, 28, 39): Create a focused contact page, rename "Company Email" to "Email", make "Company" optional, add a Calendly link or chat widget, set clear response time expectations, add form field guidance, and include industry-specific executive testimonials.

3. **Typography & Readability Upgrade** (addresses issues 5, 14): Increase body text to 18px, line-height to 1.8+, letter-spacing to 0.05em+, replace all-caps with sentence case, use sans-serif fonts, and ensure consistent contrast on hero sections.

4. **Navigation & Information Architecture Improvements** (addresses issues 6, 7, 10, 11, 12, 18, 30): Add active nav states, fix navigation labels, add section jump links, replace carousels with static grids, add hierarchy to the Work page, surface FAQ answers, and add audience-segmented navigation (e.g., "For Startups," "AI Services").

5. **Content Strategy for All Audience Segments** (addresses issues 3, 8, 13, 29, 31, 35): Adjust hero messaging to lead with "custom software" rather than AI, expand industry coverage, add visual content, mix startup and enterprise social proof, promote the Discovery Space Navigator, and bridge AI capabilities with industry-specific use cases (dedicated "AI for [Industry]" content).

6. **Credibility & Trust Improvements** (addresses issues 36, 38, 41): Attribute all statistics to specific case studies or methodologies, work to de-anonymize case study company names where possible, and fix inconsistent stats across pages.

7. **Audience Inclusivity** (addresses issues 27, 29, 30, 32): Ensure the site speaks to startups and first-time founders — not just enterprise buyers. Feature startup case studies prominently, add a "For Startups" path, humanize the team page, and use inclusive form fields.

8. **AI Education & Onboarding** (addresses issues 35, 37, 40): Create self-service educational content for AI-naive visitors (readiness assessment, business leader guide), clarify that AI services extend beyond Salesforce, and build "AI for [Industry]" bridges between service and industry pages. This directly serves the growing segment of executives who know they need AI but don't know where to start.
