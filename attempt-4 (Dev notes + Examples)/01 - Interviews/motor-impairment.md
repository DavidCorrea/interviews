# Interview: Alex Rivera — Motor Impairment (Keyboard-Only User)

**Persona:** Alex Rivera, 38, Product Manager  
**Condition:** Limited fine motor control due to cerebral palsy; uses keyboard exclusively  
**Assistive Technology:** Keyboard-only navigation (Tab, Enter, Space, Arrow keys), Sticky Keys  
**Goal:** Find what LaunchPad Lab does and how to contact them  
**Date of Evaluation:** February 2026  

---

## First Impressions

I landed on the LaunchPad Lab homepage and immediately started pressing Tab to orient myself. The very first thing that happened was encouraging—my focus landed on a "Skip to content" link. That's exactly the kind of thing I need as a keyboard user, because otherwise I'd have to tab through the entire navigation bar every single time I visit a new page. However, I have to say I'm not confident I actually *saw* the skip link. It appeared to use a `screen-reader-text` class, which typically means it's visually hidden. If it doesn't become visible when I focus on it, then I have no idea it's there. I pressed Enter on what I hoped was the skip link and moved on.

The next Tab stop brought me to the LaunchPad Lab logo, which links to the homepage. Fine. Then I started tabbing into the main navigation.

## Navigating the Header & Mega Menu

This is where things got complicated—and frustrating.

The primary navigation uses a mega menu system (Max Mega Menu). The top-level items I could tab through were: **Services**, **Technologies**, **Industries**, **Our Work**, **About Us**, **Insights**, and **Contact**. Each had `tabindex="0"`, so technically I could reach them all. Good.

But the problem hit me immediately when I landed on "Services." I know from the visual layout that this menu item is supposed to expand into a large dropdown panel showing sub-services like AI Automation, Web App Development, Mobile App Development, Salesforce Development, Product Strategy & Design, and Managed Services & Support. The menu is configured with `data-event="hover_intent"`—meaning it's designed to open when you *hover* your mouse over it.

I can't hover. I pressed Enter on "Services," hoping it would toggle the dropdown open. Instead, I was worried it would navigate me away from the page entirely, because the menu has a `data-second-click="go"` configuration, which means the first click is supposed to open the menu and the second click navigates. But as a keyboard user, the distinction between "first click" and "second click" is ambiguous—does pressing Enter count as a "click" in this context? The behavior felt unpredictable.

After some experimentation, I found that the mega menu plugin does appear to have *some* keyboard support—pressing Enter on "Services" did seem to toggle `aria-expanded` to `true`, and I could then Tab into the submenu items. But the experience was far from smooth. There was no visual indication that the submenu had opened until I started tabbing through the items inside it. The `aria-expanded` state changed, but the visual reveal of the dropdown panel is animated with a `fade_up` effect, and I couldn't tell whether the animation had completed or whether focus was correctly inside the submenu.

The same issue applied to the "Industries" dropdown. When I tabbed into it, I had to press Enter, hope the dropdown appeared, and then navigate through a dense grid of links—Financial Services, Healthcare, Professional Services, Insurance, Technology, Legal, Private Equity, Education, Social Impact—plus a text widget with a "View Industries" button. That's a *lot* of tab stops to navigate through before I could get to the next top-level menu item ("Our Work").

There is no obvious way to *close* a dropdown and skip past it. If I accidentally opened the "Services" dropdown, I had to tab through every single submenu link—AI Automation, Web App Development, Mobile App Development, Salesforce Development, Product Strategy & Design, Managed Services & Support, plus the "View Services" button embedded in a text widget—before my focus would move to "Technologies." That's roughly 8-10 extra tab stops I didn't need. There is a close button (`<button class='mega-close' aria-label='Close'>`) in the DOM, but it appears at the *end* of the menu structure, not in a position where I could easily reach it to dismiss an open dropdown.

I also noticed that the hamburger menu toggle (`<div id="burgerBtn">`) is a plain `<div>`, not a button or link. This means it's completely invisible and unreachable to my keyboard. Fortunately, the mega menu plugin provides its own toggle button with `aria-label="Toggle Menu"`, but the coexistence of these two controls is confusing—it's unclear which one is active at which viewport size.

## Finding What LaunchPad Lab Does

Despite the navigation hurdles, I *was* able to determine what LaunchPad Lab does, primarily through the homepage content itself.

After getting past the navigation, my focus moved to the hero section. The heading reads: **"AI Innovation. Digital Solutions. Results that Matter."** Below that, there's a paragraph: *"LaunchPad Lab helps organizations harness the power of AI through tailored consulting and product development services. From strategy to execution, we build high-impact digital products that modernize operations, reduce costs, and unlock growth."* That gives me a solid overview.

There's a CTA button labeled "Connect with an Expert" that links to the contact page. I could Tab to it and press Enter—that worked fine.

Continuing to tab through the page, I reached the "Trusted by Hundreds of Innovative Businesses" logo section, which is a horizontally scrolling logo carousel. The logos themselves (Kawasaki Engines, 1-800-GOT-JUNK?, Harvard University, Prosci, Whirlpool, Northwestern University, CDK Global, Lurie Children's Hospital, Indiana University, etc.) aren't interactive links, so I just tabbed past them. But the scrolling animation runs automatically, and there's no keyboard way to pause or control it. As a keyboard user, I don't have a way to stop the motion if it's distracting me.

Next, I encountered a Wistia video embed titled "LaunchPad Lab: Our Approach to Building Digital Products Video." The video is embedded in a sandboxed iframe (`sandbox="allow-scripts"`). I was able to Tab into the iframe and the Wistia player did seem to have keyboard-accessible controls, but navigating inside an iframe is always a bit unpredictable. I could play/pause with Space, which is good.

Below the video, there's a section with the heading **"AI-Powered Digital Solutions for the Modern Enterprise"** and descriptive text about their services. This was all readable via tabbing through the page.

Then I reached the **service cards** section: "Make AI Your Competitive Advantage." This section has six cards—AI Automation & Agentic AI, Web Application Development, Mobile Application Development, Salesforce Development, Product Strategy & Design, and Managed Services & Support. Each card is wrapped in an `<a>` tag, making it a large clickable target, which is good for me. I could Tab to each card and press Enter to visit the service page.

However, I noticed a problem with **duplicate links**. Each card has the outer `<a>` wrapping the entire card, AND inside each card there's another `<a class="link-black-base arrow-link">Learn More</a>` link going to the exact same URL. This means for every service card, I have to Tab through *two* focusable elements that both go to the same page. With six cards, that's 12 tab stops instead of 6 for what is essentially one choice per card. This is wasteful and confusing for a keyboard user.

**Goal achieved: Yes.** I was able to learn what LaunchPad Lab does—they're an AI-centric digital product development consultancy offering AI automation, web and mobile app development, Salesforce development, product strategy, and managed services.

## Finding How to Contact LaunchPad Lab

This was partially successful but had significant friction.

From the homepage, I eventually tabbed down to a section near the bottom with contact cards showing three options:
- **Email:** contact@launchpadlab.com (this is a `mailto:` link—keyboard accessible)
- **Call:** (312) 888-9651 (this is a `tel:` link—keyboard accessible)
- **Connect with Us on LinkedIn:** links to their LinkedIn page (keyboard accessible)

I could also Tab to the "Contact" link in the main navigation and press Enter to go to the contact page. On the contact page, the header says **"Ready to Build Something Great?"** with the instruction to *"Complete the form below to tell us about your project."*

Here's where I hit a significant barrier: **the contact form is rendered by Ninja Forms, a JavaScript-dependent form plugin.** The actual HTML in the page is just an empty container (`<div id="nf-form-13-cont" class="nf-form-cont">`) with a loading spinner. The form fields—name, email, company, message, etc.—are dynamically injected by JavaScript. There's even a `<noscript>` message that says *"Notice: JavaScript is required for this content."*

Because the form is JavaScript-rendered, I need to trust that the Ninja Forms plugin properly generates accessible form fields with correct `<label>` associations, proper `tabindex` ordering, visible focus indicators, and keyboard-operable submit buttons. In my experience, dynamically rendered forms are hit-or-miss for keyboard accessibility. Without being able to inspect the live-rendered form, I can't confirm that all fields are properly labeled or that the tab order follows a logical sequence.

Additionally, the form container has `aria-live="polite"`, which is good for announcing dynamic content changes, but it also has `aria-labelledby="nf-form-title-13"` referencing a form title element that may or may not be visible. The `role="form"` attribute is appropriate.

On the contact page, I also found the same testimonials slider that appears on the homepage. The testimonials use a **Tiny Slider** carousel configured with `controls: false` (no prev/next buttons) and `mouseDrag: true`. This means the *primary intended interaction method is mouse dragging*, and there are no visible controls for me to cycle through testimonials. There are navigation dots (`navPosition: "bottom"`), which might be keyboard focusable, but without prev/next buttons, I'm relying on the dots alone. This is far less usable than having clearly labeled "Previous" and "Next" buttons.

The footer of the contact page (and all pages) includes the physical address: **2045 W Grand Ave Ste B, PMB 37406, Chicago, Illinois 60612**, plus the phone number (312) 888-9651 and social media links (Facebook, Instagram, LinkedIn). All of these are standard links and were keyboard accessible.

**Goal achieved: Partially.** I found email, phone, address, and social links. I found the contact form but could not fully verify its keyboard accessibility because it's JavaScript-rendered.

## Focus Indicators

Throughout my experience, one of my biggest ongoing frustrations was **inconsistent or missing visible focus indicators.** The site's CSS doesn't appear to define custom `:focus` styles for interactive elements. This means I'm relying entirely on browser default focus outlines—which are often a thin dotted line or a subtle blue glow.

On the homepage hero section, which has a blue background (`#1E60BD`), the "Connect with an Expert" button—styled as `.button-white-base`—likely shows a white or light-colored focus ring. But against the already-bright design, it may not have sufficient contrast to be clearly visible. I frequently lost track of where my focus was, especially when tabbing through the service cards section, where each card has a hover-based interaction (`.hover-cards-interaction` class) that may not have an equivalent focus style.

The navigation links in the mega menu use the default browser focus, but with the dense visual layout of the mega dropdown panels, it was difficult to tell which specific link had focus at any given moment.

## Other Barriers

- **The AOS (Animate on Scroll) library** is used throughout the site to animate content into view. Content sections use `data-aos="fade-up"` with durations of 1000ms. As a keyboard user, when I tab to an element, the page scrolls to bring it into view, but the animation might not trigger at the right time or might make content temporarily invisible. This is a minor issue but adds to the overall sense of unpredictability.

- **The logo scroller** in the "Trusted by" section auto-scrolls without a pause mechanism. Under WCAG 2.2.2, moving content should have a way to be paused, stopped, or hidden. I have no keyboard control over this animation.

- **Nested invalid HTML in the footer**: The phone link has a double-quote issue (`<a href="tel:312-888-9651"">`), which while likely handled by browsers, reflects a lack of attention to HTML quality that often correlates with accessibility gaps.

- **The `<div id="burgerBtn"></div>`** element is a non-semantic, non-focusable element that appears to serve as a mobile menu trigger. While the mega menu plugin provides its own accessible button, the presence of this inaccessible `<div>` is concerning.

## Would I Stay or Leave?

I would **stay on the site**, but I'd be frustrated. My primary goals—learning what they do and finding contact information—were *technically achievable*, but the experience was full of friction. The mega menu's hover-dependent design, the excessive tab stops from duplicate links, the mouse-drag-only carousels, and the inconsistent focus indicators all made the experience feel like it wasn't designed with someone like me in mind.

The contact form is my biggest concern. As a product manager researching agencies for my company, submitting a contact form is the most likely way I'd initiate a business relationship. If that form has any keyboard traps or unlabeled fields, my ability to complete my core task is at risk.

If I were in a hurry or comparing multiple agencies, the friction on this site might push me toward a competitor with a smoother keyboard experience. I could always fall back to the email address (contact@launchpadlab.com) or the phone number, but a company that builds digital products should have a website that demonstrates the accessibility standards I'd expect them to apply to my project.

## Summary

| Goal | Achieved? | Notes |
|------|-----------|-------|
| Find what LaunchPad Lab does | Yes | Homepage content clearly describes their services |
| Find how to contact them | Partially | Email, phone, address found; contact form accessibility unverifiable |
| Navigate via keyboard only | With difficulty | Mega menu hover-dependent, excessive tab stops, no carousel controls |
| Maintain awareness of focus | Inconsistent | Default browser focus often insufficient against site's design |
