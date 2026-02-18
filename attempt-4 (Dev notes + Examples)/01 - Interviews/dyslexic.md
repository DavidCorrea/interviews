# Interview: Taylor Kim — Freelance Writer with Dyslexia

## About Me

My name's Taylor. I'm 31, a freelance writer, and I've had dyslexia since I was a kid. I read and write for a living, so I'm not someone who can't handle text — I just need it to be presented well. Good typography, clear structure, generous spacing. That's what lets me do my job. When a website gets that wrong, it's like trying to read through frosted glass. I was checking out LaunchPad Lab because I'm exploring digital product agencies for a potential collaboration. Two simple goals: figure out what they do, and find out how to contact them.

---

## Landing on the Homepage

I loaded up launchpadlab.com and my first impression was honestly mixed. The hero section hit me with a large headline — "AI Innovation. Digital Solutions. Results that Matter." — in what looked like a pretty big, bold font. That part was fine. I could read it. But right below it was a paragraph:

> "LaunchPad Lab helps organizations harness the power of AI through tailored consulting and product development services. From strategy to execution, we build high-impact digital products that modernize operations, reduce costs, and unlock growth."

This was white text on what I think is a dark blue or dark image background. The contrast there was okay, but here's where my issues started. The body text across most of the site uses a gray color — specifically `#555555` on a white `#FFFFFF` background. For most people, that's "fine." For me, it's a struggle. That gray isn't dark enough. My eyes have to work harder to distinguish the letterforms, and I start losing my place. When you have dyslexia, low contrast doesn't just make text "less pretty" — it makes letters swim together, and I end up re-reading the same line three times.

The font itself — Proxima Nova — is actually a good choice. It's a clean sans-serif, which is what I prefer. No serifs tripping me up, no decorative nonsense. I did notice the site loads "Permanent Marker" as a Google Font, which is a rough handwriting-style font. If that's used anywhere on the site, it would be an absolute nightmare for me. Handwriting fonts are one of the hardest things for someone with dyslexia to decode. I didn't spot it being used prominently on the homepage, but just knowing it's loaded made me uneasy.

---

## Assessing the Structure

This is where things got better — and then worse again. The homepage does use headings. I could see section labels like "Your Strategic AI Partner," "Driving ROI with AI," "Problems We Solve," "Our Signature Approach," and "Put AI to Work." Those are helpful. They give me anchors to jump between, so I don't have to read everything linearly.

But under each of those headings, there are paragraphs that are just *too dense* for me. For example, the section under "AI-Powered Digital Solutions for the Modern Enterprise" has a paragraph that reads:

> "At LaunchPad Lab, we combine deep expertise in product design and development with cutting-edge AI consulting to solve critical business challenges. We've helped hundreds of businesses across all industries solve complex problems that go beyond just ROI. Whether you're just getting started with AI or scaling adoption across your organization, our cross-functional teams partner with you to deliver results."

That's one solid block. No bullet points, no line breaks. I had to read it three times to absorb it. My eyes kept jumping from "cutting-edge AI consulting" back up to "deep expertise in product design," and I'd lose where I was. If that had been broken into two or three shorter chunks, or if they'd used bullet points to separate the key ideas, I would have gotten through it once and moved on.

The heading line-height was also tight. The CSS sets headings to `line-height: 1.1`, which means the lines of multi-line headings are cramped together. For body text, the `line-height` is listed as `26px` for a `16px` font — that's about 1.625, which is actually decent and close to the 1.5x minimum I need. But then the base `body` style has `line-height: 1`, which is essentially no extra spacing at all. If that cascades to any text that doesn't have a more specific override, those sections become a wall.

---

## Finding What They Do

This was achievable, but it took more effort than it should have. From the homepage, I could piece together that LaunchPad Lab is a "digital product development consultancy" that focuses on AI, builds web apps, mobile apps, does Salesforce development, product strategy and design, and managed services. The six service cards on the homepage — AI Automation & Agentic AI, Web Application Development, Mobile Application Development, Salesforce Development, Product Strategy & Design, and Managed Services & Support — each had a short tagline and a "Learn More" link. The taglines were concise enough for me to read without losing my place.

I clicked through to the Services page (`/services`) to get more detail. The structure there was actually better than the homepage. Each service had its own block with a heading and a paragraph-length description. The descriptions were longer than I'd like — for instance, the AI Automation section read:

> "Leverage AI automation capabilities and tooling to streamline operations, reduce costs, drive customer satisfaction, and enhance decision-making capabilities–faster and at scale."

That's one sentence, but it's packed with comma-separated clauses. I had to slow down, but I got through it. The "Problems We Solve" section on the Services page used bullet points for Business, IT, and Users categories, which was genuinely helpful. Bullet points are my best friend. I could scan those quickly without getting tangled up.

The FAQ section at the bottom of the Services page was well-structured — questions as headings with expandable answers. But some of those answers were *long*. The answer about "How much does it cost to build a custom software solution?" is a full paragraph with no internal structure or breaks. I had to use my finger on the screen to track my place, which I haven't had to do since middle school.

**Verdict on Goal 1:** Achieved. I figured out what LaunchPad Lab does. But the gray body text and dense paragraphs made it take about twice as long as it should have.

---

## Finding How to Contact Them

This was more straightforward. The navigation bar at the top has a "Contact" link, which I found quickly. The nav items are clearly labeled — Services, Technologies, Industries, Our Work, About Us, Insights, Contact. That's a reasonable number of items and they're legible.

The Contact page (`/contact`) has a heading "Ready to Build Something Great?" and a subheading telling me to fill out a form. The form itself requires JavaScript to render — the page says "Notice: JavaScript is required for this content." I had JavaScript enabled, so presumably the form loaded, but the reliance on JavaScript for the *only* contact form is a concern. If I'd been using a simplified browser or had scripts disabled for performance, I'd be stuck.

Below the form, there's a "Let's Connect" section with three contact methods:
- **Email:** contact@launchpadlab.com
- **Call:** (312) 888-9651
- **LinkedIn:** a "Connect" link

This was great. Clear, scannable, no walls of text. I could find what I needed in seconds.

The footer on every page also has the address (2045 W Grand Ave Ste BPMB 37406, Chicago, Illinois 60612) and phone number (312) 888-9651. Having contact info in the footer is a reliable fallback, and it's presented cleanly.

**Verdict on Goal 2:** Achieved. Contact information was easy to find. The contact page is one of the better-structured pages on the site.

---

## Other Observations

### The Logo Scroller
The homepage has an animated logo carousel — "Trusted by Hundreds of Innovative Businesses" — that auto-scrolls continuously. Moving content is distracting for me. When I'm trying to focus on reading a paragraph nearby, the scrolling logos in my peripheral vision pull my attention away. It's like someone waving their hand next to the page I'm trying to read. The site does check for `prefers-reduced-motion`, which is good, but most users with dyslexia don't know to set that preference.

### The "Permanent Marker" Font
As I mentioned, the site loads "Permanent Marker," a Google Font that looks like messy handwriting. If this is used in any headings, callouts, or decorative elements, it would be extremely difficult for me to read. Handwriting-style fonts break every rule my brain needs — inconsistent letterforms, variable spacing, no clean baseline. Even if it's only used for one word or a decorative accent, it disrupts my reading flow.

### The Statistics Blocks
The homepage has large numbers like "12+," "730+," and "240+" with labels like "Years in Business," "Projects," and "Clients." These were actually effective. Big numbers with short labels — that's easy for me to process. No complaints there.

### Line Length
Some paragraphs on wider screens appear to span quite wide. The site's max content width seems to be around 1220px, and within that, text blocks can stretch fairly wide. Best practice for readability (and especially for dyslexia) is 50–75 characters per line. When lines run too long, my eyes have trouble tracking back to the start of the next line, and I end up re-reading the same line or skipping one entirely.

### Text-to-Speech Compatibility
If I needed to use text-to-speech for longer passages (which I sometimes do for dense content), the semantic structure would mostly support it. The headings are actual `<h1>` through `<h6>` tags, and paragraphs use `<p>` tags. That's good. But any content that's only in images (like client logos without proper alt text) wouldn't be accessible via TTS.

---

## Would I Have Left the Site?

I came close. The gray body text (`#555555`) is the single biggest barrier. Combined with dense paragraphs and tight heading line-heights, reading this site is noticeably more tiring than it needs to be. After about ten minutes, I felt the familiar eye strain and mental fatigue that tells me my brain is working overtime to decode what should be easy text.

I stayed because the *structure* — the headings, the service cards, the bullet points on the Services page — gave me enough scaffolding to navigate without reading every word. If the whole site had been long-form prose with that same gray text and no structural breaks, I would have left within five minutes and looked for another agency.

The site is *usable* for me, but it's not *comfortable*. And comfort matters. If I'm evaluating whether to work with an agency, I want to feel like they've thought about how people experience their content. The typography choices here suggest they prioritized aesthetics over readability — and as someone who depends on good readability to function, that sends a message.

---

## Summary

| Goal | Achieved? | Difficulty |
|------|-----------|------------|
| Find what LaunchPad Lab does | Yes | Moderate — dense text and low contrast slowed me down |
| Find how to contact them | Yes | Easy — navigation was clear, contact info well-presented |

**Overall experience:** Functional but fatiguing. The site's structure saved it from being a failure, but the typography — especially the `#555555` body text color and dense paragraph blocks — made every page harder to read than it needed to be. With a few targeted changes to contrast, line spacing, and content chunking, this could be a comfortable site for someone like me. Right now, it's a site I'd get through if I had to, but I wouldn't enjoy the experience.
