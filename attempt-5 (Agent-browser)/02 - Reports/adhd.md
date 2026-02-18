# Accessibility Report: ADHD Persona (Jamie Rivera)
## Website: launchpadlab.com

**Date:** February 18, 2026
**Evaluator Persona:** Jamie Rivera — 28-year-old freelance graphic designer with ADHD (combined type)
**Pages Evaluated:** Homepage, Our Work, Services, Contact, About Us
**Evaluation Focus:** Cognitive accessibility for users with ADHD

---

## Executive Summary

LaunchPad Lab's website performs reasonably well at communicating its core value proposition quickly — the homepage hero section is clear, the navigation has a prominent "Contact" button, and the service cards are scannable. However, the site has several significant issues for ADHD users: dense paragraph text throughout, an overwhelming Our Work page with 40+ unsorted case studies, auto-playing carousels, repetitive content across pages, and jargon-heavy copy that obscures meaning. Contact information is ultimately easy to find (one click), but the overall browsing experience beyond the initial landing involves cognitive overload.

---

## Issues Found

### Issue 1: Dense Paragraph Text Throughout the Site

**Location:** Homepage (hero paragraph, AI Partner section, ROI section, approach section), Services page (hero, service descriptions, approach section, Discovery Space Navigator), About page (hero, Digital Potential section)

**Description:** Nearly every content section uses paragraphs of 3-5 lines to convey key information. These paragraphs are visually uniform — no bolded keywords, no inline highlighting, no bullet points. For a user scanning rapidly, the paragraphs become invisible walls of text that are skipped entirely.

**Specific examples:**
- Homepage hero: "LaunchPad Lab helps organizations harness the power of AI through tailored consulting and product development services. From strategy to execution, we build high-impact digital products that modernize operations, reduce costs, and unlock growth." — 2 sentences, ~40 words, no visual anchors.
- "AI-Powered Digital Solutions for the Modern Enterprise" section paragraph: 3 sentences with no bold text or visual differentiation.
- Services page "Discovery Space Navigator" description: ~60 words, entirely unformatted.

**Impact on ADHD Users:** Users with ADHD skim content using visual anchors (bold text, bullet points, color, icons). Uniform paragraphs provide no anchoring points, causing the content to be skipped entirely. Key messaging is lost.

**Suggested Fix:**
- Convert paragraphs to bullet-point lists where possible
- Bold key phrases within paragraphs (e.g., **AI consulting**, **product development**, **reduce costs**)
- Limit paragraphs to 2 lines maximum, breaking longer text into digestible chunks
- Use icons or visual markers to highlight key concepts

**Priority:** High

---

### Issue 2: Our Work Page — Overwhelming Number of Case Studies with No Hierarchy

**Location:** /work/

**Description:** The Our Work page displays 40+ case study cards in a flat grid with no visual hierarchy, no featured items, and no summary section. The only organizational tool is a "Select Industries" filter dropdown at the top, but there is no default curation. Users land on the page and are immediately confronted with a wall of uniformly-sized case study cards stretching across many scroll lengths.

**Impact on ADHD Users:** This triggers "paralysis of choice" — a well-documented ADHD symptom where an overwhelming number of options causes decision-making to freeze. Users cannot prioritize which case study to explore and are likely to abandon the page entirely without engaging with any content. The lack of hierarchy means there's no clear starting point.

**Suggested Fix:**
- Add a "Featured Work" section at the top with 3-5 curated, highlighted case studies
- Group case studies by industry or service type with clear section headings
- Show fewer items by default with a "Load More" or pagination approach
- Add brief summary stats or tags to each card to help users quickly assess relevance
- Consider a "Quick Filter" with visual category buttons instead of a dropdown

**Priority:** High

---

### Issue 3: Auto-Playing Carousels

**Location:** Homepage (case studies carousel), About page (case studies carousel), Contact page (testimonials carousel)

**Description:** Multiple pages feature carousels that auto-advance slides. The homepage case studies section has a carousel with dot navigation (3 pages). The About page has a similar carousel. The Contact page has a testimonials carousel with 5 slides. These carousels auto-play, changing content without user initiation.

**Impact on ADHD Users:** Auto-playing content is a significant distraction for users with ADHD. Moving or changing content involuntarily draws attention away from the user's current task, breaks concentration, and can cause the user to lose their place or forget what they were doing. When content changes before it can be fully processed, it creates anxiety and frustration.

**Suggested Fix:**
- Disable auto-play on all carousels by default
- Provide clear, large previous/next navigation controls
- Add a visible pause/play button for users who want auto-play
- Consider replacing carousels with a static grid of 3-4 items, as carousels have notoriously low engagement rates

**Priority:** High

---

### Issue 4: Repetitive Content Across Pages Creates Disorientation

**Location:** All pages (Homepage, Services, About, Our Work, Contact)

**Description:** The same content blocks appear on nearly every page:
- The same contact form appears on the Homepage, Services, About, Our Work, and Contact pages
- The same stats (12+/13+ years, 730+ projects, 240+ clients) appear on the Homepage and About page
- Similar case study carousels appear on the Homepage, Services, and About pages
- The footer content is identical across all pages (expected, but adds to repetition)

**Impact on ADHD Users:** When navigating between pages, encountering the same content blocks creates confusion about whether the user has actually navigated to a new page or is seeing the same page they were already on. This "déjà vu" effect is especially disorienting for users with ADHD who already struggle with working memory and context tracking. It also makes pages unnecessarily long, increasing scroll fatigue.

**Suggested Fix:**
- Limit the full contact form to the Contact page and possibly the Homepage
- On other pages, use a simpler CTA block (e.g., "Have a question? Contact Us" with a single button link to the Contact page)
- Ensure each page has unique, distinctive content sections that clearly differentiate it from other pages
- If repeating stats, vary the presentation so users don't confuse pages

**Priority:** Medium

---

### Issue 5: Jargon-Heavy and Buzzword-Dense Copy

**Location:** Throughout the site, especially the Homepage and Services page

**Description:** The site heavily uses enterprise/consulting jargon that obscures meaning. Examples include:
- "bespoke solutions"
- "cross-functional teams"
- "mission-critical software"
- "digital transformation initiatives"
- "agile, cross-functional expertise"
- "operating as an extension of your team"
- "bottom-line impact"
- "AI-centric digital product design and development"
- "holistic capability"

**Impact on ADHD Users:** Jargon requires additional cognitive processing to decode meaning. For ADHD users who are already scanning quickly, jargon causes confusion and disengagement. If the user can't immediately understand what a phrase means, they skip it — and potentially miss critical information about the company's actual capabilities.

**Suggested Fix:**
- Replace jargon with plain language (e.g., "custom solutions" instead of "bespoke solutions," "our team works with yours" instead of "operating as an extension of your team")
- Lead with concrete, specific language (e.g., "We build apps and websites" instead of "AI-centric digital product design and development")
- Test copy readability with a tool like Hemingway Editor — aim for Grade 8 reading level

**Priority:** Medium

---

### Issue 6: Interactive Tab Section on Homepage Is a Distraction Trap

**Location:** Homepage — "Ship Game-Changing Digital Products to Market Fast" section

**Description:** This section features a tabbed interface with six tabs (Operational Efficiency, Modern Technology, Customer Engagement, Scalable Solutions, Expansive Resources, Speed to Market). The currently selected tab shows a one-line description and app screenshots on the right side. The visual screenshots are visually engaging and draw attention.

**Impact on ADHD Users:** Interactive UI elements like tabs are "dopamine traps" for ADHD users — the novelty of clicking and seeing content change provides a small dopamine hit that encourages continued interaction, pulling the user away from their original goal. The screenshots next to the tabs are visually rich and further compound the distraction. The user may spend significant time clicking through tabs without absorbing meaningful information.

**Suggested Fix:**
- Consider displaying all six items in a static grid or list format instead of tabs
- If using tabs, avoid visually rich imagery alongside them that competes for attention
- Ensure the tab content itself is substantive enough to justify the interaction cost

**Priority:** Medium

---

### Issue 7: Clutch Award Badges Are Too Small to Read

**Location:** About page — below the "We Help Unleash Your Digital Potential" section

**Description:** A row of 7-8 Clutch badges/award images is displayed horizontally. The badges are small (approximately 80-100px wide) and contain tiny text describing the specific award (e.g., "Top Salesforce Company 2023," "Top Software Developers United States 2023"). At their displayed size, the text within the badges is nearly illegible.

**Impact on ADHD Users:** The badges create visual noise without conveying clear information. ADHD users scanning the page see a row of similar-looking gray shapes that don't communicate specific value. The effort required to zoom in or squint to read badge text is more than an ADHD user will invest. This turns a potential trust signal into visual clutter.

**Suggested Fix:**
- Increase badge sizes so text is legible at normal viewing distance
- Add text labels below each badge describing the award
- Alternatively, list awards as text with the Clutch logo, rather than relying on badge images
- Limit to 3-4 most impressive awards rather than showing all

**Priority:** Low

---

### Issue 8: Video Embed on About Page Has No Preview Information

**Location:** About page — "Solve complex problems with mission-critical software" section

**Description:** An embedded video (iframe) appears in the About page with no visible title, duration, or description of its content. The user has no information about what the video covers or how long it is before committing to watching it.

**Impact on ADHD Users:** ADHD users are unlikely to commit to watching an unknown-length video without context. The lack of preview information (title, duration, thumbnail with play button) means the video is likely to be ignored entirely. If the video contains important information about the company, this content is lost to ADHD users.

**Suggested Fix:**
- Add a visible title/heading for the video
- Display the video duration prominently
- Add a brief 1-sentence description of what the video covers
- Ensure the video thumbnail is visually engaging with a clear play button overlay

**Priority:** Low

---

### Issue 9: Long Pages Require Excessive Scrolling

**Location:** Homepage, Services page, About page

**Description:** The homepage is extremely long, containing: hero section, trust logos, AI partner section, services cards, tabs section, stats, approach/process section, AI CTA section, case studies carousel, blog post suggestions, full contact form, and footer. The Services page is similarly lengthy with hero, services list, accordion section, Discovery Space Navigator, approach section, case studies, contact form, blog suggestions, and 12-question FAQ. Users must scroll through many screens of content to reach the bottom.

**Impact on ADHD Users:** Long pages cause scroll fatigue. ADHD users lose context as they scroll — by the time they reach the middle of the page, they may have forgotten what they saw at the top or what they were originally looking for. The lack of a sticky table of contents or jump links means users can't quickly navigate to specific sections.

**Suggested Fix:**
- Add a sticky table of contents or section jump links for long pages
- Consider breaking the homepage into shorter, more focused sections with clear "above the fold" messaging
- Use a "back to top" floating button
- Prioritize content ruthlessly — not everything needs to be on the homepage

**Priority:** Medium

---

### Issue 10: Navigation Doesn't Indicate Current Page

**Location:** All pages — top navigation bar

**Description:** The top navigation bar lists Services, Technologies, Industries, Our Work, About Us, Insights, and Contact. When navigating to a specific page, there is no visible active state or indicator showing which page the user is currently on. The nav items all look the same regardless of the current page.

**Impact on ADHD Users:** Without a current-page indicator, ADHD users who have navigated through multiple pages may lose track of where they are in the site. This compounds the disorientation caused by repetitive content blocks across pages. Users may click the same nav link twice, not realizing they're already on that page.

**Suggested Fix:**
- Add a visible active state to the current page's nav item (e.g., underline, bold, color change, or background highlight)
- Consider adding breadcrumbs on sub-pages for additional context

**Priority:** Medium

---

### Issue 11: No Search Functionality

**Location:** Entire site

**Description:** The website has no visible search bar or search functionality. Users must navigate through the menu structure or scroll through pages to find specific information.

**Impact on ADHD Users:** ADHD users often know what they're looking for but don't want to browse through multiple pages to find it. A search bar provides a direct path to information, bypassing the cognitive cost of navigation. Without search, users who can't find what they need within 2-3 clicks are likely to leave.

**Suggested Fix:**
- Add a search bar in the header/navigation area
- Ensure search results are ranked by relevance and clearly formatted

**Priority:** Low

---

### Issue 12: Contact Form Fields Don't Specify Expected Format

**Location:** All contact forms across the site

**Description:** The contact form requires five fields: First Name, Last Name, Company Email, Company, and How Can We Help You. All fields are marked as required (*) but there is no indication of expected input format, character limits, or examples. The "How Can We Help You?" field is a text input with no guidance on what level of detail is expected.

**Impact on ADHD Users:** Open-ended form fields without guidance create decision paralysis. "How Can We Help You?" is a broad question that requires the user to compose a response from scratch. ADHD users may abandon the form at this field because they don't know what to write or feel overwhelmed by the open-endedness.

**Suggested Fix:**
- Add placeholder text or examples in the "How Can We Help You?" field (e.g., "Tell us briefly about your project and timeline")
- Consider offering a dropdown for project type or inquiry category to reduce cognitive load
- Add a character count or limit indicator

**Priority:** Low

---

## Summary Table

| # | Issue | Location | Priority | WCAG Related |
|---|-------|----------|----------|--------------|
| 1 | Dense paragraph text with no visual anchors | All pages | High | 3.1.5 Reading Level |
| 2 | Overwhelming Our Work page (40+ items, no hierarchy) | /work/ | High | 2.4.6 Headings and Labels |
| 3 | Auto-playing carousels | Homepage, About, Contact | High | 2.2.2 Pause, Stop, Hide |
| 4 | Repetitive content across pages | All pages | Medium | 2.4.8 Location |
| 5 | Jargon-heavy copy | All pages | Medium | 3.1.5 Reading Level |
| 6 | Tab section as distraction trap | Homepage | Medium | — |
| 7 | Clutch badges too small to read | About page | Low | 1.4.4 Resize Text |
| 8 | Video embed has no preview info | About page | Low | 1.1.1 Non-text Content |
| 9 | Long pages require excessive scrolling | Homepage, Services, About | Medium | 2.4.5 Multiple Ways |
| 10 | No current-page indicator in navigation | All pages | Medium | 2.4.8 Location |
| 11 | No search functionality | Entire site | Low | 2.4.5 Multiple Ways |
| 12 | Contact form lacks input guidance | All contact forms | Low | 3.3.2 Labels or Instructions |

---

## Positive Findings

While this report focuses on issues, several aspects of the site work well for ADHD users:

1. **Clear homepage hero text** — The value proposition ("AI Innovation. Digital Solutions. Results that Matter.") is immediately understood.
2. **Prominent "CONTACT" button** — Visually distinct in the navigation, easy to find.
3. **Service cards with short labels** — The six service categories on the homepage use concise headings and one-line descriptions, ideal for scanning.
4. **Large stat numbers** — 12+ years, 730+ projects, 240+ clients are displayed in oversized font, instantly readable.
5. **Contact form on every page** — Users can reach out from wherever they are without navigating away.
6. **Contact page simplicity** — Email, phone, LinkedIn, and form are all clearly presented.
7. **Leadership team with photos** — Humanizes the company and creates trust quickly.
8. **"Connect with an Expert" CTA** — Visible on the homepage hero, providing an immediate action path.

---

## Conclusion

LaunchPad Lab's website successfully communicates its core identity quickly — within 15-20 seconds, an ADHD user can understand that the company builds digital products and AI solutions for businesses. Contact information is also easily accessible (one click from any page). However, the experience degrades significantly when the user needs to go deeper: dense paragraphs, overwhelming case study lists, repetitive content, and jargon create cognitive overload. The most impactful improvements would be converting paragraphs to bullet points, adding hierarchy to the Our Work page, and disabling auto-play on carousels.
