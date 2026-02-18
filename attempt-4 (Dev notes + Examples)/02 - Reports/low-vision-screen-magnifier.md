# Accessibility Report: Low Vision Screen Magnifier User

**Persona**: James Okonkwo — 61-year-old retired teacher with macular degeneration, uses screen magnifier at 200–400%
**Site Tested**: https://launchpadlab.com/ (homepage and /contact page)
**Date**: February 16, 2026
**Audit Scope**: Navigation, content discovery, contact form completion through a magnified viewport (5–10% visible at a time)

---

## Executive Summary

The LaunchPad Lab website presents **significant barriers** for screen magnifier users. While the core text content (hero section, headings, and descriptions) is well-structured and readable at high magnification, the site relies heavily on wide multi-column layouts, hover-triggered mega menus, auto-scrolling carousels, and spatially separated interactive components that break down when only a small portion of the viewport is visible. The contact form is functional but uses an unnecessarily wide two-column layout. Critical contact information (phone, email) is buried below the form rather than being immediately accessible.

**Issues Found**: 14
- Critical: 3
- Major: 7
- Minor: 4

---

## Issues

### Issue 1: Mega Menu Closes During Magnified Panning

**Page**: All pages (global header navigation)
**Element**: `#mega-menu-wrap-menu-1` — Services and Industries mega dropdown menus
**Description**: The mega menu uses `data-event="hover_intent"` with a `data-hover-intent-timeout="300"` (300ms). The Services dropdown renders as a 12-column grid (`--columns:12`) spanning the full viewport width with three groups of submenu items. At 200–400% magnification, the dropdown extends far beyond the visible viewport. When the user pans their magnified view (which requires moving the mouse), the cursor exits the menu hover area, triggering the 300ms timeout and closing the menu. The user cannot explore the full contents of the mega menu without it collapsing.
**WCAG Criteria Violated**:
- **2.5.8 Target Size (Minimum)** (Level AA) — The effective interactive area of the mega menu is too large to remain within a magnified viewport while requiring the cursor to stay within bounds.
- **2.1.1 Keyboard** (Level A) — While keyboard access exists (tabindex="0" on links), the hover-intent behavior penalizes mouse users who magnify, as mouse movement to pan the screen inadvertently closes the menu.
- **1.4.10 Reflow** (Level AA) — The mega menu does not adapt to a narrower viewport; at high zoom levels, content overflows horizontally.
**Severity**: **Critical**
**Impact on User**: James cannot browse service or industry sub-pages from the navigation. The menu closes every time he tries to pan to see additional items, creating a loop of open-pan-close that makes the dropdown effectively unusable.
**Recommended Fix**:
1. Add a click-to-open option for mega menus (not just hover), so the menu stays open until explicitly dismissed.
2. Increase the hover-intent timeout to at least 1000ms, or eliminate the timeout entirely when the menu is activated.
3. Ensure the mega menu is usable via keyboard with clear focus management.
4. Consider a responsive design that collapses the mega menu into a more vertical/stacked layout at high zoom levels (detected via CSS `@media` queries or viewport width).

---

### Issue 2: Auto-Scrolling Logo Carousels Cannot Be Paused

**Page**: Homepage (`/`)
**Element**: `.logos__scroller` — Two instances: client logos ("Trusted by Hundreds of Innovative Businesses") and award badges (bottom of page)
**Description**: The logo carousels use a CSS `animation: scroll` with `linear infinite` timing. The logos scroll continuously and cannot be paused, stopped, or manually navigated. At 300%+ magnification, only one logo is visible at a time, and it moves through the viewport too quickly to read. The animation is disabled when `prefers-reduced-motion: reduce` is active, but many magnifier users do not enable that setting (magnification is not the same as motion sensitivity). There are no pause/play buttons, no hover-to-pause behavior, and no alternative static view.
**WCAG Criteria Violated**:
- **2.2.2 Pause, Stop, Hide** (Level A) — Auto-moving content that starts automatically, lasts more than 5 seconds, and is presented in parallel with other content must have a mechanism to pause, stop, or hide it.
- **1.4.10 Reflow** (Level AA) — At high zoom, the scrolling creates content that cannot be accessed within the visible viewport.
**Severity**: **Critical**
**Impact on User**: James cannot read any client logos or award badges. The continuous motion makes the content inaccessible, and without pause controls, he has no way to examine individual items. This undermines trust-building (client logos) and credibility (award badges).
**Recommended Fix**:
1. Add a visible pause/play button for each carousel.
2. Pause the animation on hover and on keyboard focus within the carousel.
3. Ensure the `prefers-reduced-motion` media query stops the animation entirely (this is already partially implemented — verify it works for both carousel instances).
4. Provide a static fallback or link to a page listing all clients/awards.

---

### Issue 3: Tabbed Interface Spatially Separates Labels from Content

**Page**: Homepage (`/`)
**Element**: `.tabs-wrapper.side-tabs` — "Problems We Solve" / "Ship Game-Changing Digital Products to Market Fast"
**Description**: The tabbed interface places tab labels (buttons) in a left column and the corresponding tab content panels (images) in a right column. At 300% magnification, the user can see either the tab labels OR the content panel, but never both simultaneously. After clicking a tab, the user must pan far to the right to see the result. The tab content panels contain only images with empty `alt=""` attributes, providing no textual information. The tab preview text (e.g., "Streamline processes with digital products to enhance productivity") is nested within the tab label area but positioned below the button, requiring additional panning within the label column.
**WCAG Criteria Violated**:
- **1.1.1 Non-text Content** (Level A) — Tab panel images have `alt=""`, treating informational images as decorative. The images (e.g., `Operational-Efficiency-2.png`, `Modern-Technology-2.png`) likely convey information about each category.
- **1.3.2 Meaningful Sequence** (Level A) — The spatial separation between tab controls and tab content breaks the reading sequence for magnified users.
- **1.4.10 Reflow** (Level AA) — The two-column tab layout does not reflow to a single column at high zoom.
**Severity**: **Major**
**Impact on User**: James clicks a tab, pans to the right to see the content, and finds only a decorative image with no text. He must pan back left, down within the tab list, to find the preview text. The disconnection between action (clicking a tab) and result (seeing content) creates significant disorientation.
**Recommended Fix**:
1. Add meaningful alt text to all tab panel images describing the visual content.
2. Include text content (not just images) in the tab panels so magnified users have something to read.
3. At high zoom / narrow viewports, stack the tab labels above the tab content so they flow vertically.
4. Ensure the tab preview text is immediately visible adjacent to the active tab button.

---

### Issue 4: Contact Form Uses Two-Column Layout for Input Fields

**Page**: Contact page (`/contact`)
**Element**: Ninja Forms form `#nf-form-13-cont` — Fields with `container_class: "half-width"` (First Name, Last Name, Company Email, Company)
**Description**: The first four form fields (First Name, Last Name, Company Email, Company) use a `half-width` CSS class, placing them in a two-column side-by-side layout. At 300% magnification, the user can only see one field at a time. When tabbing from First Name to Last Name, focus jumps to the right side of the page, requiring a horizontal pan. Then Company Email is on the left (next row), and Company is on the right again. This creates a left-right-left-right zigzag panning pattern.
**WCAG Criteria Violated**:
- **1.3.2 Meaningful Sequence** (Level A) — The visual reading order (left-to-right, top-to-bottom) creates a zigzag pattern that is disorienting when only a portion is visible.
- **1.4.10 Reflow** (Level AA) — The two-column form layout does not reflow to a single column at 400% zoom (320px equivalent viewport).
**Severity**: **Major**
**Impact on User**: James must pan horizontally after every other field, increasing cognitive load and the risk of missing a field. The zigzag pattern disrupts his systematic top-to-bottom panning strategy.
**Recommended Fix**:
1. Use a single-column layout for all form fields, especially at high zoom levels.
2. If two-column layout is desired for desktop, ensure it reflows to single-column via CSS `@media` query when the viewport width is reduced (which is the effective state at high magnification).

---

### Issue 5: Contact Information Buried Below the Form

**Page**: Contact page (`/contact`)
**Element**: `.cards-wrapper.color-tint` — Three cards (Email, Call, LinkedIn) positioned after the form and testimonials sections
**Description**: The contact page presents a full form (with reCAPTCHA) as the primary interaction. The alternative contact methods — email (`contact@launchpadlab.com`), phone (`(312) 888-9651`), and LinkedIn — are positioned below the form and below a testimonials carousel section. At 300% magnification, a user must scroll through the entire form, past testimonials, to discover these alternatives. The phone number and email are in a three-column card layout, requiring horizontal panning.
**WCAG Criteria Violated**:
- **2.4.5 Multiple Ways** (Level AA) — While contact information exists in multiple places (form, cards, footer), the non-form contact methods are not discoverable without extensive scrolling.
- **1.3.2 Meaningful Sequence** (Level A) — Placing the simplest contact methods (phone, email) after the most complex one (form with reCAPTCHA) inverts the expected difficulty progression.
**Severity**: **Major**
**Impact on User**: James had to scroll past the entire form to find that he could simply call or email. A user who struggles with the reCAPTCHA (common for magnifier users) might leave the page without ever discovering the phone number.
**Recommended Fix**:
1. Place email, phone, and other direct contact methods prominently above or beside the form.
2. Consider a brief "Prefer to talk? Call us at (312) 888-9651 or email contact@launchpadlab.com" line at the top of the contact section, before the form.

---

### Issue 6: Case Study Carousel Has No Visible Navigation Controls

**Page**: Homepage (`/`)
**Element**: `.outcome-slider` — Case studies carousel (Prosci, CDK Global, Millennium Trust Company)
**Description**: The case study carousel is implemented with tiny-slider configured with `controls: false` and `nav: false` (via navPosition configuration). The only way to navigate between slides is by mouse-dragging. The slides use `autoWidth: true` and `edgePadding: 100`, causing adjacent slides to partially overlap at the edges. At 300% magnification, there is no visible indication that this is a carousel (no dots, no arrows), and the edge-peeking of adjacent slides is not visible.
**WCAG Criteria Violated**:
- **2.1.1 Keyboard** (Level A) — Without visible controls, keyboard users have no way to navigate between slides.
- **4.1.2 Name, Role, Value** (Level A) — The carousel does not communicate its role, the number of slides, or the current position.
- **1.3.1 Info and Relationships** (Level A) — The carousel structure (multiple slides, current position) is not programmatically exposed.
**Severity**: **Major**
**Impact on User**: James does not know there are multiple case studies. He sees the Prosci case study and has no visual or programmatic indicator that CDK Global or MTC case studies exist. He cannot navigate to them via keyboard.
**Recommended Fix**:
1. Enable visible previous/next controls and dot navigation.
2. Add ARIA attributes: `role="region"`, `aria-label="Case studies"`, `aria-roledescription="carousel"`.
3. Add `aria-label` to each slide (e.g., "Slide 1 of 3: Prosci").
4. Ensure controls are keyboard-focusable and operable.

---

### Issue 7: Nested Links in Service Cards

**Page**: Homepage (`/`)
**Element**: `.cards-wrapper .card` — Six service cards in the "Make AI Your Competitive Advantage" section
**Description**: Each service card is wrapped in an `<a>` tag linking to the service page (e.g., `/services/ai-automation-agentforce/`). Inside the card, there is a second `<a>` tag with the text "Learn More" linking to the same URL. This creates nested interactive elements: `<a><div>...<a>Learn More</a>...</div></a>`. This is invalid HTML (nested `<a>` tags) and creates duplicate tab stops for the same destination.
**WCAG Criteria Violated**:
- **4.1.1 Parsing** (Level A) — Nested `<a>` elements are invalid HTML and lead to unpredictable browser behavior.
- **2.4.4 Link Purpose (In Context)** (Level A) — The duplicate links with different text ("AI Automation & Agentic AI" for the outer link vs. "Learn More" for the inner link) create ambiguity about whether they lead to different destinations.
**Severity**: **Major**
**Impact on User**: When James tabs through the page, he encounters two consecutive focus stops for each card — both going to the same URL. At his magnification level, he can only see one focused element at a time, so he may think there are 12 different links (6 cards × 2 links each) rather than 6 service pages. This doubles his panning and navigation effort.
**Recommended Fix**:
1. Remove the outer `<a>` wrapper and keep only the "Learn More" link, OR remove the inner "Learn More" link and make the entire card a single clickable area.
2. If the entire card should be clickable, use CSS to stretch a single `<a>` element over the card area rather than nesting `<a>` tags.

---

### Issue 8: AOS (Animate on Scroll) Fade-In Animations

**Page**: Homepage (`/`)
**Element**: Multiple elements with `data-aos="fade-up"` `data-aos-duration="1000"` or `data-aos-duration="200"` — hero text block, service cards, contact page cards
**Description**: Many content sections use the AOS (Animate on Scroll) library to fade content in from below as the user scrolls. At 300% magnification, the user scrolls through the page in small increments. Content may appear invisible (opacity: 0, translated downward) until the user scrolls to exactly the right position to trigger the animation. This can cause content to "pop in" unexpectedly within the magnified viewport, or worse, the user may scroll past content that hasn't yet animated into visibility.
**WCAG Criteria Violated**:
- **2.3.3 Animation from Interactions** (Level AAA) — Motion animation triggered by interaction (scrolling) cannot be disabled by the user (though `prefers-reduced-motion` may help if the AOS library respects it).
- **1.3.2 Meaningful Sequence** (Level A) — Content that is hidden until animated may be skipped by users who scroll past the trigger point.
**Severity**: **Minor**
**Impact on User**: James may encounter blank areas while panning that later "pop" into existence, disrupting his mental model of the page structure. He might think a section is empty and move on, missing content.
**Recommended Fix**:
1. Respect `prefers-reduced-motion` by disabling AOS animations entirely when the preference is set.
2. Ensure all AOS-animated content is immediately visible (opacity: 1, no transform) as a baseline, with animation as progressive enhancement.
3. Consider removing fade-in animations for text content that is essential to understanding the page.

---

### Issue 9: Empty Alt Text on Informational Award Badge Images

**Page**: Homepage (`/`)
**Element**: `.logos-wrapper.small-logos .logos__list img` — Seven award badge images (e.g., "Top-Clutch-Salesforce-Company-United-States-2025.png", "Top-Clutch-Ai-Consulting-Company-United-States-2025.png")
**Description**: The award badges in the lower logo scroller all have `alt=""`, treating them as decorative. However, these images communicate meaningful information about LaunchPad Lab's credentials and industry recognition. The image filenames suggest content like "Top Clutch Salesforce Company United States 2025" and "Top Clutch AI Consulting Company United States 2025," but this information is not available to the user.
**WCAG Criteria Violated**:
- **1.1.1 Non-text Content** (Level A) — Informational images must have text alternatives that serve the equivalent purpose.
**Severity**: **Major**
**Impact on User**: James cannot identify what awards LaunchPad Lab has won. At magnification, the badges may be partially visible, and without alt text, even the partial visual information is not supplemented by any text alternative.
**Recommended Fix**:
1. Add descriptive alt text to each award badge (e.g., `alt="Top Clutch Salesforce Company in the United States, 2025"`).
2. Consider adding a visually hidden text description near the badges for additional context.

---

### Issue 10: Footer Multi-Column Layout Scatters Related Content

**Page**: All pages (global footer)
**Element**: `.footer .footer-blocks` — Three-column layout: company info/links, Contact Us, Social
**Description**: The footer uses a three-column layout. The first column contains the company description, navigation links, and third-party review badges. The second column has "Contact Us" with the physical address and phone number. The third column has "Let's Get Social" with social media links. At 300% magnification, each column is a separate "screen" requiring horizontal panning. The phone number link has a malformed `href` attribute: `href="tel:312-888-9651""` (double closing quote).
**WCAG Criteria Violated**:
- **1.4.10 Reflow** (Level AA) — The three-column footer does not reflow to a single column at high zoom.
- **4.1.1 Parsing** (Level A) — The malformed `href` attribute (`"tel:312-888-9651""`) with a double quote may cause issues in some browsers/assistive technologies.
**Severity**: **Minor**
**Impact on User**: James must pan extensively to find footer content. He might find the navigation links in column 1 but miss the contact information in column 2 or social links in column 3. The malformed phone link might not function correctly.
**Recommended Fix**:
1. Ensure the footer reflows to a single-column layout at narrow viewport widths / high zoom levels.
2. Fix the malformed `href`: change `href="tel:312-888-9651""` to `href="tel:312-888-9651"`.

---

### Issue 11: Social Media Icons Have Empty Alt Text

**Page**: All pages (global footer)
**Element**: `.footer-block a img` — Social media icons for Facebook, Instagram, LinkedIn
**Description**: The social media icons use `<img>` elements with `alt=""`. However, each icon is followed by text ("Facebook", "Instagram", "LinkedIn") within the same `<a>` tag, so the link purpose is communicated via the text. The empty alt prevents redundant announcement. This is technically correct, though at extreme magnification the icon and text may be in separate "screens" while panning.
**WCAG Criteria Violated**: None (correctly implemented as decorative since text alternatives exist).
**Severity**: **Minor** (observation, not a violation)
**Impact on User**: At extreme magnification, James might see only the icon (which is an unrecognizable small shape) without the adjacent text label. But since the text is within the same link, this is a layout concern rather than an alt text concern.
**Recommended Fix**: No change required for WCAG compliance. Optionally, consider using CSS to place icons after the text (or inline) to keep icon and label in tighter proximity.

---

### Issue 12: reCAPTCHA Challenge on Contact Form

**Page**: Contact page (`/contact`)
**Element**: `#nf-form-13-cont` — reCAPTCHA field (Google reCAPTCHA v2 visible)
**Description**: The contact form includes a Google reCAPTCHA v2 visible widget. If triggered, the image challenge (e.g., "Select all squares with traffic lights") presents a 3x3 or 4x4 grid of images. At 300% magnification, the user can only see a portion of the grid at a time, making it extremely difficult to identify and select all correct squares. The reCAPTCHA iframe also has a fixed small size that does not scale with the page zoom.
**WCAG Criteria Violated**:
- **1.1.1 Non-text Content** (Level A) — The image challenge relies entirely on visual identification of small image tiles.
- **2.4.11 Focus Not Obscured (Minimum)** (Level AA) — The reCAPTCHA popup may be partially obscured at high zoom.
**Severity**: **Major**
**Impact on User**: If the image challenge is triggered, James cannot reliably complete it because he can only see a few tiles at a time and loses context of which tiles he's already selected. This could prevent him from submitting the contact form entirely.
**Recommended Fix**:
1. Switch to reCAPTCHA v3 (invisible, score-based) which does not require visual interaction.
2. Alternatively, provide a non-CAPTCHA fallback such as a honeypot field (the form already has one configured).
3. If reCAPTCHA v2 must be used, ensure the audio challenge alternative is available and accessible.

---

### Issue 13: Skip Link Target May Not Exist

**Page**: All pages
**Element**: `<a class="skip-link screen-reader-text" href="#primary">Skip to content</a>`
**Description**: The site includes a skip-to-content link pointing to `#primary`. However, examination of the homepage HTML does not reveal an element with `id="primary"`. If the target anchor does not exist, the skip link does nothing when activated.
**WCAG Criteria Violated**:
- **2.4.1 Bypass Blocks** (Level A) — A mechanism to bypass repeated blocks of content must function correctly.
**Severity**: **Minor**
**Impact on User**: James could press Tab on page load to reveal the skip link, then press Enter to skip the navigation — but if the `#primary` anchor doesn't exist, nothing happens and he's left in the same position, having to tab through the entire navigation anyway.
**Recommended Fix**:
1. Add `id="primary"` to the `<main>` content element (or equivalent).
2. Verify that the skip link targets the correct element on every page template.

---

### Issue 14: Testimonials Carousel Uses Tiny-Slider Without Accessible Controls

**Page**: Contact page (`/contact`) and potentially homepage
**Element**: `.single-item-slider` — Testimonials carousel (5 slides)
**Description**: The testimonials carousel is implemented with tiny-slider configured with `controls: false` (no prev/next buttons) and `navPosition: "bottom"` (dot navigation at bottom). The carousel uses `mouseDrag: true` for slide-by-drag interaction. At 300% magnification, the dot navigation may not be visible (it's below the carousel content), and mouse-dragging is unreliable when panning is the primary mouse interaction. The carousel items contain `<blockquote>` and `<cite>` elements with proper semantic markup, which is positive.
**WCAG Criteria Violated**:
- **2.1.1 Keyboard** (Level A) — Without visible prev/next controls, keyboard navigation between slides is not obvious.
- **4.1.2 Name, Role, Value** (Level A) — The carousel role and state (current slide, total slides) are not programmatically communicated.
**Severity**: **Minor**
**Impact on User**: James sees one testimonial but may not know there are four more. The dot navigation, if visible, requires precise clicking at a scale where dots are tiny targets. Mouse-dragging conflicts with panning behavior at high magnification.
**Recommended Fix**:
1. Add visible prev/next arrow buttons.
2. Increase the size of navigation dots for easier targeting.
3. Add ARIA attributes to communicate carousel semantics.
4. Ensure slides are navigable via keyboard (arrow keys or tab).

---

## Summary Table

| # | Issue | Page | Severity | WCAG Criteria |
|---|-------|------|----------|---------------|
| 1 | Mega menu closes during magnified panning | All pages | Critical | 2.5.8, 2.1.1, 1.4.10 |
| 2 | Auto-scrolling logo carousels have no pause controls | Homepage | Critical | 2.2.2, 1.4.10 |
| 3 | Tabbed interface separates labels from content; images lack alt text | Homepage | Major | 1.1.1, 1.3.2, 1.4.10 |
| 4 | Contact form uses two-column layout | Contact | Major | 1.3.2, 1.4.10 |
| 5 | Contact info buried below form | Contact | Major | 2.4.5, 1.3.2 |
| 6 | Case study carousel has no visible controls | Homepage | Major | 2.1.1, 4.1.2, 1.3.1 |
| 7 | Nested links in service cards | Homepage | Major | 4.1.1, 2.4.4 |
| 8 | AOS fade-in animations may hide content | Homepage | Minor | 2.3.3, 1.3.2 |
| 9 | Award badge images have empty alt text | Homepage | Major | 1.1.1 |
| 10 | Footer multi-column layout + malformed href | All pages | Minor | 1.4.10, 4.1.1 |
| 11 | Social media icons have empty alt (correctly) | All pages | Minor | N/A (observation) |
| 12 | reCAPTCHA image challenge inaccessible at magnification | Contact | Major | 1.1.1, 2.4.11 |
| 13 | Skip link target `#primary` may not exist | All pages | Minor | 2.4.1 |
| 14 | Testimonials carousel lacks accessible controls | Contact | Minor | 2.1.1, 4.1.2 |

---

## Priority Recommendations

### Immediate (Critical)
1. **Fix mega menu interaction**: Implement click-to-open behavior and remove the short hover timeout, or provide a mobile-style slide-out menu at high zoom levels.
2. **Add pause controls to all carousels**: Every auto-scrolling element must have a visible pause button per WCAG 2.2.2.

### Short-Term (Major)
3. **Reflow all multi-column layouts** at high zoom / narrow viewports: form fields, footer, tab interface, contact cards.
4. **Add alt text** to all informational images (tab panels, award badges).
5. **Fix nested links** in service cards — use a single link per card.
6. **Add visible controls** to all carousels (case studies, testimonials).
7. **Surface contact info** (phone, email) above or alongside the form.
8. **Replace reCAPTCHA v2** with v3 or provide a non-visual alternative.

### Long-Term (Minor)
9. **Verify skip link** target exists on all page templates.
10. **Audit AOS animations** and ensure content is visible by default.
11. **Fix malformed HTML** (double-quote in footer phone link).
