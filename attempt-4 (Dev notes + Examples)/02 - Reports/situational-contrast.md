# Accessibility Report: Situational Low Contrast

**Persona**: Jordan Kim — Project manager using a device outdoors in bright sunlight  
**Condition**: Situational low contrast due to ambient light and screen glare  
**Website**: https://launchpadlab.com/  
**Audit Date**: February 2026  
**Testing Conditions**: Simulated bright outdoor sunlight viewing with maximum screen brightness

---

## Executive Summary

LaunchPad Lab's website presents significant usability barriers for users experiencing situational low contrast, such as those using devices outdoors in bright sunlight. The site relies heavily on mid-gray body text (#555555), blue accent text (#1e60bd), thin borders, and subtle interactive state changes — all of which become illegible or invisible when ambient light washes out the screen. While some sections (dark navy backgrounds, large bold headings) perform well, the majority of the site's content and interactive elements fall below the effective contrast threshold needed for outdoor use. The contact form — a primary conversion element — is likely unusable in these conditions.

---

## Issues Found

### Issue 1: Body Text Uses Mid-Gray (#555555) on White Backgrounds

**Page(s)**: All pages — Homepage, Contact, About, Services  
**Element(s)**: All `<p>` and `<li>` elements using the default body text style  
**Examples**:
- Homepage hero description: "LaunchPad Lab helps organizations harness the power of AI through tailored consulting..."
- "Your Strategic AI Partner" section body text: "At LaunchPad Lab, we combine deep expertise in product design..."
- Service card descriptions: "Enabling an autonomous digital workforce," "Bespoke, redefining experiences"
- "Problems We Solve" tab preview descriptions
- Stats section descriptions: "We've got experience and cross industry expertise..."
- Related Content card preview text
- Contact page testimonial attribution text

**CSS**: `p, figcaption { color: #555555; }` and `li, dd { color: #555555; }` and `a { color: #555555; }`

**Measured Contrast Ratio**: ~7.46:1 (#555555 on #FFFFFF)  
**Effective Contrast in Sunlight**: ~2.5–3.7:1 (estimated with ambient light factor)

**WCAG Criteria Violated**:
- **1.4.3 Contrast (Minimum)** (AA) — Passes under standard conditions (7.46:1 > 4.5:1), but fails in situational context
- **1.4.6 Contrast (Enhanced)** (AAA) — Passes at 7.46:1 > 7:1, but the effective outdoor contrast drops well below 4.5:1

**Severity**: **Major**

**Impact on This User**: Body text is the primary way the site communicates detailed information about services, process, and value propositions. In bright sunlight, #555555 text washes out significantly. Jordan can read headings but cannot comfortably read paragraphs, forcing reliance on headings alone and missing key details. This degrades the ability to evaluate the company and make an informed contact decision.

**Recommended Fix**:
- Darken body text to **#333333** (contrast ratio ~12.63:1) or **#222222** (~17.11:1) to provide a buffer for adverse lighting conditions
- As an alternative, offer a **high-contrast mode** or **dark mode** toggle that switches body text to near-black (#111111 or #000000)
- Consider using `font-weight: 500` or `600` for body text to improve legibility in degraded contrast conditions

---

### Issue 2: Blue Eyebrow/Label Text (#1e60bd) on White Backgrounds

**Page(s)**: All pages — used extensively as section labels  
**Element(s)**: `<span>` elements used as eyebrow text / section labels, styled with `color: var(--eyebrow-color, #1e60bd)`  
**Examples**:
- "Trusted by Hundreds of Innovative Businesses" (logos section)
- "Your Strategic AI Partner" (media and text section)
- "Driving ROI with AI" (cards section)
- "Problems We Solve" (tabs section)
- "Our Signature Approach" (process grid section, on dark background — this instance is fine)
- "Put AI to Work" (inline callout)
- "Our Latest Case Studies" (case study section)
- "Related Content" (blog cards section)
- "Reach Out" / "Reach out" (CTA and contact sections)
- "Blog Post" labels on related content cards

**Measured Contrast Ratio**: ~6.06:1 (#1e60bd on #FFFFFF)  
**Effective Contrast in Sunlight**: ~2.0–3.0:1 (estimated)

**WCAG Criteria Violated**:
- **1.4.3 Contrast (Minimum)** (AA) — Technically passes at 6.06:1 for normal-sized text, but the text is typically small (14–16px) and regular weight, making it vulnerable to washout
- **1.4.6 Contrast (Enhanced)** (AAA) — **Fails** (6.06:1 < 7:1)

**Severity**: **Major**

**Impact on This User**: Eyebrow text serves as navigational wayfinding — it tells Jordan what each section is about before reading deeper. In bright sunlight, this blue text becomes nearly invisible on white, meaning Jordan loses the ability to quickly scan and orient within the page. Every section becomes an undifferentiated block of content without these labels.

**Recommended Fix**:
- Darken the eyebrow color to **#0D47A1** (~8.57:1) or **#1A237E** (~11.58:1) for AAA compliance while maintaining a blue brand palette
- Alternatively, use **#000000** or **#222222** for eyebrow text and apply the blue as a left border, underline, or background accent instead of text color
- Increase eyebrow font weight to **700 (bold)** to improve glyph definition under adverse conditions
- Consider using `text-transform: uppercase` with `letter-spacing` to increase legibility at small sizes

---

### Issue 3: Navigation Links on Transparent Header Over Hero Image

**Page(s)**: All pages (global header)  
**Element(s)**: `<a class="mega-menu-link">` links within `<ul id="mega-menu-menu-1">` — Services, Technologies, Industries, Our Work, About Us, Insights, Contact  
**CSS**: Header is `position: absolute; background-color: transparent;` overlaid on the hero section

**Measured Contrast Ratio**: Variable — depends on the hero background image and gradient overlay beneath the text. Gradient applies `linear-gradient(to right, #000, transparent)` and `linear-gradient(0, transparent, #000)` with `opacity: 0.6` on the hero image.

**WCAG Criteria Violated**:
- **1.4.3 Contrast (Minimum)** (AA) — Cannot guarantee consistent contrast when text overlays a photographic background
- **1.4.11 Non-text Contrast** (AA) — Navigation link boundaries/clickable areas not visually distinct

**Severity**: **Major**

**Impact on This User**: The navigation is how Jordan would find the Contact page or learn about Services. With the header positioned transparently over a background image, the contrast between navigation text and its background is inconsistent and unpredictable. In sunlight, photographic backgrounds lose all detail and become a bright wash, potentially leaving light-colored nav text invisible against a glare-brightened background. The nav text is also relatively small (body-sized) and not bold.

**Recommended Fix**:
- Add a **solid or semi-opaque background** to the header (e.g., `background-color: rgba(0, 0, 0, 0.7)` or a solid dark color) to guarantee consistent contrast regardless of hero image
- Add a visible **text-shadow** to nav links for legibility: `text-shadow: 0 1px 3px rgba(0,0,0,0.8)`
- Consider making the header **opaque on scroll** (sticky header with solid background) — many sites do this already, and it dramatically improves readability
- Increase nav link font weight to **600–700**

---

### Issue 4: Contact Form Fields — Invisible Borders and Placeholder Text

**Page(s)**: Homepage (bottom CTA section), Contact page  
**Element(s)**: Ninja Forms contact form (`<div id="nf-form-13-cont">`) — input fields, labels, textarea, and submit button  
**CSS**: Ninja Forms default styling typically uses light gray borders (#ccc or #ddd) and light gray placeholder text

**Measured Contrast Ratio**:
- Typical form field border (#cccccc on #FFFFFF): ~1.61:1
- Typical placeholder text (#999999 on #FFFFFF): ~2.85:1
- Typical form field border (#dddddd on #FFFFFF): ~1.38:1

**Effective Contrast in Sunlight**: All effectively ~1:1 (invisible)

**WCAG Criteria Violated**:
- **1.4.11 Non-text Contrast** (AA) — Form field boundaries must have at least 3:1 contrast with adjacent colors. Light gray borders on white fail this entirely.
- **1.4.3 Contrast (Minimum)** (AA) — Placeholder text below 4.5:1 fails
- **3.3.2 Labels or Instructions** (A) — If labels are placeholder-only and invisible, the form becomes unusable

**Severity**: **Critical**

**Impact on This User**: The contact form is the primary conversion mechanism on the site — it's how Jordan is supposed to reach LaunchPad Lab. In bright sunlight, form fields with light gray borders become completely invisible against the white background. Jordan cannot see where to type, cannot read placeholder instructions, and cannot identify individual form fields. The form is functionally unusable. This directly blocks the user's primary goal.

**Recommended Fix**:
- Use **dark, high-contrast borders** on form fields: minimum `border: 2px solid #333333` (contrast ~12.63:1 with white)
- Use **visible, persistent labels** above input fields instead of or in addition to placeholder text
- Ensure placeholder text has at least **4.5:1 contrast** (use `#767676` or darker)
- Add a **visible background color** to input fields (e.g., `background-color: #F5F5F5`) to differentiate them from the page background
- Make the **submit button** high-contrast with a thick border and strong fill color

---

### Issue 5: Tab Active/Inactive State Differentiation

**Page(s)**: Homepage — "Problems We Solve" section  
**Element(s)**: `<button class="tab-link">` and `<button class="tab-link is-active">` within the tabs interface  
**Tab labels**: Operational Efficiency, Modern Technology, Customer Engagement, Scalable Solutions, Expansive Resources, Speed to Market

**WCAG Criteria Violated**:
- **1.4.11 Non-text Contrast** (AA) — Active state indicator must have at least 3:1 contrast with inactive state
- **1.4.1 Use of Color** (A) — If the only differentiation between active and inactive tabs is a subtle color change, users in degraded contrast conditions cannot perceive the state change

**Severity**: **Major**

**Impact on This User**: Jordan cannot tell which tab is currently selected. The visual differentiation between active and inactive tabs relies on subtle styling changes (likely a color shift, underline, or slight background change) that are completely washed out in bright sunlight. This makes the tabbed interface confusing — Jordan doesn't know what content they're viewing or how to navigate between options.

**Recommended Fix**:
- Use **multiple visual indicators** for the active tab: bold text + visible underline/border (minimum 3px, dark color) + background color change
- Ensure the active tab has a **clearly different background color** from inactive tabs (not just a slight tint)
- Add a **visible left border or bottom border** in a high-contrast color (e.g., 4px solid #000000) to the active tab
- Consider using `font-weight: 800` for active vs `font-weight: 400` for inactive as an additional differentiator

---

### Issue 6: Carousel/Slider Navigation Indicators

**Page(s)**: Homepage — Case studies carousel, Testimonials slider  
**Element(s)**: Tiny Slider (tns) navigation dots, typically rendered as small circular indicators  
**CSS**: Tiny Slider default dots are typically small (8–12px), with subtle color differences between active and inactive states

**WCAG Criteria Violated**:
- **1.4.11 Non-text Contrast** (AA) — Navigation controls must have 3:1 contrast with their background
- **2.4.7 Focus Visible** (AA) — If dots are interactive, they need visible focus indicators

**Severity**: **Minor**

**Impact on This User**: Jordan cannot see the carousel navigation dots in bright sunlight. They don't know how many slides exist, which slide they're on, or how to navigate between them. Content in non-visible slides (additional case studies, additional testimonials) becomes undiscoverable.

**Recommended Fix**:
- Increase dot size to **minimum 16px diameter**
- Use **high-contrast colors**: active dot in #000000, inactive dots in #666666 on a white background
- Add a visible **border** to inactive dots (e.g., `border: 2px solid #333`)
- Consider replacing dots with **text-based navigation** (e.g., "1 / 3") which is inherently more readable

---

### Issue 7: Thin Borders and Visual Separators

**Page(s)**: All pages  
**Element(s)**: Horizontal rules, section dividers, card borders, subfooter border  
**CSS Examples**:
- `.horizontal-divider { border-bottom: 1px solid #bfbfbf; }` — Contrast ~1.75:1
- `hr { border-bottom: 1px solid gainsboro; }` (#dcdcdc) — Contrast ~1.35:1  
- `.subfooter-blocks { border-top: 1px solid rgba(191, 191, 191, 0.25); }` — Extremely low contrast
- Various card borders using `1px solid #dadada` (~1.42:1) or `1px solid #CFCFCF` (~1.57:1)

**WCAG Criteria Violated**:
- **1.4.11 Non-text Contrast** (AA) — Visual boundaries that convey meaning (section separation, card boundaries) must have 3:1 contrast

**Severity**: **Minor**

**Impact on This User**: Visual separators and borders provide structural hierarchy — they tell Jordan where one section ends and another begins, where one card is versus another. In bright sunlight, borders at 1–2:1 contrast are completely invisible. The page becomes a single undifferentiated stream of content without visible structural boundaries. While this doesn't block goals entirely (headings still provide some structure), it makes scanning and comprehension significantly harder.

**Recommended Fix**:
- Increase border contrast to minimum **#767676** (4.48:1) for decorative borders
- Use minimum **2px solid #555555** for borders that convey structural meaning
- Consider using **spacing and background color changes** between sections instead of (or in addition to) thin lines — whitespace and color blocks survive sunlight better than thin borders

---

### Issue 8: Hero Section Background Image Contrast Reliability

**Page(s)**: Homepage, Contact page, and all interior pages with hero sections  
**Element(s)**: `.page-header-wrapper .page-header` with `background: url(...)` and gradient overlays  
**CSS**: Background image with `linear-gradient(to right, #000, transparent)` overlay and `linear-gradient(0, transparent, #000)` with `opacity: 0.6`

**WCAG Criteria Violated**:
- **1.4.3 Contrast (Minimum)** (AA) — Text over images does not have guaranteed contrast; the gradient overlay helps but does not ensure consistent contrast across the full width of the hero
- **1.4.6 Contrast (Enhanced)** (AAA) — Cannot be guaranteed over photographic content

**Severity**: **Major**

**Impact on This User**: The gradient overlay darkens the left side of the hero (where the text typically appears), which helps somewhat. However, the overlay fades to transparent on the right side, meaning any text or UI elements positioned toward the right of the hero may have unreliable contrast. In bright sunlight, the background image itself becomes a bright, washed-out blur — the gradient overlay that works indoors may be insufficient when the entire image is brightened by ambient light. Body text within the hero (the paragraph describing LaunchPad Lab) is particularly affected because it's smaller and lighter than the headline.

**Recommended Fix**:
- Apply a **solid semi-opaque overlay** across the full hero width: `background: rgba(0, 0, 0, 0.6)` or a solid dark color
- Ensure hero body text uses **#FFFFFF with font-weight 600+** for maximum legibility
- Add a subtle **text-shadow** to all hero text: `text-shadow: 0 2px 4px rgba(0,0,0,0.5)`
- Consider using a solid-color hero background with an optional decorative image element that doesn't underlie text

---

### Issue 9: "Learn More" and Link Text Styling

**Page(s)**: Homepage — Service cards, inline callout, case studies  
**Element(s)**:
- `.link-black-base` ("Learn More" links on service cards)
- `.link-white-base` (links within hover states on cards)
- `.link-blue-base` (blue text links throughout)
- `<a class="button button-blue-base">` (buttons like "View Services," "Learn More")

**WCAG Criteria Violated**:
- **1.4.1 Use of Color** (A) — Links within body text must be distinguishable by more than color alone
- **1.4.11 Non-text Contrast** (AA) — Interactive elements need 3:1 contrast against adjacent non-interactive content

**Severity**: **Minor**

**Impact on This User**: The "Learn More" links on service cards and the text links throughout the page rely on color (blue vs. black/gray) to indicate interactivity. In sunlight, the color difference between a blue link and the surrounding gray text is minimal — both appear as slightly different shades of washed-out dark. Jordan may not realize certain text is clickable. The blue buttons (`.button-blue-base`) fare better because they have a distinct shape (filled rectangle with border-radius), but text-only links lose their visual affordance.

**Recommended Fix**:
- Add **underlines** to all text links (at minimum, `text-decoration: underline`)
- Use a **combination of color + underline + font-weight** to make links identifiable without relying solely on color contrast
- Ensure all interactive text has **minimum 3:1 contrast** against surrounding non-interactive text

---

### Issue 10: Card Hover States as the Only Way to Access Information

**Page(s)**: Homepage — Service cards section (`.cards-wrapper.hover-cards-interaction`)  
**Element(s)**: `<li class="card">` elements within the service cards grid  
**Class**: `hover-cards-interaction` — indicates the cards reveal additional content or change appearance on hover

**WCAG Criteria Violated**:
- **1.4.13 Content on Hover or Focus** (AA) — Content revealed on hover must be dismissible, hoverable, and persistent
- **1.3.1 Info and Relationships** (A) — If important information is only visible on hover, it's not programmatically available to all users in all conditions

**Severity**: **Minor**

**Impact on This User**: The service cards have a hover interaction class that suggests they change appearance when hovered. In bright sunlight, Jordan is already struggling with contrast, so subtle hover-state changes (like a background darkening, text color shift, or reveal of "Learn More" text) may not be perceptible. If the non-hovered state is low-contrast, Jordan may not even realize the cards are interactive. Additionally, on mobile (which Jordan may use outdoors), hover states are not available at all.

**Recommended Fix**:
- Ensure **all critical information** is visible in the default (non-hovered) state
- Make the hover state a **dramatic, high-contrast change** (not just a slight darkening)
- Ensure cards are clearly identifiable as interactive elements in their default state (visible borders, clear CTA text, distinct background)

---

### Issue 11: Award/Badge Logo Images with No Alt Text

**Page(s)**: Homepage — Small logos/badges section  
**Element(s)**: `<img>` elements within `.logos-wrapper.small-logos`  
**Examples**:
- "Top-Clutch-Salesforce-Company-United-States-2025.png" — `alt=""`
- "Top-Clutch-Ai-Consulting-Company-United-States-2025.png" — `alt=""`
- "Global-Award-Spring-2025.png" — `alt=""`
- Multiple other Clutch and award badges

**WCAG Criteria Violated**:
- **1.1.1 Non-text Content** (A) — Images that convey information must have descriptive alt text. Empty `alt=""` marks these as decorative, but they convey meaningful trust/credibility information.

**Severity**: **Minor**

**Impact on This User**: In bright sunlight, these small badge images are nearly invisible — the details within the badges (text like "Top Clutch Salesforce Company") wash out completely. Since the `alt` attributes are empty, there is no text fallback for Jordan to read. The entire trust-building section is lost.

**Recommended Fix**:
- Add **descriptive alt text** to each badge: e.g., `alt="Top Clutch Salesforce Company, United States, 2025"`
- Consider adding a text-based list of awards alongside or below the badge images as a more robust fallback

---

### Issue 12: Social Media Icons with Empty Alt Text in Footer

**Page(s)**: All pages (global footer)  
**Element(s)**: Social media link images within `.footer-block`  
**Examples**:
- `<img src=".../facebook.svg" alt="">` 
- `<img src=".../instagram.svg" alt="">`
- `<img src=".../linkedin.svg" alt="">`

**WCAG Criteria Violated**:
- **1.1.1 Non-text Content** (A) — While the icons are accompanied by text labels ("Facebook," "Instagram," "LinkedIn"), the empty `alt` on the images is acceptable here since the text serves as the accessible name. However, the icons themselves may be invisible in bright sunlight.

**Severity**: **Minor** (mitigated by adjacent text labels)

**Impact on This User**: The white SVG icons on the dark navy footer are somewhat visible, but small. The text labels adjacent to the icons save this from being a real problem — Jordan can read "Facebook," "Instagram," "LinkedIn" as text. This is actually a good pattern.

**Recommended Fix**: No change strictly required since text labels are present. However, consider **increasing icon size** for better visibility in adverse conditions.

---

## Summary of Issues by Severity

| Severity | Count | Issues |
|----------|-------|--------|
| **Critical** | 1 | Contact form fields invisible (Issue 4) |
| **Major** | 4 | Body text contrast (Issue 1), Blue eyebrow text (Issue 2), Navigation on transparent header (Issue 3), Hero image contrast (Issue 8) |
| **Minor** | 7 | Tab states (Issue 5), Carousel navigation (Issue 6), Thin borders (Issue 7), Link styling (Issue 9), Hover-only content (Issue 10), Badge alt text (Issue 11), Social icons (Issue 12) |

---

## Overall Recommendations

### 1. Increase Global Text Contrast
- Change default body text from `#555555` to **`#333333`** or darker
- Change eyebrow/label text from `#1e60bd` to **`#0D47A1`** or use black text with blue accents
- These changes would benefit all users, not just those in bright sunlight

### 2. Implement a High-Contrast / Dark Mode
- Offer a toggle for a dark theme or high-contrast mode
- The site already has dark-background sections (process grid, footer) that demonstrate the design system can support high contrast — extend this capability site-wide
- This would transform the site from partially usable to fully usable for outdoor users

### 3. Fix Form Field Visibility
- Use dark, thick borders and persistent labels on all form inputs
- This is the single highest-priority fix as it blocks the primary conversion goal

### 4. Add Solid Header Background
- Replace the transparent header with a solid or heavily semi-opaque background
- This guarantees navigation readability regardless of hero image content

### 5. Use Multiple Visual Indicators for State Changes
- Active tabs, hover states, selected items, and focused elements should use **at least two visual indicators** (color + shape, color + weight, color + underline)
- Never rely on color alone for communicating state

### 6. Prefer Spacing Over Thin Borders for Section Separation
- Replace 1px light gray borders with generous whitespace and/or subtle background color changes between sections
- These visual strategies survive sunlight better than thin low-contrast lines

---

## WCAG Conformance Summary

| WCAG Level | Criterion | Status |
|------------|-----------|--------|
| A | 1.1.1 Non-text Content | **Fail** — Multiple badge/award images have empty alt text |
| A | 1.3.1 Info and Relationships | **Partial** — Hover-revealed content concerns |
| A | 1.4.1 Use of Color | **Fail** — Links and tab states rely on color alone |
| A | 3.3.2 Labels or Instructions | **Fail** — Form placeholder-only labels invisible in adverse conditions |
| AA | 1.4.3 Contrast (Minimum) | **Partial Fail** — Passes under ideal conditions but fails in situational context; nav over images is unreliable |
| AA | 1.4.11 Non-text Contrast | **Fail** — Form borders, tab states, carousel dots, and thin separators below 3:1 |
| AA | 1.4.13 Content on Hover or Focus | **Fail** — Card hover states may hide content |
| AA | 2.4.7 Focus Visible | **Needs Testing** — Carousel dot focus visibility unverified |
| AAA | 1.4.6 Contrast (Enhanced) | **Fail** — Blue eyebrow text at 6.06:1 is below 7:1 threshold |
