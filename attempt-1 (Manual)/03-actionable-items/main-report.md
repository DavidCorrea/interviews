# Accessibility Action Items

Consolidated from 17 user experience reports covering: screen reader, low vision, screen magnifier, color blindness (red-green & blue-yellow), motor impairment, cognitive disability, dyslexia, ADHD, motion sensitivity, low contrast sensitivity, situational contrast (bright sunlight), voice control, non-native English speaker, senior user, stressed user, and skeptical user.

---

## Critical Priority

These issues severely impact usability and block or exclude entire user groups. They should be addressed first.

### 1. Low Contrast Body Text

**Ticket:** [story-01-low-contrast-body-text.md](story-01-low-contrast-body-text.md)

**Reports:** Low Vision User, Senior, Low Vision Magnifier, Situational Contrast, Cognitive Disability, Stressed User, Low Contrast Sensitivity, Dyslexic User

**Issue:** The majority of body text across the site uses light gray colors (estimated #666 or #777) on white backgrounds. This makes 60-70% of content nearly unreadable for users with low vision, low contrast sensitivity, or those browsing in bright environments. Service descriptions, testimonials, process details, and introductory paragraphs all suffer from this problem.

**Estimated Complexity:** Low -- Likely a global CSS change to body text color variables or utility classes. If the site uses a design system or CSS variables, this could be a single-line change that cascades everywhere. If colors are scattered across component-level styles, it may require a find-and-replace audit but the changes themselves are trivial.

**Possible Solution:**
- Change all body text to #333333 or darker (ideally #000000 for maximum readability)
- Ensure a minimum contrast ratio of 4.5:1 for normal text and 3:1 for large text (WCAG AA), aiming for 7:1 (WCAG AAA) where possible
- Increase font weight from 300-400 to at least 500 for body text
- Never use gray lighter than #555 for any readable text

---

### 2. Layouts Do Not Reflow at High Zoom Levels

**Ticket:** [story-02-layout-reflow-high-zoom.md](story-02-layout-reflow-high-zoom.md)

**Reports:** Low Vision Magnifier, Stressed User

**Issue:** At 200-300% browser zoom, multi-column grid layouts (services, problems, logos, case studies, statistics) do not collapse into a single column. This forces users to scroll both horizontally and vertically, creating a two-dimensional navigation puzzle. Users reported 50-60 horizontal pans and 100+ vertical scrolls just to view the homepage. This is a WCAG 1.4.10 (Reflow) failure.

**Estimated Complexity:** Medium-High -- Requires reviewing grid/flexbox layouts across multiple page sections and components (services, problems, logos, case studies, statistics, awards). Each section likely has its own layout rules. If the site already has mobile breakpoints, it may be a matter of adjusting breakpoint thresholds. If layouts use fixed widths or non-standard grids, refactoring could be more involved. Thorough cross-browser and multi-zoom-level QA is essential.

**Possible Solution:**
- Implement responsive CSS that collapses all multi-column grids to single-column at viewport widths equivalent to 200%+ zoom (effectively 320px-640px equivalent)
- Test at 200%, 300%, and 400% browser zoom to ensure no horizontal scrolling is required
- Adopt a mobile-first CSS approach so narrow layouts are the default, enhanced for wider screens
- Eliminate any fixed-width containers that prevent content reflow

---

### 3. Excessive Animations Without prefers-reduced-motion Support

**Ticket:** [story-03-prefers-reduced-motion.md](story-03-prefers-reduced-motion.md)

**Reports:** Motion Sensitivity

**Issue:** The site has scroll-triggered fade-in/slide-in animations on nearly every section, hover lift/scale effects on cards and buttons, possible counting animations on statistics, and potential auto-rotating carousels. A user with a vestibular disorder had to close the page within seconds due to vertigo, nausea, and headaches. The site was rated 2/10 for motion sensitivity and deemed "completely unusable" with JavaScript enabled.

**Estimated Complexity:** Medium -- The `prefers-reduced-motion` CSS media query itself is simple to add. However, the work involves auditing every animation source: CSS transitions, CSS keyframe animations, JavaScript-driven scroll-triggered effects (likely from a library like AOS, GSAP, or Framer Motion), hover transforms, and potential carousel plugins. Each source needs to be wrapped or disabled conditionally. If animations are centralized through a single library, a global disable flag may suffice. If scattered across components, each must be addressed individually.

**Possible Solution:**
- Implement the `prefers-reduced-motion: reduce` CSS media query to disable all animations for users who have requested reduced motion in their OS settings
- Add a visible "Reduce Motion" toggle in the site header that persists across pages
- Remove auto-playing carousels or make them paused by default with manual controls
- Eliminate scroll-triggered animations entirely or make them opt-in
- Replace animated hover effects with instant state changes (color swap, underline) with no transitions
- Remove number counting animations; display final values immediately
- Reserve space for lazy-loaded images to prevent layout shifts

---

### 4. Duplicate and Non-Descriptive Link Labels

**Ticket:** [story-04-descriptive-link-labels.md](story-04-descriptive-link-labels.md)

**Reports:** Screen Reader, Voice Control, ADHD

**Issue:** There are 6-7 "Learn More" links on the homepage that are all identically labeled. Screen reader users cannot distinguish them in a links list. Voice control users saying "Click Learn More" are presented with a numbered overlay of 7 options with no way to tell which is which. The LinkedIn "Connect" link is also ambiguous alongside the "Connect with an Expert" CTA.

**Estimated Complexity:** Low -- This involves changing link text or adding `aria-label` attributes to a finite number of elements (roughly 7-10 links on the homepage, plus a few on subpages). If links are rendered from a CMS or data array, a single template change could fix all instances at once. Straightforward HTML/template edits with no risk of side effects.

**Possible Solution:**
- Make each link unique and descriptive: "Learn More about AI Automation," "Learn More about Web Development," etc.
- At minimum, add `aria-label` attributes: `<a aria-label="Learn more about AI Automation">Learn More</a>`
- Change the LinkedIn link from "Connect" to "Connect with LaunchPad Lab on LinkedIn"
- Audit all links on the site and ensure no two links on the same page share identical text unless they go to the same destination
- Avoid generic CTAs like "Click Here" or "Read More" without context

---

### 5. Broken Heading Hierarchy

**Ticket:** [story-05-heading-hierarchy.md](story-05-heading-hierarchy.md)

**Reports:** Screen Reader

**Issue:** Almost every section has duplicate H2 headings (a section label and a subtitle both marked as H2). Statistics like "12+ Years in Business" are incorrectly marked as H2 headings. The heading hierarchy jumps inconsistently (H1 to H2 to H3 without clear parent-child relationships). This makes heading-based navigation confusing and inefficient for screen reader users.

**Estimated Complexity:** Low -- Changing HTML heading tags (e.g., `<h2>` to `<h3>` or `<p>`) across page templates. The number of headings to fix is moderate (estimated 15-25 across the homepage and key subpages). The main risk is that heading styles may be tied to tag names rather than CSS classes, so some styling adjustments may be needed. No logic or behavior changes involved.

**Possible Solution:**
- Use exactly one H1 per page (the main page title)
- Each major section should have a single H2; subtitles should be H3 or regular paragraph text
- Remove heading tags from statistics; use a definition list (`<dl>`) or regular `<div>` elements instead
- Ensure heading hierarchy never skips levels (H2 > H3 > H4, not H2 > H4)
- Audit the heading outline using browser dev tools or accessibility checkers

---

### 6. Contact Form Not Keyboard Accessible or Missing

**Ticket:** [story-06-contact-form-keyboard-access.md](story-06-contact-form-keyboard-access.md)

**Reports:** Screen Reader

**Issue:** The contact page says "Complete the form below to tell us about your project," but a screen reader user could not locate any form fields when navigating with Tab or the F key. The form either does not exist, is loaded dynamically without focus management, or is entirely inaccessible to keyboard users. This is a critical WCAG 2.1.1 (Keyboard) failure.

**Estimated Complexity:** Medium -- Depends heavily on the root cause. If the form is embedded via a third-party service (e.g., HubSpot, Marketo) loaded in an iframe or injected via JS, fixing keyboard accessibility may require changes to the embed method or third-party configuration. If the form is custom-built but hidden behind a JS render condition, the fix could be straightforward. Investigation is needed first to diagnose why the form is invisible to keyboard/screen reader navigation.

**Possible Solution:**
- Ensure the contact form renders in the DOM on page load (not behind a client-side render that blocks access)
- Make all form fields focusable and reachable via Tab key
- Associate every `<input>` with a `<label>` using matching `for`/`id` attributes
- Mark required fields with `aria-required="true"` and visible text, not just color
- Provide clear, specific error messages associated with their fields via `aria-describedby`
- Ensure the submit button is clearly labeled (e.g., "Submit Contact Form")

---

### 7. Overly Complex Language and Jargon

**Ticket:** [story-07-plain-language.md](story-07-plain-language.md)

**Reports:** Senior, Cognitive Disability, Non-Native English Speaker, Stressed User, ADHD, Dyslexic User

**Issue:** The site uses extensive business jargon ("agentic," "bespoke," "cross-functional"), undefined acronyms (ROI, UAT, UI/UX, CSAT), metaphorical language ("harness the power," "unlock growth"), and long, complex sentences (20+ words with multiple clauses). Six different user groups reported confusion, frustration, or inability to understand the site's core message.

**Estimated Complexity:** High -- This is primarily a content/copywriting effort, not a code change. Every page's copy needs to be rewritten for clarity: homepage, services pages, process section, case studies, FAQs, and CTAs. Requires collaboration between a copywriter (or content strategist) and stakeholders who understand the brand voice. The technical implementation (updating CMS content or template strings) is trivial, but the content creation and approval process is time-intensive.

**Possible Solution:**
- Simplify the main headline to something immediately clear: "We Build Custom Software and AI Tools for Businesses"
- Replace jargon with plain English: "bespoke" -> "custom-made," "deploy" -> "launch," "leverage" -> "use"
- Spell out all acronyms on first use: "ROI (Return on Investment)"
- Limit sentences to 15-20 words maximum
- Use bullet points instead of dense paragraphs for service descriptions
- Consider adding a glossary or tooltip definitions for technical terms
- Add TLDR/summary boxes at the top of each page or section
- Test content readability with tools targeting a Grade 8 reading level or below

---

### 8. Small Click/Touch Targets and Tight Spacing

**Ticket:** [story-08-click-target-sizes.md](story-08-click-target-sizes.md)

**Reports:** Motor Impairment, Stressed User, Low Vision Magnifier

**Issue:** Navigation menu links are packed too close together. "Learn More" links and arrow icons are too small to click accurately. "Problems We Solve" tabs have very tight spacing. Dropdown menu options in the contact form are narrow. Users with hand tremors reported multiple misclicks and exhaustion from trying to hit small targets. This is a WCAG 2.5.8 (Target Size) failure.

**Estimated Complexity:** Medium -- Requires CSS changes to padding, min-height, and gap properties across navigation, service cards, problem tabs, and form elements. Making entire cards clickable may involve wrapping cards in `<a>` tags or adding click handlers, which could affect existing layout/styles. Each component needs individual attention. Low risk of breaking functionality, but visual regression testing is needed to ensure layouts still look right with larger targets.

**Possible Solution:**
- Ensure all interactive elements meet a minimum size of 44x44px (WCAG recommendation)
- Add at least 8px of padding/spacing between adjacent clickable elements
- Make entire service/problem cards clickable, not just the small "Learn More" text link
- Replace dropdown menus in forms with radio buttons or larger checkbox-style options
- Remove or increase the size of small arrow icons
- Add generous padding to navigation links

---

## High Priority

These issues significantly degrade the experience for multiple user groups and should be addressed after critical items.

### 9. Contact Information Hard to Find

**Ticket:** [story-09-prominent-contact-info.md](story-09-prominent-contact-info.md)

**Reports:** Nearly all testers (Senior, ADHD, Cognitive Disability, Stressed User, Motor Impairment, Low Vision Magnifier, Low Vision User, Screen Reader)

**Issue:** The phone number and email are only available at the bottom of the contact page, below testimonials and a form prompt. Users had to scroll through the entire homepage, click "Connect with an Expert," then scroll through the entire contact page to find basic contact details. Multiple users considered giving up before finding this information.

**Estimated Complexity:** Low -- Adding text content (phone number and email) to the header and footer templates. These are typically shared layout components, so a single edit propagates site-wide. Reordering the contact page content is also straightforward. Minor CSS may be needed to style the header contact info without breaking the existing layout.

**Possible Solution:**
- Add the phone number and email to the site header, visible on every page
- Include contact information in the site footer as well
- On the contact page, place the phone number and email above the form, not below it
- Consider adding a "Skip to Contact Information" link at the top of the page

---

### 10. Information Overload and Too Many Choices

**Ticket:** [story-10-reduce-information-overload.md](story-10-reduce-information-overload.md)

**Reports:** Senior, ADHD, Cognitive Disability, Stressed User

**Issue:** The homepage presents 6 service boxes, 6 problem boxes, 3 case studies, 7+ award badges, a process section, statistics, related content, and multiple CTAs. Users reported decision paralysis, cognitive exhaustion, and inability to process so much information. Several testers forgot earlier content by the time they reached the bottom.

**Estimated Complexity:** High -- This is a major content strategy and UX redesign effort. It requires stakeholder alignment on which content to keep, remove, or relocate. New subpages may need to be created. The homepage layout and section order need to be rethought. Progressive disclosure (accordions/toggles) requires both design and JS implementation. This is less of a code task and more of a design/strategy project.

**Possible Solution:**
- Reduce service categories on the homepage to 2-3 main groups with an option to explore more
- Use progressive disclosure: show summaries with "expand" toggles for details
- Shorten the homepage significantly; move detailed content to dedicated subpages
- Add a progress indicator (e.g., "Section 3 of 5") for long pages
- Limit CTAs to one primary action per viewport
- Add a clear visual hierarchy so users know what to focus on first

---

### 11. Missing ARIA Landmarks

**Ticket:** [story-11-aria-landmarks.md](story-11-aria-landmarks.md)

**Reports:** Screen Reader

**Issue:** The site does not appear to use proper ARIA landmark regions. Screen reader users cannot jump between navigation, main content, and footer using landmark navigation (D key in NVDA). This forces sequential reading of the entire page.

**Estimated Complexity:** Low -- Replacing generic `<div>` wrappers with semantic HTML5 elements (`<header>`, `<nav>`, `<main>`, `<footer>`) in the main layout template. If the site already uses these elements, it may just need `aria-label` additions. If it uses `<div>` for everything, the refactor is still quick but requires checking that CSS selectors still match after tag changes.

**Possible Solution:**
- Use semantic HTML5 elements: `<header>`, `<nav>`, `<main>`, `<aside>`, `<footer>`
- Ensure there is exactly one `<main>` element per page
- Label multiple `<nav>` elements with `aria-label` (e.g., "Primary Navigation," "Footer Navigation")
- Test landmark regions with NVDA/JAWS to confirm they are announced correctly

---

### 12. Italic Text in Testimonials

**Ticket:** [story-12-remove-italic-testimonials.md](story-12-remove-italic-testimonials.md)

**Reports:** Dyslexic User

**Issue:** Testimonial quotes are displayed in italic text, which is extremely difficult for dyslexic users to read. Italic letters appear "swirly" and blend together, causing the user to skip entire testimonials.

**Estimated Complexity:** Low -- A CSS change removing `font-style: italic` from the testimonial component and replacing it with an alternative visual treatment (left border, quotation marks, background color). Likely a single CSS rule targeting the testimonial/blockquote class.

**Possible Solution:**
- Replace italic text with regular (roman) weight text
- Use quotation marks, indentation, or a left border to distinguish quotes visually
- If emphasis is needed, use bold or a slightly larger font size instead of italics
- Apply this principle site-wide: avoid italics for any substantial blocks of text

---

### 13. Font Size Too Small and Thin Font Weight

**Ticket:** [story-13-font-size-weight.md](story-13-font-size-weight.md)

**Reports:** Low Vision User, Senior, Low Contrast Sensitivity, Situational Contrast

**Issue:** Body text appears to be 14px or smaller with a font weight of 300-400. Multiple users had to lean forward, squint, or zoom their browser significantly just to read basic content.

**Estimated Complexity:** Low -- Global CSS typography change. If the site uses CSS custom properties or a base stylesheet for typography, updating `font-size` and `font-weight` on the body or root element will cascade site-wide. Minor layout shifts may occur from the size increase (text wrapping differently), requiring a visual QA pass.

**Possible Solution:**
- Set the base font size to at least 16px (ideally 18px) for all body text
- Use a font weight of 400-500 minimum for body copy
- Ensure headings are proportionally larger and bolder
- Avoid using light/thin font weights (100-300) for any text smaller than 24px

---

### 14. Hover-Dependent Interactions

**Ticket:** [story-14-hover-dependent-interactions.md](story-14-hover-dependent-interactions.md)

**Reports:** Voice Control, Motor Impairment

**Issue:** Navigation menus may require hovering to reveal submenus. Hover effects on cards cause confusion for tremor users (constant on/off triggering). Voice control users cannot trigger hover states at all.

**Estimated Complexity:** Medium -- Changing navigation from hover-to-open to click-to-open requires JS logic changes and potentially different CSS states. Simplifying card hover animations is a CSS change. The navigation rework is the main effort, especially if submenus are involved and both desktop and mobile behaviors must be handled.

**Possible Solution:**
- Make all dropdown/navigation menus open on click, not hover
- Remove or simplify hover animations on cards and buttons
- Ensure all content is accessible without hovering
- Provide keyboard and click alternatives for any hover-revealed content

---

### 15. Visited Link States Indistinguishable for Color Blind Users

**Ticket:** [story-15-visited-link-states.md](story-15-visited-link-states.md)

**Reports:** Blue-Yellow Color Blind

**Issue:** Standard blue-to-purple visited link color change is invisible to users with tritanopia. They cannot tell which "Learn More" links or blog posts they have already clicked.

**Estimated Complexity:** Low -- A CSS `:visited` pseudo-class style change. Adding an underline style or opacity change for visited links is a one-line CSS addition. Adding a checkmark icon requires slightly more work (CSS `::after` pseudo-element or a small JS/CSS approach), but is still straightforward.

**Possible Solution:**
- Add non-color indicators for visited links: a checkmark icon, strikethrough, reduced opacity, or "(visited)" text
- Alternatively, use a dramatic color shift (e.g., blue to gray) instead of blue to purple
- Ensure visited state is indicated by more than just color (underline style change, font weight change)

---

### 16. Color Used as the Only Information Carrier

**Ticket:** [story-16-color-not-only-indicator.md](story-16-color-not-only-indicator.md)

**Reports:** Red-Green Color Blind, Blue-Yellow Color Blind

**Issue:** Status indicators in case studies (increase/decrease arrows) may rely solely on green vs. red to convey meaning. Form validation likely uses red for errors and green for success without additional cues. Chart data in screenshots may be indistinguishable.

**Estimated Complexity:** Medium -- Requires an audit of all places where color conveys meaning (status icons, form validation, chart colors in case study images). Adding icons and text labels to form validation messages is a moderate code change. Updating case study screenshot images may require new assets from a designer. The scope depends on how many color-dependent elements exist across the site.

**Possible Solution:**
- Always pair color with a secondary indicator: icons (checkmark for success, X for error), text labels ("Error:", "Success:"), or patterns
- Use color-blind-friendly palettes: blue + orange, blue + yellow; avoid red vs. green
- For form validation: prefix errors with an icon and "Error:" text; prefix success with a checkmark and "Success:" text
- Add patterns or direct labels to any charts or data visualizations
- Test the site in grayscale to verify all information is still conveyed

---

### 17. Missing Physical Address and Trust Signals

**Ticket:** [story-17-trust-signals-address.md](story-17-trust-signals-address.md)

**Reports:** Skeptical User

**Issue:** No physical address is displayed on the site. There are no BBB accreditation badges, verifiable third-party review links, privacy policy, or terms of service readily visible. Case studies cannot be independently verified. This erodes trust for cautious users.

**Estimated Complexity:** Low -- Mostly content additions to the footer template and contact page. Adding address text, links to review sites, and privacy policy/terms links are simple HTML additions. Writing the actual privacy policy and terms of service documents (if they don't exist) would be a separate legal/content effort.

**Possible Solution:**
- Add the physical address (2045 W Grand Ave Ste B, Chicago IL 60612) to the footer and contact page
- Link to third-party review sites (Clutch, G2, Google Reviews) for independent verification
- Add a visible privacy policy and terms of service link in the footer
- Display verifiable partnership badges (e.g., official Salesforce Partner)
- Consider adding video testimonials from real clients for stronger social proof

---

### 18. No Pricing Transparency

**Ticket:** [story-18-pricing-transparency.md](story-18-pricing-transparency.md)

**Reports:** Skeptical User

**Issue:** No pricing information or even ballpark ranges are provided anywhere. Everything requires "contact us." This feels like a pressure tactic and creates suspicion among cautious users.

**Estimated Complexity:** Medium -- The technical implementation is trivial (adding text to a page), but the real complexity is a business decision. Stakeholders need to agree on what pricing information to share publicly, which may require internal discussions about positioning, competitive concerns, and sales strategy. An FAQ about pricing is a good compromise that is easy to implement once the content is approved.

**Possible Solution:**
- Add at least general pricing guidance: "Projects typically start at $X" or offer pricing tiers
- If exact pricing is not possible, add an FAQ explaining how pricing works and what factors affect cost
- Provide a free, no-obligation consultation offer to lower the barrier to contact

---

## Medium Priority

These issues cause friction and discomfort but have workarounds or affect fewer users. They should be addressed as part of ongoing improvement.

### 19. Insufficient Line Spacing

**Ticket:** [story-19-line-spacing.md](story-19-line-spacing.md)

**Reports:** Dyslexic User

**Issue:** Lines of text are too close together, causing dyslexic users to jump to the wrong line while reading and lose their place.

**Estimated Complexity:** Low -- A single CSS property change (`line-height`) on the body or base text styles. May cause minor layout shifts as text takes up more vertical space, requiring a visual check but no logic changes.

**Possible Solution:**
- Set line-height to 1.5-2.0 for all body text (WCAG recommends at least 1.5)
- Ensure paragraph spacing is at least 1.5x the font size
- Use left-aligned text only; never justify body text (uneven spacing worsens readability)

---

### 20. Excessive Homepage Length / Too Much Scrolling

**Ticket:** [story-20-shorten-homepage.md](story-20-shorten-homepage.md)

**Reports:** Senior, ADHD, Cognitive Disability, Low Vision Magnifier, Stressed User

**Issue:** The homepage is extremely long with 10+ sections. Users got lost, forgot earlier content, and felt exhausted by the time they reached the bottom. High-zoom users had to scroll 100+ times.

**Estimated Complexity:** High -- Same scope as item #10. Requires content strategy decisions about what to cut, move, or restructure. New page templates may be needed for relocated content. Impacts SEO, analytics, and potentially marketing funnels. Needs design and stakeholder collaboration. Overlaps significantly with item #10 and can be addressed together.

**Possible Solution:**
- Reduce the homepage to 4-5 focused sections
- Move detailed content (full process breakdown, all case studies, awards) to dedicated subpages
- Use collapsible/accordion sections for supplementary information
- Add anchor navigation or a table of contents for remaining long pages

---

### 21. Missing Skip Links for Key Content

**Ticket:** [story-21-skip-links.md](story-21-skip-links.md)

**Reports:** Low Vision Magnifier, ADHD, Screen Reader (noted existing skip-to-content link)

**Issue:** While a "Skip to content" link exists, there are no skip links to important sections like "Contact Information" or "Services." Magnifier and ADHD users must scroll through enormous amounts of content to find what they need.

**Estimated Complexity:** Low -- Adding a small block of hidden anchor links at the top of the page, styled to appear on keyboard focus. Requires adding `id` attributes to target sections and a few lines of HTML/CSS. A well-established, low-risk pattern.

**Possible Solution:**
- Add skip links for: "Skip to Services," "Skip to Contact Information," "Skip to Main Content"
- Make skip links visible on focus (hidden until Tab key is pressed)
- Consider adding a persistent section navigation for long pages

---

### 22. Sticky Header Occupying Viewport at High Zoom

**Ticket:** [story-22-sticky-header-zoom.md](story-22-sticky-header-zoom.md)

**Reports:** Low Vision Magnifier

**Issue:** If the navigation header is sticky/fixed, it may consume 30-40% of the visible area at 300% zoom, leaving little space for actual content.

**Estimated Complexity:** Low-Medium -- If the header is purely CSS `position: sticky/fixed`, adding a media query to remove it at narrow viewport widths is simple. If an auto-hide-on-scroll behavior is desired, it requires a small JS scroll listener (or an existing library). The simpler approach (just unstick at narrow widths) is a one-line CSS media query.

**Possible Solution:**
- Make the sticky header auto-hide on scroll down and reappear on scroll up
- At high zoom levels (detected via CSS media queries on viewport width), switch to a non-sticky header
- Reduce header height or make it collapsible

---

### 23. Poor Alt Text on Images

**Ticket:** [story-23-image-alt-text.md](story-23-image-alt-text.md)

**Reports:** Screen Reader

**Issue:** Award badge images may only have filename-based alt text. Case study screenshots have generic descriptions like "Prosci Interface Screenshot" rather than meaningful descriptions of what is shown.

**Estimated Complexity:** Low -- A content-only task. Requires writing new alt text strings and updating `alt` attributes in HTML templates or CMS image fields. No logic or styling changes. The effort is proportional to the number of images (estimated 20-30 across the site), and each is a quick edit.

**Possible Solution:**
- Write descriptive alt text for award badges: "2025 Clutch Top Salesforce Company award for the United States"
- Provide meaningful descriptions for case study screenshots: "Screenshot showing Prosci's 360-degree customer view dashboard in Salesforce"
- Mark purely decorative images with `alt=""` or `aria-hidden="true"` so screen readers skip them
- Ensure all company logos in the client section have alt text with the company name

---

### 24. Icon-Only Interactive Elements Lack Text Labels

**Ticket:** [story-24-icon-text-labels.md](story-24-icon-text-labels.md)

**Reports:** Voice Control, Low Vision User

**Issue:** Arrow icons next to "Learn More" links, social media icons, and the hamburger menu icon may lack text labels. Voice control users cannot reference them ("Click arrow" is ambiguous), and screen reader users may hear nothing useful.

**Estimated Complexity:** Low -- Adding `aria-label` attributes to a small number of icon-only elements (hamburger menu, social media icons, arrow icons). Estimated 5-10 elements across the site. Each is a one-attribute HTML addition. Adding visible text labels is slightly more work as it may affect layout/styling.

**Possible Solution:**
- Add `aria-label` to all icon-only buttons and links
- For the hamburger menu: add visible "Menu" text or at minimum `aria-label="Open navigation menu"`
- For social media icons: use `aria-label="Follow us on LinkedIn"` etc.
- Where possible, add visible text alongside icons

---

### 25. Dropdown Menus Difficult for Motor Impairment Users

**Ticket:** [story-25-replace-dropdowns.md](story-25-replace-dropdowns.md)

**Reports:** Motor Impairment

**Issue:** The contact form uses dropdown menus with narrow, tightly-stacked options. Users with hand tremors accidentally select wrong options and struggle with precision.

**Estimated Complexity:** Medium -- Replacing a dropdown `<select>` with radio buttons or card-style options requires both HTML restructuring and new CSS for the replacement UI. Form submission logic may also need updating if field names or value formats change. If the form is managed by a third-party tool (HubSpot, etc.), the customization options may be limited.

**Possible Solution:**
- Replace dropdowns with radio buttons or large, clickable card-style options
- If dropdowns must be used, increase the height of each option and add spacing between them
- Consider using a searchable/filterable dropdown for long lists

---

### 26. Auto-Playing Carousels or Sliders

**Ticket:** [story-26-auto-playing-carousels.md](story-26-auto-playing-carousels.md)

**Reports:** Motion Sensitivity, Voice Control

**Issue:** Company logos and/or award badges may be in auto-rotating carousels that create constant motion and make it difficult for voice control users to target elements.

**Estimated Complexity:** Low-Medium -- If carousels use a library (Swiper, Slick, Embla, etc.), disabling autoplay is typically a single configuration option. Adding pause/play controls requires a small JS and HTML addition. Replacing a carousel with a static grid is a more involved layout change but removes future maintenance burden. Overlaps with item #3 (motion reduction).

**Possible Solution:**
- Remove auto-play from all carousels; let users advance manually
- Add visible pause/play controls
- Respect `prefers-reduced-motion` to disable carousel movement
- Consider replacing carousels with static grid layouts

---

### 27. Faint Company Logos on White Background

**Ticket:** [story-27-logo-contrast.md](story-27-logo-contrast.md)

**Reports:** Situational Contrast, Low Contrast Sensitivity

**Issue:** Several client logos (Prosci, Whirlpool, and others) use light colors that wash out on white backgrounds, especially in bright environments.

**Estimated Complexity:** Low -- A CSS background-color change on the logo section container, or adding a border/shadow to logo items. If higher-contrast logo versions are needed, that requires requesting new assets from a designer, but the CSS-only approach is immediate and effective.

**Possible Solution:**
- Place logos on a very light gray background (#F5F5F5) instead of pure white
- Add subtle borders or shadows around logo containers
- Ensure all logos use dark or high-contrast versions
- Add text labels next to or below logos with client names

---

### 28. Text Overlaid on Images Reduces Readability

**Ticket:** [story-28-text-over-images.md](story-28-text-over-images.md)

**Reports:** Low Vision Magnifier, Senior, Situational Contrast

**Issue:** In some sections, text is placed over photographs or background images. When the background washes out (bright environments, high zoom), the text becomes unreadable.

**Estimated Complexity:** Medium -- Requires identifying all sections where text overlays images and restructuring the layout so text sits on solid backgrounds instead. This may involve significant design changes to hero sections or card layouts. If the overlay approach is deeply embedded in the design system, a designer should propose alternative treatments. CSS overlay darkness can be increased as a quick interim fix.

**Possible Solution:**
- Keep all important text on solid-color backgrounds
- If text must overlay images, use a solid dark overlay with very high contrast (not semi-transparent)
- Ensure overlaid text meets WCAG contrast requirements against the worst-case area of the image

---

### 29. Downloads Feel Unsafe to Cautious Users

**Ticket:** [story-29-download-reassurance.md](story-29-download-reassurance.md)

**Reports:** Stressed User, Skeptical User

**Issue:** "Download Our Guide" links trigger fear of viruses and scams among less tech-savvy or cautious users. There is no reassurance about the safety or nature of the download.

**Estimated Complexity:** Low -- Content text additions next to existing download links. No structural or logic changes needed. Just updating link text and adding a short reassurance sentence nearby.

**Possible Solution:**
- Add context to download links: "Download Our Free PDF Guide (2.3 MB, PDF format)"
- Include reassurance text: "Safe download - no signup required"
- Consider offering content as web pages instead of downloads when possible

---

### 30. No Video Explanation of Services

**Ticket:** [story-30-video-explainer.md](story-30-video-explainer.md)

**Reports:** Senior, Stressed User, Cognitive Disability

**Issue:** Users who struggle with dense text requested a short video explaining what the company does in plain language. Auditory and visual learners would benefit from a video alternative.

**Estimated Complexity:** High -- This is primarily a production effort, not a code task. Requires scriptwriting, filming (or animation), editing, captioning, and transcript creation. Embedding the video on the site is trivial (a `<video>` tag or YouTube/Vimeo embed), but creating the video content itself is a significant project involving people outside the dev team.

**Possible Solution:**
- Create a 1-2 minute explainer video with a team member speaking directly to the camera
- Include closed captions and a text transcript for accessibility
- Place the video prominently near the top of the homepage
- Keep the language simple and jargon-free

---

### 31. No Accessibility Statement or Reduced-Motion Toggle

**Ticket:** [story-31-accessibility-statement.md](story-31-accessibility-statement.md)

**Reports:** Motion Sensitivity, Screen Reader

**Issue:** There is no accessibility statement communicating the site's commitment to accessibility, and no user-facing controls to reduce motion or adjust the experience.

**Estimated Complexity:** Low-Medium -- The accessibility statement is a new static page (content writing + a simple template). The "Reduce Motion" toggle requires a small JS component that toggles a CSS class on the body and persists the preference in `localStorage`. A full accessibility toolbar with multiple controls is more complex but is an optional enhancement beyond the basics.

**Possible Solution:**
- Add an accessibility statement page linked from the footer
- Include a "Reduce Motion" toggle in the header that disables all animations and saves the preference
- Provide contact information for reporting accessibility issues
- Consider an accessibility toolbar with font size, contrast, and motion controls

---

### 32. Form Fills Are Stressful and Inaccessible

**Ticket:** [story-32-form-experience.md](story-32-form-experience.md)

**Reports:** Cognitive Disability, Stressed User, Motor Impairment, Senior

**Issue:** The contact form creates anxiety for multiple user groups. Users with cognitive disabilities are unsure what information to provide. Users with tremors struggle to type accurately. Seniors worry about data privacy. No alternative is clearly presented alongside the form.

**Estimated Complexity:** Medium -- Involves content changes (reassurance text, reordering), HTML modifications (moving contact info above form, adding placeholders), and potentially form logic changes (reducing required fields, adding autocomplete attributes). If the form is a third-party embed, customization may be constrained by the vendor's options. The content and UX decisions (what to say, how to phrase reassurance) require more thought than the code changes.

**Possible Solution:**
- Clearly present phone and email as equal alternatives above the form: "Call us, email us, or fill out this form"
- Add reassurance: "We will never share your information" and "All fields are optional except email"
- Minimize required fields (email only, with optional details)
- Add clear placeholder text and example input in form fields
- Support browser autofill by using proper field types and autocomplete attributes

---

## Summary Table

| # | Action Item | Ticket | Priority | Complexity | WCAG Criteria | Affected User Groups |
|---|------------|--------|----------|------------|---------------|---------------------|
| 1 | Increase body text contrast | [Story 01](story-01-low-contrast-body-text.md) | Critical | Low | 1.4.3, 1.4.6 | Low vision, senior, cognitive, situational, dyslexic, low contrast sensitivity |
| 2 | Fix layout reflow at high zoom | [Story 02](story-02-layout-reflow-high-zoom.md) | Critical | Medium-High | 1.4.10 | Low vision magnifier, stressed user |
| 3 | Implement prefers-reduced-motion | [Story 03](story-03-prefers-reduced-motion.md) | Critical | Medium | 2.3.3 | Motion sensitivity, vestibular disorders |
| 4 | Make link labels unique and descriptive | [Story 04](story-04-descriptive-link-labels.md) | Critical | Low | 2.4.4, 2.4.9 | Screen reader, voice control, ADHD |
| 5 | Fix heading hierarchy | [Story 05](story-05-heading-hierarchy.md) | Critical | Low | 1.3.1 | Screen reader |
| 6 | Make contact form keyboard accessible | [Story 06](story-06-contact-form-keyboard-access.md) | Critical | Medium | 2.1.1 | Screen reader, keyboard users |
| 7 | Simplify language and define jargon | [Story 07](story-07-plain-language.md) | Critical | High | 3.1.3, 3.1.5 | Senior, cognitive, non-native, stressed, ADHD, dyslexic |
| 8 | Increase touch/click target sizes | [Story 08](story-08-click-target-sizes.md) | Critical | Medium | 2.5.8 | Motor impairment, stressed user, low vision |
| 9 | Make contact info prominent | [Story 09](story-09-prominent-contact-info.md) | High | Low | 2.4.5 | Nearly all user groups |
| 10 | Reduce information overload | [Story 10](story-10-reduce-information-overload.md) | High | High | — | Senior, ADHD, cognitive, stressed |
| 11 | Add ARIA landmarks | [Story 11](story-11-aria-landmarks.md) | High | Low | 1.3.1, 4.1.2 | Screen reader |
| 12 | Remove italics from testimonials | [Story 12](story-12-remove-italic-testimonials.md) | High | Low | 1.4.8 | Dyslexic |
| 13 | Increase font size and weight | [Story 13](story-13-font-size-weight.md) | High | Low | 1.4.8 | Low vision, senior, low contrast |
| 14 | Remove hover-dependent interactions | [Story 14](story-14-hover-dependent-interactions.md) | High | Medium | 2.1.1 | Voice control, motor impairment |
| 15 | Add non-color visited link indicators | [Story 15](story-15-visited-link-states.md) | High | Low | 1.4.1 | Blue-yellow color blind |
| 16 | Don't rely on color alone | [Story 16](story-16-color-not-only-indicator.md) | High | Medium | 1.4.1 | Red-green color blind, blue-yellow color blind |
| 17 | Add physical address and trust signals | [Story 17](story-17-trust-signals-address.md) | High | Low | — | Skeptical users |
| 18 | Add pricing transparency | [Story 18](story-18-pricing-transparency.md) | High | Medium | — | Skeptical users |
| 19 | Increase line spacing | [Story 19](story-19-line-spacing.md) | Medium | Low | 1.4.8 | Dyslexic |
| 20 | Shorten homepage | [Story 20](story-20-shorten-homepage.md) | Medium | High | — | Senior, ADHD, cognitive, low vision |
| 21 | Add skip links for key sections | [Story 21](story-21-skip-links.md) | Medium | Low | 2.4.1 | Low vision magnifier, ADHD, screen reader |
| 22 | Fix sticky header at high zoom | [Story 22](story-22-sticky-header-zoom.md) | Medium | Low-Medium | 1.4.10 | Low vision magnifier |
| 23 | Improve image alt text | [Story 23](story-23-image-alt-text.md) | Medium | Low | 1.1.1 | Screen reader |
| 24 | Add text labels to icon-only elements | [Story 24](story-24-icon-text-labels.md) | Medium | Low | 1.1.1, 4.1.2 | Voice control, low vision |
| 25 | Replace dropdowns with larger controls | [Story 25](story-25-replace-dropdowns.md) | Medium | Medium | 2.5.8 | Motor impairment |
| 26 | Remove auto-playing carousels | [Story 26](story-26-auto-playing-carousels.md) | Medium | Low-Medium | 2.2.2 | Motion sensitivity, voice control |
| 27 | Increase logo contrast | [Story 27](story-27-logo-contrast.md) | Medium | Low | 1.4.3 | Situational contrast, low contrast |
| 28 | Avoid text over images | [Story 28](story-28-text-over-images.md) | Medium | Medium | 1.4.3 | Low vision, senior, situational |
| 29 | Add reassurance to downloads | [Story 29](story-29-download-reassurance.md) | Medium | Low | — | Stressed user, skeptical user |
| 30 | Add video explainer | [Story 30](story-30-video-explainer.md) | Medium | High | — | Senior, stressed, cognitive |
| 31 | Add accessibility statement and motion toggle | [Story 31](story-31-accessibility-statement.md) | Medium | Low-Medium | — | Motion sensitivity, screen reader |
| 32 | Improve form experience | [Story 32](story-32-form-experience.md) | Medium | Medium | 3.3.2 | Cognitive, stressed, motor, senior |
