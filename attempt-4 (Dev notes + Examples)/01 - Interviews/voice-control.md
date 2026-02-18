# Interview: Marcus Webb — Voice Control User (ALS)

**Persona:** Marcus Webb, 52  
**Condition:** ALS (amyotrophic lateral sclerosis); cannot use keyboard or mouse. Uses Dragon NaturallySpeaking for all computer interaction. Five years of proficiency with voice control software.  
**Assistive Technology:** Dragon NaturallySpeaking (voice control). Navigates by speaking commands like "Click [label]," "Press [label]," targeting elements by their visible text or accessible name.  
**Goal:** Find what LaunchPad Lab does and how to contact them  
**Date of Evaluation:** February 2026  

---

## First Impressions

I navigate to launchpadlab.com by saying "Go to launchpadlab.com." The page loads. The title reads "AI-Centric Digital Product Design & Development | LaunchPad Lab." Good — I already have a hint about what this company does.

Now I need to orient myself. With Dragon, I typically scan the page visually and speak the name of whatever I want to click. I'm looking at the header area and the navigation. The first thing I need to understand is: what can I say to interact with this page?

I can see the LaunchPad Lab logo in the top-left corner. There's a navigation bar with text links. And there's a prominent button-style link. Let me start exploring.

## The Navigation Bar

The main navigation is visible across the top of the page. I can see text labels: **Services**, **Technologies**, **Industries**, **Our Work**, **About Us**, **Insights**, and **Contact**. These are all clearly visible words. I say:

**"Click Services."**

Dragon identifies the "Services" link and activates it. But here's my first problem. The Services menu is configured to open on **hover** — it uses `hover_intent` as its trigger event. When Dragon "clicks" the element, it may toggle the `aria-expanded` state, but the mega menu's visual reveal is designed around mouse hover behavior. The interaction is unpredictable. Sometimes the dropdown panel appears; sometimes Dragon navigates me directly to the Services page because the menu has a `data-second-click="go"` configuration. I'm not sure whether my voice click counts as a "first click" (open menu) or a "second click" (navigate away).

After a few attempts, I find that saying **"Click Services"** usually opens the dropdown mega menu. Inside it, I can see submenu items with visible text: **AI Automation**, **Web App Development**, **Mobile App Development**, **Salesforce Development**, **Product Strategy & Design**, **Managed Services & Support**, and a link that says **"View Services."** Each of these has a visible text label, and each is accompanied by a small icon image. The icons are decorative (they have `aria-hidden="true"` and `alt=""`), and the text labels provide the speakable names. I can say **"Click AI Automation"** and Dragon targets the correct link. That works.

However, the **Industries** dropdown has the same hover-triggered problem. And critically, the dropdown includes a **close button** (`<button class="mega-close" aria-label="Close">`). I look at it on screen — it appears as a small **X icon** with no visible text label. The `aria-label` says "Close," but there is no visible word "Close" next to the icon. Can I say **"Click Close"**? Dragon NaturallySpeaking matches speech to the **accessible name** when visible text is absent, so saying "Click Close" might work — but only if Dragon can read the `aria-label`. In practice, this is inconsistent. Some voice control software (like macOS Voice Control) will match `aria-label`, but Dragon's behavior varies. If it doesn't work, I have no visible text to target this button. I'm stuck with an open dropdown I can't close by voice. I'd have to say **"Show numbers"** — Dragon's fallback command that overlays numbers on every clickable element — and then say the number. That's a design failure.

The other navigation items — **Technologies**, **Our Work**, **About Us**, **Insights**, **Contact** — are plain links without dropdowns. I say **"Click Contact"** and Dragon takes me to the contact page cleanly. I say **"Click About Us"** and it works. These are straightforward and functional.

## The Hamburger Menu

At narrower viewport widths (or on certain devices), the site shows a **hamburger menu icon** (`<div id="burgerBtn">`). This is a critical failure point for me. The hamburger icon is a `<div>` element — not a `<button>`, not a link. It has no visible text label. It has no `aria-label`. It's a purely visual three-line icon.

I look at it and ask myself: what would I say to click this? **"Click Menu"**? **"Click Navigation"**? **"Click Hamburger"**? None of these would work because the element has no accessible name whatsoever. It's a plain `<div>` with a CSS-generated icon.

The mega menu plugin does provide a separate toggle button with `aria-label="Toggle Menu"`, but this button may not be visible in all viewport states. If the visible hamburger icon is what I see on screen, and the plugin's accessible toggle is hidden or elsewhere in the DOM, I have an element I can see but cannot activate by voice.

If I encounter this site on a tablet or smaller screen where the hamburger menu is the only way to access navigation, I am **completely locked out**. I cannot open the navigation. I cannot find what LaunchPad Lab does. I cannot reach the contact page. The site is unusable.

For the rest of this evaluation, I'll assume I'm on a desktop viewport where the full navigation bar is visible.

## Finding What LaunchPad Lab Does

The hero section of the homepage displays a large heading: **"AI Innovation. Digital Solutions. Results that Matter."** Below it, a paragraph reads: *"LaunchPad Lab helps organizations harness the power of AI through tailored consulting and product development services. From strategy to execution, we build high-impact digital products that modernize operations, reduce costs, and unlock growth."*

I don't need to interact with anything to read this — it's static text. I now have a good initial understanding: they're an AI-focused digital product consultancy.

Below the hero, there's a CTA link: **"Connect with an Expert."** This has clear, unique visible text. I say **"Click Connect with an Expert"** and Dragon activates it correctly. This link takes me to the contact page. I'll come back to that.

### The Service Cards — The "Learn More" Problem

Scrolling down the homepage, I reach a section headed **"Make AI Your Competitive Advantage."** Below it are six service cards:

1. **AI Automation & Agentic AI** — with a "Learn More" link
2. **Web Application Development** — with a "Learn More" link
3. **Mobile Application Development** — with a "Learn More" link
4. **Salesforce Development** — with a "Learn More" link
5. **Product Strategy & Design** — with a "Learn More" link
6. **Managed Services & Support** — with a "Learn More" link

Each card has a heading and a brief description, followed by a link that says **"Learn More."** Six identical "Learn More" links.

I say: **"Click Learn More."**

Dragon highlights all six instances. It doesn't know which one I mean. Dragon overlays numbers on each "Learn More" link — 1 through 6 — and waits for me to say a number. But I can't tell which number corresponds to which service without carefully cross-referencing the numbered overlay with the card layout. The numbers are positioned on the links themselves, not on the card headings. If the layout is dense, the numbered overlays may even overlap.

This is a significant usability barrier. If the links said **"Learn More about AI Automation"** or **"Learn More about Mobile App Development,"** I could say the specific phrase and Dragon would target the correct link without ambiguity. Instead, I'm forced into the "show numbers" fallback every time.

There's also a structural issue: each service card is wrapped in an `<a>` tag that makes the entire card a clickable link, AND inside each card there's a separate "Learn More" `<a>` link going to the same URL. So for each card, Dragon sees **two** clickable elements going to the same destination — the card wrapper and the "Learn More" link. When I say "Click Learn More," I'm targeting the inner link. But if I try to click the card heading text instead (say, **"Click AI Automation and Agentic AI"**), Dragon might target the outer card link or the heading text inside it, depending on how it parses the nested structure. The double-linking creates confusion for voice control software.

Further down the page, there's an additional **"Learn More"** link in the AI callout section — bringing the total to **seven** identical "Learn More" links on a single page.

### The Tab Interface

Below the service cards, there's a tabbed section: **"Ship Game-Changing Digital Products to Market Fast."** The tabs are labeled **Operational Efficiency**, **Modern Technology**, **Customer Engagement**, **Scalable Solutions**, **Expansive Resources**, and **Speed to Market**. These tab labels are visible text.

I say **"Click Operational Efficiency"** and Dragon activates the tab. The corresponding tab panel appears. I say **"Click Customer Engagement"** and it switches. The tab labels are unique and descriptive — this is one of the better-functioning interactive patterns on the site for voice control.

### The Case Study Carousel

The case studies section features a carousel/slider with project highlights. Each slide has a heading (like **"360-Customer View in Salesforce"**), statistics, and a CTA button. The button text is just the client company name — **"Prosci"**, **"CDK Global"**, **"Millennium Trust Company"**.

Saying **"Click Prosci"** activates the link. These labels are at least unique, so Dragon can distinguish them. But the link purpose is ambiguous — "Prosci" could take me to Prosci's website or to a case study. There's no verb ("View Prosci Case Study") to clarify intent.

The carousel itself may have **navigation arrows** — left and right arrows to cycle between slides. These are typically icon-only buttons (a chevron or arrow SVG) with no visible text. If they exist on this carousel, I cannot activate them by voice unless they have accessible names that Dragon can match. Similarly, the **dots/indicators** at the bottom of carousals are usually small clickable circles with no text. I cannot say **"Click dot 3"** — there's nothing speakable.

The testimonials carousel on the contact page uses **Tiny Slider** configured with `controls: false` — meaning there are literally **no previous/next buttons rendered**. The only way to cycle testimonials is mouse dragging. I cannot drag by voice. The testimonials carousel is completely inaccessible to me.

### The Logo Carousel

There's an auto-scrolling logo carousel showing client logos (Kawasaki Engines, Harvard University, Whirlpool, etc.). This carousel scrolls automatically. There are no visible controls to pause or stop the animation. Since the logos aren't interactive links, I don't need to click them. But the automatic motion is distracting and there's no voice-accessible way to pause it.

## Finding How to Contact Them

I say **"Click Contact"** in the navigation bar. Dragon activates it and I land on the Contact page. The heading reads **"Ready to Build Something Great?"**

### Contact Information

Scrolling down, I find a **"Let's Connect"** section with three contact methods:

1. **Email** — with a link showing **"contact@launchpadlab.com"**. I say **"Click contact at launchpadlab dot com"** and Dragon activates the mailto link. That works.

2. **Call** — with a link showing **(312) 888-9651**. I say **"Click 312 888 9651"** and Dragon activates the tel link. That works.

3. **Connect with Us on LinkedIn** — with a link that says just **"Connect."** I say **"Click Connect"** and Dragon activates it. The word "Connect" is unique on this page, so there's no ambiguity. However, the visible text "Connect" doesn't tell me where I'm going. It opens LinkedIn in a new tab. The heading above it says "Connect with Us on LinkedIn," but the link itself is vague.

### The Contact Form

Now for the critical test. The contact form is rendered by Ninja Forms via JavaScript. Once loaded, the form fields are:

- **First Name** — with a visible label above the input field. I say **"Click First Name"** and Dragon moves focus to the input. I then dictate my name: "Marcus Webb." Dragon types it into the field. This works.
- **Last Name** — visible label. **"Click Last Name"** works. I dictate my last name.
- **Company Email** — visible label. **"Click Company Email"** works. I dictate my email address.
- **Company** — visible label. **"Click Company"** works.
- **How Can We Help You?** — visible label on the textarea. **"Click How Can We Help You"** works.

Each form field has a visible label that matches the accessible name (set via `aria-labelledby`). This is critical for voice control: the visible label is what I read on screen, and the accessible name is what Dragon uses to target the element. When they match, my voice command works. When they don't match (e.g., visible text says "Submit" but `aria-label` says "Send form"), my command fails. Here, they match. Well done.

The **Submit button** has the visible text **"Submit."** I say **"Click Submit"** and Dragon activates it. The form submits. If there were validation errors, the form uses `aria-live="polite"` to announce them dynamically. Dragon doesn't interact with aria-live announcements directly (that's a screen reader feature), but I can see the error messages appear visually and respond to them.

There's also a **reCAPTCHA** widget. reCAPTCHA is notoriously difficult for voice control users. The checkbox ("I'm not a robot") requires a click, which I can do by saying **"Click I'm not a robot."** But if the reCAPTCHA escalates to an image challenge ("Select all images with traffic lights"), I'm in serious trouble. Clicking specific grid squares by voice requires the "show numbers" fallback, and the time pressure of CAPTCHA challenges makes this extremely stressful. This is a known accessibility barrier across the web, not specific to LaunchPad Lab, but it's worth noting.

### The Footer

The footer provides redundant contact information, which is good:
- **Physical address:** 2045 W Grand Ave Ste B, PMB 37406, Chicago, Illinois 60612
- **Phone:** (312) 888-9651 as a clickable `tel:` link
- Social links: **Facebook**, **Instagram**, **LinkedIn** — each with visible text labels next to the icon. I can say **"Click Facebook"** or **"Click LinkedIn"** and Dragon targets the correct link. The icons have `alt=""` because the adjacent text provides the label. This is well-implemented.

## Icon-Only Elements — My Biggest Barriers

Let me catalog every icon-only interactive element I found and whether I can activate it by voice:

| Element | Visible Text | Accessible Name | Can I Click It By Voice? |
|---------|-------------|-----------------|--------------------------|
| Hamburger menu (`<div id="burgerBtn">`) | None | None | **No** — completely unusable |
| Mega menu close button (`<button class="mega-close">`) | None (X icon) | `aria-label="Close"` | **Maybe** — depends on Dragon matching aria-label; unreliable |
| Mega menu toggle (`<button>` from plugin) | None visible | `aria-label="Toggle Menu"` | **Maybe** — same aria-label matching concern |
| Carousel prev/next arrows (if present) | None | Unknown | **No** — icon-only with no visible text |
| Testimonial carousel controls | None (controls disabled) | N/A | **No** — controls don't exist at all |
| Logo carousel pause control | None | N/A | **No** — control doesn't exist |
| reCAPTCHA image grid cells | None | Grid coordinates | **No** — requires "show numbers" fallback |

## What Worked

1. **Main navigation links** — Services, Technologies, Industries, Our Work, About Us, Insights, Contact all have clear visible text. I can say "Click Contact" or "Click About Us" and it works perfectly.
2. **Mega menu submenu items** — AI Automation, Web App Development, etc. have visible text labels. Once the dropdown is open, I can target them.
3. **"Connect with an Expert" CTA** — Unique, descriptive visible text. Easy to target.
4. **Tab interface labels** — Operational Efficiency, Modern Technology, etc. Each tab has a unique visible name.
5. **Contact form fields** — Every field has a visible label that matches its accessible name. "Click First Name," "Click Company Email," "Click Submit" all work.
6. **Footer social links** — Facebook, Instagram, LinkedIn all have visible text.
7. **Email and phone links on contact page** — Clear visible text.

## What Failed

1. **Hamburger menu** — A `<div>` with no text and no accessible name. Completely unusable by voice.
2. **Six (seven) identical "Learn More" links** — Cannot distinguish by voice. Forces "show numbers" fallback every time.
3. **Mega menu hover trigger** — Designed for mouse hover. Voice click behavior is unpredictable.
4. **Mega menu close button** — Icon-only X with only an `aria-label`. Unreliable for voice targeting.
5. **Carousel controls** — Testimonial carousel has no controls at all. Other carousels may have icon-only arrows.
6. **Duplicate card links** — Each service card has two links to the same URL (the card wrapper and the "Learn More" link), creating unnecessary ambiguity.
7. **Case study button text** — Just company names with no action verb. Ambiguous but functional.

## Did I Achieve My Goals?

**Goal 1: Find what LaunchPad Lab does.** Yes. The homepage hero text, navigation labels, service card headings, and tab interface gave me a thorough picture. They're an AI-focused digital product development firm offering AI automation, web and mobile development, Salesforce development, product strategy, and managed services. I could reach this information using voice commands on the desktop version of the site.

**Goal 2: Find how to contact them.** Yes. I said "Click Contact," reached the contact page, filled out the form field by field using voice commands ("Click First Name," dictate, "Click Last Name," dictate, etc.), and said "Click Submit." I also found the email address, phone number, and physical address. The contact flow was actually one of the better voice control experiences on this site.

## Would I Leave the Site?

On desktop, no — I was able to complete both goals, though with significant friction around the "Learn More" links and the hover-triggered mega menu. The contact form was a genuinely good experience for voice control.

On a mobile or tablet viewport where the hamburger menu is the only navigation? **Absolutely yes, I would leave immediately.** If the only way to access the navigation is an unlabeled `<div>` icon, the site is completely unusable for me. I cannot open the menu. I cannot find what they do. I cannot reach the contact page. I would close the tab and look for a competitor.

Even on desktop, the experience is rougher than it should be. The seven identical "Learn More" links are a constant annoyance — every time I encounter them, I have to fall back to "show numbers," which breaks my conversational flow with the computer. The hover-triggered menus add uncertainty to every dropdown interaction. And the icon-only close buttons mean that if I accidentally open a mega menu dropdown, I may have difficulty closing it.

If LaunchPad Lab wants voice control users to have a smooth experience, they need visible text labels on every interactive element, unique link text that distinguishes each destination, and click-based (not hover-based) menu triggers. The foundations are there — the navigation labels, form labels, and tab labels are all well done. But the gaps around icon-only elements and duplicate link text create real barriers that add up over the course of a visit.
