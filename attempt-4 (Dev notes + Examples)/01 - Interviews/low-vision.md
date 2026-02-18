# Interview: Rosa Martínez — Low Vision User (No Screen Magnifier)

**Persona:** Rosa Martínez, 48  
**Condition:** Low vision due to glaucoma; does not use a screen magnifier. Relies on browser zoom (125–200%), OS-level large text settings, and increased font sizes.  
**Task:** Visit LaunchPad Lab's website, find out what they do, and find how to contact them.  
**Device/Setup:** Laptop (1440px display), browser zoom set to 150%, OS large text settings enabled, larger cursor  

---

## The Experience

My daughter-in-law told me about a company called LaunchPad Lab — she said they build apps and digital products and they might be a good fit for the nonprofit I volunteer with. We need someone to build a donor portal, so I said I'd look into it. I open my laptop, set my browser to 150% zoom like I always do, and navigate to launchpadlab.com.

### Landing on the Homepage

The page loads and the first thing I see is a large blue header area with a background image. There's a headline that reads **"AI Innovation. Digital Solutions. Results that Matter."** in white text on a blue photographic background. The headline text is big and bold — I can read it at 150% zoom without difficulty. That's good. The font weight is heavy (it looks like extra-bold), and the white-on-blue has enough contrast for me to make out the words even with my reduced vision.

Below the headline there's a paragraph of body text, also in white, explaining what LaunchPad Lab does. It says they help organizations "harness the power of AI through tailored consulting and product development services." The font here is noticeably thinner — it looks like a regular or even light weight. Against the photographic background, this thinner white text is harder for me to read. Where the background image has lighter areas, the white text starts to wash out and I have to lean in and squint. With glaucoma affecting my contrast sensitivity, this kind of text-over-image combination is a problem. If the background were a solid, dark color, I'd be fine. But the image behind it introduces inconsistent contrast.

There's also a **"Connect with an Expert"** button — white text in a white-bordered button on the blue background. I can see it because it's in the general area I'm looking, but the button outline is thin. It's not filled — it's a ghost button with a thin border. For someone with my vision, a solid, filled button would be much easier to spot. Ghost buttons blend into the background when you can't see fine details.

### The Navigation — Where Did It Go?

Here's where things start to go wrong. At 150% zoom, the browser window width effectively shrinks to about 960 pixels. The site's navigation menu has a breakpoint at 1069 pixels. That means at my zoom level, the full desktop navigation — Services, Technologies, Industries, Our Work, About Us, Insights, Contact — **disappears entirely**. It gets replaced by a hamburger menu icon.

And this hamburger icon? It's just a small element — the `#burgerBtn` div. It has no label, no visible text next to it saying "Menu." It's just three thin lines (I assume — I can barely see them). On my screen at 150% zoom, this hamburger button is tiny. I stare at the header area for a good ten seconds trying to find the navigation. I know there has to be a menu somewhere. I finally notice the small hamburger icon in the upper right area, but it took effort. Someone with worse vision than mine might miss it entirely.

I click it, and the mobile menu slides in. The navigation items are listed vertically, which is actually easier for me to read than a horizontal bar would be. The text is a reasonable size. So the mobile navigation layout itself isn't terrible — the problem is *finding* the hamburger trigger in the first place. It's too small and too subtle for a low-vision user at zoom.

I also notice that the **mega-menu toggle button** (which exists as an alternative hamburger) does have an `aria-label="Toggle Menu"`, but the visual representation — the animated hamburger lines (`.mega-toggle-animated-inner`) — is made of very thin CSS lines. These thin lines are extremely difficult for me to see. They might be 2–3 pixels wide before zoom, which at 150% becomes about 3–4.5 pixels. Still thin. Still hard to see.

### Understanding What They Do

I scroll down past the hero section. Immediately below is a **scrolling logo ticker** — client logos like Kawasaki, Harvard, Whirlpool, Northwestern — sliding across the screen. The logos themselves are constrained to a maximum height of 50 pixels and max width of 140 pixels. At 150% zoom, those are effectively 75px and 210px, which is small but just barely legible for the biggest logos. The problem is they're **moving**. Continuously. The scrolling motion makes it very hard for me to actually read any individual logo name. With my reduced visual acuity, I need things to stay still so I can focus on them. A moving target is nearly impossible for me to parse. I can tell there are logos — I can see colored shapes sliding by — but I can't read most of them. It's frustrating because I think they're there to build trust, and I can't benefit from that.

Above the logos, there's a label that says **"Trusted by Hundreds of Innovative Businesses"** — this text is styled as a `<span>` element, likely in a smaller, lighter font. At my zoom level I can just barely read it, but it's not bold and it's noticeably smaller than the headings.

Below the logos, I find a section with a video embed and text: **"Your Strategic AI Partner"** (another small span label) and **"AI-Powered Digital Solutions for the Modern Enterprise"** as an h2 heading. The heading is bold and large enough at 150% zoom — proxima-nova at 44px desktop, zoomed to about 66px. I can read that.

The paragraph below it, though, uses `font-weight: 400` (normal weight) and is colored `#555555` on a white background. The contrast ratio of #555555 on white is technically about 7.85:1, which passes WCAG requirements. But for my glaucoma-affected eyes, lighter-weight text at that color is still harder to read than, say, #333333 or black. The characters feel thin. I can read it, but I have to work harder than I should.

Then I reach the **service cards** section: six cards in a row labeled AI Automation & Agentic AI, Web Application Development, Mobile Application Development, Salesforce Development, Product Strategy & Design, and Managed Services & Support. On a full desktop these display as six columns. But at my 150% zoom (effective 960px viewport), the layout should be reflowing to fewer columns. The cards themselves have small icon images at the top (displayed small, maybe 40–50px), a heading, a thin divider line, and a short tagline.

The **"Learn More"** link on each card uses a small right-arrow icon image (`arrow-right-black.svg` or `arrow-right-white.svg`) with `alt=""`. The link text plus arrow is the clickable area. The arrow is tiny — I can barely see it. But the card headings (h3 elements at about 30px, zoomed to ~45px) are bold and readable. I can at least understand what each service is from the headings alone. The taglines below ("Enabling an autonomous digital workforce," "Bespoke, redefining experiences") are in that same #555555 light-weight font. Readable, but effortful.

I now understand what LaunchPad Lab does: they're a digital product consultancy that does AI, web apps, mobile apps, Salesforce, design, and managed services. Goal #1 achieved — but it required scrolling through quite a bit of content and effortful reading of thin-weight text.

### The Tabs Section — Problems We Solve

Below the services, there's a tabbed section: **"Ship Game-Changing Digital Products to Market Fast."** It has six tabs: Operational Efficiency, Modern Technology, Customer Engagement, Scalable Solutions, Expansive Resources, Speed to Market. The tabs use `role="tab"` with proper ARIA, and they have h3 headings inside the buttons.

Each tab, when active, shows a preview text and an image on the right side. The images have **empty alt text** (`alt=""`). For me, this isn't a screen reader issue since I don't use one, but the images themselves are important visual content — they appear to be screenshots or illustrations. At 150% zoom, the images are reasonably sized, but I notice some of them might get cut off if the layout doesn't reflow properly.

The tab buttons themselves are text-based and reasonably large. The active tab has a visible active state (`.is-active` class). This section is actually one of the better-designed parts of the page for me — clear labels, contained content, no excessive scrolling required within the section.

### Statistics Section

Further down, there's a statistics block: **"12+ Years in Business," "730+ Projects," "240+ Clients."** The numbers are large and displayed with a `<span class="black-color">` element. These are bold and black — high contrast, large text. I can read them easily. The descriptions below each stat are in the standard paragraph styling (#555555, normal weight). Not as easy, but manageable.

### Finding Contact Information

Now for goal #2: finding how to contact them. I have a few paths.

**Path 1: The navigation.** I already found the hamburger menu. Inside it, there's a "Contact" link. I click it and land on the contact page (`/contact`). The page header says **"Ready to Build Something Great?"** in large white text on a blue background. Below that: "Complete the form below to tell us about your project."

The contact form itself is rendered by **Ninja Forms** via JavaScript. When it loads (and it takes a second to render), I see fields for **First Name, Last Name, Company Email, Company, and "How Can We Help You?"** The First Name and Last Name fields use a `half-width` container class, meaning they sit side by side. At 150% zoom, these side-by-side fields are **narrow**. Each field gets about half the container width, which at my effective viewport is maybe 350–400 pixels each. It's tight. The input text I type is in the default browser font size, and the fields themselves are small enough that I worry about accidentally clicking the wrong one.

The form labels are positioned "above" the fields, which is good — I can see what each field is for. The labels are in that same normal-weight font, which is readable but not ideal. The **Submit button** at the bottom has the label "Submit" — it's a button element, which should be large enough to click.

But there's a significant concern: the form has a **reCAPTCHA** element. At 150% zoom, the reCAPTCHA widget can sometimes overflow or overlap with other elements. And for someone with my vision, the small checkbox and the "I'm not a robot" text in the reCAPTCHA are already at the edge of what I can comfortably see and click.

If JavaScript fails to load for any reason, the form is completely gone. All that's shown is **"Notice: JavaScript is required for this content."** This small notice in a `<noscript>` tag doesn't offer any alternative — no email address, no phone number. Just a dead end. (JavaScript does load for me, so the form works, but this is a fragile single point of failure.)

**Path 2: The footer.** I scroll all the way down to the footer on any page and find a **"Contact Us"** section with:
- Address: 2045 W Grand Ave Ste B, PMB 37406, Chicago, Illinois 60612
- Phone: (312) 888-9651

This is plain text and a phone link. I can read it at 150% zoom. The phone number is a `tel:` link, so I could click it on a mobile device. This is actually the easiest contact method for me. The address is in a reasonable font size, and the phone number is in plain text with a clickable link. Good.

I also notice the footer has a minor HTML error — the phone link has a double quote in the `href`: `href="tel:312-888-9651""`. Not sure if that causes any actual issues, but it's sloppy.

**Path 3: The contact page alternative contact cards.** Below the form on the contact page, there's a **"Let's Connect"** section with three cards: Email (contact@launchpadlab.com), Call ((312) 888-9651), and Connect with Us on LinkedIn. These are clearly labeled with icons and text. The icons have empty alt text, but the text labels are sufficient for me. I can read the email and phone number. These cards are actually more useful to me than the form — I'd rather just email or call than fill out a form with small fields.

### Other Observations Throughout

**Links without underlines:** Across the entire site, links are styled with `text-decoration: none` and the same color as body text (#555555). This means **I cannot visually distinguish links from regular text** unless I happen to hover over them (at which point the color changes to #222222). For someone with low vision, this is a real problem. I'm scanning the page trying to find clickable things, and they look identical to non-clickable text. The only links I can reliably identify are the ones styled as buttons (the blue "Learn More" buttons, the "Connect with an Expert" CTA). Inline text links are invisible to me.

**Font weight throughout:** The site uses `proxima-nova` with weight 400 (normal) for body text. For headings, weight 800 (extra-bold) is used. The headings are very readable. But the body text, while technically at sufficient contrast, feels thin for my vision. I'd prefer at least 500 or semi-bold for body copy. The testimonial blockquotes on the contact page use `font-weight: lighter`, which makes them even harder to read — these are long quotes from clients and I struggle to get through them.

**Carousel/slider navigation dots:** The testimonial section on the contact page uses a tiny-slider carousel. The navigation dots for these sliders are small — typically 8–10 pixels. At 150% zoom that's 12–15 pixels, which is still small. They're hard for me to see and even harder to click accurately. I'd prefer arrow buttons or swipe indicators that are larger.

**Social media icons in the footer:** The Facebook, Instagram, and LinkedIn icons have **empty `alt` attributes** (`alt=""`). Since I don't use a screen reader, this doesn't directly affect me, but the icons themselves are small SVG images. At 150% zoom they're visible because they have text labels next to them ("Facebook," "Instagram," "LinkedIn"), so I can identify them. But if the text labels weren't there, I'd have no idea what those tiny icons represent.

**Background images used for card previews:** The blog post cards in the "You Might Also be Interested In" section use CSS `background-image` for their thumbnails. These are set with `background-size: cover`. At 150% zoom, these images scale with the container, so they don't break. But the text overlay on these cards — a span for "Blog Post" and an h3 for the title — might get cramped if the card width narrows too much.

**The "Skip to content" link:** The site has a `.skip-link.screen-reader-text` that says "Skip to content." This is visually hidden (screen-reader-only text). For me, as a low-vision user who doesn't use a screen reader, this link is invisible. If it were visible on focus (like it is on many accessible sites), I could use it to jump past the header. But it's permanently hidden visually, so it's useless to me.

### Would I Leave This Site?

Honestly? I almost did. The moment the navigation disappeared into a tiny hamburger icon at my zoom level, I was disoriented. I spent real time trying to find how to navigate the site. If I hadn't been persistent — if I'd been in a hurry or more frustrated — I might have closed the tab.

But I stuck with it, and I was able to find what I needed. I now know that LaunchPad Lab is a digital product consultancy based in Chicago that does AI, web apps, mobile apps, Salesforce, design, and managed services. And I have their phone number and email. Both goals accomplished.

The site isn't *hostile* to me — it's not broken. But it's not designed with me in mind. The thin fonts, the invisible links, the tiny hamburger menu, the moving logo ticker I can't pause, the narrow form fields, the ghost buttons — all of these are small friction points that add up. Each one costs me a few extra seconds and a bit more effort. Over the course of a full visit, that adds up to fatigue.

What I'd want to see: bolder body text (at least font-weight 500), underlined links, a larger and more visible mobile menu trigger, a static logo display instead of a scrolling ticker, a visible skip-navigation link, and form fields that don't split into cramped half-widths at zoom. None of these are major redesigns. They're refinements that would make a meaningful difference for someone like me.

---

## Summary of Experience

| Goal | Achieved? | Difficulty |
|------|-----------|------------|
| Find what LaunchPad Lab does | Yes | Moderate — required scrolling through thin-weight text; service cards were most helpful |
| Find how to contact them | Yes | Moderate — hamburger menu was hard to find at zoom; footer contact info was easiest path |
| Overall usability at 150% zoom | Functional but fatiguing | Multiple small barriers compounded into significant cognitive and visual effort |
