# Interview: Morgan Taylor — Screen Reader User (Blind)

**Persona:** Morgan Taylor, 36  
**Condition:** Blind since childhood. Uses a screen reader (VoiceOver, NVDA, or JAWS) for all computer interaction. Cannot see anything on screen. Relies entirely on auditory output: semantic HTML, ARIA labels, heading hierarchy, landmarks, alt text, and descriptive link text.  
**Task:** Visit LaunchPad Lab's website, find out what they do, and find how to contact them.  
**Device/Setup:** MacBook with VoiceOver enabled, keyboard-only navigation  

---

## The Experience

I'm an accessibility consultant. A client recently asked me to evaluate digital agencies for a potential partnership on a new enterprise platform. LaunchPad Lab came up as a candidate, so I need to find out what they do and how to reach them. I open Safari, activate VoiceOver, and navigate to launchpadlab.com.

### Landing on the Homepage

VoiceOver announces the page title: **"AI-Centric Digital Product Design & Development | LaunchPad Lab."** That's a strong start. The title is descriptive — I immediately know this is some kind of digital product company with an AI focus. The `<html>` element has `lang="en-US"`, so VoiceOver is using the correct language profile. Good.

The first thing VoiceOver announces after the page loads is a link: **"Skip to content."** This is a skip navigation link — exactly what I need to bypass repetitive headers and jump to the main content. I activate it.

And nothing happens. Or rather, nothing seems to change. VoiceOver doesn't move my focus to a new region. I press VO+F3 to try to move to the main content area, and VoiceOver doesn't announce any `main` landmark. I try using the rotor to navigate by landmarks and I find: **banner** (the header), **navigation**, and **content information** (the footer). But there is no **main** landmark. There is no `<main>` element on this page at all.

This is a significant problem. The skip link targets `#primary`, but there appears to be no element on the page with `id="primary"`. The skip link is a dead link. It doesn't take me anywhere. For a sighted user, this is invisible — they never needed it. For me, it's a broken promise. I was told I could skip to content, but the content region doesn't exist as a landmark or as a target for that link.

I have to navigate the old-fashioned way — moving forward through the page element by element.

### Navigating the Header and Navigation

VoiceOver identifies the banner landmark (the `<header>` element has `role="banner"`). Inside it, I find a link with an image: **"LaunchPad Lab"** — the logo image has `alt="LaunchPad Lab"`, which is correct. I know I'm on the LaunchPad Lab website and this link goes to the homepage.

Next, I encounter the navigation region. VoiceOver announces the `<nav>` element, but it has no `aria-label`. It's just "navigation." On a page with potentially multiple nav elements (main nav, footer nav), this lack of labeling means I can't distinguish between them when I list landmarks with the rotor. It would be much more helpful if this were labeled "Main navigation" or "Primary navigation."

Inside the navigation, I find a mega-menu. The top-level items are announced as links:

- **"Services"** — VoiceOver announces this link and notes it has `aria-expanded="false"`. Good — I know this is an expandable menu item.
- **"Technologies"** — a plain link.
- **"Industries"** — another expandable link with `aria-expanded="false"`.
- **"Our Work"** — plain link.
- **"About Us"** — plain link.
- **"Insights"** — plain link.
- **"Contact"** — plain link.

This is useful. I can already tell from the navigation structure that this company has services, works across industries, and has a contact page. The navigation links have text labels that make sense. The `tabindex="0"` on each ensures they're keyboard-focusable.

I decide to explore the Services submenu. I activate the "Services" link. The `aria-expanded` attribute should toggle to `"true"` and a submenu should appear. The submenu items are inside `<ul>` elements with `role="presentation"`, which suppresses the list semantics. This is intentional for the mega-menu — the items are still links and VoiceOver announces them individually:

- **"AI Automation"** — the link contains an `<img>` with `aria-hidden="true"` and `alt=""`, followed by a `<span>` with the text. The icon is correctly hidden from screen readers and the text label is exposed. Good.
- **"Web App Development"**
- **"Mobile App Development"**
- **"Salesforce Development"**
- **"Product Strategy & Design"**
- **"Managed Services & Support"**

There's also a text widget inside the menu that says **"Explore all Services"** and a link: **"View Services."** This is adequate — the link text tells me where it goes.

So from the navigation alone, I now have a reasonable idea of what LaunchPad Lab does: AI automation, web development, mobile development, Salesforce development, product strategy and design, and managed services. That's a good start on my first goal.

### The Hero Section — Where Is the H1?

I press VO+Command+H to jump to the next heading. VoiceOver announces: **"AI Innovation. Digital Solutions. Results that Matter. Heading level 1."** 

Good — there's exactly one `<h1>` on the page, and it's the main headline. This tells me the page's primary topic. Below it, VoiceOver reads a paragraph: *"LaunchPad Lab helps organizations harness the power of AI through tailored consulting and product development services. From strategy to execution, we build high-impact digital products that modernize operations, reduce costs, and unlock growth."*

Now I have a clear understanding of what they do. They're an AI-focused digital product consultancy. Goal partially achieved.

There's also a link: **"Connect with an Expert."** The link text is descriptive — I know this will take me to a contact or consultation page. I note it for later when I pursue my contact-finding goal.

### Moving Through the Page by Headings

I continue pressing VO+Command+H to navigate by headings. Here is the heading sequence I hear:

1. **h1:** "AI Innovation. Digital Solutions. Results that Matter."
2. **h2:** "AI-Powered Digital Solutions for the Modern Enterprise"
3. **h2:** "Make AI Your Competitive Advantage"
4. **h3:** "AI Automation & Agentic AI"
5. **h3:** "Web Application Development"
6. **h3:** "Mobile Application Development"
7. **h3:** "Salesforce Development"
8. **h3:** "Product Strategy & Design"
9. **h3:** "Managed Services & Support"
10. **h2:** "Ship Game-Changing Digital Products to Market Fast"
11. **h3:** "Operational Efficiency"
12. **h3:** "Modern Technology"
13. **h3:** "Customer Engagement"
14. **h3:** "Scalable Solutions"
15. **h3:** "Expansive Resources"
16. **h3:** "Speed to Market"
17. **h2:** "Years in Business"
18. **h2:** "Projects"
19. **h2:** "Clients"
20. **h2:** "Accelerate Digital Product Speed to Market"
21. **h3:** "Discover"
22. **h4:** "Research & Define"
23. **h3:** "Deliver"
24. **h4:** "Development"
25. **h4:** "QA Testing"
26. **h3:** "Release"
27. **h4:** "Deploy"
28. **h4:** "Ongoing Support"
29. **h2:** "Transform how your business operates with custom AI solutions"
30. **h2:** "We Help Shape Our Clients' Digital Future"
31. **h3:** "360-Customer View in Salesforce"
32. **h3:** "Sales Discovery Portal for Automotive Companies"
33. **h3:** "Spurring Enterprise Innovation"
34. **h2:** "You Might Also be Interested In"
35. **h3:** "The Business Value of Building Applications and Portals"
36. **h3:** "Download Our Guide: Building Your Competitive Advantage With Salesforce"
37. **h3:** "How Automated Intelligence Is Reshaping the Way Businesses Scale"
38. **h2:** "Let's Build Something Great."
39. **h2:** "Contact Us"
40. **h2:** "Let's Get Social"

The heading hierarchy is mostly logical — h1 at the top, h2 for major sections, h3 for subsections, h4 for sub-subsections under the process grid. I can move through the page efficiently using heading navigation and understand the content structure.

However, there are issues. Headings 17–19 — **"Years in Business," "Projects," "Clients"** — are all `<h2>` elements. These are stat labels (the numbers like "12+", "730+", "240+" are in separate `<span>` elements). Semantically, these aren't section headings — they're data labels. Using `<h2>` for them creates noise in my heading navigation. When I'm pressing H to jump through sections, I expect headings to represent meaningful content sections, not individual statistics. These three h2s break my mental model of the page structure. I pass through them quickly, confused about whether I've entered a new section or not.

### The "Learn More" Problem

After hearing the six service card headings (h3s like "AI Automation & Agentic AI," "Web Application Development," etc.), I explore each card. Below each heading and description, VoiceOver announces a link: **"Learn More."**

Then the next card: another heading, another description, another link: **"Learn More."**

And again: **"Learn More."**

Six identical "Learn More" links in a row. When I use VoiceOver's rotor to list all links on the page, I see a block of six links all announced as "Learn More" with no distinguishing context. I have no idea which "Learn More" goes to which service. WCAG requires that link purpose be determinable from the link text alone, or at minimum from the link text together with its programmatically determined context. In this case, the links are inside card containers — but the `<a>` elements themselves contain only the text "Learn More." There is no `aria-label`, no `aria-labelledby` pointing to the card heading, nothing.

If I pull up the links list in VoiceOver, I see:
- Learn More
- Learn More
- Learn More
- Learn More
- Learn More
- Learn More

This is useless. I would need to navigate to each link individually and check its surrounding context to understand where it goes. That's a significant inefficiency for a screen reader user who relies on link lists to quickly jump to destinations.

### Images Without Alt Text

As I move through the page, I encounter many images. VoiceOver either skips them (if they have `alt=""`) or announces them. The navigation icons are correctly hidden with `aria-hidden="true"` and `alt=""` — they're decorative since the text label provides meaning.

But the tab section images are a problem. Each tab panel (Operational Efficiency, Modern Technology, etc.) contains an image with `alt=""`. VoiceOver skips these entirely. If these images are purely decorative, that's fine. But given their placement as the primary visual content of each tab panel — they appear to be screenshots or illustrations of the concepts being described — I suspect they carry information. Without alt text, I receive only the brief preview text ("Streamline processes with digital products to enhance productivity"), which may be insufficient.

Similarly, in the **awards/badges section**, there are multiple images for Clutch awards and badges — things like "Top Clutch Salesforce Company United States 2025" and "Top Clutch AI Consulting Company United States 2025." All of these have `alt=""`. VoiceOver skips every single one. These badges convey important trust signals — they're telling potential clients that LaunchPad Lab has been recognized by Clutch. But I hear none of that. I don't even know this section exists unless I stumble into it linearly and hear the surrounding structure.

The **client logos** in the scrolling ticker, on the other hand, have good alt text: "Kawasaki Engines," "1-800-GOT-JUNK?," "Harvard University," "Prosci," "Whirlpool," "Northwestern University," "CDK Global," "Ann & Robert H. Lurie Children's Hospital of Chicago," "Indiana University," "Select Home Warranty," "MD Anderson Cancer Center," "Bullhorn." That's excellent. I can hear exactly which clients they work with. The scrolling animation itself isn't relevant to me — I can't see it, and VoiceOver reads through the list linearly.

In the case studies section, there are small "increase" arrow icons (`increase.svg`) next to statistics like percentage improvements. These have `alt=""`. The increase arrows are conveying meaning — they indicate that a metric went up. Without alt text, I just hear the number and description, but I miss the "increase" indicator. This is a minor issue since the surrounding text usually implies improvement, but it's technically a missing alt text on a meaningful image.

### The Footer Social Media Links

In the footer, I find social media links: **Facebook**, **Instagram**, **LinkedIn**. Each link contains an `<img>` with `alt=""` followed by the text name ("Facebook," "Instagram," "LinkedIn"). VoiceOver announces the link text, so I hear "Facebook, link" — that works. The empty alt on the icon is correct here because the visible text provides the label.

But wait — I also notice the footer images for the Salesforce Partner badge (`alt="Salesforce Partner"`) — this one actually has alt text. Good. The LaunchPad Lab logo in the footer also has `alt="LaunchPad Lab"`. Good.

### Finding Contact Information

Now for my second goal: finding how to contact LaunchPad Lab. I have several paths.

**Path 1: The "Contact" link in the navigation.** I already noted this. I press VO+U to open the rotor, navigate to links, and find the "Contact" link. I activate it and land on the contact page.

VoiceOver announces the page title: **"Contact Us | LaunchPad Lab."** I navigate by headings and hear:

1. **h1:** "Ready to Build Something Great?"
2. **h2:** "Ready to Build Something Great?"
3. **h2:** "Hear From Some of Our Recent Clients"
4. **h2:** "Let's Connect"
5. **h3:** "Email"
6. **h3:** "Call"
7. **h3:** "Connect with Us on Linkedin"
8. **h2:** "Contact Us"
9. **h2:** "Let's Get Social"

The first issue: the h1 and h2 have the **exact same text** — "Ready to Build Something Great?" This is confusing. When I'm navigating by headings, I hear the same text twice and I'm not sure if I've moved or if VoiceOver is repeating itself. The h1 appears to be in a hero/banner area, and the h2 is likely a subheading for the form section below it. But having identical text at two heading levels is disorienting.

Under the **"Let's Connect"** heading (h2), I find:
- **"Email"** (h3) with a link: **"contact@launchpadlab.com"** — a `mailto:` link. The link text is the email address itself. This is descriptive and functional.
- **"Call"** (h3) with a link: **"(312) 888-9651"** — a `tel:` link. Again, descriptive and functional.
- **"Connect with Us on Linkedin"** (h3) with a link: **"Connect"** — this link text is vague. Just "Connect." Connect to what? If I encountered this link in a links list without context, I'd have no idea where it leads. It should say "Connect with LaunchPad Lab on LinkedIn" or at least "LinkedIn" as the link text.

There's also a contact form on the page. VoiceOver announces the form region: it has `role="form"`, `aria-live="polite"`, and `aria-labelledby="nf-form-title-13"`. This is a Ninja Forms form. The form title is "General Contact" but it's configured with `show_title: 0`, so the title element may not be visually rendered — but VoiceOver may still reference it via `aria-labelledby`.

The form fields are:
- **"First Name"** — required, text input
- **"Last Name"** — required, text input
- **"Company Email"** — required, email input
- **"Company"** — required, text input
- **"How Can We Help You?"** — required, textarea

Each field has proper `aria-labelledby` pointing to its label, `aria-describedby` for error messages, and `aria-invalid="false"`. The labels are positioned above the inputs. VoiceOver announces "First Name, required, text field" — I know exactly what to enter. This is well-done.

There's also a reCAPTCHA field and a **"Submit"** button. The submit button is properly labeled.

However, the form is rendered entirely via JavaScript. If JavaScript fails to load, the `<noscript>` element shows only: **"Notice: JavaScript is required for this content."** There's no fallback contact method within the form area — no email address, no phone number. If I were using a browser with JavaScript disabled (some screen reader users do this for performance or security), I'd hit a dead end.

**Path 2: The footer.** On any page, I can scroll to the footer and find:
- **"Contact Us"** (h2 in footer)
- Address text (though I have to navigate through the list items to find it — it appears to be: 2045 W Grand Ave Ste B, PMB 37406, Chicago, Illinois 60612)
- Phone: **(312) 888-9651** as a `tel:` link

The footer provides a reliable fallback for contact information. The phone link has a minor HTML error — `href="tel:312-888-9651""` — with a double closing quote. This shouldn't affect functionality, but it's sloppy markup that could theoretically cause issues in some parsers.

**Path 3: The homepage CTA section.** Near the bottom of the homepage, there's a section headed **"Let's Build Something Great."** (h2). This contains the same Ninja Forms contact form. So I can actually submit a contact request without ever leaving the homepage.

### Did I Achieve My Goals?

**Goal 1: Find what LaunchPad Lab does.** Yes. Between the page title, the h1 headline, the hero paragraph text, the navigation menu items, and the service card headings, I built a clear picture. LaunchPad Lab is an AI-focused digital product development consultancy based in Chicago. They do AI automation, web app development, mobile app development, Salesforce development, product strategy and design, and managed services. They work across industries including financial services, healthcare, professional services, insurance, technology, and legal. They've been in business 12+ years with 730+ projects and 240+ clients.

**Goal 2: Find how to contact them.** Yes. I found multiple contact methods:
- Email: contact@launchpadlab.com
- Phone: (312) 888-9651
- Contact form on the contact page and on the homepage
- LinkedIn
- Physical address in the footer

### Would I Leave the Site?

No — I was able to achieve both goals. But the experience was rougher than it should have been. The broken skip link forced me to navigate linearly through the entire header. The missing `<main>` landmark meant I couldn't jump to content using landmark navigation. The six identical "Learn More" links made the service section's link list useless. The empty alt text on award badges meant I missed trust-building information. The identical h1/h2 on the contact page was confusing.

If I were a less experienced screen reader user — someone who doesn't know to use heading navigation as a fallback when landmarks fail, or who doesn't know to explore surrounding context when link text is ambiguous — this site would be considerably more frustrating. The bones are there: the heading hierarchy is mostly sound, the form ARIA is good, the navigation labels are descriptive, and key images (logos, brand images) have alt text. But the structural issues (no main landmark, broken skip link) and the link text issues (six "Learn More" links, "Connect" on LinkedIn) undermine what should be a competent experience.

As an accessibility consultant, I'd say this site is about 70% of the way to good screen reader accessibility. The foundations are solid but there are meaningful gaps that need to be addressed.
