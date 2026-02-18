# Accessibility Report: Dyslexic User Experience

**Website:** https://launchpadlab.com/
**Persona:** Sam Chen — User with Dyslexia
**Evaluator:** AI-assisted accessibility audit via persona simulation
**Date:** February 18, 2026
**Pages Tested:** Homepage, Services, About Us, Contact

---

## Executive Summary

The LaunchPad Lab website has a visually polished design with several structural elements that benefit dyslexic users — including clear headings, statistics blocks, and client logos. However, the site relies heavily on dense paragraph text with complex vocabulary and business jargon. Key issues include insufficient line spacing in body text, paragraph-heavy content sections without visual breaks, use of non-plain language, and a confusing Contact page redirect. These issues create significant reading fatigue and comprehension barriers for users with dyslexia.

---

## Issues

### Issue 1: Dense Paragraph Blocks Throughout the Site

**Location:** Homepage hero section, Homepage "AI-Powered Digital Solutions" section, Services page intro, About page company description
**Description:** Multiple sections across the site feature paragraphs of 3-5 sentences with complex, multi-clause structures. Body paragraphs contain no internal formatting (no bold, no bullet points, no sentence breaks) to help readers anchor their position in the text.
**Examples:**
- Homepage: "LaunchPad Lab helps organizations harness the power of AI through tailored consulting and product development services. From strategy to execution, we build high-impact digital products that modernize operations, reduce costs, and unlock growth."
- Services page: "Our cross-functional teams have the skills and experience to support the full digital product lifecycle, using proven methods to deliver more better and faster with AI at the core."
- About page: "We work closely with our clients to first understand their unique business challenges and opportunities, then design, develop, and deliver bespoke solutions."

**Impact on Dyslexic Users:** Dense blocks of text cause letters and words to appear to shift, blur, or merge for dyslexic readers. Long sentences with multiple clauses require holding many concepts in working memory simultaneously, which is especially taxing for dyslexic users. Leads to re-reading, fatigue, and potential abandonment.
**Suggested Fix:**
- Limit paragraphs to 2-3 sentences maximum
- Use bullet points or numbered lists to break up information
- Bold key phrases within paragraphs to create visual anchors
- Add whitespace between paragraphs (increase `margin-bottom`)

**Priority:** High

---

### Issue 2: Complex Vocabulary and Business Jargon

**Location:** Throughout all pages
**Description:** The site uses specialized and complex terminology without definitions or context: "bespoke," "cross-functional," "agentic AI," "holistic capability," "operational efficiency," "digital transformation initiatives," "mission-critical," "industry-agnostic."
**Examples:**
- "Bespoke, redefining experiences" (Services card)
- "Agentic AI" (Services heading)
- "Holistic Capability" (About page feature card)
- "Cross-functional teams partner with you to deliver results"
- "Digital transformation initiatives"

**Impact on Dyslexic Users:** Complex and uncommon words require more processing time. Dyslexic readers may misread unfamiliar words (e.g., reading "Agentic" as "Genetic" or "Agentive"), leading to confusion about meaning. Business jargon creates additional cognitive load on top of the reading difficulty already present.
**Suggested Fix:**
- Replace jargon with plain-language alternatives ("custom" instead of "bespoke," "teams with different skills" instead of "cross-functional teams")
- Add brief inline definitions or tooltips for technical terms
- Follow plain language guidelines (e.g., plainlanguage.gov)
- Use shorter, more common words where possible

**Priority:** High

---

### Issue 3: Similar-Looking Words Causing Misreading

**Location:** Homepage tabs section, Homepage process section, About page description
**Description:** Several words on the site are visually similar and can cause confusion for dyslexic readers:
- "modernize" vs. "monetize" (Homepage hero paragraph)
- "Expansive" vs. "Expensive" (Homepage tab label)
- "develop" vs. "deliver" vs. "deploy" (Used in close proximity across the site)
- "consultation" vs. "consolidation" (potential confusion in service descriptions)
- "AI-Centered" vs. "AI-Censored" (Services hero heading)

**Impact on Dyslexic Users:** Dyslexic readers frequently swap, transpose, or misread letters. Words that differ by only one or two characters are particularly prone to confusion. Misreading a single word can change the entire meaning of a sentence, requiring re-reading and increasing frustration.
**Suggested Fix:**
- Avoid placing visually similar words near each other
- Use bold or distinctive styling on key differentiating words
- Increase letter-spacing (tracking) to make individual letters more distinguishable
- Consider alternative word choices where confusion risk is high

**Priority:** Medium

---

### Issue 4: Insufficient Body Text Size and Line Spacing

**Location:** All pages — body paragraph text
**Description:** Body text across the site appears to be approximately 16px with standard line-height. For dyslexic readers, this size is at the lower end of comfortable reading. Line-height and letter-spacing do not appear to have been optimized for readability. The navigation links in the header are in all-caps with relatively tight spacing.
**Examples:**
- Hero section sub-paragraphs
- Service descriptions
- About page company description
- Footer text (even smaller)

**Impact on Dyslexic Users:** Smaller text makes individual letter shapes harder to distinguish. Tight line spacing causes lines to visually merge, making it difficult to track which line the reader is on. All-caps text in the navigation removes ascender/descender cues that help dyslexic readers differentiate letters.
**Suggested Fix:**
- Increase body text to 18px minimum
- Set line-height to at least 1.8 (ideally 2.0) for body text
- Increase letter-spacing to 0.05em–0.12em
- Avoid all-caps text; use sentence case or title case instead
- Increase paragraph spacing
- Consider offering a text size adjustment widget

**Priority:** High

---

### Issue 5: No Dedicated Contact Page

**Location:** Navigation → Contact link (`/contact/`)
**Description:** The "Contact" link in the main navigation navigates to a page that displays the same content as the "About Us" page. There is no dedicated, simple contact page. Users must scroll through the entire About page content (company description, award badges, leadership team of 15 people, case studies, and feature cards) before reaching the contact form at the bottom.

**Impact on Dyslexic Users:** Dyslexic users experiencing reading fatigue are especially disadvantaged by this. When a user specifically seeks contact information — a task with clear intent — forcing them to navigate past extensive text-heavy content creates unnecessary friction. The cognitive overload of scrolling past content they're not looking for adds frustration and may cause them to abandon the task.
**Suggested Fix:**
- Create a dedicated `/contact/` page with only the contact form, phone number, email, and address
- Alternatively, ensure the Contact link scrolls directly to the contact form section using an anchor
- Keep the contact form simple and prominent without surrounding it with unrelated content

**Priority:** High

---

### Issue 6: All-Caps Section Labels

**Location:** Homepage ("TRUSTED BY HUNDREDS OF INNOVATIVE BUSINESSES," "PROBLEMS WE SOLVE," "YOUR 3-STEP BLUEPRINT FOR WHAT TO BUILD"), Services page ("WHAT WE DO," "OUR APPROACH"), About page ("PROVEN PARTNER," "ROOTED IN EXPERIENCE")
**Description:** Section label text (the small text above main headings) is rendered in all uppercase with wide letter-spacing. While this is a common design pattern, it reduces readability for dyslexic users.

**Impact on Dyslexic Users:** All-caps text removes the distinctive word shapes created by ascenders (b, d, f, h, k, l, t) and descenders (g, j, p, q, y). Dyslexic readers rely heavily on these shape patterns for word recognition. All-caps text forces letter-by-letter reading, which is slower and more fatiguing.
**Suggested Fix:**
- Use sentence case or small-caps (with a proper small-caps font variant)
- Increase the font size of section labels if removing all-caps
- Use a distinct color or weight to differentiate section labels without relying on capitalization

**Priority:** Medium

---

### Issue 7: Long Page Length and Excessive Scrolling

**Location:** All pages, especially Homepage and About page
**Description:** The homepage contains approximately 10+ distinct content sections requiring extensive scrolling. The About page includes company description, awards, trust signals, 15 leadership team member bios, a video section, stats, case studies, partner benefits, and a contact form — all on a single page.

**Impact on Dyslexic Users:** Long pages increase reading fatigue and make it harder to maintain orientation. Dyslexic users may lose track of where they are or what section they've already read. The sheer volume of content can create anxiety and may lead to site abandonment.
**Suggested Fix:**
- Break long pages into smaller, focused sub-pages
- Add a sticky table of contents or section navigation for long pages
- Provide a "jump to contact" button that is always visible
- Reduce content on each page to essential information only

**Priority:** Medium

---

### Issue 8: Serif/Decorative Font in Hero Headlines

**Location:** Homepage hero heading, Services hero heading, About hero heading, Contact form section heading
**Description:** The primary hero headlines appear to use a serif or semi-serif font style with italic weight. While visually striking, serif fonts and italics are harder for dyslexic readers to process because the decorative elements (serifs, italic slant) add visual noise.
**Examples:**
- "AI Innovation. Digital Solutions. Results that Matter." (serif/italic)
- "Ready to Build Something Great?" (bold italic serif)

**Impact on Dyslexic Users:** Serif fonts add small decorative strokes to letter endings that can make similar letters (like 'l', 'I', '1') harder to distinguish. Italic text changes the angle and spacing of letters, disrupting familiar letter patterns. This is especially problematic for dyslexic users who rely on clear, consistent letter shapes.
**Suggested Fix:**
- Use a clean sans-serif font for all text, including headings
- If a serif font is preferred for brand identity, ensure it has a large x-height and distinct letterforms
- Avoid italic styles for headings; use weight (bold) for emphasis instead
- Recommended fonts for dyslexia-friendly design: Open Sans, Lexie Readable, Atkinson Hyperlegible, or Verdana

**Priority:** Medium

---

### Issue 9: Limited Use of Visual Content to Supplement Text

**Location:** Homepage paragraph sections, Services page service descriptions, About page company description
**Description:** While the site includes some visual elements (client logos, team photos, product screenshots), the core informational content is almost entirely text-based. There are no infographics, diagrams, or illustrations explaining what the company does or how their process works. There is one embedded video on the About page, but text content is not supplemented with visual alternatives elsewhere.

**Impact on Dyslexic Users:** Dyslexic users process visual information (diagrams, icons, illustrations, videos) significantly faster and more accurately than text. When core concepts are only available as text paragraphs, dyslexic users are at a disadvantage. They may fail to fully understand the company's offerings or process because the information isn't available in their preferred format.
**Suggested Fix:**
- Add explanatory illustrations or icons alongside service descriptions
- Create an infographic showing the Discover → Deliver → Release process
- Add short explainer videos for key service areas
- Use icons consistently with text labels in service cards and feature lists
- Consider providing text-to-speech functionality

**Priority:** Medium

---

### Issue 10: Navigation Labels Could Be Confusing

**Location:** Main navigation bar (all pages)
**Description:** Some navigation labels are similar in meaning and could be confused by dyslexic readers: "Services" vs. "Technologies" vs. "Industries" are three distinct but related concepts. Without hovering or clicking, it's unclear how they differ. Additionally, "Our Work" and "Insights" are both content-focused links that could be confusing.

**Impact on Dyslexic Users:** When navigation labels are conceptually similar, dyslexic users may click the wrong one and become disoriented. The cognitive effort of distinguishing between similar concepts adds to overall fatigue.
**Suggested Fix:**
- Add brief descriptive subtitles to navigation items (e.g., on hover or in a mega-menu)
- Use more distinct terminology (e.g., "What We Build" instead of "Technologies")
- Consider adding icons next to navigation labels to provide visual differentiation
- Reduce the number of top-level navigation items if possible

**Priority:** Low

---

### Issue 11: Hero Text Over Background Images

**Location:** Homepage hero, About page hero, Services page hero
**Description:** Hero sections use white text overlaid on photographic backgrounds. While a dark overlay is applied to improve contrast, the variable nature of photographic backgrounds means contrast can be inconsistent across the text area. Some letters may fall over lighter portions of the image, reducing readability.

**Impact on Dyslexic Users:** Inconsistent contrast makes letters harder to distinguish, especially for readers who already struggle with letter recognition. Moving between areas of good and poor contrast disrupts reading flow and requires extra effort to decode characters.
**Suggested Fix:**
- Increase the opacity of the dark overlay to ensure consistent contrast
- Add a solid background behind the text block specifically (semi-transparent box)
- Ensure a minimum contrast ratio of 7:1 (WCAG AAA) for text over images
- Test with a contrast analyzer across the entire text area, not just the darkest point

**Priority:** Medium

---

### Issue 12: No Accessibility Customization Options

**Location:** Site-wide
**Description:** The site does not offer any user-facing accessibility controls such as text size adjustment, contrast toggling, line-spacing controls, dyslexia-friendly font switching, or a reading mode.

**Impact on Dyslexic Users:** While Sam uses a browser extension (OpenDyslexic), not all dyslexic users have this. Site-provided accessibility controls demonstrate awareness and provide immediate relief without requiring users to install third-party tools.
**Suggested Fix:**
- Add an accessibility widget/toolbar with options for:
  - Text size increase/decrease
  - Line-height adjustment
  - Letter-spacing adjustment
  - High-contrast mode
  - Dyslexia-friendly font toggle
- Alternatively, integrate a solution like UserWay, AccessiBe, or a custom accessibility panel
- Ensure the site's CSS custom properties are structured to support runtime theming

**Priority:** Low

---

## Summary Table

| # | Issue | Location | Priority | WCAG |
|---|-------|----------|----------|------|
| 1 | Dense paragraph blocks | All pages | High | 3.1.5 (Reading Level) |
| 2 | Complex vocabulary / jargon | All pages | High | 3.1.3 (Unusual Words), 3.1.5 |
| 3 | Similar-looking words | Homepage, Services | Medium | 3.1.5 (Reading Level) |
| 4 | Insufficient text size / line spacing | All pages — body text | High | 1.4.8 (Visual Presentation) |
| 5 | No dedicated contact page | Navigation → /contact/ | High | 2.4.5 (Multiple Ways) |
| 6 | All-caps section labels | All pages | Medium | 1.4.8 (Visual Presentation) |
| 7 | Long page length | Homepage, About | Medium | 2.4.1 (Bypass Blocks) |
| 8 | Serif/italic font in headings | Hero sections | Medium | 1.4.8 (Visual Presentation) |
| 9 | Limited visual content | Services, Homepage | Medium | 1.1.1 (Non-text Content) |
| 10 | Confusing navigation labels | Main nav | Low | 2.4.6 (Headings & Labels) |
| 11 | Text over variable backgrounds | Hero sections | Medium | 1.4.3 (Contrast) |
| 12 | No accessibility customization | Site-wide | Low | 1.4.8 (Visual Presentation) |

---

## Priority Distribution

- **High:** 4 issues (Issues 1, 2, 4, 5)
- **Medium:** 6 issues (Issues 3, 6, 7, 8, 9, 11)
- **Low:** 2 issues (Issues 10, 12)

---

## Recommendations for Immediate Action

1. **Simplify text content** — Rewrite body paragraphs using plain language, shorter sentences, and bullet points. This single change would have the largest positive impact on dyslexic users.
2. **Create a dedicated Contact page** — The Contact nav link should lead to a focused page with just the form and contact details.
3. **Increase body text size and spacing** — Set body text to 18px+, line-height to 1.8+, and add letter-spacing of 0.05em minimum.
4. **Replace jargon with plain language** — Audit all content for readability at an 8th-grade reading level using tools like Hemingway Editor.
