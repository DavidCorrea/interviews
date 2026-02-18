# Accessibility Report: Tritanopia (Blue-Yellow Color Blindness)

**Persona:** Marcus Webb, 42, small business owner with Tritanopia  
**Site Tested:** https://launchpadlab.com/ and https://launchpadlab.com/contact/  
**Date:** February 16, 2026  
**Goals:** Find what LaunchPad Lab does; find how to contact them  
**Goals Achieved:** Yes (both)  

---

## Executive Summary

The LaunchPad Lab website is largely functional for a user with tritanopia (blue-yellow color blindness). Both primary goals—understanding the company's services and finding contact information—were achievable. However, the site's heavy reliance on blue as its primary brand and interactive color (#1E60BD, #2363BB, #006cfa) means that a significant portion of the visual hierarchy, branding emphasis, and interactive element distinction is lost for this user type. Several elements use color as the sole or primary differentiator, which reduces usability and visual clarity. No critical blockers were found, but multiple moderate and minor issues affect the quality of the experience.

---

## Issues Found

### Issue 1: Tab Active State Relies Primarily on Color

**Page:** Homepage — "Ship Game-Changing Digital Products to Market Fast" section  
**Element:** `.tabs-wrapper .tab-link.is-active` (tab buttons: Operational Efficiency, Modern Technology, Customer Engagement, etc.)  
**WCAG Criterion:** 1.4.1 Use of Color (Level A)  
**Severity:** Major  

**Description:** The active tab in the tabbed interface is distinguished from inactive tabs primarily through a color change (blue highlight/underline vs. default state). For a user with tritanopia, blue renders as gray, making the active tab visually indistinguishable from inactive tabs. The tab does use `aria-selected="true"` for assistive technology, but the visual distinction is insufficient.

**Impact on User:** Marcus had to look at which tab's content panel was visible to determine which tab was active, rather than being able to quickly scan the tab bar. This slows navigation and creates uncertainty.

**Recommended Fix:**  
- Add a non-color visual indicator for the active tab: bold text weight, an underline with sufficient thickness, a background fill change, a border on multiple sides, or an icon/arrow indicator.
- Ensure the active state is distinguishable through at least two visual properties (e.g., color + font weight, or color + border + background).

---

### Issue 2: Blue CTA Buttons Lack Non-Color Visual Emphasis

**Page:** Homepage, Contact page, and mega menu dropdowns  
**Element:** `.button-blue-base` (e.g., "View Services" in Services mega menu, "View Industries" in Industries mega menu, "Learn More" in AI callout section)  
**WCAG Criterion:** 1.4.1 Use of Color (Level A)  
**Severity:** Major  

**Description:** The blue call-to-action buttons (class `button-blue-base`) are used to draw attention and indicate primary actions. For a user with tritanopia, these buttons appear as gray, which significantly reduces their visual prominence. They blend into the page rather than standing out as the intended primary action. While the buttons do have text labels and button-like shapes (which makes them functionally identifiable), their role as *primary* CTAs vs. secondary elements is diminished.

**Impact on User:** Marcus could identify these elements as buttons due to their shape and text, but they did not draw his eye as primary calls to action. In contexts like the mega menu dropdown where they sit alongside body text, they appeared as generic gray boxes rather than attention-grabbing action items.

**Recommended Fix:**  
- Add non-color emphasis to primary CTAs: a visible border, shadow, increased font weight, an arrow/icon, or higher contrast with surrounding elements.
- Consider using patterns, gradients, or other visual treatments that remain visible regardless of color perception.
- Ensure CTA buttons are differentiated from surrounding content through multiple visual properties, not just background color.

---

### Issue 3: Navigation "Contact" Link Color Distinction Potentially Lost

**Page:** All pages — primary navigation bar  
**Element:** `#mega-menu-item-29 .mega-menu-link` (the Contact link with class `navigation-contact`)  
**WCAG Criterion:** 1.4.1 Use of Color (Level A)  
**Severity:** Minor  

**Description:** The "Contact" navigation item has a special class (`navigation-contact`, `mega-navigation-contact`) that suggests it is styled differently from other navigation items—likely with a distinct blue background or color treatment to make it stand out as the primary action link. For a user with tritanopia, this blue styling would appear gray and thus fail to differentiate "Contact" from the other navigation items visually.

**Impact on User:** Marcus found the Contact link by reading text labels sequentially. He did not benefit from any visual highlighting that might draw a user's eye directly to it as the primary CTA in the navigation bar.

**Recommended Fix:**  
- Style the Contact navigation item with multiple visual differentiators: a visible border/outline, distinct background shape (e.g., pill/rounded rectangle), bold text weight, or an icon, in addition to any color treatment.
- Ensure the visual distinction persists under color vision deficiency simulations.

---

### Issue 4: Service Card Accent Lines Are Color-Only Decorative Elements

**Page:** Homepage — "Make AI Your Competitive Advantage" cards section; Contact page — "Let's Connect" cards section  
**Element:** `.cards-wrapper .line` with inline style `border-color: #2363BB`  
**WCAG Criterion:** 1.4.1 Use of Color (Level A)  
**Severity:** Minor  

**Description:** Each service card features a blue accent line (`<span class="line" style="border-color: #2363BB">`) below the heading. For a user with tritanopia, this blue line appears as a faint gray line, losing its visual impact and branding significance. While these lines are decorative and don't convey essential information, they represent the brand's visual system failing for this user type.

**Impact on User:** The cards remain fully usable, but the visual design appears flat and generic. The branded blue accent that ties the cards to the company's identity is invisible.

**Recommended Fix:**  
- Since these are decorative, this is lower priority. However, consider increasing the line thickness or using a pattern/gradient that maintains visual interest regardless of color perception.
- Alternatively, add a subtle pattern or texture to the line.

---

### Issue 5: Case Study "Increase" Icons Have Empty Alt Text

**Page:** Homepage — Case Studies carousel, CDK Global card  
**Element:** `<img src="/wp-content/themes/some-like-it-neat/assets/images/increase.svg" class="increase" alt="">`  
**WCAG Criterion:** 1.1.1 Non-text Content (Level A)  
**Severity:** Major  

**Description:** In the CDK Global case study card, two metrics use an "increase" arrow icon instead of a numeric value to indicate positive outcomes ("Improved Sales Team Alignment" and "Streamlined Discovery & Quoting Process"). These icons have empty alt text (`alt=""`), meaning they convey no information to any user relying on something other than the visual arrow. For a tritanopia user, if the arrow icon is blue or color-dependent, it may also lack visual clarity.

**Impact on User:** Marcus saw arrow images with no textual or semantic explanation. He understood the descriptive text but lost the quantitative/directional meaning the icon was intended to convey.

**Recommended Fix:**  
- Add meaningful alt text to the increase icons, e.g., `alt="Improvement"` or `alt="Increase"`.
- Alternatively, replace the icon with a text-based indicator (e.g., a "+" symbol, or the word "Improved") that conveys the same meaning.

---

### Issue 6: Award/Badge Images Have Empty Alt Text

**Page:** Homepage — second logo/badge carousel (Clutch awards section)  
**Element:** Multiple `<img>` elements in `.logos-wrapper.small-logos` with `alt=""`  
**WCAG Criterion:** 1.1.1 Non-text Content (Level A)  
**Severity:** Minor  

**Description:** The awards/badge section contains seven badge images from Clutch (e.g., "Top Clutch Salesforce Company," "Top Clutch AI Consulting Company," "Global Award Spring 2025," etc.) that all have empty alt text (`alt=""`). These images convey meaningful credibility information—they are not purely decorative. For any user who cannot perceive the visual content of these badges (whether due to color confusion, low vision, or screen reader use), this information is completely lost.

**Impact on User:** Marcus saw badge-shaped images but could not determine what awards or recognitions they represented, especially since some badges might use blue/yellow color schemes that appear washed out with tritanopia.

**Recommended Fix:**  
- Add descriptive alt text to each badge image, e.g., `alt="Top Clutch Salesforce Company - United States 2025"`.
- Alternatively, add a visually hidden text label adjacent to each badge.

---

### Issue 7: Yellow Star in AgencyReview Badge Disappears for Tritanopia

**Page:** Homepage and Contact page — footer  
**Element:** AgencyReview badge inline SVG star with `fill="#eab308"` (yellow)  
**WCAG Criterion:** 1.4.1 Use of Color (Level A), 1.4.11 Non-text Contrast (Level AA)  
**Severity:** Minor  

**Description:** The AgencyReview badge in the footer uses a yellow star (`fill="#eab308"`) as a visual indicator of the rating. For a user with tritanopia, yellow appears as a very light pinkish-gray that nearly blends into the white badge background. The star effectively becomes invisible. The accompanying "10.0" text rating compensates somewhat, but the star icon—a universally recognized symbol for ratings—loses its visual meaning.

**Impact on User:** Marcus almost missed the star entirely. He relied on the "10.0" text to understand it was a rating. The visual hierarchy of "star = rating" was broken.

**Recommended Fix:**  
- Add a visible border or outline to the star icon that does not depend on fill color alone.
- Use a star with both fill and a dark stroke/border for visibility across color vision types.
- Alternatively, add alt text to the star image describing it as a rating star.

---

### Issue 8: Hero and Section Backgrounds Rely on Blue for Visual Hierarchy

**Page:** Homepage — hero section, "Our Signature Approach" process grid section; Contact page — hero section  
**Element:** `.page-header-wrapper` with `background-color: #1E60BD`; `.process-grid-wrapper.dark-blue-background`  
**WCAG Criterion:** 1.4.1 Use of Color (Level A)  
**Severity:** Minor  

**Description:** The hero section uses a blue background (#1E60BD) and the process grid uses a dark blue background to create visual sections and establish brand identity. For a user with tritanopia, these blues render as gray tones. While the white text on these backgrounds maintains sufficient contrast (the dark gray appearance still contrasts with white), the visual brand impact and section differentiation is significantly reduced. The page feels monotonically gray rather than having distinct blue-branded sections.

**Impact on User:** The site is usable but visually flat. Sections that are meant to feel like distinct branded areas all merge into a gray palette. Marcus perceived a less professional, less visually engaging experience than intended.

**Recommended Fix:**  
- This is primarily a branding/experience issue rather than a functional barrier. Consider supplementing color-based section differentiation with texture, patterns, or border treatments.
- Ensure important sections are differentiated not just by background color but by layout, spacing, and typography changes.

---

### Issue 9: Social Media Icons in Footer Have Empty Alt Text

**Page:** All pages — footer  
**Element:** Social media link icons: `<img src=".../facebook.svg" alt="">`, `<img src=".../instagram.svg" alt="">`, `<img src=".../linkedin.svg" alt="">`  
**WCAG Criterion:** 1.1.1 Non-text Content (Level A)  
**Severity:** Minor (mitigated)  

**Description:** The social media icons (Facebook, Instagram, LinkedIn) in the footer have empty alt attributes. However, each icon is accompanied by visible text labels ("Facebook", "Instagram", "LinkedIn") within the same link element, which effectively compensates. The empty alt text prevents redundant screen reader announcements but means the icon itself is not described.

**Impact on User:** Minimal direct impact for Marcus since the text labels are visible and clear. The icons themselves, being white SVGs on a dark background, are visually identifiable by shape regardless of color.

**Recommended Fix:**  
- The current implementation is acceptable since text labels are present. For best practice, consider using `aria-hidden="true"` explicitly on the icons (which `alt=""` effectively does) to confirm this is intentional, not an oversight.

---

### Issue 10: Form Validation Error States (Potential Issue)

**Page:** Homepage and Contact page — contact form (Ninja Forms)  
**Element:** Form fields (First Name, Last Name, Company Email, Company, How Can We Help You?)  
**WCAG Criterion:** 1.4.1 Use of Color (Level A), 3.3.1 Error Identification (Level A)  
**Severity:** Major (potential — conditional on implementation)  

**Description:** The contact form uses Ninja Forms, which by default displays validation errors using a combination of red border color and error text messages. While red is generally visible to users with tritanopia (tritanopia primarily affects blue-yellow perception, not red-green), if the form uses *only* a colored border (without accompanying error text) to indicate invalid fields, this could be a barrier. The form configuration shows error messages like "This is a required field" and "Please enter a valid email address!" which suggests text-based error feedback is present, but the visual indicator (border color change) could still rely on color alone.

**Impact on User:** If Marcus submitted the form with missing fields, he would likely see the text error messages. However, if only the field border changed color (without an adjacent error message appearing), he might miss which specific field needs attention.

**Recommended Fix:**  
- Ensure all form validation errors include both a visible text message AND a non-color visual indicator (such as an error icon, a bold border, or a shift in field styling that goes beyond color alone).
- Verify that Ninja Forms displays inline error text adjacent to each invalid field, not just a summary at the top of the form.

---

## Summary Table

| # | Issue | Page | WCAG | Severity | User Impact |
|---|-------|------|------|----------|-------------|
| 1 | Tab active state relies on color | Homepage | 1.4.1 (A) | Major | Cannot quickly identify active tab |
| 2 | Blue CTA buttons lack non-color emphasis | All pages | 1.4.1 (A) | Major | Primary CTAs don't visually stand out |
| 3 | Contact nav link color distinction lost | All pages | 1.4.1 (A) | Minor | CTA nav item doesn't draw attention |
| 4 | Card accent lines are color-only | Homepage, Contact | 1.4.1 (A) | Minor | Decorative branding lost |
| 5 | Case study "increase" icons empty alt | Homepage | 1.1.1 (A) | Major | Directional meaning not conveyed |
| 6 | Award badges have empty alt text | Homepage | 1.1.1 (A) | Minor | Credibility information inaccessible |
| 7 | Yellow star invisible for tritanopia | Footer | 1.4.1 (A), 1.4.11 (AA) | Minor | Rating star not perceivable |
| 8 | Blue backgrounds lose brand hierarchy | Homepage, Contact | 1.4.1 (A) | Minor | Flat visual experience, reduced branding |
| 9 | Social media icons empty alt (mitigated) | Footer | 1.1.1 (A) | Minor | Mitigated by text labels |
| 10 | Form error states potentially color-only | Homepage, Contact | 1.4.1 (A), 3.3.1 (A) | Major | May miss field-level error indicators |

---

## Positive Findings

The following accessibility practices were done well and should be maintained:

1. **Text-based navigation labels:** All navigation items use clear text labels, not color-coded icons alone.
2. **Required field asterisks:** The contact form marks required fields with `*` symbols in addition to any color treatment.
3. **Skip to content link:** The site includes `<a class="skip-link screen-reader-text" href="#primary">Skip to content</a>`.
4. **ARIA roles on tabs:** The tab component uses `role="tablist"`, `role="tab"`, `role="tabpanel"`, `aria-selected`, and `aria-controls` attributes.
5. **Semantic HTML structure:** Proper heading hierarchy (h1, h2, h3, h4) enables content scanning via structure.
6. **Form ARIA attributes:** The form container uses `aria-live="polite"`, `aria-labelledby`, `aria-describedby`, and `role="form"`.
7. **Button text labels:** All interactive buttons have descriptive text ("Connect with an Expert," "Learn More," "Submit").
8. **Arrow icons on card links:** Service card "Learn More" links include arrow icons, providing a non-color indicator of interactivity.
9. **Social media links have text labels:** Footer social links pair icons with text ("Facebook," "Instagram," "LinkedIn").
10. **Reduced motion respect:** The logo carousel checks `prefers-reduced-motion` media query before applying animations.
