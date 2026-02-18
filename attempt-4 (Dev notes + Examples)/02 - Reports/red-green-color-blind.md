# Accessibility Report: Red-Green Color Blindness (Protanopia/Deuteranopia)

**Persona:** David Kim, 45, Operations Director  
**Condition:** Protanopia/Deuteranopia (red-green color blindness)  
**Date:** February 16, 2026  
**Site Evaluated:** https://launchpadlab.com/  
**Pages Reviewed:** Homepage (/), Contact (/contact)  
**Auditor Perspective:** User who cannot distinguish red from green; relies on text, icons, shape, contrast, underlines, and patterns to identify interactive elements and understand state.

---

## Summary

LaunchPad Lab's website is largely navigable for users with red-green color blindness. The site's strong text hierarchy, labeled navigation, and clear content structure allow goal completion. However, several issues exist where color is used as the sole or primary means of conveying information, identifying interactive elements, or distinguishing states. These issues range from Minor to Major severity and span multiple WCAG criteria, primarily **1.4.1 Use of Color** and **1.4.11 Non-text Contrast**.

---

## Issues Found

### Issue 1: Body Text Links Lack Non-Color Visual Indicator

**Page(s):** All pages (Homepage, Contact, Footer)  
**Element(s):**
- Inline links throughout body text (e.g., `<a href="mailto:contact@launchpadlab.com">contact@launchpadlab.com</a>` on the Contact page)
- "Learn More" links within service cards on the homepage (class `link-black-base arrow-link`)
- Mega menu widget links (e.g., `<a class="button button-blue-base scroll-on-page-link" href="/services">View Services</a>`)
- Footer links (e.g., `/services`, `/technologies`, `/about`)

**Description:**  
Links within body text and card elements are not underlined and do not have any non-color visual indicator (such as an underline, bold weight, or icon) to distinguish them from surrounding non-link text. Users with color vision deficiency who cannot perceive the color difference between link text and body text may not recognize these elements as interactive.

The "Learn More" links on service cards do include an arrow icon (`arrow-right-black.svg`), which provides a secondary cue — but only when the card is in its default state. Other inline links (e.g., in the mega menu widget text, in the footer, in body paragraphs) rely solely on color differentiation.

**WCAG Criterion:** 1.4.1 Use of Color (Level A)  
**Severity:** **Major**  
**Impact on User:** David cannot distinguish link color from body text color. He must rely on context clues (e.g., an email address is "probably" a link) rather than clear visual affordance. This causes uncertainty, increased cognitive load, and potential missed interactions.

**Recommended Fix:**
- Add `text-decoration: underline` to all inline text links, or provide a visible underline on focus/hover at minimum.
- Ensure a contrast ratio of at least 3:1 between link text and surrounding non-link text if underlines are not used (per WCAG technique G183).
- For card-based links, ensure the arrow icon is always visible (not just on hover) and that the entire card is perceived as clickable through cursor changes and visual affordance.

---

### Issue 2: Tab Active State May Rely on Color Alone

**Page:** Homepage (/)  
**Element:** "Problems We Solve" tab interface — `.tabs-wrapper .tab-link.is-active`  
**Tabs:** Operational Efficiency, Modern Technology, Customer Engagement, Scalable Solutions, Expansive Resources, Speed to Market

**Description:**  
The tab interface uses an `is-active` class on the selected tab button. The visual distinction between active and inactive tabs appears to be communicated through a color or background-color change. No additional non-color indicators are visible in the markup (such as a bold font weight, underline, border-bottom, or icon) to distinguish the active tab from inactive ones.

For a user with red-green color blindness, if the active state shifts between colors that are not perceptually distinct (e.g., a green highlight vs. a gray default, or a subtle hue shift), the selected tab becomes indistinguishable from unselected tabs.

**WCAG Criterion:** 1.4.1 Use of Color (Level A)  
**Severity:** **Major**  
**Impact on User:** David cannot confidently determine which tab is currently selected without watching the content panel change. This degrades usability and forces a trial-and-error approach.

**Recommended Fix:**
- Add a visible non-color indicator to the active tab: a bottom border (e.g., `border-bottom: 3px solid`), bold font weight, an underline, or a distinct background shape/pattern.
- Ensure `aria-selected="true"` is correctly toggled (it is in the current markup — good for screen readers, but insufficient for sighted users with CVD).
- Consider adding a left-edge accent bar or a filled-background treatment with sufficient luminance contrast change (not just hue change).

---

### Issue 3: Case Study Green Background (#318500) — Reduced Perceptual Distinction

**Page:** Homepage (/)  
**Element:** Millennium Trust Company (MTC) case study card in the carousel  
**Specific markup:** `<div class="case-study-expanded light" style="background-color: #318500;">`  
**Button:** `<a class="button button-white-base" style="color: #318500;" href="...">Millennium Trust Company</a>`

**Description:**  
The MTC case study uses a pure green background color (`#318500`). For users with protanopia, this green is perceived as a brownish, olive, or dark yellow tone rather than vibrant green. While the white text on the green background maintains sufficient luminance contrast (approximately 4.8:1, meeting WCAG AA), the **CTA button** inverts this — rendering green text (`color: #318500`) on a white background. This green text on white has a contrast ratio of approximately 4.8:1, which technically passes WCAG AA for normal text.

However, the perceptual quality of the green is the issue: it appears as a muddy, ambiguous color to protanopic users, which may reduce the visual "pop" and call-to-action prominence that the design intends. It does not look like a distinct, intentional accent color — it looks like a brownish smear.

The other two case study cards use blue/purple tones (#30327d and #006cfa), which are clearly distinguishable for users with protanopia.

**WCAG Criterion:** 1.4.1 Use of Color (Level A), 1.4.3 Contrast (Minimum) (Level AA)  
**Severity:** **Minor**  
**Impact on User:** The MTC card's green styling is not a functional barrier (David can still read the text and click the button), but it is a perceptual quality issue. The button's text color looks ambiguous rather than vibrant, reducing its effectiveness as a CTA.

**Recommended Fix:**
- Consider using a blue or high-saturation blue-violet accent for the MTC card (consistent with other cards) rather than pure green.
- If green must be used, pair it with an additional affordance (icon, underline, border) on the CTA button to reinforce interactivity.
- Test all card color schemes through a CVD simulator (e.g., Coblis, Sim Daltonism) to ensure perceptual distinction.

---

### Issue 4: Form Validation Error States Likely Use Color Alone

**Page(s):** Homepage (/) — CTA contact form; Contact (/contact) — main contact form  
**Element:** Ninja Forms contact form (form ID 13)  
**Fields:** First Name (required), Last Name (required), Company Email (required), Company (required), How Can We Help You? (required)

**Description:**  
The contact form is built with Ninja Forms, which by default highlights invalid fields with a **red border** and displays error text. The form configuration includes the error messages:
- `"validateRequiredField": "This is a required field."`
- `"formErrorsCorrectErrors": "Please correct errors before submitting this form."`
- `"changeEmailErrorMsg": "Please enter a valid email address!"`

The form includes an error container with `role="alert"` (`<div id="nf-form-errors-13" class="nf-form-errors" role="alert">`), and per-field error elements (`<div class="nf-error-wrap nf-error" role="alert">`). The presence of text-based error messages is positive.

However, the **field-level visual indicator** (the red border on the input) is likely the primary sighted-user cue for identifying which specific field has an error. For a user with protanopia, a red border may appear as a dark brown or dark gray, indistinguishable from the field's default border or focus state. If the per-field error text message ("This is a required field") is displayed adjacent to the field, this mitigates the issue — but if the error text only appears in a summary at the top or if it disappears after interaction, the red border becomes the sole indicator.

**WCAG Criterion:** 1.4.1 Use of Color (Level A), 3.3.1 Error Identification (Level A)  
**Severity:** **Major**  
**Impact on User:** David may not be able to identify which specific fields have errors if the red border is the only visual indicator. This could lead to form submission failures and frustration, potentially causing him to abandon the contact attempt.

**Recommended Fix:**
- Ensure per-field error messages are displayed as visible text directly adjacent to (above or below) the invalid field and remain visible until the error is corrected.
- Add a non-color visual indicator to error fields: an error icon (e.g., ⚠ or ✕) inside or next to the input, a change in border width/style (e.g., dashed or double border), or a background pattern.
- Verify that the `role="alert"` on per-field error containers triggers correctly and that the error text is perceivable.
- Add `aria-invalid="true"` to invalid fields and associate error messages via `aria-describedby`.

---

### Issue 5: Empty Alt Text on Informational Increase/Growth Icons

**Page:** Homepage (/)  
**Element:** CDK Global case study in the carousel  
**Specific markup:**
```html
<img src="/wp-content/themes/some-like-it-neat/assets/images/increase.svg" class="increase" alt="">
```

**Description:**  
In the CDK Global case study, two metrics ("Improved Sales Team Alignment" and "Streamlined Discovery & Quoting Process") use an upward-pointing arrow icon (`increase.svg`) instead of a numerical stat value. These icons have empty alt text (`alt=""`), treating them as decorative. However, they are **not decorative** — they replace a stat value and convey the meaning "this metric improved." The icon is likely rendered in green (signifying growth/improvement), which would be ambiguous to a user with protanopia.

Without alt text and without a visible textual stat (like "90%" or "5,400+"), these two metrics have no machine-readable or color-independent way to communicate "improvement."

**WCAG Criterion:** 1.1.1 Non-text Content (Level A), 1.4.1 Use of Color (Level A)  
**Severity:** **Major**  
**Impact on User:** David sees a small indistinct icon of ambiguous color with no text alternative. He cannot determine whether this represents an increase, decrease, or neutral state. The metric's meaning is effectively lost.

**Recommended Fix:**
- Add meaningful alt text: `alt="Improvement"` or `alt="Increased"`.
- Alternatively, include a visible text label adjacent to the icon (e.g., "Improved" or "↑ Improved") that conveys the same information without relying on the icon's color.
- If the icon color (green) is used to indicate "positive," provide that information through text as well.

---

### Issue 6: Award/Badge Images Lack Descriptive Alt Text

**Page:** Homepage (/)  
**Element:** Scrolling award badge logos section (`.logos-wrapper.small-logos`)  
**Specific markup examples:**
```html
<img src="...Top-Clutch-Salesforce-Company-United-States-2025.png" alt="" />
<img src="...Top-Clutch-Ai-Consulting-Company-United-States-2025.png" alt="" />
<img src="...Global-Award-Spring-2025.png" alt="" />
```

**Description:**  
Seven award/badge images are displayed in a scrolling logo bar. All have empty `alt=""` attributes, treating them as decorative. However, these images convey meaningful information — they represent awards and recognition (e.g., "Top Clutch Salesforce Company," "Top Clutch AI Consulting Company," "Global Award Spring 2025," "Best Places to Work Chicago").

While this is not strictly a color-blindness issue, it compounds the problem: award badges often use color-coded visual systems (stars, colors, tier indicators) that may be indistinguishable for users with CVD. Without alt text, there is no fallback.

**WCAG Criterion:** 1.1.1 Non-text Content (Level A)  
**Severity:** **Minor**  
**Impact on User:** David cannot understand what awards or recognition these badges represent. The information is completely inaccessible.

**Recommended Fix:**
- Add descriptive alt text to each badge image, e.g., `alt="Top Clutch Salesforce Company in the United States 2025"`.
- If the badges are purely decorative and not intended to convey information, consider whether they should be displayed at all in a credibility section — if they're meant to build trust, they need to be accessible.

---

### Issue 7: Card Hover State Relies on Color Change

**Page:** Homepage (/)  
**Element:** Service cards in "Make AI Your Competitive Advantage" section (`.cards-wrapper .hover-cards-interaction .card`)

**Description:**  
The service cards use a hover interaction (class `hover-cards-interaction`) where the card's visual appearance changes on mouse hover. Based on the markup, the card transitions between a light/default state and an expanded/highlighted state. This transition appears to involve a background color change (from light to a darker/blue tone) and text color inversion (from dark text to light text).

While the color change is accompanied by structural changes (the card may expand, reveal additional text, or change layout), the initial hover feedback — the moment the user mouses over the card — likely relies on a color shift as the primary indicator. For users with limited color perception, a subtle color change may not register as a state change.

**WCAG Criterion:** 1.4.1 Use of Color (Level A), 1.4.11 Non-text Contrast (Level AA)  
**Severity:** **Minor**  
**Impact on User:** David may not immediately perceive the hover state change, though the structural changes (text appearance, layout shift) provide secondary cues. The initial hover feedback is diminished.

**Recommended Fix:**
- Add non-color hover indicators: a visible border or shadow change, a scale transform, or an icon/arrow animation.
- Ensure the hover state has at least a 3:1 contrast ratio change from the non-hover state against adjacent colors (per WCAG 1.4.11).
- Consider using `cursor: pointer` (likely already present) and adding a subtle elevation/shadow effect on hover.

---

### Issue 8: Navigation "Contact" Link — Special Styling May Rely on Color

**Page:** All pages  
**Element:** Main navigation "Contact" link  
**Specific markup:** `<li class="mega-navigation-contact ... navigation-contact menu-item"><a class="mega-menu-link" href="https://launchpadlab.com/contact/">Contact</a></li>`

**Description:**  
The "Contact" navigation item has additional classes (`mega-navigation-contact`, `navigation-contact`) that distinguish it from other nav items. This likely means it receives special CSS styling — possibly a different background color, text color, or button-like treatment to make it stand out as a primary CTA.

If this distinct styling is achieved solely through color (e.g., a green or orange background while other items are unstyled), users with CVD may not perceive the Contact link as more prominent than other nav items.

**WCAG Criterion:** 1.4.1 Use of Color (Level A)  
**Severity:** **Minor**  
**Impact on User:** David can still find the "Contact" link by reading the text label and its position at the right end of the navigation. However, the intended visual prominence may be lost if it relies only on color differentiation.

**Recommended Fix:**
- If the Contact link is intended to be a CTA, style it as a visually distinct button with a visible border, background fill, border-radius, or padding that clearly differentiates it from plain text links regardless of color perception.
- Ensure the styling difference is not solely a color change but includes structural/shape differences.

---

### Issue 9: Social Media Icons Have Empty Alt Text

**Page:** All pages (Footer)  
**Element:** Social media links in footer  
**Specific markup:**
```html
<a href="https://www.facebook.com/LaunchPadLab"><img src=".../facebook.svg" alt=""> Facebook</a>
<a href="https://www.instagram.com/launchpadlab/"><img src=".../instagram.svg" alt=""> Instagram</a>
<a href="https://www.linkedin.com/company/launchpad-lab"><img src=".../linkedin.svg" alt=""> LinkedIn</a>
```

**Description:**  
The social media icons in the footer have empty `alt=""` attributes. However, each icon is accompanied by a visible text label ("Facebook", "Instagram", "LinkedIn") within the same `<a>` tag. This makes the icons effectively decorative, which is acceptable — the text provides the accessible name.

**WCAG Criterion:** 1.1.1 Non-text Content (Level A)  
**Severity:** **Informational (No Issue)**  
**Impact on User:** No barrier. The text labels are sufficient. The empty alt text correctly prevents redundant announcements for screen readers.

**Note:** This is documented as a positive finding — the pattern of icon + text label is a good accessibility practice.

---

## Summary Table

| # | Issue | Page | WCAG | Severity | Status |
|---|-------|------|------|----------|--------|
| 1 | Links lack underline/non-color indicator | All pages | 1.4.1 (A) | **Major** | Needs fix |
| 2 | Tab active state relies on color alone | Homepage | 1.4.1 (A) | **Major** | Needs fix |
| 3 | Green (#318500) case study — reduced perceptual distinction | Homepage | 1.4.1 (A) | **Minor** | Recommended |
| 4 | Form validation errors likely use color-only border | Homepage, Contact | 1.4.1 (A), 3.3.1 (A) | **Major** | Needs fix |
| 5 | Increase icons have empty alt text | Homepage | 1.1.1 (A), 1.4.1 (A) | **Major** | Needs fix |
| 6 | Award badge images lack descriptive alt text | Homepage | 1.1.1 (A) | **Minor** | Recommended |
| 7 | Card hover state relies on color change | Homepage | 1.4.1 (A), 1.4.11 (AA) | **Minor** | Recommended |
| 8 | Contact nav link styling may rely on color | All pages | 1.4.1 (A) | **Minor** | Recommended |
| 9 | Social media icons with empty alt (text labels present) | All pages (Footer) | 1.1.1 (A) | **None** | Positive finding |

---

## Positive Findings

1. **Text-based navigation labels:** All navigation items use clear text labels, not color-coded icons alone.
2. **Required field asterisks:** Form fields use the asterisk (*) symbol to indicate required status, not color alone.
3. **Skip to content link:** Present in the page markup (`<a class="skip-link screen-reader-text" href="#primary">Skip to content</a>`).
4. **Proper ARIA on tabs:** The tab interface uses `role="tablist"`, `role="tab"`, `role="tabpanel"`, `aria-selected`, and `aria-controls` — correct semantic structure.
5. **Form error container with `role="alert"`:** The Ninja Forms error containers use `role="alert"` for live announcement of errors.
6. **Social media links pair icons with text:** The footer social links include visible text labels alongside icons.
7. **Multiple contact pathways:** Contact information is available through navigation, inline CTAs, the contact form, and the footer — redundancy improves findability.
8. **Blue primary brand color (#1E60BD, #2363BB):** The site's primary accent color is blue, which is generally well-perceived by users with protanopia/deuteranopia. This is a good default choice.
9. **High contrast hero text:** White text on blue backgrounds in hero sections provides strong luminance contrast regardless of color perception.

---

## Recommendations Priority

### Critical (Address Immediately)
*None — no issues fully block task completion.*

### High Priority (Major Issues)
1. **Underline or visually mark all text links** with a non-color indicator (Issue #1)
2. **Add non-color active state to tabs** — border, bold, or underline (Issue #2)
3. **Ensure form validation uses text + icons**, not color-only borders (Issue #4)
4. **Add meaningful alt text to informational icons** like increase arrows (Issue #5)

### Medium Priority (Minor Issues)
5. Review green (#318500) usage in case studies for CVD perceptual quality (Issue #3)
6. Add descriptive alt text to award/badge images (Issue #6)
7. Enhance card hover states with non-color feedback (Issue #7)
8. Ensure Contact nav CTA uses shape/structure, not just color (Issue #8)

### Ongoing
- Test all new designs and components through CVD simulators before deployment
- Establish a design system rule: "Never use color as the sole means of conveying information"
- Include red-green color blindness as a standard test case in QA processes
