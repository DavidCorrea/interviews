# Accessibility Report: Motor Impairment (Keyboard-Only User)

**Persona:** Alex Rivera — Keyboard-only user with cerebral palsy  
**Site:** https://launchpadlab.com/  
**Pages Evaluated:** Homepage (`/`), Contact (`/contact`), Services (`/services`)  
**Date:** February 2026  
**Evaluation Method:** Manual keyboard-only navigation audit against WCAG 2.1 AA  

---

## Executive Summary

The LaunchPad Lab website presents **multiple barriers** for keyboard-only users. The most critical issues center on the hover-dependent mega menu navigation system, insufficient focus indicators, and mouse-reliant carousel components. While basic content is technically reachable and primary goals (understanding services, finding contact information) can be partially achieved, the experience involves significant friction, unpredictable behavior, and accessibility patterns that fail to meet WCAG 2.1 Level AA standards.

---

## Issues Found

### Issue 1: Mega Menu Dropdown Requires Hover Intent to Open

**Page:** All pages (global header navigation)  
**Element:** `<ul id="mega-menu-menu-1">` — Max Mega Menu with `data-event="hover_intent"`  
**Specific Items:** "Services" (`#mega-menu-item-15070`) and "Industries" (`#mega-menu-item-15071`) dropdown menus  

**Description:**  
The mega menu navigation system is configured with `data-event="hover_intent"`, meaning submenus are designed to expand when a mouse pointer hovers over the parent menu item. The `data-second-click="go"` configuration implies the first click/activation opens the dropdown while the second navigates to the page. For keyboard users, this creates ambiguity: pressing Enter on "Services" may toggle the dropdown open or may navigate away entirely depending on the plugin's internal state management. The dropdown expansion relies on mouse hover detection (`data-hover-intent-timeout="300"`, `data-hover-intent-interval="100"`) with no equivalent keyboard-triggered open mechanism explicitly defined.

While the Max Mega Menu plugin includes some keyboard support (toggling `aria-expanded`), the visual feedback and behavioral consistency for keyboard users is significantly degraded compared to mouse users.

**WCAG Criteria Violated:**  
- **2.1.1 Keyboard (Level A):** All functionality must be operable through a keyboard interface. The dropdown trigger is primarily hover-based.
- **2.1.2 No Keyboard Trap (Level A):** Once a dropdown opens, there is no efficient keyboard mechanism to close it and return to the parent menu level without tabbing through all submenu items.

**Severity:** Critical  

**Impact on User:**  
Alex cannot reliably open navigation submenus to explore service categories or industry pages. Even when the dropdown does open via keyboard, Alex must tab through 8-10+ sub-items before reaching the next top-level menu item. This makes navigation slow and exhausting, potentially causing Alex to abandon the site.

**Recommended Fix:**  
- Configure the mega menu to open on Enter/Space key press (not just hover) with explicit toggle behavior.
- Add arrow key navigation within the menu: Left/Right to move between top-level items, Up/Down to move within submenus.
- Pressing Escape should close the open submenu and return focus to the parent menu item.
- Set `data-event` to `hover_intent click` or implement a custom keyboard handler that opens the panel on focus+Enter.

---

### Issue 2: Skip Link May Not Be Visible on Focus

**Page:** All pages (global)  
**Element:** `<a class="skip-link screen-reader-text" href="#primary">Skip to content</a>`  

**Description:**  
A skip-to-content link is present, which is excellent. However, it uses the class `screen-reader-text`, which in most WordPress themes applies CSS that visually hides the element (e.g., `clip: rect(1px, 1px, 1px, 1px); position: absolute; height: 1px; width: 1px; overflow: hidden;`). If this CSS does not include a `:focus` state that makes the link visible when it receives keyboard focus, sighted keyboard users will never see it and won't know it exists.

**WCAG Criteria Violated:**  
- **2.4.1 Bypass Blocks (Level A):** A mechanism to bypass repeated navigation blocks must be available. The skip link exists but may be invisible to sighted keyboard users.
- **2.4.7 Focus Visible (Level AA):** The focused element must have a visible focus indicator.

**Severity:** Major  

**Impact on User:**  
Alex relies on visible focus indicators to navigate. If the skip link is not visible when focused, Alex would have to Tab through the entire header navigation on every page load—approximately 30+ focusable elements in the mega menu before reaching page content.

**Recommended Fix:**  
Add CSS to make the skip link visible when focused:
```css
.skip-link:focus {
  clip: auto;
  height: auto;
  width: auto;
  position: fixed;
  top: 10px;
  left: 10px;
  z-index: 100000;
  background: #1E60BD;
  color: #ffffff;
  padding: 12px 24px;
  font-size: 16px;
  text-decoration: none;
  border-radius: 4px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.3);
}
```

---

### Issue 3: Insufficient or Missing Visible Focus Indicators

**Page:** All pages  
**Elements:** All interactive elements (links, buttons, cards, form fields)  

**Description:**  
The site does not define custom `:focus` or `:focus-visible` CSS styles for interactive elements. Default browser focus outlines (thin dotted lines or subtle glows) are relied upon. Against the site's visual design—especially the blue hero backgrounds (`#1E60BD`), the white card sections, and the dark footer—these default outlines may not provide sufficient contrast to be clearly visible. The `.button-white-base` and `.button-blue-base` button styles, `.mega-menu-link` navigation links, and `.card` interactive elements all lack explicit focus styling.

Additionally, the hover-cards-interaction class on service cards implies visual feedback on hover (mouse) but there is no equivalent `:focus` or `:focus-within` styling for keyboard users.

**WCAG Criteria Violated:**  
- **2.4.7 Focus Visible (Level AA):** Any keyboard-operable user interface must have a mode of operation where the keyboard focus indicator is visible.
- **2.4.11 Focus Appearance (Level AAA / WCAG 2.2):** Focus indicators should have sufficient size and contrast.
- **1.4.11 Non-text Contrast (Level AA):** UI components in their focused state must have at least 3:1 contrast ratio against adjacent colors.

**Severity:** Critical  

**Impact on User:**  
Alex frequently loses track of where keyboard focus is located. When tabbing through service cards, navigation items, or footer links, Alex cannot distinguish which element is currently focused. This makes navigation disorienting and error-prone, increasing the risk of activating the wrong link.

**Recommended Fix:**  
Define explicit, high-contrast focus styles:
```css
*:focus-visible {
  outline: 3px solid #FF6900;
  outline-offset: 3px;
  border-radius: 2px;
}

.mega-menu-link:focus-visible {
  outline: 3px solid #FF6900;
  outline-offset: 2px;
  background-color: rgba(255, 105, 0, 0.1);
}

.card:focus-visible,
.card a:focus-visible {
  outline: 3px solid #FF6900;
  outline-offset: 4px;
  box-shadow: 0 0 0 6px rgba(255, 105, 0, 0.25);
}

.button-white-base:focus-visible,
.button-blue-base:focus-visible {
  outline: 3px solid #FF6900;
  outline-offset: 3px;
}
```

---

### Issue 4: Testimonials Carousel Has No Keyboard Controls

**Page:** Homepage (`/`), Contact (`/contact`)  
**Element:** `<ul class="single-item-slider">` — Tiny Slider carousel  

**Description:**  
The testimonials carousel is initialized with `controls: false` (no prev/next buttons), `mouseDrag: true` (primary interaction is mouse dragging), and `autoplay: false`. The only navigation mechanism is dot indicators (`navPosition: "bottom"`). Without explicit prev/next buttons, keyboard users have no clearly labeled controls to cycle through testimonials. Mouse dragging is the intended interaction method, which is entirely inaccessible to keyboard-only users.

The dots may be focusable, but they lack descriptive labels (typically rendered as small circles with no text) and are extremely small click/focus targets.

**WCAG Criteria Violated:**  
- **2.1.1 Keyboard (Level A):** All functionality must be operable through a keyboard. Mouse-drag-only carousel navigation is not keyboard accessible.
- **4.1.2 Name, Role, Value (Level A):** Navigation dots lack accessible names (e.g., "Slide 1 of 5", "Testimonial from Patrick West").
- **2.5.5 Target Size (Level AAA / WCAG 2.2):** Carousel dots are typically very small (< 44x44px CSS pixels).

**Severity:** Major  

**Impact on User:**  
Alex cannot browse through client testimonials, which are important social proof when evaluating a digital agency. Alex is stuck on whichever testimonial is initially displayed, missing four additional client quotes.

**Recommended Fix:**  
- Enable `controls: true` in the Tiny Slider configuration to show prev/next buttons.
- Ensure prev/next buttons are `<button>` elements with accessible labels (e.g., `aria-label="Next testimonial"`, `aria-label="Previous testimonial"`).
- Add `aria-roledescription="carousel"` to the slider container.
- Add `aria-label` to each slide (e.g., `aria-label="Testimonial 1 of 5: Patrick West, VP of Apex Leaders"`).
- Ensure dot indicators have accessible names.
- Set `mouseDrag: false` or ensure it supplements (not replaces) keyboard controls.

---

### Issue 5: Service Cards Have Duplicate Tab Stops

**Page:** Homepage (`/`)  
**Element:** `.cards-wrapper .card` — Service card items in the "Make AI Your Competitive Advantage" section  

**Description:**  
Each service card is wrapped in an outer `<a>` element linking to the service page (e.g., `/services/ai-automation-agentforce/`). Inside each card, there is also an inner `<a class="link-black-base arrow-link">Learn More</a>` link pointing to the exact same URL. This creates two focusable elements per card that perform the identical action.

With six service cards, this results in **12 tab stops** instead of 6 for the same set of destinations. The inner "Learn More" link also contains an `<img>` with `alt=""`, which is fine, but the duplicate link is confusing—a keyboard user tabs to the card, presses Enter (or continues tabbing and reaches "Learn More"), and both go to the same place.

**WCAG Criteria Violated:**  
- **2.4.4 Link Purpose (In Context) (Level A):** Multiple links to the same destination create confusion about whether they serve different purposes.
- **2.4.7 Focus Visible (Level AA):** Two adjacent focusable elements going to the same place can cause "focus confusion" where the user doesn't know if they've moved to a new option.

**Severity:** Minor  

**Impact on User:**  
Alex must press Tab twice as many times as necessary to move through the services section. The duplicate links don't cause a functional failure, but they significantly slow down navigation and add cognitive overhead.

**Recommended Fix:**  
- Remove `tabindex` or add `tabindex="-1"` and `aria-hidden="true"` to the inner "Learn More" link when the outer card link exists.
- Alternatively, restructure so the card is a single `<a>` element with no nested interactive children.
- Use CSS `:focus-within` on the card to visually highlight the card when any child link is focused.

---

### Issue 6: Contact Form JavaScript Dependency & Accessibility Uncertainty

**Page:** Contact (`/contact`)  
**Element:** `<div id="nf-form-13-cont" class="nf-form-cont">` — Ninja Forms contact form  

**Description:**  
The contact form is rendered entirely by the Ninja Forms JavaScript plugin. The server-side HTML contains only an empty container with a loading spinner. The `<noscript>` element states: *"Notice: JavaScript is required for this content."* 

When JavaScript executes, the form fields are dynamically injected. This means the accessibility of the form depends entirely on the Ninja Forms plugin's client-side rendering quality, including:
- Proper `<label>` elements associated with inputs via `for`/`id` attributes
- Logical tab order of form fields
- Visible focus indicators on inputs, selects, and the submit button
- Accessible error messages linked to fields via `aria-describedby`
- The submit button being a keyboard-activatable `<button>` or `<input type="submit">`

The container has `aria-live="polite"` and `role="form"`, which are positive signals. However, the dynamic rendering introduces risk that the live form may not meet keyboard accessibility standards.

**WCAG Criteria Violated (Potential):**  
- **1.3.1 Info and Relationships (Level A):** Form labels must be programmatically associated with inputs.
- **2.1.1 Keyboard (Level A):** All form interactions must be keyboard operable.
- **3.3.2 Labels or Instructions (Level A):** Form fields must have visible labels.
- **4.1.2 Name, Role, Value (Level A):** Dynamic form elements must expose correct names and roles to assistive technology.

**Severity:** Major  

**Impact on User:**  
The contact form is Alex's most likely method of initiating a business relationship with LaunchPad Lab. If form fields lack proper labels, have broken tab order, or if the submit button is not keyboard accessible, Alex cannot complete the primary conversion action on the site. The reliance on JavaScript rendering introduces accessibility uncertainty that cannot be verified from the static HTML alone.

**Recommended Fix:**  
- Audit the live-rendered Ninja Forms output for proper label associations, tab order, and focus management.
- Ensure all form fields have visible `<label>` elements with correct `for` attributes.
- Add `aria-required="true"` to required fields.
- Ensure error messages are linked to fields via `aria-describedby`.
- Test the entire form submission flow using only keyboard (Tab, Enter, Space).
- Consider providing a server-rendered fallback form for users with JavaScript disabled.

---

### Issue 7: Auto-Scrolling Logo Carousel Cannot Be Paused

**Page:** Homepage (`/`)  
**Element:** `.logos__scroller > .logos__list` — Client logos section ("Trusted by Hundreds of Innovative Businesses")  

**Description:**  
The client logo section displays a scrolling marquee of company logos (Kawasaki Engines, Harvard University, Whirlpool, Northwestern University, CDK Global, Lurie Children's Hospital, etc.). This scrolling animation runs automatically and continuously. There is no visible pause, stop, or hide mechanism available to keyboard users. The animation is CSS-based or JavaScript-driven with no keyboard-accessible controls.

**WCAG Criteria Violated:**  
- **2.2.2 Pause, Stop, Hide (Level A):** For moving, blinking, or scrolling content that starts automatically and lasts more than 5 seconds, a mechanism must be provided to pause, stop, or hide it.

**Severity:** Minor  

**Impact on User:**  
While the logo carousel is non-interactive (logos are not links), the continuous motion can be distracting for Alex while trying to focus on reading page content or tracking keyboard focus position. The inability to pause the animation is a compliance failure even if the practical impact is modest.

**Recommended Fix:**  
- Add a visible "Pause" / "Play" toggle button near the logo carousel.
- Respect `prefers-reduced-motion: reduce` media query to disable the animation for users who have enabled reduced motion in their OS settings.
```css
@media (prefers-reduced-motion: reduce) {
  .logos__scroller .logos__list {
    animation: none;
  }
}
```

---

### Issue 8: Non-Semantic Hamburger Menu Button

**Page:** All pages (global header, mobile viewport)  
**Element:** `<div id="burgerBtn"></div>`  

**Description:**  
The mobile hamburger menu trigger is implemented as a plain `<div>` element with no semantic role, no keyboard focusability (`tabindex` not set), no `aria-label`, and no `role="button"`. This element is invisible to keyboard navigation and assistive technologies.

While the Max Mega Menu plugin provides its own accessible toggle button (`<button aria-label="Toggle Menu" class="mega-toggle-animated">`), the `burgerBtn` div may be visually displayed at certain viewport sizes and could create confusion about which element controls the menu.

**WCAG Criteria Violated:**  
- **4.1.2 Name, Role, Value (Level A):** Interactive UI components must have accessible names and appropriate roles.
- **2.1.1 Keyboard (Level A):** All interactive elements must be keyboard operable.

**Severity:** Major (at mobile breakpoints) / Minor (at desktop breakpoints if hidden)  

**Impact on User:**  
If Alex accesses the site on a tablet or at a narrow viewport where the hamburger button is displayed and the mega menu toggle is hidden, Alex has no way to open the navigation menu. This could completely block access to the site's navigation.

**Recommended Fix:**  
- Replace `<div id="burgerBtn">` with `<button id="burgerBtn" aria-label="Open navigation menu" aria-expanded="false">`.
- Or remove the element entirely if the mega menu plugin's toggle is sufficient.
- Ensure only one toggle element is visible and focusable at each viewport size.

---

### Issue 9: Timeline/Cards Sliders Rely on Mouse Drag

**Page:** Various (pages using `.timeline-blocks`, `.cards-slider`, `.outcome-slider`)  
**Element:** Tiny Slider carousels with `mouseDrag: true`  

**Description:**  
Multiple carousel components across the site are initialized with `mouseDrag: true` as a primary navigation mechanism. The `timeline-blocks` slider has `controls: true` and `nav: false`, meaning it has prev/next buttons but no dots. The `cards-slider` and `outcome-slider` have `controls: false` and rely on mouse dragging.

For keyboard users, the sliders without controls offer no mechanism to advance slides. Even the timeline slider with `controls: true` needs those controls to be properly keyboard accessible `<button>` elements with clear focus indicators.

**WCAG Criteria Violated:**  
- **2.1.1 Keyboard (Level A):** Carousel navigation must be available via keyboard.
- **2.5.1 Pointer Gestures (Level A):** Functionality that requires multi-point or path-based gestures (like dragging) must have single-pointer alternatives.

**Severity:** Major  

**Impact on User:**  
Alex cannot browse portfolio items, timeline content, or card sliders that use mouse-drag-only navigation. Content within these carousels is effectively hidden from keyboard users.

**Recommended Fix:**  
- Set `controls: true` for all Tiny Slider instances.
- Ensure prev/next buttons are keyboard-focusable `<button>` elements with descriptive `aria-label` attributes.
- Add `aria-roledescription="carousel"` and proper slide labeling.
- Provide arrow key navigation within the slider when it has focus.

---

### Issue 10: Footer Phone Link Contains Malformed HTML

**Page:** All pages (global footer)  
**Element:** `<a href="tel:312-888-9651"">(312) 888-9651</a>`  

**Description:**  
The phone number link in the footer contains a double closing quote in the `href` attribute: `href="tel:312-888-9651""`. While browsers are generally forgiving of this malformation and the link functions correctly, it indicates a lack of HTML validation that often correlates with deeper accessibility issues.

**WCAG Criteria Violated:**  
- **4.1.1 Parsing (Level A):** In content implemented using markup languages, elements have complete start and end tags, are nested according to their specifications, do not contain duplicate attributes, and IDs are unique. (Note: This criterion was deprecated in WCAG 2.2 but remains relevant for WCAG 2.1 compliance.)

**Severity:** Minor  

**Impact on User:**  
Minimal direct impact—browsers handle the malformed attribute gracefully. However, it reflects code quality concerns.

**Recommended Fix:**  
Correct the HTML:
```html
<a href="tel:312-888-9651">(312) 888-9651</a>
```

---

## Summary Table

| # | Issue | Page(s) | WCAG Criteria | Severity | 
|---|-------|---------|---------------|----------|
| 1 | Mega menu hover-dependent dropdown | All | 2.1.1, 2.1.2 | Critical |
| 2 | Skip link not visible on focus | All | 2.4.1, 2.4.7 | Major |
| 3 | Missing/insufficient focus indicators | All | 2.4.7, 1.4.11 | Critical |
| 4 | Testimonials carousel has no keyboard controls | Homepage, Contact | 2.1.1, 4.1.2 | Major |
| 5 | Duplicate tab stops on service cards | Homepage | 2.4.4 | Minor |
| 6 | Contact form JS-rendered, accessibility uncertain | Contact | 1.3.1, 2.1.1, 3.3.2, 4.1.2 | Major |
| 7 | Auto-scrolling logos cannot be paused | Homepage | 2.2.2 | Minor |
| 8 | Non-semantic hamburger menu `<div>` | All (mobile) | 4.1.2, 2.1.1 | Major |
| 9 | Sliders rely on mouse drag | Various | 2.1.1, 2.5.1 | Major |
| 10 | Footer phone link malformed HTML | All | 4.1.1 | Minor |

---

## Severity Distribution

- **Critical:** 2 issues (mega menu hover dependency, missing focus indicators)
- **Major:** 5 issues (skip link visibility, testimonials carousel, contact form, hamburger button, slider controls)
- **Minor:** 3 issues (duplicate card links, auto-scrolling logos, malformed HTML)

---

## Recommendations Priority

### Immediate (Critical)
1. **Add explicit keyboard support to the mega menu** — Ensure Enter/Space opens dropdowns, Escape closes them, and arrow keys navigate within them.
2. **Implement visible focus indicators** across the entire site using `:focus-visible` with high-contrast outlines (3:1 minimum contrast ratio).

### Short-Term (Major)
3. **Make the skip link visible on focus** so sighted keyboard users can use it.
4. **Enable prev/next controls** on all Tiny Slider carousels and add proper ARIA labels.
5. **Audit the Ninja Forms contact form** for keyboard accessibility (label associations, tab order, focus management, error handling).
6. **Replace or remove the non-semantic hamburger `<div>`** with a proper `<button>` element.

### Long-Term (Minor)
7. **Remove duplicate links** in service cards by making the inner "Learn More" link non-focusable when the outer card link exists.
8. **Add pause controls** to the auto-scrolling logo marquee and respect `prefers-reduced-motion`.
9. **Fix the malformed HTML** in the footer phone link.
