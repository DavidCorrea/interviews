# Accessibility Report: Low Vision (No Screen Magnifier) Evaluation

**Website:** https://launchpadlab.com/  
**Evaluator Persona:** Rosa Martínez — 48-year-old volunteer coordinator with low vision due to glaucoma, using browser zoom at 150%, no screen magnifier  
**Date:** February 2026  
**Pages Evaluated:** Homepage (`/`), Contact (`/contact`), About (`/about`), Services (`/services`)  

---

## Executive Summary

The LaunchPad Lab website presents multiple accessibility barriers for users with low vision who rely on browser zoom rather than dedicated screen magnification software. While the site has notable strengths — bold, heavy-weight headings (800 weight), a reasonably structured heading hierarchy, proper form labels, and ARIA-labeled tab components — it is undermined by thin body text weight, links that are visually indistinguishable from plain text, a navigation that collapses to a tiny and poorly visible hamburger icon at zoom levels as low as 150%, continuously moving content that cannot be paused, ghost-style buttons with thin borders, and form layouts that become cramped at zoom. These issues create a cumulative experience of visual strain and navigational confusion that, while not completely preventing task completion, significantly increases the effort required and risks user abandonment.

---

## Issues Found

### Issue 1: Navigation Collapses to Small, Low-Visibility Hamburger Icon at 150% Zoom

**Page:** All pages  
**Element:** `#burgerBtn` (div element, no visible text) and `.mega-toggle-animated` button (hamburger icon with thin CSS lines), breakpoint at 1069px  
**WCAG Criteria:** [1.4.4 Resize Text (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html), [2.4.5 Multiple Ways (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/multiple-ways.html)  
**Severity:** Critical  

**Description:**  
The site's mega-menu navigation has a CSS breakpoint at `data-breakpoint="1069"`. At 150% browser zoom on a standard 1440px display, the effective CSS viewport width is approximately 960px (1440 ÷ 1.5), which falls below this breakpoint. As a result, the full desktop navigation (Services, Technologies, Industries, Our Work, About Us, Insights, Contact) is entirely replaced by a hamburger menu icon.

The hamburger icon is rendered via thin CSS pseudo-elements (`.mega-toggle-animated-inner` and its `::before`/`::after`), typically 2–3px lines. The `#burgerBtn` div has no visible text label. While the mega-menu toggle button has `aria-label="Toggle Menu"`, this is not visible on screen. The hamburger trigger is small and uses very thin visual indicators that are extremely difficult for low-vision users to perceive.

**Impact on this user:**  
Rosa spent approximately 10 seconds scanning the header area before locating the hamburger icon. The seven navigation items that are clearly visible at default zoom become invisible at her standard zoom level, leaving her reliant on a small, unlabeled icon that her glaucoma-affected vision struggles to detect. This is the primary navigation mechanism for the entire site — if she can't find it, she can't navigate.

**Recommended Fix:**  
- Add a visible text label "Menu" next to or below the hamburger icon, visible at all breakpoints where the hamburger appears.  
- Increase the size of the hamburger icon lines to at least 4px thickness.  
- Increase the overall touch/click target of the hamburger button to at least 44×44 CSS pixels.  
- Consider raising the mega-menu breakpoint so that the full navigation remains visible at zoom levels up to 200% on common screen sizes, or provide a secondary horizontal scrollable nav.  
- Ensure the hamburger icon has sufficient contrast against the header background.

---

### Issue 2: Links Visually Indistinguishable from Body Text

**Page:** All pages  
**Element:** All inline `<a>` elements in body content; CSS rule `a { color: #555555; text-decoration: none; }`  
**WCAG Criteria:** [1.4.1 Use of Color (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)  
**Severity:** Critical  

**Description:**  
All hyperlinks across the site are styled with the same color as body text (`#555555`) and have `text-decoration: none` (no underline). The only visual differentiation on hover is a color change to `#222222`, which is subtle. Links are visually identical to non-interactive body text in their default state.

This is visible in the CSS:
```css
a {
  color: #555555;
  font-family: "proxima-nova", sans-serif;
  font-weight: normal;
  transition: all 0.3s ease-in-out;
  text-decoration: none;
}
```

**Impact on this user:**  
Rosa cannot identify which text elements are clickable and which are not. When scanning the page to find navigation paths, contact information, or "Learn More" links embedded in body copy, she must hover over every piece of text to discover if it's a link. This dramatically increases the time and effort required to navigate. For a user whose reduced vision already demands more effort per visual scan, this is a severe barrier.

**Recommended Fix:**  
- Add `text-decoration: underline` to all inline text links, or at minimum provide a non-color visual indicator (underline, border-bottom, icon, or distinct font weight).  
- Ensure links have at least a 3:1 contrast ratio against surrounding non-link text, per WCAG 1.4.1 requirements when color alone is used.  
- CTA buttons (which are already styled distinctly) can remain as-is, but all inline text links need a visible affordance.

---

### Issue 3: Thin Body Text Font Weight Reduces Readability

**Page:** All pages  
**Element:** Body text (`p`, `li`, `dd`, `a` elements); CSS `font-weight: normal` (400)  
**WCAG Criteria:** [1.4.12 Text Spacing (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/text-spacing.html) (related), [1.4.8 Visual Presentation (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/visual-presentation.html)  
**Severity:** Major  

**Description:**  
All body text, paragraphs, list items, and links use `font-weight: normal` (400) with the `proxima-nova` typeface. While the font size (16px / 1rem, scaling to 24px effective at 150% zoom) and contrast ratio (#555555 on white ≈ 7.85:1) technically pass WCAG AA requirements, the combination of a 400-weight sans-serif font with a medium-gray color creates characters that appear thin and low-contrast to users with conditions affecting contrast sensitivity, such as glaucoma.

The issue is compounded for testimonial blockquotes, which use `font-weight: lighter` — even thinner than normal:
```css
blockquote {
  font-weight: lighter;
  /* ... */
}
```

**Impact on this user:**  
Rosa can technically read the body text, but it requires noticeably more effort and concentration compared to the bold headings (weight 800). Over the course of reading multiple paragraphs — especially the value proposition text on the homepage and the long testimonial quotes on the contact page — the thin font causes visual fatigue. The `font-weight: lighter` on blockquotes is particularly problematic; these testimonials are long sentences that Rosa struggles to get through.

**Recommended Fix:**  
- Increase body text font-weight to 500 (medium) for improved character definition.  
- Change body text color from `#555555` to `#333333` or darker for improved perceived contrast.  
- Remove `font-weight: lighter` from blockquotes; use at least `font-weight: 400` or preferably `500`.  
- Consider offering a "high contrast" or "bold text" toggle that applies bolder weights site-wide.

---

### Issue 4: Ghost/Outline Buttons Have Low Visual Prominence

**Page:** Homepage (`/`)  
**Element:** Hero CTA button "Connect with an Expert" (`.button-white-base`), case study buttons (`.button-white-base` with inline `style="color: #30327d"` etc.)  
**WCAG Criteria:** [1.4.11 Non-text Contrast (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html)  
**Severity:** Major  

**Description:**  
The primary hero CTA "Connect with an Expert" uses a ghost/outline button style — white text with a thin white border on a blue photographic background. The button is not filled with a solid background color. Similarly, case study cards use white-bordered buttons on colored backgrounds (e.g., `style="color: #30327d"` on a purple background, `style="color: #006cfa"` on a blue background).

Ghost buttons rely on a thin border (typically 1–2px) to define their boundaries. At 150% zoom, this border scales to 1.5–3px, which is still thin.

**Impact on this user:**  
Rosa identified the hero CTA only because it was in the general area she was looking. The thin border blended with the photographic background, making the button's boundaries unclear. She described it as harder to spot than a solid, filled button. For the case study buttons further down the page, the ghost style against colored backgrounds made them similarly easy to overlook.

**Recommended Fix:**  
- Replace ghost buttons with solid filled buttons (e.g., solid white background with dark text, or solid blue background with white text).  
- If ghost buttons are retained, increase the border width to at least 3px and add a subtle background tint or drop shadow to differentiate the button from the background.  
- Ensure button borders meet the 3:1 contrast ratio against the adjacent background, per WCAG 1.4.11.

---

### Issue 5: Continuously Scrolling Logo Ticker Cannot Be Paused

**Page:** Homepage (`/`)  
**Element:** `.logos__scroller` — infinite CSS animation scrolling client logos (Kawasaki, Harvard, Whirlpool, etc.) with `animation: scroll var(--_logo-scroll-duration, 20s) linear infinite`  
**WCAG Criteria:** [2.2.2 Pause, Stop, Hide (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)  
**Severity:** Major  

**Description:**  
The client logo section uses a continuous horizontal scrolling animation. Logos are duplicated (cloned with `aria-hidden="true"`) to create a seamless loop effect. The animation runs indefinitely with no mechanism for users to pause, stop, or hide it. The CSS uses `will-change: transform` for performance.

The code does check for `prefers-reduced-motion: reduce`:
```javascript
if (!window.matchMedia("(prefers-reduced-motion: reduce)").matches) {
  addAnimation();
}
```
However, this relies on the user having the OS-level "reduce motion" preference enabled. There is no on-page control.

**Impact on this user:**  
Rosa uses browser zoom, not OS-level accessibility settings, as her primary accommodation. She does not have `prefers-reduced-motion` enabled. The continuously scrolling logos are nearly impossible for her to read — the motion combined with her reduced visual acuity means she can see colored shapes moving but cannot identify individual logos. Additionally, the constant peripheral motion is distracting when she's trying to read the static content above and below the ticker.

**Recommended Fix:**  
- Add a visible pause/play button adjacent to the logo ticker.  
- Alternatively, display logos in a static grid or a manually-controlled carousel with previous/next buttons.  
- Ensure the `prefers-reduced-motion` check halts animation completely (not just reduces speed).  
- Consider making the default behavior static, with animation as an opt-in.

---

### Issue 6: Hero Text Over Photographic Background Creates Inconsistent Contrast

**Page:** Homepage (`/`)  
**Element:** `.page-header` with `background: url('...Home-Hero-V2.jpg') no-repeat center; background-size: cover;` and white text overlay  
**WCAG Criteria:** [1.4.3 Contrast (Minimum) (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html), [1.4.6 Contrast (Enhanced) (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/contrast-enhanced.html)  
**Severity:** Major  

**Description:**  
The homepage hero section places white heading and paragraph text directly over a photographic background image. While the `background-color: #1E60BD` provides a fallback, the actual rendered background is a photograph with varying light and dark regions. The h1 text ("AI Innovation. Digital Solutions. Results that Matter.") is in heavy weight (800) and large size, which helps. But the body paragraph text below the heading uses normal weight (400) and is smaller, making contrast against the variable photographic background inconsistent.

There is no semi-transparent overlay or text shadow to ensure consistent contrast across the image.

**Impact on this user:**  
Rosa could read the bold heading but struggled with the paragraph text beneath it. In areas where the background photo had lighter regions, the white text lost contrast and became difficult to distinguish. This is particularly problematic for users with glaucoma, which affects contrast sensitivity more than visual acuity alone.

**Recommended Fix:**  
- Add a semi-transparent dark overlay (e.g., `background: rgba(0, 0, 0, 0.5)`) between the image and the text.  
- Alternatively, add a `text-shadow` to all text over the image (e.g., `text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5)`).  
- Increase the paragraph text weight to at least 500 when displayed over images.  
- Test contrast at multiple points across the background image to ensure 4.5:1 minimum at all positions.

---

### Issue 7: Form Fields Use Half-Width Layout That Becomes Cramped at Zoom

**Page:** Homepage (`/`) contact section, Contact page (`/contact`)  
**Element:** Ninja Forms fields with `container_class: "half-width"` — First Name, Last Name, Company Email, Company fields  
**WCAG Criteria:** [1.4.10 Reflow (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/reflow.html), [1.4.4 Resize Text (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)  
**Severity:** Major  

**Description:**  
The contact form uses Ninja Forms with four fields (First Name, Last Name, Company Email, Company) configured with `container_class: "half-width"`. This places two fields side-by-side per row. At 150% browser zoom, the effective viewport width is approximately 960px. The form container within the page layout narrows accordingly, resulting in each half-width field being approximately 350–400px wide. The input fields themselves become narrow, reducing the visible area for typed text and making it harder to target individual fields.

**Impact on this user:**  
Rosa found the side-by-side form fields cramped at her zoom level. The input areas were narrow enough that she worried about clicking the wrong field. When typing longer values (company name, email address), the text overflowed the visible area of the input, requiring horizontal scrolling within the field. For a user who already has difficulty with fine motor targeting due to her larger cursor and reduced vision, narrow fields increase error rates.

**Recommended Fix:**  
- At viewport widths below 1024px (which includes 150% zoom on common displays), stack form fields vertically (full-width) instead of side-by-side.  
- Ensure input fields have a minimum height of 44px and adequate padding for comfortable targeting.  
- Test the form at 200% zoom to ensure all fields remain fully usable without horizontal scrolling.

---

### Issue 8: Skip Navigation Link Is Visually Hidden and Inaccessible to Low-Vision Users

**Page:** All pages  
**Element:** `<a class="skip-link screen-reader-text" href="#primary">Skip to content</a>`  
**WCAG Criteria:** [2.4.1 Bypass Blocks (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)  
**Severity:** Major  

**Description:**  
The site includes a "Skip to content" link as the first interactive element, which is good practice. However, it uses the class `screen-reader-text`, which applies CSS to make the element permanently visually hidden (typically `position: absolute; width: 1px; height: 1px; clip: rect(0,0,0,0); overflow: hidden`). The link does not become visible on keyboard focus.

**Impact on this user:**  
Rosa does not use a screen reader, so she never perceives this skip link. She navigates primarily with a mouse and visual scanning. A visible-on-focus skip link would allow her to bypass the header and navigation when using keyboard navigation as a supplement. Its permanent invisibility means she must scroll past the header/navigation manually on every page load. This is especially costly given that the navigation at her zoom level is already problematic (see Issue 1).

**Recommended Fix:**  
- Make the skip link visible on focus using CSS:
```css
.skip-link:focus {
  position: fixed;
  top: 10px;
  left: 10px;
  z-index: 10000;
  padding: 10px 20px;
  background: #000;
  color: #fff;
  font-size: 18px;
  clip: auto;
  width: auto;
  height: auto;
}
```
- Ensure the skip link target (`#primary`) exists and correctly points to the main content area.

---

### Issue 9: Small Carousel Navigation Dots

**Page:** Contact page (`/contact`) — testimonial slider; Homepage (`/`) — case study outcome slider  
**Element:** Tiny-slider navigation dots (`.tns-nav button` elements), typically 8–12px  
**WCAG Criteria:** [2.5.8 Target Size (Minimum) (Level AA)](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html), [1.4.11 Non-text Contrast (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html)  
**Severity:** Major  

**Description:**  
The testimonial and case study carousels use the tiny-slider library with `controls: false` and `navPosition: "bottom"`. Navigation between slides relies on small circular dot indicators at the bottom of the slider. These dots are typically rendered at 8–12px in diameter. At 150% zoom, they scale to approximately 12–18px — still below the WCAG 2.2 recommended minimum target size of 24×24px.

**Impact on this user:**  
Rosa can barely see the navigation dots and cannot click them accurately. She resorted to mouse-dragging the slider content directly (`mouseDrag: true` is enabled), which works but is not intuitive. The dots' small size and lack of visible labels mean she might not even realize there are multiple testimonials to view.

**Recommended Fix:**  
- Increase dot size to at least 24×24px, or replace dots with visible previous/next arrow buttons of at least 44×44px.  
- Add visible labels or a slide count indicator (e.g., "1 of 5") to communicate the number of slides.  
- Ensure dot contrast meets 3:1 against the background for both active and inactive states.

---

### Issue 10: Social Media Icons in Footer Have Empty Alt Text

**Page:** All pages (footer)  
**Element:** Footer social media links — `<img src=".../facebook.svg" alt="">`, `<img src=".../instagram.svg" alt="">`, `<img src=".../linkedin.svg" alt="">`  
**WCAG Criteria:** [1.1.1 Non-text Content (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)  
**Severity:** Minor  

**Description:**  
The footer social media links include SVG icon images with empty `alt=""` attributes. While each link does include visible text labels ("Facebook," "Instagram," "LinkedIn") adjacent to the icons, the icons themselves are treated as purely decorative. The empty alt is acceptable when the adjacent text provides the label.

However, this becomes a concern if the page layout at zoom causes the text labels to wrap away from or below the icons, potentially separating the icon from its label visually.

**Impact on this user:**  
At 150% zoom, Rosa can identify the social media links because the text labels are present next to the icons. This is a minor issue since the text provides the necessary information. However, the icons themselves are small (~16px rendered, ~24px at zoom) and would be unidentifiable on their own.

**Recommended Fix:**  
- Keep `alt=""` on icons when adjacent text labels exist (current approach is acceptable).  
- Ensure text labels remain visually adjacent to icons at all zoom levels and breakpoints.  
- Consider increasing icon size to at least 24px rendered (36px at 150% zoom) for better visibility.

---

### Issue 11: Award/Badge Images Missing Meaningful Alt Text

**Page:** Homepage (`/`) — awards/badges logo section  
**Element:** Award badge images in `.logos-wrapper.small-logos` — Clutch awards, global awards badges. All have `alt=""`  
**WCAG Criteria:** [1.1.1 Non-text Content (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)  
**Severity:** Minor  

**Description:**  
The awards section on the homepage displays seven badge/award images (e.g., "Top Clutch Salesforce Company United States 2025," "Top Clutch AI Consulting Company United States 2025," "Global Award Spring 2025"). All of these images have empty `alt=""` attributes, treating them as decorative. However, these images convey meaningful information about the company's achievements and credibility — they are not purely decorative.

**Impact on this user:**  
At 150% zoom, Rosa can see the badge images but may struggle to read the small text within them. The constrained sizes (`max-height: 50px`, `max-width: 140px`) mean the text within these badge images is very small — often 8–10px at source, or about 12–15px at zoom. Since there are no alt-text descriptions and the text is baked into the images, Rosa cannot benefit from browser text scaling for this content.

**Recommended Fix:**  
- Add descriptive alt text to each award image (e.g., `alt="Top Clutch Salesforce Company, United States, 2025"`).  
- Consider adding visible text captions below each badge for users who cannot read the small text within the images.

---

### Issue 12: JavaScript-Dependent Contact Form with No Fallback

**Page:** Homepage (`/`) contact section, Contact page (`/contact`)  
**Element:** `<div id="nf-form-13-cont">` (Ninja Forms container), `<noscript>` fallback  
**WCAG Criteria:** [4.1.2 Name, Role, Value (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html) (degraded access), [3.3.2 Labels or Instructions (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)  
**Severity:** Minor  

**Description:**  
The contact form is rendered entirely via JavaScript (Ninja Forms). If JavaScript fails to load, the only fallback is: `<noscript class="ninja-forms-noscript-message">Notice: JavaScript is required for this content.</noscript>`. No alternative contact method (email address, phone number) is provided in this fallback message.

While JavaScript loads successfully in normal circumstances, this creates a single point of failure. The `<noscript>` notice is also styled as small, gray text that is easy to overlook.

**Impact on this user:**  
Rosa's JavaScript loaded correctly, so the form was accessible. However, as a user who might use browser extensions or accessibility tools that interfere with JavaScript execution, the complete absence of a fallback is a risk. The footer does contain contact details (phone and email), but a user who navigates directly to the contact page form area would not know to scroll past it to find alternatives.

**Recommended Fix:**  
- Add a static fallback within the `<noscript>` tag that includes the company email and phone number.  
- Example: "JavaScript is required for this form. You can also reach us at contact@launchpadlab.com or (312) 888-9651."  
- Include the same fallback as visible text below the form container for users whose JavaScript partially fails (form doesn't render but `<noscript>` doesn't trigger).

---

### Issue 13: Minor HTML Error in Footer Phone Link

**Page:** All pages (footer)  
**Element:** `<a href="tel:312-888-9651"">(312) 888-9651</a>` — double quote in href attribute  
**WCAG Criteria:** [4.1.1 Parsing (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/parsing.html) (deprecated in WCAG 2.2 but still relevant)  
**Severity:** Minor  

**Description:**  
The footer phone link contains a stray double-quote character in the `href` attribute: `href="tel:312-888-9651""`. The extra `"` after the phone number may cause inconsistent parsing across browsers.

**Impact on this user:**  
In most modern browsers, this error is silently corrected and the phone link works as expected. Rosa was able to use the link. However, in edge cases or with assistive tools that parse HTML strictly, this could cause the link to malfunction.

**Recommended Fix:**  
- Remove the extra double-quote: `<a href="tel:312-888-9651">(312) 888-9651</a>`

---

### Issue 14: Tab Panel Images Have Empty Alt Text

**Page:** Homepage (`/`)  
**Element:** Tab panel images in "Problems We Solve" section — six `<img>` elements with `alt=""` (e.g., `Operational-Efficiency-2.png`, `Modern-Technology-2.png`, etc.)  
**WCAG Criteria:** [1.1.1 Non-text Content (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)  
**Severity:** Minor  

**Description:**  
The "Problems We Solve" tabbed section displays an image for each tab panel. These images appear to be screenshots, illustrations, or conceptual graphics related to each problem category (Operational Efficiency, Modern Technology, Customer Engagement, etc.). All six images have `alt=""`, treating them as decorative.

If these images convey meaningful content (e.g., showing a product interface, a workflow diagram), they should have descriptive alt text. If they are purely decorative/ambient, empty alt is acceptable.

**Impact on this user:**  
Rosa can see the images at 150% zoom but may not be able to discern fine details within them. Without alt text, she gets no text-based description to supplement what she can see. This is a minor issue since the tab text labels provide the primary content, but it reduces the richness of the experience.

**Recommended Fix:**  
- If images are informative, add descriptive alt text (e.g., `alt="Dashboard showing operational efficiency metrics"`).  
- If purely decorative, empty alt is acceptable but consider adding a visible caption.

---

## Summary Table

| # | Issue | Page(s) | WCAG Criterion | Severity |
|---|-------|---------|----------------|----------|
| 1 | Navigation collapses to tiny, low-visibility hamburger at 150% zoom | All | 1.4.4, 2.4.5 | Critical |
| 2 | Links visually indistinguishable from body text (no underline, same color) | All | 1.4.1 | Critical |
| 3 | Thin body text font weight (400) reduces readability; blockquotes use lighter | All | 1.4.8, 1.4.12 | Major |
| 4 | Ghost/outline buttons have low visual prominence | Homepage | 1.4.11 | Major |
| 5 | Continuously scrolling logo ticker with no pause control | Homepage | 2.2.2 | Major |
| 6 | Hero text over photographic background creates inconsistent contrast | Homepage | 1.4.3, 1.4.6 | Major |
| 7 | Half-width form fields become cramped at 150% zoom | Homepage, Contact | 1.4.10, 1.4.4 | Major |
| 8 | Skip navigation link permanently visually hidden | All | 2.4.1 | Major |
| 9 | Small carousel navigation dots (below 24px minimum target) | Contact, Homepage | 2.5.8, 1.4.11 | Major |
| 10 | Social media footer icons have empty alt text (mitigated by text labels) | All | 1.1.1 | Minor |
| 11 | Award/badge images missing meaningful alt text | Homepage | 1.1.1 | Minor |
| 12 | JavaScript-dependent contact form with no fallback | Homepage, Contact | 4.1.2, 3.3.2 | Minor |
| 13 | HTML error (double quote) in footer phone link | All | 4.1.1 | Minor |
| 14 | Tab panel images have empty alt text | Homepage | 1.1.1 | Minor |

---

## Severity Definitions

| Level | Definition |
|-------|-----------|
| **Critical** | Prevents the user from completing a core task or makes a core element inaccessible. Must be fixed. |
| **Major** | Significantly impedes the user's ability to complete tasks or understand content. Creates substantial friction. Should be prioritized. |
| **Minor** | Causes inconvenience or reduced experience quality but does not prevent task completion. Should be addressed in regular maintenance. |

---

## Positive Findings

The following aspects of the site worked well for this user type and should be preserved:

1. **Bold heading typography:** Headings use font-weight 800 (extra-bold), which provides excellent readability for low-vision users at zoom.
2. **Proper heading hierarchy:** h1 through h4 elements are used in a logical order, helping Rosa scan and understand content structure.
3. **Form labels above fields:** Ninja Forms labels are positioned "above" input fields, making them clearly associated with their fields.
4. **Tab component ARIA:** The "Problems We Solve" tabbed section uses proper `role="tab"`, `role="tabpanel"`, `aria-controls`, `aria-selected`, and `aria-labelledby` attributes.
5. **Footer contact information:** The phone number and address in the footer are in plain text, easily readable at zoom, and the phone number is a clickable `tel:` link.
6. **Contact page alternative methods:** The "Let's Connect" cards provide email, phone, and LinkedIn options outside of the form, giving multiple contact paths.
7. **Responsive layout reflow:** The overall page layout reflows to narrower viewports at zoom without introducing horizontal scrolling — the CSS handles most breakpoints gracefully.
8. **`prefers-reduced-motion` check on logo ticker:** While not sufficient on its own (Issue 5), the JavaScript does check for the reduced motion preference, which is a good foundation to build on.
