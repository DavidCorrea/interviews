# Accessibility Report — Low Contrast Sensitivity

**Persona**: Morgan Chen (Low Contrast Sensitivity — cataracts, age-related vision changes)  
**Site**: https://launchpadlab.com/  
**Pages Audited**: Homepage (`/`), Services (`/services/`), About (`/about/`), Contact (`/contact/`)  
**Date**: February 2026  
**Methodology**: Manual audit against WCAG 2.1 AA criteria, with CSS source analysis and computed contrast ratio calculations  

---

## Executive Summary

The LaunchPad Lab website presents **11 distinct contrast and visibility issues** impacting users with low contrast sensitivity. Of these, **3 are Critical**, **5 are Major**, and **3 are Minor**. The most severe issues involve completely invisible content hidden behind hover interactions, form input fields with no visible boundaries, and decorative borders that fail to delineate interactive components. While headings, footer content, and primary call-to-action buttons perform well, the site's reliance on mid-gray body text, opacity-based hover states, and subtle visual cues creates cumulative barriers that degrade the experience for users with contrast sensitivity impairments.

---

## Issues

### Issue 1: Hover-Reveal Content on Service Cards (Homepage)

**Page**: Homepage (`/`)  
**Element**: Service cards in the "Make AI Your Competitive Advantage" section (`.cards-wrapper.hover-cards-interaction .card`)  
**Description**: The descriptive text within each service card (AI Automation, Web Application Development, etc.) is initially rendered at `opacity: 0` and only becomes visible when the user hovers over the card. The card heading is visible, but the supporting paragraph text and "Learn More" link are completely invisible until hover.  

**CSS Evidence**:  
```
.cards-wrapper.hover-cards-interaction .card .text-block-inner { opacity: 0; }
```

**Computed Contrast Ratio**: 1.00:1 (invisible — no foreground/background distinction)

**WCAG Criteria Violated**:  
- **1.4.3 Contrast (Minimum)** — Level AA: Text must have a contrast ratio of at least 4.5:1 against its background. Text at opacity 0 has no contrast.  
- **1.3.1 Info and Relationships** — Level A: Information conveyed visually must be programmatically determinable. Content hidden by default with no non-hover mechanism to reveal it fails this criterion.  
- **2.1.1 Keyboard** — Level A: If keyboard users cannot trigger the hover state, the content is completely inaccessible.  

**Severity**: **Critical**

**Impact on User**: Morgan cannot scan or read service descriptions without accidentally discovering the hover behavior. Content that is invisible cannot be evaluated, compared, or understood. Morgan would believe the cards contain only titles and assume the page lacks detailed service information.

**Recommended Fix**:  
- Make all card text visible by default at full opacity.  
- If a reveal animation is desired, use it as an enhancement (e.g., expand additional detail) rather than hiding primary content.  
- Ensure all revealed content is also accessible via keyboard focus, not just mouse hover.

---

### Issue 2: Form Input Fields with No Visible Border on Colored Backgrounds

**Page**: All pages with inline CTA forms (Homepage, Services, About, Contact footer sections)  
**Element**: Form inputs within `.contact-block` and `.cta-block-container` sections  
**Description**: Form inputs use a semi-transparent white background (`rgba(255, 255, 255, 0.2)`) with no border (`border: none`). When placed on a blue or dark background, the form fields are nearly indistinguishable from the surrounding area.  

**CSS Evidence**:  
```
.contact-block form input,
.contact-block form textarea,
.contact-block form select {
    background-color: rgba(255, 255, 255, 0.2);
    border: none;
}
```

**Computed Contrast Ratio (input boundary vs. background)**: ~1.51:1 (effective input background `#4b80ca` vs. surrounding `#1e60bd`)

**WCAG Criteria Violated**:  
- **1.4.11 Non-text Contrast** — Level AA: UI components must have a contrast ratio of at least 3:1 against adjacent colors. The input boundary (1.51:1) fails this requirement.  
- **1.3.1 Info and Relationships** — Level A: Form fields must be visually identifiable.  

**Severity**: **Critical**

**Impact on User**: Morgan cannot locate form fields to complete the contact form. The inputs blend into the blue background with no border or shadow to define their boundaries. Morgan would be unable to determine where to click to begin typing, effectively blocking the contact goal.

**Recommended Fix**:  
- Add a visible border to all form inputs (e.g., `border: 1px solid rgba(255, 255, 255, 0.6)` or a solid white border).  
- Alternatively, increase the input background opacity to at least `rgba(255, 255, 255, 0.5)` to achieve a 3:1 boundary contrast.  
- Ensure the fix applies to both light and dark background contexts.

---

### Issue 3: Card Container Borders Insufficient for Component Delineation

**Page**: Homepage (`/`), Services (`/services/`), About (`/about/`)  
**Element**: Card components throughout the site (`.cards-wrapper.hover-cards-interaction .card`, service cards, problem cards)  
**Description**: Cards are bordered with `#CFCFCF` on a `#FFFFFF` background, producing a 1.56:1 contrast ratio. This is insufficient for users with low contrast sensitivity to distinguish card boundaries from the surrounding white space.  

**CSS Evidence**:  
```
.cards-wrapper.hover-cards-interaction .card { border: 1px solid #CFCFCF; }
```

**Computed Contrast Ratio**: 1.56:1

**WCAG Criteria Violated**:  
- **1.4.11 Non-text Contrast** — Level AA: UI component boundaries must have at least 3:1 contrast against adjacent colors.  

**Severity**: **Critical**

**Impact on User**: Morgan cannot perceive card boundaries. The page appears as an undifferentiated white expanse with floating text blocks. Morgan cannot determine which heading belongs to which description, where one card ends and another begins, or which areas are interactive.

**Recommended Fix**:  
- Darken card borders to at least `#767676` (4.5:1) or use `#949494` (3:1 minimum).  
- Alternatively, use a visible box-shadow (e.g., `box-shadow: 0 2px 8px rgba(0,0,0,0.15)`) to create perceived depth and separation.  
- Consider adding a subtle background fill to cards to further distinguish them from the page background.

---

### Issue 4: Links Indistinguishable from Body Text

**Page**: All pages  
**Element**: Inline links (`a` tags), "Learn More" links on cards, arrow links  
**Description**: Default link styling uses `color: #555555` — the same color as body paragraph text — with no underline. The only visual differentiation is a small arrow icon appended to "Learn More" links and a cursor change on hover. In the absence of color differentiation or underline, links are visually identical to surrounding text.  

**CSS Evidence**:  
```
a { color: #555555; }
p, figcaption { color: #555555; }
.arrow-link:after { background: url("images/icons/arrow-right-black.svg"); }
```

**WCAG Criteria Violated**:  
- **1.4.1 Use of Color** — Level A: Color (or in this case, the lack of color differentiation) must not be the only means of conveying information. Links must be distinguishable from non-link text by means other than color alone. When links and text share the same color, there is no color-based cue at all.  
- **WCAG Technique G183**: Requires a 3:1 contrast ratio between link text and surrounding non-link text if underline is not present. Since both are `#555`, the ratio is 1:1.  

**Severity**: **Major**

**Impact on User**: Morgan cannot identify which text elements are clickable without hovering over every word. This forces a "hunt and peck" navigation style that is slow, frustrating, and error-prone. Morgan would miss links that lead to important content.

**Recommended Fix**:  
- Add `text-decoration: underline` to all inline links, or  
- Use a distinctly different link color (e.g., `#1e60bd` — the brand blue, which provides 6.06:1 on white) for all links, or  
- Apply both underline and color differentiation for maximum clarity.

---

### Issue 5: Hero Text Over Background Images with Inconsistent Gradient Overlay

**Page**: Homepage (`/`), Services (`/services/`), About (`/about/`)  
**Element**: `.page-header-wrapper .page-header` — hero sections with background images and gradient overlays  
**Description**: Hero headings and body text are rendered in `#FFFFFF` over photographic background images. A gradient overlay (`linear-gradient(to right, #000, transparent)` at varying opacities) is applied to improve contrast, but the overlay fades to transparent on one or more sides. This creates zones where white text sits against light or mid-tone areas of the photograph with insufficient contrast.  

**CSS Evidence**:  
```
.page-header-wrapper .page-header:after {
    background-image: linear-gradient(to right, #000, transparent);
}
.page-header-wrapper .page-header:before {
    opacity: 0.6;
    background-image: linear-gradient(0, transparent, #000);
}
```

**Computed Contrast Ratio**: Varies — estimated 3:1 to 8:1 depending on the region of the background image. Fails in lighter regions.

**WCAG Criteria Violated**:  
- **1.4.3 Contrast (Minimum)** — Level AA: Text must maintain at least 4.5:1 (normal text) or 3:1 (large text) contrast against its background in all visible areas.  

**Severity**: **Major**

**Impact on User**: Morgan can read the hero text in areas where the gradient overlay is darkest but struggles or fails in areas where the overlay fades. The hero tagline and descriptive paragraph partially "disappear" into the lighter portions of the photograph, requiring Morgan to piece together words from the readable portions.

**Recommended Fix**:  
- Apply a uniform solid or semi-transparent dark overlay across the entire hero image (e.g., `background-color: rgba(0, 0, 0, 0.55)`) rather than a gradient that fades to transparent.  
- Alternatively, place text within a solid-background container overlaid on the image.  
- Test all hero images at various viewport sizes to ensure consistent minimum contrast.

---

### Issue 6: Section Dividers and Stat Separators Below Minimum Non-Text Contrast

**Page**: Homepage (`/`), About (`/about/`)  
**Element**: Stats section borders (`.stats-wrapper.unique-grid ul li` borders), accordion borders (`.accordion-block-container details`), general section separators  
**Description**: Horizontal and vertical separating borders between content sections use `#bfbfbf` (1.84:1) or `#CFCFCF` (1.56:1) on white backgrounds, both far below the 3:1 minimum for meaningful visual boundaries.  

**CSS Evidence**:  
```
.stats-wrapper.unique-grid ul li:first-child { border-right: 1px solid #bfbfbf; }
.stats-wrapper.unique-grid ul li:nth-child(3) { border-top: 1px solid #bfbfbf; }
.accordion-block-container details { border-bottom: 1px solid #CFCFCF; }
.cards.list-with-icon.style-line .card { border-bottom: 1px solid #CFCFCF; }
```

**Computed Contrast Ratios**: `#bfbfbf` on `#FFFFFF` = 1.84:1; `#CFCFCF` on `#FFFFFF` = 1.56:1

**WCAG Criteria Violated**:  
- **1.4.11 Non-text Contrast** — Level AA: Meaningful visual boundaries must have at least 3:1 contrast.  

**Severity**: **Major**

**Impact on User**: Morgan cannot perceive the separation between statistics ("12+ Years," "730+ Projects," "240+ Clients"), causing the content to run together as an undifferentiated text block. Accordion section separators are also invisible, making it unclear where one FAQ entry ends and the next begins.

**Recommended Fix**:  
- Darken all structural borders to at least `#949494` for 3:1 compliance.  
- For stats sections specifically, consider adding background color alternation or increased spacing in addition to borders.  
- For accordions, consider a thicker border or visual marker (e.g., a left-side color bar) for better section delineation.

---

### Issue 7: Link Hover State Reduces Contrast via Opacity

**Page**: All pages  
**Element**: `.link-blue-base:hover`, `.link-black-base:hover`, general link and footer link hover states  
**Description**: Multiple link hover styles apply `opacity: 0.6` or `opacity: 0.5` to the link text. This reduces the effective contrast ratio from a passing level to a failing level precisely when the user is interacting with the element.  

**CSS Evidence**:  
```
.link-blue-base:hover { color: #1e60bd; opacity: 0.6; }
.link-black-base:hover { color: #555555; opacity: 0.6; }
footer.footer a:hover { color: #FFFFFF; opacity: 0.5; }
```

**Computed Contrast Ratios on Hover**:  
- `.link-blue-base` at 60% opacity on white: effectively ~`#7da0d7` on `#FFFFFF` ≈ 2.96:1 (FAIL for normal text)  
- `.link-black-base` at 60% opacity on white: effectively ~`#a8a8a8` on `#FFFFFF` ≈ 2.38:1 (FAIL)  
- Footer links at 50% opacity on `#021C41`: effectively ≈ 6.04:1 (PASS, but reduced from 16.87:1)  

**WCAG Criteria Violated**:  
- **1.4.3 Contrast (Minimum)** — Level AA: Interactive text must maintain 4.5:1 contrast in all states, including hover and focus.  

**Severity**: **Major**

**Impact on User**: Morgan experiences the counterintuitive phenomenon of links becoming harder to read when they try to interact with them. This is particularly disorienting because the hover state is supposed to confirm interactivity, not degrade legibility. Morgan may second-guess whether they've correctly identified a link.

**Recommended Fix**:  
- Replace opacity-based hover effects with color-shift hover states that maintain or increase contrast (e.g., darken the link color on hover rather than fading it).  
- For footer links, use `color: #CCCCCC` or similar instead of opacity reduction.  
- Ensure all interactive states (hover, focus, active) meet or exceed the resting-state contrast ratio.

---

### Issue 8: Body Text Color (#555555) Experientially Insufficient Despite Technical Compliance

**Page**: All pages  
**Element**: `p`, `li`, `dd`, body copy throughout the site  
**Description**: Body paragraph text uses `color: #555555` on `#FFFFFF` backgrounds, producing a contrast ratio of 7.46:1. This technically passes WCAG AA (4.5:1) and AAA (7:1). However, for users with cataracts and reduced contrast sensitivity, mid-gray text creates cumulative reading fatigue, particularly in longer passages on the Services and About pages.  

**CSS Evidence**:  
```
p, figcaption { color: #555555; }
li, dd { color: #555555; }
```

**Computed Contrast Ratio**: 7.46:1 (PASSES AA and AAA)

**WCAG Criteria Violated**:  
- No strict violation — this is a **best-practice recommendation** that goes beyond minimum compliance.  

**Severity**: **Minor**

**Impact on User**: Morgan can read body text but experiences noticeable eye strain after extended reading. The medium-gray color perceptually "washes out" for a user with cataracts, requiring more conscious effort to process. Over the course of evaluating the full site (homepage, services, about, contact), this accumulated fatigue becomes a significant usability concern.

**Recommended Fix**:  
- Darken body text to `#333333` (12.63:1 on white) or `#222222` (17.15:1 on white) for improved legibility.  
- This change would cost nothing visually but dramatically improve readability for users with contrast sensitivity impairments.

---

### Issue 9: Placeholder Text Styled as White on Potentially Light Backgrounds

**Page**: Any page with native WordPress/theme form elements  
**Element**: `input::placeholder`, `select::placeholder`, `textarea::placeholder`  
**Description**: The theme's global CSS sets placeholder text to `color: #FFFFFF`. On form inputs with white or light backgrounds (outside of the dark CTA sections), this would render placeholder text completely invisible.  

**CSS Evidence**:  
```
input::placeholder,
select::placeholder,
textarea::placeholder { color: #FFFFFF; }
```

**Computed Contrast Ratio**: 1.00:1 on white backgrounds (invisible)

**WCAG Criteria Violated**:  
- **1.4.3 Contrast (Minimum)** — Level AA: Placeholder text, while not a label substitute, must be legible when present. White text on white is invisible.  
- **3.3.2 Labels or Instructions** — Level A: If placeholders serve as the primary label (poor practice but common), their invisibility prevents form completion.  

**Severity**: **Major**

**Impact on User**: On any form rendered with the theme's default styling (not overridden by HubSpot or Ninja Forms), Morgan would see empty input fields with no indication of what data to enter. The placeholder hints — which many forms rely on for guidance — would be completely invisible.

**Recommended Fix**:  
- Change placeholder text color to a context-aware value: `#767676` for light backgrounds (4.5:1 on white) or keep `#FFFFFF` scoped only to inputs within `.contact-block` or dark-background contexts.  
- Never use white placeholder text as a global default.  
- Ensure all forms use proper `<label>` elements in addition to placeholders, so information is not lost even if placeholders are invisible.

---

### Issue 10: Dark-Background Card Components Have Insufficient Internal Contrast

**Page**: Homepage (`/`), sections using `.cards-wrapper.dark-blue-background`  
**Element**: Cards on dark navy backgrounds (`.cards-wrapper.dark-blue-background .card`)  
**Description**: When the cards component is placed on a dark navy background (`#021C41`), individual cards are styled with `background-color: rgba(255, 255, 255, 0.1)`. The effective card background is approximately `#1a3057`, which provides only 1.29:1 contrast against the surrounding `#021C41` navy.  

**CSS Evidence**:  
```
.cards-wrapper.dark-blue-background .card { background-color: rgba(255, 255, 255, 0.1); }
.cards-wrapper.dark-blue-background { background-color: #021C41; }
```

**Computed Contrast Ratio**: ~1.29:1 (card background vs. section background)

**WCAG Criteria Violated**:  
- **1.4.11 Non-text Contrast** — Level AA: The card container boundary must have 3:1 contrast against the adjacent background.  

**Severity**: **Minor**

**Impact on User**: Morgan cannot distinguish individual cards from the dark background. The white text within the cards is legible against the dark surface, but the card containers themselves are invisible — content appears to float without structure.

**Recommended Fix**:  
- Increase the card background opacity to at least `rgba(255, 255, 255, 0.25)` for better separation.  
- Add a subtle visible border (e.g., `border: 1px solid rgba(255, 255, 255, 0.3)`).  
- Consider using a slightly lighter solid background for cards on dark sections.

---

### Issue 11: Hamburger Menu Icon on Light Backgrounds

**Page**: All pages (responsive/mobile breakpoint, or narrow viewports)  
**Element**: `.mega-toggle-animated-inner` (hamburger menu toggle icon)  
**Description**: The hamburger menu icon uses `background-color: #ddd` for its three bars. On pages or viewports where the header background is light (white or near-white), this light gray on light background produces a contrast ratio of approximately 1.36:1.  

**CSS Evidence**:  
```
#mega-menu-wrap-menu-1 .mega-menu-toggle .mega-toggle-block-0
  .mega-toggle-animated-inner,
  .mega-toggle-animated-inner::before,
  .mega-toggle-animated-inner::after {
    background-color: #ddd;
}
```

**Computed Contrast Ratio**: ~1.36:1 (against white/light page backgrounds)

**WCAG Criteria Violated**:  
- **1.4.11 Non-text Contrast** — Level AA: The primary navigation control must have at least 3:1 contrast against its background.  

**Severity**: **Minor**

**Impact on User**: On mobile or narrow viewports, the hamburger icon is the sole means of accessing site navigation. If Morgan cannot see it, they cannot navigate the site at all on mobile devices. This would be Critical on mobile; it is Minor here because on desktop viewports, the full navigation bar is visible.

**Recommended Fix**:  
- Change the hamburger icon color to adapt to the background context — use a dark color (e.g., `#333`) on light backgrounds and `#ddd` or `#fff` on dark backgrounds.  
- Alternatively, use a universally high-contrast color like `#555555` (7.46:1 on white, and still visible on moderately dark backgrounds).

---

## Summary Table

| # | Issue | Page(s) | WCAG Criterion | Contrast Ratio | Severity |
|---|-------|---------|----------------|----------------|----------|
| 1 | Hover-reveal card content (opacity: 0) | Homepage | 1.4.3, 1.3.1, 2.1.1 | 1.00:1 | Critical |
| 2 | Borderless form inputs on colored backgrounds | All (CTA sections) | 1.4.11, 1.3.1 | ~1.51:1 | Critical |
| 3 | Card container borders too faint | Homepage, Services, About | 1.4.11 | 1.56:1 | Critical |
| 4 | Links same color as body text, no underline | All | 1.4.1 | 1.00:1 (vs. surrounding text) | Major |
| 5 | Hero text over inconsistent gradient overlays | Homepage, Services, About | 1.4.3 | ~3:1–8:1 (variable) | Major |
| 6 | Section dividers/stat separators invisible | Homepage, About | 1.4.11 | 1.56:1–1.84:1 | Major |
| 7 | Hover states reduce contrast via opacity | All | 1.4.3 | 2.38:1–2.96:1 on hover | Major |
| 8 | Body text #555 fatiguing despite compliance | All | Best practice | 7.46:1 (passes) | Minor |
| 9 | White placeholder text on light backgrounds | Forms (theme default) | 1.4.3, 3.3.2 | 1.00:1 | Major |
| 10 | Dark-section cards indistinguishable from background | Homepage | 1.4.11 | ~1.29:1 | Minor |
| 11 | Hamburger icon on light backgrounds | All (mobile) | 1.4.11 | ~1.36:1 | Minor |

---

## Prioritized Recommendations

### Immediate (Critical)
1. **Make all card content visible by default** — remove `opacity: 0` from hover-card text. Use progressive enhancement for animation, not content hiding.
2. **Add visible borders to all form inputs** — especially in CTA sections on colored backgrounds. Minimum 3:1 boundary contrast.
3. **Darken card borders** site-wide from `#CFCFCF` to at least `#949494` or add visible box-shadows.

### Short-Term (Major)
4. **Differentiate link styling** — add underlines or use the brand blue (`#1e60bd`) for all inline links to distinguish from body text.
5. **Standardize hero overlays** — replace fading gradients with uniform semi-transparent overlays ensuring consistent 4.5:1 contrast for text.
6. **Darken section dividers** — step all structural borders from `#bfbfbf`/`#CFCFCF` to at least `#949494`.
7. **Replace opacity-based hover effects** with color-shift hovers that maintain contrast ratios.
8. **Fix placeholder text color** — scope white placeholders to dark contexts only; use `#767676` as default.

### Long-Term (Minor / Best Practice)
9. **Darken body text** from `#555555` to `#333333` for improved readability.
10. **Increase dark-section card background contrast** — raise `rgba(255, 255, 255, 0.1)` to `0.25` or add borders.
11. **Context-aware hamburger icon color** — adapt to light/dark backgrounds dynamically.

---

## Tools & Methodology

- **Contrast Ratios**: Calculated using the WCAG 2.1 relative luminance formula per [W3C Understanding SC 1.4.3](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
- **CSS Source Analysis**: Theme stylesheet (`/wp-content/themes/lpl/style.css`), Max Mega Menu stylesheet (`/wp-content/uploads/maxmegamenu/style.css`), inline styles
- **Content Extraction**: HTML source analysis of homepage, services, about, and contact pages
- **Persona Simulation**: Evaluation performed through the lens of a user with cataracts and low contrast sensitivity, using macOS Increase Contrast mode
