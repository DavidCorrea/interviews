# Accessibility Report: Voice Control User Evaluation

**Website:** https://launchpadlab.com/  
**Evaluator Persona:** Marcus Webb — 52-year-old voice control user with ALS. Cannot use keyboard or mouse. Uses Dragon NaturallySpeaking for all computer interaction. Navigates by speaking commands like "Click [label]" to target elements by their visible text or accessible name.  
**Date:** February 2026  
**Pages Evaluated:** Homepage (`/`), Contact (`/contact`), Services (`/services`), About (`/about`)  

---

## Executive Summary

The LaunchPad Lab website presents a **mixed experience for voice control users**. Several critical interactive patterns work well: the main navigation links have clear, unique visible text labels (Services, Technologies, Industries, Our Work, About Us, Insights, Contact); the contact form fields have visible labels that match their accessible names; the tab interface uses unique, descriptive tab labels; and the footer social links have visible text alongside their icons. These elements allow a voice control user to say "Click Contact," "Click First Name," "Click Submit," or "Click Operational Efficiency" and have the correct element activate.

However, significant barriers exist. The most severe is the **hamburger menu icon**, which is an unlabeled `<div>` with no accessible name — completely unusable by voice on mobile/tablet viewports. Seven identical **"Learn More" links** on the homepage cannot be distinguished by voice command, forcing reliance on Dragon's "show numbers" fallback. The **mega menu dropdowns are triggered by hover**, an interaction voice control cannot perform reliably. Several **icon-only buttons** (mega menu close, carousel controls) lack visible text labels. And each service card contains **duplicate links** to the same destination, creating ambiguity for voice targeting.

On a desktop viewport with the full navigation bar visible, both user goals (finding what LaunchPad Lab does and how to contact them) were achievable with friction. On a mobile/tablet viewport where the hamburger menu is the sole navigation method, the site would be **completely unusable** for a voice control user.

---

## Issues Found

### Issue 1: Hamburger Menu Icon Is an Unlabeled `<div>` — Completely Unusable by Voice

**Page:** All pages (at mobile/tablet viewport widths)  
**Element:** `<div id="burgerBtn">` — the hamburger menu icon that appears at narrower viewports  
**WCAG Criteria:** [4.1.2 Name, Role, Value (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html), [2.1.1 Keyboard (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/keyboard.html)  
**Severity:** Critical  

**Description:**  
The hamburger menu icon is implemented as a `<div>` element (`<div id="burgerBtn">`), not a `<button>` or `<a>`. It has:
- No visible text label (it is a CSS-generated three-line icon)
- No `aria-label` or `aria-labelledby` attribute
- No semantic role (`role="button"` is missing)
- No accessible name of any kind

Voice control software identifies interactive elements by their visible text or accessible name. This element has neither. A voice control user looking at the hamburger icon cannot say "Click Menu," "Click Navigation," "Click Hamburger," or any other phrase that would target this element. It is invisible to voice control software.

The Max Mega Menu plugin does generate a separate `<button>` with `aria-label="Toggle Menu"`, but this button may not be visually rendered at all viewports, and its accessible name ("Toggle Menu") has no corresponding visible text — creating an accessible name mismatch even if the button is present.

**Impact on this user:**  
Marcus cannot open the navigation menu at mobile or tablet viewport widths. Without navigation, he cannot reach any page — Services, About, Contact — and both user goals become unachievable. The site is entirely unusable on any viewport where the hamburger menu replaces the full navigation bar. This is a complete access barrier.

**Recommended Fix:**  
- Replace the `<div id="burgerBtn">` with a `<button>` element.
- Add visible text: `<button id="burgerBtn" aria-expanded="false"><span class="sr-only">Menu</span></button>` at minimum, or preferably a visible "Menu" label alongside the icon.
- Add `aria-expanded="false/true"` to indicate open/closed state.
- Ensure the visible text and `aria-label` (if used) match, per WCAG 2.5.3 (Label in Name).

---

### Issue 2: Seven Identical "Learn More" Links Cannot Be Distinguished by Voice

**Page:** Homepage (`/`)  
**Element:** Seven `<a>` elements with the text "Learn More" — six in the service cards section, one in the AI callout section  
**WCAG Criteria:** [2.5.3 Label in Name (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/label-in-name.html), [2.4.4 Link Purpose (In Context) (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html), [2.4.9 Link Purpose (Link Only) (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-link-only.html)  
**Severity:** Critical  

**Description:**  
The homepage services section contains six service cards, each with a link reading "Learn More":

```html
<a href=".../services/ai-automation-agentforce/" class="link-black-base arrow-link">Learn More</a>
<a href=".../services/web-app-development/" class="link-black-base arrow-link">Learn More</a>
<a href=".../services/mobile-app-development/" class="link-black-base arrow-link">Learn More</a>
<a href=".../services/salesforce-development/" class="link-black-base arrow-link">Learn More</a>
<a href=".../services/digital-design-product-development/" class="link-black-base arrow-link">Learn More</a>
<a href=".../services/managed-support-enhancement/" class="link-black-base arrow-link">Learn More</a>
```

A seventh "Learn More" link appears in the AI callout section further down the page. None of these links have `aria-label` or `aria-labelledby` attributes.

When a voice control user says "Click Learn More," the software detects all seven instances and cannot determine which one the user intends. Dragon NaturallySpeaking falls back to overlaying numbers on each matching element, requiring the user to visually cross-reference the number overlay with the surrounding card content and then say the number. This "show numbers" fallback is a design failure indicator — it means the interface is not voice-navigable by label.

**Impact on this user:**  
Marcus cannot directly target any specific service's "Learn More" link. Every time he wants to explore a service, he must: (1) say "Click Learn More," (2) wait for Dragon to overlay numbers, (3) visually identify which number corresponds to the desired service card, (4) say the number. This multi-step fallback is slow, cognitively demanding, and error-prone. With six services, it happens six times in one page section.

**Recommended Fix:**  
- Make each link's visible text unique: "Learn More about AI Automation," "Learn More about Web App Development," etc.
- Alternatively, add `aria-label` to each link (e.g., `aria-label="Learn more about AI Automation & Agentic AI"`), but **the `aria-label` must contain the visible text "Learn More"** to comply with WCAG 2.5.3 Label in Name. The visible text must be included in the accessible name.
- Or use visually hidden text: `Learn More <span class="sr-only">about Salesforce Development</span>`.

---

### Issue 3: Mega Menu Dropdowns Triggered by Hover — Not Reliably Activated by Voice Click

**Page:** All pages (header navigation)  
**Element:** Top-level mega menu items for "Services" and "Industries" — configured with `data-event="hover_intent"`  
**WCAG Criteria:** [2.1.1 Keyboard (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/keyboard.html), [2.5.1 Pointer Gestures (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/pointer-gestures.html)  
**Severity:** Major  

**Description:**  
The mega menu uses `hover_intent` as its event trigger for opening dropdown panels. The "Services" and "Industries" navigation items expand to reveal submenu panels when the user hovers the mouse cursor over them. Voice control software simulates a "click" when the user says "Click Services" — it does not simulate a "hover."

The menu has a `data-second-click="go"` configuration, meaning the first click should open the dropdown and the second click should navigate to the page. However, the interaction between voice-initiated clicks and hover-intent JavaScript is unpredictable. In some cases, saying "Click Services" opens the dropdown; in others, it navigates directly to the Services page (bypassing the submenu). This inconsistency makes the mega menu unreliable for voice control users.

**Impact on this user:**  
Marcus cannot reliably open the Services or Industries dropdown menus. He may inadvertently navigate away from the homepage when he intended to browse submenu items. The inconsistency forces trial-and-error interaction, which is frustrating and time-consuming.

**Recommended Fix:**  
- Change the mega menu event trigger from `hover_intent` to `click` (or support both).
- Ensure that the first click/activation consistently opens the dropdown, and provide a separate, clearly labeled "View All Services" link for navigation.
- Test the menu interaction with voice control software to confirm consistent behavior.

---

### Issue 4: Mega Menu Close Button Is Icon-Only — No Visible Text Label

**Page:** All pages (header navigation, when mega menu dropdown is open)  
**Element:** `<button class="mega-close" aria-label="Close">` — the X icon button that closes the mega menu dropdown  
**WCAG Criteria:** [2.5.3 Label in Name (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/label-in-name.html), [4.1.2 Name, Role, Value (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)  
**Severity:** Major  

**Description:**  
When a mega menu dropdown is open, a close button appears. This button renders as an X icon with no visible text. It has `aria-label="Close"`, which provides an accessible name for screen readers. However, there is no visible text label on the button.

Voice control software like Dragon NaturallySpeaking primarily matches speech to **visible text**. When no visible text is present, some voice control tools will fall back to matching the `aria-label`, but this behavior is inconsistent across platforms (Dragon, macOS Voice Control, Windows Speech Recognition). The WCAG 2.5.3 (Label in Name) criterion requires that when an accessible name exists, the visible label text must be contained within the accessible name — but this button has **no visible label at all**, meaning there is nothing for the user to read and speak.

**Impact on this user:**  
If Marcus accidentally opens a mega menu dropdown, he may not be able to close it by voice. Saying "Click Close" may or may not work depending on his voice control software's ability to match `aria-label`. If it fails, he is stuck with an open dropdown overlaying the page content and must resort to "show numbers" to find and click the close button.

**Recommended Fix:**  
- Add visible text to the close button: `<button class="mega-close"><span>Close</span></button>` — the text can be styled small or positioned alongside the X icon.
- Ensure `aria-label="Close"` matches the visible text, or remove `aria-label` entirely and let the visible text serve as the accessible name.
- At minimum, add a visually hidden `<span class="sr-only">Close</span>` inside the button, but a visible label is strongly preferred for voice control users.

---

### Issue 5: Duplicate Links on Service Cards — Two Links to Same URL Per Card

**Page:** Homepage (`/`)  
**Element:** Each service card has an outer `<a>` wrapping the entire card AND an inner `<a class="link-black-base arrow-link">Learn More</a>` link — both pointing to the same service URL  
**WCAG Criteria:** [2.4.4 Link Purpose (In Context) (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html), [1.3.1 Info and Relationships (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)  
**Severity:** Major  

**Description:**  
Each of the six service cards on the homepage is implemented as a large clickable `<a>` element wrapping the card content (heading, description, icon). Inside each card, there is also a separate `<a>` element with the text "Learn More" linking to the same URL. This creates two overlapping interactive elements per card.

When a voice control user attempts to interact with a service card, the software detects both the outer card link and the inner "Learn More" link. If the user says the card heading text (e.g., "Click AI Automation and Agentic AI"), Dragon may target the outer `<a>` wrapper, the `<h3>` heading text inside it, or neither — the behavior is unpredictable with nested interactive elements. The "Learn More" link inside the card is separately targetable but suffers from the duplicate label problem (Issue 2).

**Impact on this user:**  
Marcus encounters ambiguity when trying to click service cards. Nested links create multiple clickable regions within a single visual card, and voice control software may misidentify which element the user intends to activate. This adds confusion and increases the likelihood of needing the "show numbers" fallback.

**Recommended Fix:**  
- Remove the duplicate inner "Learn More" link and keep only the outer card-level `<a>` wrapper. Add a unique accessible name to the card link using `aria-label` (e.g., `aria-label="Learn more about AI Automation & Agentic AI"`).
- Or remove the outer card `<a>` wrapper and make only the "Learn More" link interactive, with unique accessible text per card.
- Do not nest `<a>` elements or create overlapping clickable regions.

---

### Issue 6: Testimonials Carousel Has No Controls — Cannot Be Navigated by Voice

**Page:** Contact (`/contact`), Homepage (`/`)  
**Element:** Tiny Slider testimonials carousel configured with `controls: false` and `mouseDrag: true`  
**WCAG Criteria:** [2.1.1 Keyboard (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/keyboard.html), [2.5.1 Pointer Gestures (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/pointer-gestures.html)  
**Severity:** Major  

**Description:**  
The testimonials carousel on the contact page (and possibly the homepage) uses Tiny Slider with `controls: false`, which disables the rendering of "Previous" and "Next" buttons entirely. The primary interaction method is `mouseDrag: true` — the user is expected to click and drag with a mouse to cycle through testimonials. Navigation dots (`navPosition: "bottom"`) may be present but are small, unlabeled circle icons.

Voice control users cannot perform drag gestures. Without "Previous" and "Next" buttons (or any labeled controls), there is no voice-speakable element to cycle through testimonials. Navigation dots, if present, have no visible text labels — they are just small circles.

**Impact on this user:**  
Marcus can only see the first testimonial in the carousel. He cannot cycle to other testimonials. While this doesn't block his primary goals (finding what they do and how to contact them), it means he receives an incomplete picture of client satisfaction compared to sighted mouse users who can freely browse all testimonials.

**Recommended Fix:**  
- Enable carousel controls: set `controls: true` in the Tiny Slider configuration.
- Add visible text labels to the controls: "Previous testimonial" and "Next testimonial."
- If navigation dots are used, add `aria-label` attributes: `aria-label="Testimonial 1 of 5"`, etc.
- Provide a "Pause" button to stop auto-advancing, if applicable.

---

### Issue 7: Mega Menu Toggle Button Has Accessible Name Mismatch with No Visible Text

**Page:** All pages  
**Element:** `<button aria-label="Toggle Menu" aria-expanded="false">` — the mega menu plugin's toggle button  
**WCAG Criteria:** [2.5.3 Label in Name (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/label-in-name.html)  
**Severity:** Major  

**Description:**  
The Max Mega Menu plugin generates a toggle button with `aria-label="Toggle Menu"`. This button may render as an icon (three lines or similar) with no visible text. The `aria-label` provides an accessible name for assistive technology, but:

1. There is no visible text label for the user to read and speak.
2. WCAG 2.5.3 (Label in Name) requires that when a component has a visible text label, the accessible name must contain that visible text. Here, the inverse problem exists: the accessible name exists but the visible label does not, leaving voice control users with nothing to read and speak.
3. A voice control user would need to guess "Click Toggle Menu" — a phrase they would not naturally derive from looking at a three-line icon.

**Impact on this user:**  
Marcus sees a hamburger-style icon but has no visible text to guide his voice command. He might guess "Click Menu," but the accessible name is "Toggle Menu" — if his voice control software matches on accessible name, "Click Menu" might work (since "Menu" is contained within "Toggle Menu"), but this depends on the software's matching algorithm. The interaction is unreliable.

**Recommended Fix:**  
- Add visible text "Menu" next to or below the icon.
- Ensure `aria-label` matches or contains the visible text (e.g., `aria-label="Menu"` or `aria-label="Open menu"`).
- Consider removing `aria-label` entirely and using visible text as the accessible name.

---

### Issue 8: Logo Carousel Auto-Scrolls with No Pause Control

**Page:** Homepage (`/`)  
**Element:** Client logos horizontal scrolling carousel (Kawasaki Engines, Harvard University, Whirlpool, etc.)  
**WCAG Criteria:** [2.2.2 Pause, Stop, Hide (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)  
**Severity:** Minor  

**Description:**  
The client logos section features a horizontally auto-scrolling carousel displaying brand logos. The animation runs continuously. There is no visible pause button, stop button, or any other control to halt the motion. The logos are not interactive links — they are display-only images.

**Impact on this user:**  
Marcus cannot pause the scrolling animation by voice. While the logos are not interactive (he doesn't need to click them), the continuous motion can be distracting. For voice control users who are scanning the page visually to identify clickable elements, auto-moving content can disrupt visual focus and make it harder to locate the element they want to target.

**Recommended Fix:**  
- Add a visible "Pause" button with clear text label near the carousel.
- Alternatively, pause the animation on any user interaction with the page.
- Respect `prefers-reduced-motion` media query to disable the animation for users who have enabled reduced motion in their OS settings.

---

### Issue 9: Case Study CTA Buttons Use Company Names Without Action Verbs

**Page:** Homepage (`/`)  
**Element:** Case study slide CTA buttons: `<a class="button button-white-base">Prosci</a>`, `<a class="button button-white-base">CDK Global</a>`, `<a class="button button-white-base">Millennium Trust Company</a>`  
**WCAG Criteria:** [2.4.4 Link Purpose (In Context) (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)  
**Severity:** Minor  

**Description:**  
The case studies carousel features CTA buttons whose visible text is simply the client company name — "Prosci," "CDK Global," "Millennium Trust Company." These links lead to LaunchPad Lab's case study pages about those clients. However, the link text contains no action verb ("View," "Read," "Explore") to indicate what will happen when clicked.

For voice control, these labels are at least **unique** — saying "Click Prosci" or "Click CDK Global" targets a single element without ambiguity. However, the user cannot determine from the visible text alone whether the link goes to Prosci's external website or to a LaunchPad Lab case study page.

**Impact on this user:**  
Marcus can successfully target these buttons by voice, but he may hesitate to click them because the link purpose is ambiguous. He might worry that "Click Prosci" will navigate him away from LaunchPad Lab's site.

**Recommended Fix:**  
- Change link text to include an action verb: "View Prosci Case Study" or "Read CDK Global Project."
- Alternatively, add `aria-label="View Prosci case study"` while keeping the visible text as "Prosci" — but note that this creates an accessible name mismatch, which is problematic for voice control (WCAG 2.5.3). The preferred approach is to change the visible text.

---

### Issue 10: "Connect" Link on Contact Page Has Vague Visible Text

**Page:** Contact (`/contact`)  
**Element:** `<a href="https://www.linkedin.com/company/launchpad-lab/mycompany/" target="_blank" rel="noopener">Connect</a>` — under the "Connect with Us on LinkedIn" heading  
**WCAG Criteria:** [2.4.4 Link Purpose (In Context) (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)  
**Severity:** Minor  

**Description:**  
The contact page has a section headed "Connect with Us on LinkedIn" (h3) containing a link with the visible text "Connect." While the heading provides visual context, the link text alone is vague. For voice control, saying **"Click Connect"** does work because the word is unique on the page. However, the visible text doesn't communicate the destination (LinkedIn) or the action (opening an external site).

**Impact on this user:**  
Marcus can target the link successfully. The uniqueness of "Connect" on this page means Dragon won't show a disambiguation overlay. The issue is mild — the link is functional but its text is not self-descriptive.

**Recommended Fix:**  
- Change the link text to "Connect on LinkedIn" or "Visit our LinkedIn page."

---

### Issue 11: reCAPTCHA Widget on Contact Form — Potential Voice Control Barrier

**Page:** Contact (`/contact`), Homepage (`/`) (footer form)  
**Element:** Google reCAPTCHA widget embedded in the Ninja Forms contact form  
**WCAG Criteria:** [2.1.1 Keyboard (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/keyboard.html), [1.1.1 Non-text Content (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)  
**Severity:** Minor  

**Description:**  
The contact form includes a Google reCAPTCHA widget. The initial "I'm not a robot" checkbox can be activated by voice ("Click I'm not a robot"). However, if the reCAPTCHA escalates to an image-based challenge (e.g., "Select all images with traffic lights"), the user must click specific grid squares. These grid cells have no visible text labels — they are images in a grid.

This is a well-known industry-wide accessibility barrier, not unique to LaunchPad Lab's implementation. However, it represents a potential failure point for voice control users attempting to submit the contact form.

**Impact on this user:**  
If the reCAPTCHA image challenge triggers, Marcus must use Dragon's "show numbers" fallback to overlay numbers on each grid cell, then say numbers one by one — a slow, error-prone process under time pressure. If the challenge is too complex, he may be unable to submit the form.

**Recommended Fix:**  
- Use reCAPTCHA v3 (invisible, score-based) instead of reCAPTCHA v2 (checkbox/challenge) to eliminate the interactive challenge entirely.
- Alternatively, use a honeypot field or server-side spam detection to avoid CAPTCHA altogether.
- As a fallback, provide alternative contact methods (email, phone) prominently near the form.

---

### Issue 12: Broken Skip Navigation Link

**Page:** All pages  
**Element:** `<a class="skip-link screen-reader-text" href="#primary">Skip to content</a>`  
**WCAG Criteria:** [2.4.1 Bypass Blocks (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)  
**Severity:** Minor (for voice control specifically)  

**Description:**  
The skip link targets `#primary`, but no element in the DOM has `id="primary"`. The link is non-functional. Additionally, the skip link has a `screen-reader-text` class, making it visually hidden. A voice control user cannot see it, so they cannot say "Click Skip to content."

For voice control users, skip links are less critical than for keyboard or screen reader users, because voice control users can visually scan the page and target any visible element directly. However, a functional, visible-on-focus skip link could still be useful for jumping past navigation quickly.

**Impact on this user:**  
Minimal direct impact. Marcus navigates visually and targets elements by their visible text. He would not typically use a skip link. However, the broken link represents a general accessibility failure.

**Recommended Fix:**  
- Add `id="primary"` to the `<main>` element.
- Make the skip link visible on focus (`:focus` styles) so it's accessible to both keyboard and voice control users.

---

## Positive Findings

The following elements work well for voice control and should be maintained:

### 1. Clear, Unique Navigation Link Labels
All main navigation items — Services, Technologies, Industries, Our Work, About Us, Insights, Contact — have visible text labels that are unique and descriptive. A voice control user can say "Click Contact" or "Click About Us" and the correct link activates without ambiguity.

### 2. Mega Menu Submenu Items Have Visible Text
Inside the mega menu dropdowns, submenu items have visible text labels: AI Automation, Web App Development, Mobile App Development, Salesforce Development, Product Strategy & Design, Managed Services & Support, View Services. Decorative icons are hidden from assistive technology. Voice control users can target each submenu item by name.

### 3. Contact Form Fields Have Visible Labels Matching Accessible Names
Every contact form field (First Name, Last Name, Company Email, Company, How Can We Help You?) has a visible label positioned above the input that matches the `aria-labelledby` accessible name. The Submit button has clear visible text. This is critical for voice control — "Click First Name," "Click Company Email," and "Click Submit" all work correctly.

### 4. "Connect with an Expert" CTA Has Unique, Descriptive Text
The primary CTA button on the homepage reads "Connect with an Expert" — unique, descriptive, and easy to speak. A voice control user can say the full phrase and Dragon targets it immediately.

### 5. Tab Interface Has Unique, Descriptive Labels
The tabbed section labels (Operational Efficiency, Modern Technology, Customer Engagement, Scalable Solutions, Expansive Resources, Speed to Market) are all unique visible text. Saying "Click Customer Engagement" or "Click Speed to Market" activates the correct tab.

### 6. Footer Social Links Have Visible Text
Social media links in the footer include visible text labels — Facebook, Instagram, LinkedIn — alongside their icons. The icons have `alt=""` (correctly hidden), and the text provides the speakable label.

### 7. Email and Phone Links on Contact Page
The email link ("contact@launchpadlab.com") and phone link ("(312) 888-9651") on the contact page are unique, visible, and voice-targetable.

### 8. Blog/Resource Card Links Have Descriptive Accessible Names
The "You Might Also be Interested In" section uses `aria-label` attributes on card links that include the full article title (e.g., `aria-label="View The Business Value of Building Applications and Portals Blog Post"`). This pattern should be replicated on the service "Learn More" links.

---

## Summary of Issues by Severity

| Severity | Count | Issues |
|----------|-------|--------|
| Critical | 2 | Hamburger menu unlabeled `<div>` (#1), Seven identical "Learn More" links (#2) |
| Major | 5 | Hover-triggered mega menu (#3), Icon-only mega close button (#4), Duplicate service card links (#5), Testimonials carousel no controls (#6), Toggle button no visible text (#7) |
| Minor | 5 | Auto-scrolling logo carousel (#8), Ambiguous case study button text (#9), Vague "Connect" link (#10), reCAPTCHA challenge barrier (#11), Broken skip link (#12) |

---

## Priority Recommendations

### 1. Immediate (Critical)

**Fix the hamburger menu.** Replace `<div id="burgerBtn">` with a `<button>` element that has visible text (e.g., "Menu") and an appropriate `aria-expanded` state. This single change unlocks the entire site for voice control users on mobile and tablet viewports.

**Make "Learn More" links unique.** Add the service name to each link's visible text or use visually hidden text to distinguish them. Change "Learn More" to "Learn More about AI Automation," "Learn More about Web App Development," etc. Ensure any `aria-label` used contains the visible text per WCAG 2.5.3.

### 2. High (Major)

**Switch mega menu trigger from hover to click.** Ensure dropdown menus open reliably on click/activation, not just hover. Test with voice control software.

**Add visible text to the mega menu close button.** Replace the icon-only X button with a button that has visible "Close" text (even if small) alongside the icon.

**Remove duplicate links on service cards.** Each card should have one link, not two overlapping links to the same destination.

**Add controls to the testimonials carousel.** Enable "Previous" and "Next" buttons with visible text labels.

### 3. Medium (Minor)

**Add a pause button to the logo carousel** or stop auto-scrolling animation.

**Improve case study CTA text** — add action verbs like "View Case Study."

**Change the "Connect" link on the contact page** to "Connect on LinkedIn."

**Consider reCAPTCHA v3** to eliminate image challenges.

**Fix the broken skip link** by adding `id="primary"` to the main content area.

---

## Key Principle for Voice Control Accessibility

> **Every interactive element must have visible text that a user can read and speak to activate it.**

Voice control users navigate by looking at the screen and speaking what they see. If an element has no visible text (icon-only buttons), they cannot target it. If multiple elements share the same visible text ("Learn More" ×7), they cannot distinguish them. If the accessible name doesn't match the visible text, their spoken command may fail. Designing for voice control means ensuring that every clickable, tappable, or activatable element has a **unique, visible, speakable label**.
