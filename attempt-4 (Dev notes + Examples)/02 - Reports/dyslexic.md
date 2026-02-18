# Accessibility Report: Dyslexia Persona (Taylor Kim)

**Audit Date:** February 16, 2026
**Site:** https://launchpadlab.com/
**Pages Reviewed:** Homepage (`/`), Services (`/services`), About (`/about`), Contact (`/contact`), Careers (`/careers`)
**Persona:** Taylor Kim, 31-year-old freelance writer with dyslexia
**Assistive Strategies:** Browser zoom, text-to-speech (occasional), reliance on clear typography and structural hierarchy

---

## Executive Summary

The LaunchPad Lab website is *navigable* for a user with dyslexia but presents several significant readability barriers. The primary font (Proxima Nova) is a good choice, and the site uses heading hierarchy to organize content. However, insufficient body text contrast, dense paragraph blocks, tight heading line-height, and the loading of a decorative handwriting font (Permanent Marker) create cumulative fatigue that materially slows comprehension and increases reading errors. The user achieved both goals (understanding what LaunchPad Lab does and finding contact information) but reported moderate difficulty and eye strain.

---

## Issues Found

### Issue 1: Insufficient Body Text Contrast

| Field | Detail |
|-------|--------|
| **Severity** | **Critical** |
| **Pages Affected** | All pages (sitewide) |
| **Element** | `<p>`, `<li>`, `<dd>`, `<a>` — all body text elements |
| **Current State** | Body text color is `#555555` on a `#FFFFFF` background. This yields a contrast ratio of approximately **4.63:1**. |
| **WCAG Criteria** | **1.4.3 Contrast (Minimum) — Level AA**: Requires 4.5:1 for normal text. The ratio *barely* passes AA for normal-sized text (16px), but **fails** for any text rendered below 16px (e.g., the 14px `<h6>`, 9px font-size used in inline badge elements). **1.4.6 Contrast (Enhanced) — Level AAA**: Requires 7:1 for normal text. Fails significantly at 4.63:1. |
| **Impact on User** | Taylor reported that the gray text causes letters to "swim together," requiring repeated re-reading of paragraphs. The low contrast is the single most fatiguing element on the site. For a user with dyslexia who relies on clear letterform distinction, this contrast level forces the brain to work harder to distinguish characters — increasing transposition errors, line-skipping, and fatigue. |
| **Recommended Fix** | Change body text color to `#333333` (contrast ratio ~12.63:1) or at minimum `#444444` (~9.73:1) to meet AAA standards. Apply this change globally to `p`, `li`, `dd`, and `a` elements in the theme stylesheet. |

---

### Issue 2: Dense Paragraph Blocks Without Chunking

| Field | Detail |
|-------|--------|
| **Severity** | **Major** |
| **Pages Affected** | Homepage (hero description, "AI-Powered Digital Solutions" section, "Driving ROI with AI" section), Services page (service descriptions, FAQ answers), About page (intro paragraph) |
| **Element** | Long `<p>` elements within `.text-block` and content sections |
| **Current State** | Multiple key content sections present information as single continuous paragraphs of 3–5 sentences (40–80 words) without internal line breaks, bullet points, or sub-headings. Examples include: (1) The homepage hero subtext: "LaunchPad Lab helps organizations harness the power of AI through tailored consulting and product development services. From strategy to execution, we build high-impact digital products that modernize operations, reduce costs, and unlock growth." (2) The "AI-Powered Digital Solutions" paragraph under "Your Strategic AI Partner" (~55 words, single block). (3) FAQ answers on the Services page (some exceeding 80 words in a single paragraph). |
| **WCAG Criteria** | **1.4.8 Visual Presentation — Level AAA**: Text blocks should be no more than 80 characters wide, and content should allow user customization. **3.1.5 Reading Level — Level AAA**: Content should be written or supplemented to be understandable, especially for users with reading disabilities. While not a strict WCAG failure at AA level, WCAG Cognitive Accessibility guidance strongly recommends short paragraphs, bullet points, and clear chunking. |
| **Impact on User** | Taylor re-read the "AI-Powered Digital Solutions" paragraph three times before comprehending it. Dense paragraphs force a linear reading strategy that conflicts with the scanning/skimming pattern that users with dyslexia rely on. Without visual break-points, the user's eye cannot find a "re-entry point" after losing their place. |
| **Recommended Fix** | Break paragraphs longer than ~40 words into shorter chunks. Where content lists multiple benefits or features (e.g., "modernize operations, reduce costs, and unlock growth"), convert to bullet points. Use sub-headings within long content sections to provide scannable anchors. |

---

### Issue 3: Tight Line-Height on Headings

| Field | Detail |
|-------|--------|
| **Severity** | **Major** |
| **Pages Affected** | All pages (sitewide) |
| **Element** | `h1`, `h2`, `h3`, `h4`, `h5`, `h6` elements |
| **Current State** | Heading elements use `line-height: 1.1` as declared in the theme CSS. For multi-line headings (common on mobile viewports and at larger font sizes), this results in lines that nearly touch, with only 10% of the font size as inter-line space. The page header `h1` uses `line-height: 1` (zero extra leading) in some contexts. |
| **WCAG Criteria** | **1.4.12 Text Spacing — Level AA**: Users must be able to override text spacing without loss of content. While this criterion is about user overridability, the default values should be accessible. WCAG recommends line spacing of at least 1.5x the font size for body text. **1.4.8 Visual Presentation — Level AAA**: Line spacing should be at least 1.5x within paragraphs, and paragraph spacing at least 1.5x larger than line spacing. |
| **Impact on User** | When headings wrap to multiple lines (especially on narrower viewports), the cramped spacing makes it difficult for Taylor to distinguish which line is which. Characters from one line visually intrude on the line above or below, triggering transposition confusion. This is especially problematic for headings like "AI-Powered Digital Solutions for the Modern Enterprise," which wraps on most screen sizes. |
| **Recommended Fix** | Increase heading `line-height` to at least `1.3` (preferably `1.4`) for all heading levels. For the page header `h1` elements that currently use `line-height: 1`, increase to `1.3` minimum. |

---

### Issue 4: Base Body Line-Height Reset to 1

| Field | Detail |
|-------|--------|
| **Severity** | **Major** |
| **Pages Affected** | All pages — any element inheriting the base `body` style without a more specific override |
| **Element** | `body` element CSS declaration |
| **Current State** | The CSS reset sets `body { line-height: 1; }`. While the `<p>` tag overrides this with `line-height: 26px` (for 16px text, ~1.625 ratio), any other text-containing elements that don't have a specific line-height override (e.g., `<div>`, `<span>`, form labels, navigation dropdowns, footer text) inherit the body's `line-height: 1`, resulting in zero inter-line spacing. |
| **WCAG Criteria** | **1.4.12 Text Spacing — Level AA** |
| **Impact on User** | Elements that inherit the base `line-height: 1` become difficult to read when they wrap. This is particularly problematic in the navigation mega-menu, where descriptive text like "Our cross-functional teams have the skills and experience to support the full digital product lifecycle, using proven methods to deliver more better and faster with AI at the core" may inherit the tight base line-height depending on its container element. |
| **Recommended Fix** | Change the base `body` line-height from `1` to at least `1.5`. This ensures all text elements have a readable baseline, even those without specific overrides. The explicit `<p>` line-height can be retained or adjusted accordingly. |

---

### Issue 5: Decorative Font (Permanent Marker) Loaded

| Field | Detail |
|-------|--------|
| **Severity** | **Major** |
| **Pages Affected** | All pages (font is loaded in the `<head>` on every page) |
| **Element** | `<link href="https://fonts.googleapis.com/css?family=Permanent+Marker&display=swap">` in the document `<head>` |
| **Current State** | The site loads "Permanent Marker," a Google Font that simulates rough handwriting. This font is loaded globally. While it may not be prominently visible on the currently audited pages (it may be used in specific blog posts, landing pages, or CMS-managed content), its global inclusion means it can appear anywhere content editors apply it. Handwriting fonts feature irregular letterforms, inconsistent baselines, variable spacing, and character shapes that closely mimic the visual distortions dyslexia already creates. |
| **WCAG Criteria** | **1.4.8 Visual Presentation — Level AAA**: Fonts should support readability. WCAG Cognitive Accessibility guidelines recommend avoiding decorative or handwriting fonts for content text. **3.1.5 Reading Level — Level AAA**: Content should be presented in the most readable form. |
| **Impact on User** | Taylor identified handwriting fonts as "one of the hardest things for someone with dyslexia to decode." If Permanent Marker is applied to any heading, callout, or body text, it would be effectively illegible for this user — requiring either abandonment of that content or reliance on text-to-speech to decode it. Even decorative use of a single word can disrupt reading flow. |
| **Recommended Fix** | Remove the Permanent Marker font from the global template. If decorative typography is desired for specific visual elements, ensure it is applied only to non-informational decorative content (and mark that content with `aria-hidden="true"` with an accessible text alternative). Ideally, replace all uses with the existing Proxima Nova in a bold or black weight for visual emphasis. |

---

### Issue 6: Auto-Scrolling Logo Carousel

| Field | Detail |
|-------|--------|
| **Severity** | **Minor** |
| **Pages Affected** | Homepage, About page (any page with the "Trusted by Hundreds" logo scroller) |
| **Element** | `.logos__scroller` with CSS `animation: scroll` (continuous linear infinite animation) |
| **Current State** | The logo scroller animates continuously with no pause, stop, or user control. The site does check `prefers-reduced-motion: reduce` and conditionally disables the animation, which is positive. However, this media query is not set by default on most operating systems, and many users with dyslexia or cognitive disabilities are unaware it exists. |
| **WCAG Criteria** | **2.2.2 Pause, Stop, Hide — Level A**: For any moving, blinking, or scrolling information that starts automatically, lasts more than 5 seconds, and is presented in parallel with other content, there must be a mechanism to pause, stop, or hide it. The logo scroller has no visible pause/stop control. |
| **Impact on User** | The continuous motion in Taylor's peripheral vision while reading adjacent paragraphs was reported as distracting and contributed to losing place in text. While the `prefers-reduced-motion` check is a partial mitigation, it does not satisfy the WCAG requirement for a user-facing pause mechanism. |
| **Recommended Fix** | Add a visible pause/play button to the logo carousel. Additionally, consider reducing the animation speed or pausing the carousel when it is not in the viewport. The existing `prefers-reduced-motion` check is a good complement but should not be the sole mechanism. |

---

### Issue 7: JavaScript-Dependent Contact Form

| Field | Detail |
|-------|--------|
| **Severity** | **Minor** |
| **Pages Affected** | Contact page (`/contact`), Homepage (bottom "Reach Out" section) |
| **Element** | Ninja Forms contact form |
| **Current State** | The contact form is rendered entirely via JavaScript (Ninja Forms). When JavaScript is disabled or fails to load, the page displays: "Notice: JavaScript is required for this content." No fallback contact method is presented *adjacent to the form* — users must scroll down to find the email address and phone number in a separate "Let's Connect" section. |
| **WCAG Criteria** | **4.1.1 Parsing — Level A** (legacy) and general robustness principles. While WCAG doesn't strictly require forms to work without JavaScript, progressive enhancement best practices recommend providing fallback mechanisms. |
| **Impact on User** | Taylor sometimes uses simplified browsers or reading-mode tools that may strip JavaScript. If the form fails to render, the "JavaScript is required" message provides no actionable alternative. The email and phone number are available further down the page, but a user who doesn't scroll past the broken form area may assume contact is impossible. |
| **Recommended Fix** | Add a static fallback directly adjacent to the form placeholder — e.g., "Having trouble with this form? Email us at contact@launchpadlab.com or call (312) 888-9651." This ensures contact information is immediately available regardless of JavaScript status. |

---

### Issue 8: Excessive Line Length on Wide Viewports

| Field | Detail |
|-------|--------|
| **Severity** | **Minor** |
| **Pages Affected** | Homepage, Services page, About page — any page with full-width text blocks |
| **Element** | Text containers within the max-width `1220px` layout |
| **Current State** | On screens wider than ~1024px, body text paragraphs in some sections can span up to approximately 90–100+ characters per line (CPL). Optimal reading width for all users is 50–75 CPL; for users with dyslexia, the lower end of that range (50–65 CPL) is strongly preferred. |
| **WCAG Criteria** | **1.4.8 Visual Presentation — Level AAA**: Width should be no more than 80 characters or glyphs. |
| **Impact on User** | Long lines force Taylor's eyes to travel far from the end of one line to the beginning of the next, increasing the likelihood of re-reading the same line or skipping a line entirely. This is a common dyslexia-specific difficulty that compounds with low contrast and dense text. |
| **Recommended Fix** | Constrain body text containers to a maximum width of `680px` to `720px` (approximately 65–75 characters at 16px Proxima Nova). This can be achieved with a `max-width` on text-containing elements or by using a narrower content column within the existing layout grid. |

---

### Issue 9: Museo Slab Font Available for Use

| Field | Detail |
|-------|--------|
| **Severity** | **Minor** |
| **Pages Affected** | Potentially any page where CMS content uses the font class |
| **Element** | Typekit font declaration: `museo-slab` (serif slab font, weight 300/light) |
| **Current State** | The site loads Museo Slab via Adobe Typekit alongside Proxima Nova. Museo Slab is a slab-serif font loaded at weight 300 (light). Serif fonts, especially at light weights, are harder for users with dyslexia to read because the serifs create visual "hooks" that can be confused with parts of adjacent letters. The CSS class `.tk-museo-slab` is available for use throughout the site. |
| **WCAG Criteria** | **1.4.8 Visual Presentation — Level AAA**: Font choices should support readability. |
| **Impact on User** | If Museo Slab is applied to any body text or headings, it would reduce readability for Taylor. A light-weight serif font on a white background with #555555 color would compound the existing contrast issues significantly. |
| **Recommended Fix** | Audit all CMS content and templates for usage of `museo-slab` or `.tk-museo-slab`. If the font is not actively used, remove it from the Typekit kit to reduce page load and eliminate the risk of accidental use. If it is used, restrict its use to large decorative headings (32px+) with adequate contrast, never for body text. |

---

### Issue 10: Navigation Mega-Menu Text Density

| Field | Detail |
|-------|--------|
| **Severity** | **Minor** |
| **Pages Affected** | All pages (global navigation) |
| **Element** | Mega-menu dropdown for "Services" and "Industries" navigation items |
| **Current State** | The mega-menu dropdowns contain descriptive paragraphs alongside the navigation links. For example, the Services mega-menu includes: "Our cross-functional teams have the skills and experience to support the full digital product lifecycle, using proven methods to deliver more better and faster with AI at the core." This is a 28-word sentence presented within a dropdown that typically has constrained width, potentially inheriting the base `line-height: 1` if not specifically overridden. |
| **WCAG Criteria** | **3.2.3 Consistent Navigation — Level AA**, general usability. Navigation should be scannable and not overloaded with prose. |
| **Impact on User** | Taylor relies on navigation as a structural scanning tool. Dense descriptive text within dropdown menus makes it harder to quickly identify and select the desired link. The user must parse through prose to find clickable items, increasing cognitive load. |
| **Recommended Fix** | Remove or significantly shorten descriptive prose in mega-menu dropdowns. If context is needed, limit descriptions to 8–10 words maximum. Ensure all text in the mega-menu has an explicit `line-height` of at least `1.5`. |

---

## Summary of Findings

| # | Issue | Severity | WCAG Level | Criterion |
|---|-------|----------|------------|-----------|
| 1 | Body text contrast (#555 on #FFF) | Critical | AA / AAA | 1.4.3, 1.4.6 |
| 2 | Dense paragraph blocks without chunking | Major | AAA / Cognitive | 1.4.8, 3.1.5 |
| 3 | Tight heading line-height (1.1) | Major | AA | 1.4.12, 1.4.8 |
| 4 | Base body line-height reset to 1 | Major | AA | 1.4.12 |
| 5 | Decorative font (Permanent Marker) loaded | Major | AAA / Cognitive | 1.4.8, 3.1.5 |
| 6 | Auto-scrolling logo carousel without pause control | Minor | A | 2.2.2 |
| 7 | JavaScript-dependent contact form | Minor | Robustness | 4.1.1 |
| 8 | Excessive line length on wide viewports | Minor | AAA | 1.4.8 |
| 9 | Museo Slab serif font available for use | Minor | AAA | 1.4.8 |
| 10 | Navigation mega-menu text density | Minor | AA | 3.2.3 |

---

## Positive Findings

The following aspects of the site worked well for this persona:

1. **Primary font choice (Proxima Nova):** A clean, well-spaced sans-serif that is among the best mainstream fonts for dyslexic readers. Good x-height, open counters, and clear letter differentiation.

2. **Heading hierarchy:** The site uses semantic heading elements (`h1`–`h6`) with clear visual differentiation between levels. This provides the structural scaffolding that Taylor depends on for navigation and scanning.

3. **Service cards with short taglines:** The six service categories on the homepage and Services page use brief, scannable labels (e.g., "Enabling an autonomous digital workforce") that are easy to process.

4. **Bullet points on Services page:** The "Problems We Solve" section uses bullet lists for Business, IT, and Users categories, which is the most accessible content format for this persona.

5. **Contact information placement:** Email, phone, and address are presented clearly on the Contact page and in the site footer, with good scannability.

6. **Statistics blocks:** Large numbers with short labels (e.g., "730+ Projects") are highly effective for a user who struggles with prose — they communicate key information visually and concisely.

7. **`prefers-reduced-motion` check:** The logo carousel respects the reduced motion preference, demonstrating awareness of motion sensitivity (though it needs a manual control to fully comply with WCAG).

8. **Left-aligned text:** The site consistently uses left-aligned text throughout. No justified text was found, which avoids the irregular word spacing that creates significant reading difficulties for users with dyslexia.

---

## Priority Recommendations

### Immediate (High Impact, Low Effort)

1. **Darken body text color** from `#555555` to `#333333` across the sitewide stylesheet — single CSS change with the greatest readability improvement.
2. **Increase heading line-height** from `1.1` to `1.3–1.4` — single CSS change.
3. **Change base body line-height** from `1` to `1.5` — single CSS change.

### Short-Term (Moderate Effort)

4. **Remove Permanent Marker font** from the global template, or restrict to non-informational decorative use with accessible alternatives.
5. **Add pause/play button** to the logo carousel.
6. **Add static fallback** contact info adjacent to the JavaScript form.

### Ongoing (Content Strategy)

7. **Audit and chunk dense paragraphs** — break blocks longer than 40 words into bullets or shorter paragraphs. Establish content guidelines for maximum paragraph length.
8. **Constrain body text line length** to 65–75 characters per line with CSS `max-width` on text containers.
9. **Audit Museo Slab usage** and remove or restrict the font.
10. **Simplify mega-menu** descriptive text to reduce cognitive load in navigation.
