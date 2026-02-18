# Main Accessibility Report — launchpadlab.com

## Executive Summary

| Metric | Count |
|---|---|
| **Total Unique Issues** | 67 |
| **Critical** | 10 |
| **High** | 20 |
| **Medium** | 17 |
| **Low** | 17 (informational) |

**Site Tested:** https://launchpadlab.com/

**Personas Tested (17):** ADHD, Big Company Owner, Blue-Yellow Color Blind, Cognitive Disability, Dyslexic, Low Contrast Sensitivity, Low Vision Screen Magnifier, Low Vision, Motion Sensitivity, Motor Impairment, Non-Native Speaker, Red-Green Color Blind, Screen Reader, Senior Person, Situational Contrast, Skeptical User, Voice Control.

### Most Impactful Issues (by number of affected personas)

1. **C-03: Contact Form Requires JavaScript with No Fallback** — 10 personas
2. **C-05: Mega Menu Hover-Only Activation** — 6 personas
3. **C-07: Navigation Collapses to Tiny Unlabeled Hamburger** — 5 personas
4. **C-10: Auto-Scrolling Logo Carousels with No Pause Control** — 8 personas
5. **H-14: Pervasive Jargon and Complex Language** — 5 personas

---

## Critical Priority

### C-01: Missing `<main>` Landmark

**Summary:** No `<main>` element exists on any page. Screen reader users cannot jump to the primary content region, and the page lacks a fundamental document landmark required for assistive technology navigation.

**WCAG:** 1.3.1 Info and Relationships (A), 2.4.1 Bypass Blocks (A)

**Affected Elements:** Entire page structure — no `<main>` element present in the DOM.

**Affected Personas:** Screen Reader

---

### C-02: Broken Skip Navigation Link

**Summary:** The skip-to-content link targets `#primary`, but no element with `id="primary"` exists anywhere in the page. The link fails silently, providing no bypass mechanism for keyboard or assistive technology users.

**WCAG:** 2.4.1 Bypass Blocks (A)

**Affected Elements:** Skip link `<a href="#primary">` in the site header.

**Affected Personas:** Screen Reader, Voice Control, Motor Impairment, Low Vision

---

### C-03: Contact Form Requires JavaScript with No Fallback

**Summary:** The Ninja Forms contact form renders entirely via client-side JavaScript. The `<noscript>` fallback only displays "JavaScript is required to submit this form" with no alternative contact method (phone, email, mailto link). Users with JS disabled or broken JS execution have zero way to contact the company.

**WCAG:** 4.1.2 Name, Role, Value (A), 1.3.1 Info and Relationships (A), 3.3.2 Labels or Instructions (A)

**Affected Elements:** Ninja Forms container on the Contact page; `<noscript>` block.

**Affected Personas:** ADHD, Cognitive Disability, Dyslexic, Low Vision, Motor Impairment, Non-Native Speaker, Screen Reader, Senior Person, Skeptical User, Voice Control

---

### C-04: Hover-Reveal Content on Service Cards

**Summary:** Service card descriptions and "Learn More" links are hidden at `opacity: 0` until mouse hover. Content is completely invisible and inaccessible without a mouse — keyboard focus does not trigger the reveal, and voice control users cannot target hidden elements.

**WCAG:** 1.4.3 Contrast (Minimum) (AA), 1.3.1 Info and Relationships (A), 2.1.1 Keyboard (A), 1.4.13 Content on Hover or Focus (AA)

**Affected Elements:** `.service-card` overlays; descriptions and inner `<a>` links with `opacity: 0` default state.

**Affected Personas:** Low Contrast Sensitivity, Motor Impairment, Voice Control, Situational Contrast

---

### C-05: Mega Menu Hover-Only Activation

**Summary:** Navigation dropdown menus use a `hover_intent` pattern with a 300ms timeout. Keyboard users cannot reliably open submenus; screen magnifier users lose the menu while panning the viewport; voice control users experience inconsistent activation behavior.

**WCAG:** 2.1.1 Keyboard (A), 2.1.2 No Keyboard Trap (A), 2.5.1 Pointer Gestures (A)

**Affected Elements:** Primary navigation `<nav>` mega menu dropdowns; `hover_intent` JavaScript handlers.

**Affected Personas:** Motor Impairment, Low Vision Screen Magnifier, Voice Control, Senior Person, ADHD, Cognitive Disability

---

### C-06: Insufficient/Missing Visible Focus Indicators

**Summary:** No custom `:focus` or `:focus-visible` styles are defined in the site CSS. The default browser focus outlines are insufficient on colored backgrounds (blue hero sections, dark footers) and provide no visible indication of the currently focused element for keyboard navigators.

**WCAG:** 2.4.7 Focus Visible (AA), 2.4.11 Focus Not Obscured (AA), 1.4.11 Non-text Contrast (AA)

**Affected Elements:** All interactive elements site-wide — links, buttons, form inputs, navigation items.

**Affected Personas:** Motor Impairment, ADHD, Low Vision

---

### C-07: Navigation Collapses to Tiny Unlabeled Hamburger

**Summary:** At 150%+ zoom or on mobile viewports, the navigation collapses to a hamburger icon. The toggle is a `<div id="burgerBtn">` rather than a `<button>`, has no ARIA role, no `aria-label`, and no `aria-expanded` state. It is invisible to screen readers, unreachable by keyboard, and untargetable by voice control.

**WCAG:** 4.1.2 Name, Role, Value (A), 2.1.1 Keyboard (A), 1.4.4 Resize Text (AA)

**Affected Elements:** `<div id="burgerBtn">` in the site header.

**Affected Personas:** Voice Control, Low Vision, Senior Person, Cognitive Disability, Motor Impairment

---

### C-08: Form Input Fields Have No Visible Border

**Summary:** Contact form inputs use `background-color: rgba(255,255,255,0.2)` with `border: none` on the blue background section. The resulting contrast ratio is approximately 1.51:1 — far below the 3:1 minimum for UI components. Fields are effectively invisible in bright ambient light.

**WCAG:** 1.4.11 Non-text Contrast (AA), 1.3.1 Info and Relationships (A), 3.3.2 Labels or Instructions (A)

**Affected Elements:** Contact form `<input>` and `<textarea>` fields.

**Affected Personas:** Low Contrast Sensitivity, Situational Contrast

---

### C-09: AOS Animations Do Not Respect `prefers-reduced-motion`

**Summary:** The AOS (Animate On Scroll) library is initialized without the `disable` option for reduced-motion preferences. Content blocks start at `opacity: 0` and animate into view on scroll. The CSS contains zero `@media (prefers-reduced-motion)` queries, meaning users who have requested reduced motion still experience all animations.

**WCAG:** 2.3.3 Animation from Interactions (AAA), 2.2.2 Pause, Stop, Hide (A)

**Affected Elements:** AOS library initialization; all elements with `data-aos` attributes; site-wide CSS.

**Affected Personas:** Motion Sensitivity, ADHD, Senior Person, Low Vision Screen Magnifier

---

### C-10: Auto-Scrolling Logo Carousels with No Pause Control

**Summary:** Client logo marquee sections scroll infinitely via CSS/JS animation with no pause, stop, or manual control mechanism. This is persistent, distracting motion that cannot be dismissed, and the content within is inaccessible to users who need more time.

**WCAG:** 2.2.2 Pause, Stop, Hide (A)

**Affected Elements:** Client logo marquee/carousel sections on the homepage and other pages.

**Affected Personas:** ADHD, Dyslexic, Low Vision Screen Magnifier, Low Vision, Motor Impairment, Senior Person, Skeptical User, Voice Control

---

## High Priority

### H-11: Links Visually Indistinguishable from Body Text

**Summary:** In-line links use `color: #555555`, identical to body text, with no underline or other non-color visual differentiator. The only indication is a color change on hover, which is not available to keyboard or touch users.

**WCAG:** 1.4.1 Use of Color (A)

**Affected Elements:** All inline `<a>` elements within body content.

**Affected Personas:** Low Contrast Sensitivity, Low Vision, Red-Green Color Blind, Situational Contrast

---

### H-12: Identical "Learn More" Links (6–7 Instances)

**Summary:** Service cards each contain a "Learn More" link with no distinguishing `aria-label` or context. When a screen reader lists all links, 6–7 identical "Learn More" entries appear. Voice control users saying "click Learn More" trigger disambiguation dialogs.

**WCAG:** 2.4.4 Link Purpose (In Context) (A), 2.4.9 Link Purpose (Link Only) (AAA), 2.5.3 Label in Name (A)

**Affected Elements:** `<a>` elements within `.service-card` components containing text "Learn More."

**Affected Personas:** Screen Reader, Voice Control, ADHD, Cognitive Disability

---

### H-13: Duplicate/Nested Links on Service Cards

**Summary:** Each service card has an outer `<a>` wrapper element plus an inner `<a>Learn More</a>` both pointing to the same URL. This is invalid nested `<a>` HTML, creates duplicate tab stops, and doubles the announced links for screen readers.

**WCAG:** 4.1.1 Parsing (A), 2.4.4 Link Purpose (In Context) (A)

**Affected Elements:** `.service-card` outer `<a>` wrappers and inner `<a class="learn-more">` elements.

**Affected Personas:** Low Vision Screen Magnifier, Motor Impairment, Voice Control, Screen Reader

---

### H-14: Pervasive Jargon and Complex Language

**Summary:** Site copy is saturated with unexplained jargon ("Agentic AI," "bespoke," "cross-functional teams"), acronyms (ROI, CSAT), and idioms ("ship game-changing products," "harness the power"). No glossary, tooltips, or plain-language alternatives are provided.

**WCAG:** 3.1.5 Reading Level (AAA), 3.1.3 Unusual Words (AAA), 3.1.4 Abbreviations (AAA)

**Affected Elements:** Body copy, headings, CTAs, and mega menu descriptions across all pages.

**Affected Personas:** Cognitive Disability, Non-Native Speaker, Senior Person, Big Company Owner, Skeptical User

---

### H-15: Body Text Contrast (#555555 on White)

**Summary:** Body text at `#555555` on `#FFFFFF` achieves 7.46:1, passing AA but failing AAA (7:1 for normal text). Under bright ambient lighting conditions, effective contrast drops to an estimated 2.5–3.7:1, causing significant fatigue for extended reading sessions.

**WCAG:** 1.4.3 Contrast (Minimum) (AA), 1.4.6 Contrast (Enhanced) (AAA)

**Affected Elements:** All `<p>`, `<li>`, and body-level text elements with `color: #555555`.

**Affected Personas:** Dyslexic, Low Contrast Sensitivity, Situational Contrast, Low Vision

---

### H-16: Hero Text on Photographic Background with Inconsistent Contrast

**Summary:** White hero text is placed over photographic backgrounds with gradient overlays that fade to transparent. Contrast varies significantly across different viewport sizes and positions within the image, with some areas falling well below the 4.5:1 minimum.

**WCAG:** 1.4.3 Contrast (Minimum) (AA), 1.4.6 Contrast (Enhanced) (AAA)

**Affected Elements:** Hero section `<h1>`, `<h2>`, and `<p>` elements overlaying background images.

**Affected Personas:** Low Contrast Sensitivity, Low Vision, Situational Contrast

---

### H-17: Contact Info Buried Below Form and Testimonials

**Summary:** On the Contact page, the phone number and email address appear only after the full contact form and five testimonial cards. Users must scroll extensively to find direct contact information, which is a critical conversion path for enterprise buyers and less technical users.

**WCAG:** 2.4.5 Multiple Ways (AA)

**Affected Elements:** Contact page layout — phone/email placement below form and testimonials.

**Affected Personas:** Big Company Owner, Senior Person, Low Vision Screen Magnifier, Non-Native Speaker

---

### H-18: Hero Headline Fails to Communicate Core Offering

**Summary:** The homepage hero reads "AI Innovation. Digital Solutions. Results that Matter." — a string of vague buzzwords that does not communicate what the company actually does. Users must read multiple paragraphs below the fold to understand the service offering.

**WCAG:** 3.1.5 Reading Level (AAA)

**Affected Elements:** Homepage hero `<h1>` and supporting `<p>` text.

**Affected Personas:** Big Company Owner, Senior Person, Cognitive Disability, Non-Native Speaker, Skeptical User

---

### H-19: Award/Badge Images Missing Alt Text

**Summary:** Seven Clutch award badge images have `alt=""`, treating them as decorative. These badges convey meaningful credibility information (ratings, rankings, award year) that is completely lost for screen reader users and when images fail to load.

**WCAG:** 1.1.1 Non-text Content (A)

**Affected Elements:** Clutch badge `<img>` elements with empty `alt` attributes.

**Affected Personas:** Screen Reader, Blue-Yellow Color Blind, Red-Green Color Blind, Low Vision Screen Magnifier, Low Vision, Skeptical User, Situational Contrast

---

### H-20: Carousel/Slider Content Not Keyboard Accessible

**Summary:** Case study and testimonial carousels are initialized with `controls: false` and `nav: false`. No arrow buttons or dot indicators are rendered. The only interaction method is mouse click-and-drag, making all carousel content inaccessible to keyboard and voice control users.

**WCAG:** 2.1.1 Keyboard (A), 4.1.2 Name, Role, Value (A), 2.5.1 Pointer Gestures (A)

**Affected Elements:** Tiny Slider (tns) carousel instances for case studies and testimonials.

**Affected Personas:** Motor Impairment, Voice Control, Low Vision Screen Magnifier, Senior Person

---

### H-21: Tab Active State Relies on Color Alone

**Summary:** The "Problems We Solve" tabbed interface differentiates the active tab solely through a color change. No additional visual indicator (underline, border, background fill, icon, or font weight change) is present to convey state for color-blind users.

**WCAG:** 1.4.1 Use of Color (A)

**Affected Elements:** Tab buttons in the "Problems We Solve" section.

**Affected Personas:** Blue-Yellow Color Blind, Red-Green Color Blind, Situational Contrast

---

### H-22: Inconsistent CTA Terminology

**Summary:** The site uses 5+ different phrases for what is essentially the same action (contact/connect): "Connect with an Expert," "Let's Build Something Great," "Reach Out," "Let's Connect," "Let's Get Social." This inconsistency increases cognitive load and creates uncertainty about what each CTA does.

**WCAG:** 3.2.4 Consistent Identification (AA)

**Affected Elements:** CTA buttons and links across all pages.

**Affected Personas:** Cognitive Disability, Non-Native Speaker, Senior Person

---

### H-23: Statistics Counter Animation Ignores `prefers-reduced-motion`

**Summary:** Numerical statistics animate from 0 to their final value over ~2 seconds using `requestAnimationFrame`. There is no check for `prefers-reduced-motion`, so the animation plays regardless of user system preferences.

**WCAG:** 2.3.3 Animation from Interactions (AAA)

**Affected Elements:** Counter animation JavaScript; statistics number elements on homepage and About page.

**Affected Personas:** Motion Sensitivity

---

### H-24: CSS Has Zero `prefers-reduced-motion` Media Queries

**Summary:** The site's CSS includes multiple `@keyframes` animations and transition declarations that run unconditionally. Not a single `@media (prefers-reduced-motion: reduce)` query exists in any stylesheet to disable or simplify animations for users who have requested reduced motion.

**WCAG:** 2.3.3 Animation from Interactions (AAA)

**Affected Elements:** All CSS files; `@keyframes` declarations; `transition` properties site-wide.

**Affected Personas:** Motion Sensitivity, ADHD

---

### H-25: Smooth Scrolling Ignores `prefers-reduced-motion`

**Summary:** All anchor link navigation uses `scrollIntoView({ behavior: 'smooth' })` without checking `window.matchMedia('(prefers-reduced-motion: reduce)')`. Users who have requested reduced motion still experience animated scrolling.

**WCAG:** 2.3.3 Animation from Interactions (AAA)

**Affected Elements:** Smooth scroll JavaScript handlers on anchor links.

**Affected Personas:** Motion Sensitivity

---

### H-26: Service Card Hover Animations Not Reducible

**Summary:** Service cards apply multi-property CSS transitions (transform, opacity, box-shadow) on hover that are not disabled or simplified when `prefers-reduced-motion` is active.

**WCAG:** 2.3.3 Animation from Interactions (AAA)

**Affected Elements:** `.service-card` hover transition CSS.

**Affected Personas:** Motion Sensitivity

---

### H-27: Contact Form Two-Column Layout Doesn't Reflow

**Summary:** The contact form uses a two-column layout with half-width fields that does not properly reflow to a single column at high magnification levels. Users at 200%+ zoom encounter a zigzag reading pattern and horizontal scrolling.

**WCAG:** 1.4.10 Reflow (AA), 1.4.4 Resize Text (AA)

**Affected Elements:** Contact form `<div>` grid/flex containers with half-width field wrappers.

**Affected Personas:** Low Vision Screen Magnifier, Low Vision

---

### H-28: Duplicate h1/h2 on Contact Page

**Summary:** The Contact page has both an `<h1>` and an `<h2>` with the identical text "Ready to Build Something Great?" This creates confusion for screen reader users navigating by headings and provides no meaningful document structure differentiation.

**WCAG:** 1.3.1 Info and Relationships (A), 2.4.6 Headings and Labels (AA)

**Affected Elements:** Contact page `<h1>` and `<h2>` elements.

**Affected Personas:** Screen Reader, ADHD, Non-Native Speaker

---

### H-29: Form Validation Likely Uses Color Alone

**Summary:** Ninja Forms' default validation styling uses a red border to indicate errors. No icon, text prefix, or other non-color indicator accompanies the error state, making it imperceptible to color-blind users.

**WCAG:** 1.4.1 Use of Color (A), 3.3.1 Error Identification (A)

**Affected Elements:** Ninja Forms error state CSS; `.nf-error` class styling.

**Affected Personas:** Red-Green Color Blind, Blue-Yellow Color Blind

---

### H-30: Mega Menu Close Button Is Icon-Only

**Summary:** The mega menu close button uses an "X" icon with `aria-label="Close"` but no visible text label. Voice control users cannot reliably target the button since the visible label does not match the accessible name.

**WCAG:** 2.5.3 Label in Name (A), 4.1.2 Name, Role, Value (A)

**Affected Elements:** Mega menu close button element.

**Affected Personas:** Voice Control

---

## Medium Priority

### M-31: Tab Panel Images Have Empty Alt Text

**Summary:** Six images within the "Problems We Solve" tab panels have `alt=""`, treating them as decorative. These images illustrate specific solutions and convey meaningful context about the tab content.

**WCAG:** 1.1.1 Non-text Content (A)

**Affected Elements:** `<img>` elements within `.tab-panel` containers.

**Affected Personas:** Screen Reader, Low Vision Screen Magnifier, Skeptical User

---

### M-32: Tabbed Interface Spatial Separation

**Summary:** The "Problems We Solve" tabbed interface places tab labels on the left and tab content on the right in a side-by-side layout. At magnification levels of 200%+, users can only see one side at a time, breaking the visual association between tabs and content.

**WCAG:** 1.3.2 Meaningful Sequence (A), 1.4.10 Reflow (AA)

**Affected Elements:** "Problems We Solve" tab container layout.

**Affected Personas:** Low Vision Screen Magnifier

---

### M-33: Dense Paragraph Text Without Chunking

**Summary:** Body copy across the site consists of 40–80+ word paragraphs without bullet points, sub-headings, or other visual chunking. Long unbroken text blocks increase cognitive load and reduce scanability.

**WCAG:** 3.1.5 Reading Level (AAA), 1.4.8 Visual Presentation (AAA)

**Affected Elements:** Body `<p>` elements across all pages, particularly Services and About.

**Affected Personas:** ADHD, Dyslexic, Non-Native Speaker

---

### M-34: Tight Line-Height on Headings (1.1)

**Summary:** Multi-line headings use a `line-height` of approximately 1.1, causing lines to appear nearly touching. This significantly reduces readability for users with dyslexia or visual processing differences.

**WCAG:** 1.4.12 Text Spacing (AA), 1.4.8 Visual Presentation (AAA)

**Affected Elements:** `<h1>`, `<h2>`, `<h3>` elements with multi-line content.

**Affected Personas:** Dyslexic

---

### M-35: Body Line-Height Reset to 1

**Summary:** The CSS rule `body { line-height: 1 }` removes default line spacing for all elements that do not have a more specific override, resulting in cramped text in edge cases throughout the site.

**WCAG:** 1.4.12 Text Spacing (AA)

**Affected Elements:** `body` CSS rule; any text elements inheriting this value.

**Affected Personas:** Dyslexic

---

### M-36: Decorative Font (Permanent Marker) Loaded

**Summary:** The "Permanent Marker" Google Font — an irregular handwriting-style typeface — is loaded globally and applied to certain decorative text elements. This font is largely illegible for users with dyslexia due to its inconsistent letter shapes and spacing.

**WCAG:** 1.4.8 Visual Presentation (AAA)

**Affected Elements:** Elements styled with `font-family: 'Permanent Marker'`.

**Affected Personas:** Dyslexic

---

### M-37: Ghost/Outline Buttons Have Low Visual Prominence

**Summary:** Ghost-style CTA buttons use white text with a thin (1px) border on colored backgrounds. The low visual weight makes them hard to identify as interactive elements, especially for users with reduced visual acuity.

**WCAG:** 1.4.11 Non-text Contrast (AA)

**Affected Elements:** `.btn-outline`, `.ghost-btn` (or equivalent) button elements.

**Affected Personas:** Low Vision, Situational Contrast

---

### M-38: Card Borders Insufficient Contrast (1.56:1)

**Summary:** Card component borders use `#CFCFCF` on a `#FFFFFF` background, yielding only 1.56:1 contrast — well below the 3:1 minimum for meaningful UI boundaries.

**WCAG:** 1.4.11 Non-text Contrast (AA)

**Affected Elements:** `.card` border styles.

**Affected Personas:** Low Contrast Sensitivity

---

### M-39: Section Dividers/Separators Below 3:1

**Summary:** Various section dividers and horizontal rules use border colors in the 1.56:1–1.84:1 contrast range against their backgrounds, failing the 3:1 non-text contrast requirement.

**WCAG:** 1.4.11 Non-text Contrast (AA)

**Affected Elements:** `<hr>`, section border-bottom, and divider elements site-wide.

**Affected Personas:** Low Contrast Sensitivity, Situational Contrast

---

### M-40: Link Hover State Reduces Contrast via Opacity

**Summary:** Links apply `opacity: 0.6` on hover, which drops the text contrast of `#555555` on white from 7.46:1 to below the 4.5:1 AA threshold for the hover state.

**WCAG:** 1.4.3 Contrast (Minimum) (AA)

**Affected Elements:** `a:hover` CSS rule with `opacity: 0.6`.

**Affected Personas:** Low Contrast Sensitivity

---

### M-41: Placeholder Text White on Light Backgrounds

**Summary:** A global CSS rule sets `::placeholder { color: #FFF }`, which renders placeholder text completely invisible on white or light-colored input backgrounds outside the blue contact section.

**WCAG:** 1.4.3 Contrast (Minimum) (AA), 3.3.2 Labels or Instructions (A)

**Affected Elements:** `::placeholder` global CSS rule; any `<input>` or `<textarea>` on light backgrounds.

**Affected Personas:** Low Contrast Sensitivity

---

### M-42: reCAPTCHA Inaccessible at Magnification/Voice

**Summary:** The Google reCAPTCHA image grid challenge becomes impossible to complete at 300%+ zoom due to tiny image tiles, and voice control users have no text labels to target individual grid cells.

**WCAG:** 1.1.1 Non-text Content (A), 2.1.1 Keyboard (A)

**Affected Elements:** reCAPTCHA `<iframe>` on the Contact page.

**Affected Personas:** Low Vision Screen Magnifier, Voice Control

---

### M-43: Statistics Labels Misused as H2

**Summary:** Numerical statistics labels (e.g., "Years in Business," "Projects Delivered") are coded as `<h2>` headings. This pollutes the heading hierarchy and creates misleading navigation landmarks for screen reader users.

**WCAG:** 1.3.1 Info and Relationships (A), 2.4.6 Headings and Labels (AA)

**Affected Elements:** Statistics section `<h2>` elements used as data labels.

**Affected Personas:** Screen Reader, ADHD, Cognitive Disability

---

### M-44: About Page Team Photos Have Empty Alt Text

**Summary:** Fifteen leadership team photos on the About page have `alt=""`, hiding team members' names and roles from screen reader users. This reduces trust and transparency since users cannot confirm who is behind the company.

**WCAG:** 1.1.1 Non-text Content (A)

**Affected Elements:** Team member `<img>` elements on the About page.

**Affected Personas:** Skeptical User

---

### M-45: "Case Study Increase" Icons Missing Alt Text

**Summary:** Arrow/increase icons in case study statistics have `alt=""` but convey directional meaning (increase/growth). The visual information is lost for screen reader users and color-blind users who may not distinguish the icon color.

**WCAG:** 1.1.1 Non-text Content (A)

**Affected Elements:** Arrow/trend `<img>` icons within case study stat blocks.

**Affected Personas:** Screen Reader, Blue-Yellow Color Blind, Red-Green Color Blind

---

### M-46: No Phone Number in Site Header

**Summary:** The company phone number and email are only available in the footer and buried on the Contact page. Enterprise buyers and less tech-savvy users expect quick access to a phone number in the header.

**WCAG:** 2.4.5 Multiple Ways (AA)

**Affected Elements:** Site header — missing phone/email contact info.

**Affected Personas:** Big Company Owner, Senior Person

---

### M-47: Bloom Popup Interrupts User Flow

**Summary:** A timed Bloom (Elegant Themes) email opt-in popup appears as a modal overlay, interrupting reading flow. No advance warning is given, and the popup traps attention at an arbitrary point during content consumption.

**WCAG:** 2.2.4 Interruptions (AAA)

**Affected Elements:** Bloom popup modal overlay.

**Affected Personas:** ADHD

---

## Low Priority

### L-48: Excessive Homepage Length (11+ Sections)

**Summary:** The homepage contains 11+ full-width sections requiring extensive scrolling. This creates information overload, particularly for users with attention or cognitive differences and enterprise decision-makers looking for quick answers.

**WCAG:** 2.4.1 Bypass Blocks (A)

**Affected Elements:** Homepage section structure and page length.

**Affected Personas:** ADHD, Big Company Owner, Senior Person

---

### L-49: No Pricing or Engagement Model Info

**Summary:** The site provides zero information about pricing, engagement models, or the process of working with the company. Decision-makers must submit a form just to learn basic business terms.

**WCAG:** N/A (UX / trust concern)

**Affected Elements:** Site-wide content — missing pricing/process pages or sections.

**Affected Personas:** Skeptical User, Big Company Owner

---

### L-50: AI Keyword Saturation Without Substantiation

**Summary:** "AI" appears in nearly every heading and section but is not backed by specific AI case studies, technical details, or measurable outcomes. This erodes trust with savvy evaluators.

**WCAG:** N/A (content credibility concern)

**Affected Elements:** Headings, hero copy, and service descriptions across all pages.

**Affected Personas:** Skeptical User, Big Company Owner

---

### L-51: "Insights" Nav Label Instead of "Blog"

**Summary:** The navigation uses "Insights" as the label for the blog section, but the URL is `/blog/`. This mismatch creates confusion for non-native speakers and users unfamiliar with corporate euphemisms.

**WCAG:** 2.4.6 Headings and Labels (AA)

**Affected Elements:** Primary navigation "Insights" link pointing to `/blog/`.

**Affected Personas:** Non-Native Speaker, Senior Person

---

### L-52: Grammar Error "deliver more better"

**Summary:** The Services mega menu contains the grammatically incorrect phrase "deliver more better," which undermines professionalism and creates confusion for non-native speakers.

**WCAG:** 3.1.5 Reading Level (AAA)

**Affected Elements:** Services mega menu description text.

**Affected Personas:** Non-Native Speaker, Cognitive Disability

---

### L-53: Footer Phone Link Malformed HTML

**Summary:** The phone link in the footer has a double closing quote in the `href` attribute: `href="tel:312-888-9651""`. This invalid HTML may cause inconsistent behavior across browsers and assistive technologies.

**WCAG:** 4.1.1 Parsing (A)

**Affected Elements:** Footer `<a href="tel:...">` element.

**Affected Personas:** Screen Reader, Senior Person, Skeptical User

---

### L-54: Social Media Icons Have Empty Alt Text

**Summary:** Social media icon images use `alt=""`. The impact is mitigated by adjacent visible text labels, but the icons themselves are invisible to screen readers if encountered in isolation.

**WCAG:** 1.1.1 Non-text Content (A)

**Affected Elements:** Social media icon `<img>` elements in footer/header.

**Affected Personas:** Screen Reader (mitigated)

---

### L-55: Navigation `<nav>` Lacks `aria-label`

**Summary:** Multiple `<nav>` elements exist on each page (primary nav, footer nav) but none have distinguishing `aria-label` or `aria-labelledby` attributes. Screen reader users cannot differentiate between navigation regions.

**WCAG:** 1.3.1 Info and Relationships (A), 4.1.2 Name, Role, Value (A)

**Affected Elements:** All `<nav>` elements site-wide.

**Affected Personas:** Screen Reader

---

### L-56: Wistia Video Embed Lacks Context

**Summary:** An embedded Wistia video has no visible title, description, or surrounding text to explain its content before a user decides to play it.

**WCAG:** 1.1.1 Non-text Content (A)

**Affected Elements:** Wistia video embed `<iframe>` / `<div>`.

**Affected Personas:** ADHD

---

### L-57: No Site-Level Accessibility Preferences

**Summary:** The site offers no user-facing toggles for dark mode, increased text size, reduced motion, or other accessibility preferences — features increasingly common and expected on modern sites.

**WCAG:** 1.4.8 Visual Presentation (AAA)

**Affected Elements:** Site header/footer — missing accessibility preference controls.

**Affected Personas:** ADHD, Motion Sensitivity

---

### L-58: Excessive Line Length on Wide Viewports

**Summary:** On wide viewports (1440px+), body text lines extend to 90–100+ characters, exceeding the recommended 80-character maximum for comfortable reading.

**WCAG:** 1.4.8 Visual Presentation (AAA)

**Affected Elements:** Body text containers on wide viewports — missing `max-width` constraints.

**Affected Personas:** Dyslexic

---

### L-59: Museo Slab Serif Font

**Summary:** The site uses Museo Slab — a serif font at light weight — as the primary body typeface. Serif fonts with thin strokes are harder to read for users with dyslexia compared to sans-serif alternatives.

**WCAG:** 1.4.8 Visual Presentation (AAA)

**Affected Elements:** `body { font-family: 'Museo Slab', ... }` CSS rule.

**Affected Personas:** Dyslexic

---

### L-60: Dev Environment URL in Production

**Summary:** At least one image loads from `dev-launchpadlab.pantheonsite.io` instead of the production domain, suggesting incomplete deployment hygiene and reducing perceived trustworthiness.

**WCAG:** N/A (trust/quality concern)

**Affected Elements:** Image `src` attribute referencing `dev-launchpadlab.pantheonsite.io`.

**Affected Personas:** Skeptical User

---

### L-61: Inconsistent Stats (12+ vs 13+ Years)

**Summary:** The homepage states "12+ Years" while the About page states "13+ Years in Business." This inconsistency raises questions about content accuracy and attention to detail.

**WCAG:** N/A (content accuracy concern)

**Affected Elements:** Homepage statistics section; About page statistics section.

**Affected Personas:** Skeptical User

---

### L-62: No Language Toggle/Multilingual Support

**Summary:** The site has no language selector or multilingual content, limiting access for non-native English speakers despite serving an international market.

**WCAG:** 3.1.1 Language of Page (A)

**Affected Elements:** Site header — missing language selection mechanism.

**Affected Personas:** Non-Native Speaker

---

### L-63: Case Study Button Text Is Ambiguous

**Summary:** Case study CTA buttons display only the client company name (e.g., "Cameo," "GoHealth") with no action verb. Users cannot determine what clicking the button will do without additional context.

**WCAG:** 2.4.4 Link Purpose (In Context) (A)

**Affected Elements:** Case study carousel/card CTA `<a>` elements.

**Affected Personas:** Screen Reader, Voice Control

---

### L-64: Small Font Size Preset (13px)

**Summary:** Some body text is set at 13px, below the commonly recommended 16px minimum for comfortable reading on screens, particularly for older users.

**WCAG:** 1.4.4 Resize Text (AA)

**Affected Elements:** Body text elements with `font-size: 13px`.

**Affected Personas:** Senior Person

---

### L-65: Contact Form Assumes Business Context

**Summary:** The contact form requires "Company Email" and "Company" as mandatory fields, creating barriers for individual users, freelancers, or retirees who may not have a company affiliation.

**WCAG:** N/A (UX concern)

**Affected Elements:** Contact form "Company Email" and "Company" required fields.

**Affected Personas:** Senior Person

---

### L-66: Blue CTA Buttons Lack Non-Color Emphasis

**Summary:** Blue CTA buttons appear as a muted gray to users with tritanopia (blue-yellow color blindness). Without an additional non-color visual indicator (bold border, icon, size difference), the buttons lose their visual prominence.

**WCAG:** 1.4.1 Use of Color (A)

**Affected Elements:** Primary CTA `<a>` / `<button>` elements with blue background.

**Affected Personas:** Blue-Yellow Color Blind

---

### L-67: Multiple Competing CTAs Create Choice Overload

**Summary:** The homepage contains 15+ call-to-action elements across its many sections. The sheer volume of CTAs competes for attention and creates decision paralysis, particularly for older users and those with attention differences.

**WCAG:** N/A (UX / cognitive load concern)

**Affected Elements:** Homepage CTA buttons and links across 11+ sections.

**Affected Personas:** Senior Person, ADHD

---

## Appendix: Persona Cross-Reference

| Persona | Issues Affecting This Persona |
|---|---|
| **ADHD** | C-03, C-05, C-06, C-09, C-10, H-12, H-24, H-28, M-33, M-43, M-47, L-48, L-57, L-67 |
| **Big Company Owner** | H-14, H-17, H-18, M-46, L-48, L-49, L-50 |
| **Blue-Yellow Color Blind** | H-19, H-21, H-29, M-45, L-66 |
| **Cognitive Disability** | C-03, C-05, C-07, H-12, H-14, H-18, H-22, M-43, L-52 |
| **Dyslexic** | C-03, C-10, H-15, M-33, M-34, M-35, M-36, L-58, L-59 |
| **Low Contrast Sensitivity** | C-04, C-08, H-11, H-15, H-16, M-38, M-39, M-40, M-41 |
| **Low Vision Screen Magnifier** | C-05, C-09, C-10, H-13, H-17, H-19, H-20, H-27, M-31, M-32, M-42 |
| **Low Vision** | C-02, C-03, C-06, C-07, C-10, H-11, H-15, H-16, H-19, H-27, M-37 |
| **Motion Sensitivity** | C-09, H-23, H-24, H-25, H-26, L-57 |
| **Motor Impairment** | C-02, C-03, C-04, C-05, C-06, C-07, C-10, H-13, H-20 |
| **Non-Native Speaker** | C-03, H-14, H-17, H-22, H-28, M-33, L-51, L-52, L-62 |
| **Red-Green Color Blind** | H-11, H-19, H-21, H-29, M-45 |
| **Screen Reader** | C-01, C-02, C-03, H-12, H-13, H-19, H-28, M-31, M-43, M-45, L-53, L-54, L-55, L-63 |
| **Senior Person** | C-03, C-05, C-07, C-09, C-10, H-14, H-17, H-18, H-20, H-22, M-46, L-48, L-51, L-53, L-64, L-65, L-67 |
| **Situational Contrast** | C-04, C-08, H-11, H-15, H-16, H-19, H-21, M-37, M-39 |
| **Skeptical User** | C-03, C-10, H-14, H-18, H-19, M-31, M-44, L-49, L-50, L-53, L-60, L-61 |
| **Voice Control** | C-02, C-03, C-04, C-05, C-07, C-10, H-12, H-13, H-20, H-30, M-42, L-63 |
