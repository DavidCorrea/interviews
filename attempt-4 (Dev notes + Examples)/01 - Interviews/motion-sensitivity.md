# Interview: Taylor Kim — Motion Sensitivity / Vestibular Disorder

**Persona**: Taylor Kim, 34, vestibular disorder and motion sensitivity
**Date**: February 16, 2026
**Site Tested**: https://launchpadlab.com/
**OS Setting**: `prefers-reduced-motion: reduce` enabled
**Goals**: (1) Visit the site, (2) Find what LaunchPad Lab does, (3) Find how to contact them

---

## Initial Impressions

I opened launchpadlab.com with my reduced motion preference enabled in macOS, as I always do. My browser is set to tell every site I visit that I need less motion. It's not a preference — it's a medical necessity. When sites ignore that setting, I pay for it with dizziness, nausea, and sometimes a headache that lasts the rest of my day.

The page loaded, and the first thing I saw was a large hero section with a background image and the heading "AI Innovation. Digital Solutions. Results that Matter." Immediately beneath that text there was a description of what LaunchPad Lab does and a "Connect with an Expert" button. So far, so good — the hero content itself was static and readable.

But then the problem started. The hero text block animated in. It faded up from below into its resting position — a `fade-up` animation that took a full second to complete. I could see the text sliding upward and resolving into place. My `prefers-reduced-motion` setting was completely ignored. That initial motion was disorienting. It wasn't catastrophic on its own, but it was the first sign that this site wasn't built with someone like me in mind.

## Attempting to Browse — The Scroll Problem

I started scrolling down the page, hoping the hero animation was an isolated issue. It was not.

### The Logo Scroller — A Rare Win

Just below the hero, there's a client logo bar labeled "Trusted by Hundreds of Innovative Businesses" with logos for Kawasaki Engines, Harvard University, Whirlpool, and others. On a normal visit without my reduced motion setting, these logos scroll horizontally in a continuous infinite loop. But — and I genuinely want to credit this — the site *does* check `prefers-reduced-motion` for this specific element. The logo scroller was static for me. The logos just sat in a row. I could see them. No nausea. This is exactly what I need, and it tells me someone on the development team knows how to do this. They just didn't do it everywhere.

### AOS Scroll-Triggered Animations — The Core Problem

As I scrolled further, I hit the services section: "Make AI Your Competitive Advantage." There are six service cards — AI Automation & Agentic AI, Web Application Development, Mobile Application Development, Salesforce Development, Product Strategy & Design, and Managed Services & Support. Every single one of these cards has a `fade-up` animation triggered by scrolling. As each card entered my viewport, it slid upward and faded in from transparent to opaque.

Six cards. Six separate animations. All firing in sequence as I scrolled. My `prefers-reduced-motion` setting made no difference. The site uses the AOS (Animate on Scroll) library, and it's initialized with `AOS.init()` — completely bare, with no configuration to disable animations when the user's system preference requests reduced motion. AOS *supports* a `disable` option that can detect the `prefers-reduced-motion` media query, but LaunchPad Lab simply didn't use it.

I had to slow my scrolling and partially look away. The fade-up motion on each card is relatively quick (200 milliseconds), but the cumulative effect of six of them in sequence, combined with the scroll-triggering behavior, was genuinely uncomfortable. I could feel the beginnings of that familiar vestibular unease — a slight dizziness, a sense that the content was swimming rather than stationary.

### Stats Counter Animation

Further down, there's a statistics section: "12+ Years in Business," "730+ Projects," "240+ Clients." When this section scrolled into view, all three numbers animated — they counted up from zero to their final values over two seconds. The "12" ticked up digit by digit, the "730" spun through hundreds, the "240" climbed. This counting animation uses `requestAnimationFrame` and does *not* check `prefers-reduced-motion` at all. There's no guard, no fallback. Numbers just animate regardless of my settings.

Watching numbers count up rapidly is one of those things that might seem harmless to someone without a vestibular condition, but the constant visual change within a fixed area of the screen is exactly the kind of motion that makes me feel unsteady. I had to look away and wait a couple of seconds, then look back once I hoped the animation had completed.

### Card Hover Interactions

The service cards also have a significant hover interaction. When I hovered over a card to read more about it, the entire card changed — the background turned blue, the icon and heading faded to invisible (opacity 0), and a new text block with white text animated into view from a hidden state. This is a multi-property CSS transition involving background color, opacity, max-height, and position, all with cubic-bezier easing. None of it respects `prefers-reduced-motion`. The transition effectively makes the card feel like it's flipping or transforming, which is disorienting when it happens under my mouse cursor unexpectedly.

### The Video Embed

Below the hero area, there's a section called "Your Strategic AI Partner" with an embedded Wistia video titled "LaunchPad Lab: Our Approach to Building Digital Products Video." I was relieved that the video did *not* autoplay. It just sat there as an iframe, waiting for me to click. That's the correct behavior. I chose not to play it because I couldn't be certain the video content itself wouldn't contain rapid motion or transitions, but the fact that it didn't force itself on me was appreciated.

### Mega Menu Dropdown

The navigation uses a mega menu with dropdown submenus for "Services" and "Industries." When I hovered over "Services," the dropdown panel animated in with a `fade_up` effect at 200ms speed. This is a relatively subtle animation, but it's still motion that fires every time I interact with the navigation. Over the course of exploring multiple pages, this adds up. There's no reduced-motion alternative for the menu.

### Case Study Carousel

The "Our Latest Case Studies" section is a carousel powered by tiny-slider. Thankfully, autoplay is set to false, so the slides don't move on their own. However, when I dragged or clicked to navigate between slides, the transition between case studies involved a sliding animation. This is somewhat expected behavior for a carousel, but the horizontal sliding motion is exactly the kind of thing that triggers my symptoms when I encounter it repeatedly.

### Smooth Scrolling

The site implements smooth scrolling for all anchor links using `scrollIntoView({ behavior: 'smooth' })`. This means any click on an in-page anchor causes the viewport to glide to the target rather than jump. For most people, this feels polished. For me, it means every anchor click creates a scrolling motion that I didn't choose and can't control. The `behavior: 'smooth'` property does not automatically respond to `prefers-reduced-motion` — the site would need to check the preference and switch to `behavior: 'auto'` (instant jump) for users like me.

## Finding What LaunchPad Lab Does

Despite the motion, I was able to piece together what LaunchPad Lab does. They're a "digital product development consultancy" based in Chicago that builds "mission-critical digital solutions with AI at the center." Their services include AI Automation, Web App Development, Mobile App Development, Salesforce Development, Product Strategy & Design, and Managed Services & Support. They work across financial services, healthcare, professional services, insurance, technology, legal, private equity, education, and social impact. They've been in business 12+ years with 730+ projects and 240+ clients.

I got this information, but not without cost. Every section I scrolled through triggered animations. The information was there, but the delivery was physically uncomfortable.

## Finding Contact Information

I found contact information in two places:

1. **The homepage itself** has a "Reach Out" section at the bottom with a contact form (Ninja Forms) asking for First Name, Last Name, Company Email, Company, and "How Can We Help You?" There's also a "Connect with an Expert" button in the hero that links to `/contact/`.

2. **The footer** contains:
   - Address: 2045 W Grand Ave Ste B, PMB 37406, Chicago, Illinois 60612
   - Phone: (312) 888-9651
   - Social links: Facebook, Instagram, LinkedIn

3. **The Contact page** (`/contact/`) has the same sort of structure — a hero with an AOS fade-up animation, testimonial quotes, and the same form.

I could find and use the contact form. The form itself doesn't have problematic animations. But getting *to* the form required navigating through all the motion described above.

## The Bigger Picture

What frustrates me most is the inconsistency. The logo scroller checks `prefers-reduced-motion` and correctly disables its animation when my preference is set. Someone on the team clearly understood the concept. But that same respect wasn't extended to:

- The AOS scroll-triggered animations (hero fade-up, card fade-ups on every page)
- The stats counter animation
- The card hover transitions
- The mega menu dropdown effect
- The smooth scrolling behavior
- Any CSS keyframe animation in the stylesheet (`fade-in`, `slide-in-left`, `fade-in-right`, `fade-in-left`, `fade-in-bottom` are all defined with no `prefers-reduced-motion` override)

The site's CSS file has **zero** `@media (prefers-reduced-motion: reduce)` queries. Not one. The only reduced-motion checks exist in the inline JavaScript for the logo scroller and the separate `logo-animation.js` file. Everything else — every transition, every keyframe, every scroll-triggered animation — plays at full intensity regardless of what my operating system is telling the browser.

## Would I Stay or Leave?

I completed my goals. I found what LaunchPad Lab does, and I found how to contact them. But I completed them with mounting discomfort. If I were casually browsing — comparing agencies, doing research — I would have left after hitting the third or fourth scroll-triggered animation. The cumulative effect is what gets me. One animation is tolerable. A page full of them, multiplied across every page of the site, is a physical barrier.

If I needed to hire a digital product agency and my only option was this site, I could push through. But if a competitor's site respected my motion preferences, I'd choose them every time — not because their work is better, but because their site doesn't make me sick.

The irony is that LaunchPad Lab builds digital products for clients. They describe themselves as delivering "bespoke, redefining experiences." For someone with a vestibular disorder, the experience their own site delivers is one of exclusion. The content is good. The information is clear. But the presentation physically hurts.

---

**Task Completion Summary**:
| Goal | Achieved? | Comfort Level |
|------|-----------|---------------|
| Visit the site | Yes | Uncomfortable — animations triggered immediately |
| Find what they do | Yes | Required enduring multiple scroll-triggered animations |
| Find how to contact | Yes | Contact form accessible, but navigating to it involved motion |

**Overall Assessment**: The site is technically navigable but physically uncomfortable for someone with motion sensitivity. The selective implementation of `prefers-reduced-motion` (logo scroller only) demonstrates awareness of the issue but a failure to apply it comprehensively.
