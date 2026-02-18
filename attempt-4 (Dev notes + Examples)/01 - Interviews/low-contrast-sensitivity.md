# Morgan Chen — Low Contrast Sensitivity Interview

**Persona**: Morgan Chen, 52, Marketing Director  
**Condition**: Low contrast sensitivity due to cataracts and age-related vision changes  
**Assistive Setup**: macOS "Increase Contrast" enabled, display brightness at maximum, browser zoom at 125%  
**Date**: February 2026  
**Site Tested**: https://launchpadlab.com/

---

## First Impressions

When I first load the LaunchPad Lab homepage, I'm immediately hit with a large hero section — a photograph of people working at computers with text overlaid on top. The headline reads "AI Innovation. Digital Solutions. Results that Matter." in white lettering. There's a gradient overlay darkening parts of the image, and in those darker areas, I can make out the text reasonably well. But where the gradient fades to transparent — particularly toward the right side of the hero — the white text starts to blend into the lighter portions of the background photograph. It's not unreadable for me, but it requires effort. I have to squint a bit to confirm I'm reading it correctly. For a first impression, this already tells me the designers were thinking about aesthetics over legibility.

Below the hero text, there's a blue button labeled "Connect with an Expert." The white text on the medium-blue button background is clear enough for me — it stands out well against the blue. That's a relief. I can identify it as a button because of its shape, color fill, and distinct text. This is one of the stronger elements on the page.

## Navigating the Site

### The Header and Navigation

The top navigation bar sits over the hero image with a transparent background. The navigation links — "Services," "Technologies," "Industries," "Our Work," "About Us," "Insights," and "Contact" — are rendered in white text floating over whatever the hero image shows behind them. When I hover over "Services," a mega-menu dropdown appears. Here's where things get complicated.

The mega-menu panel has a light background (off-white, around `#f1f1f1`). The submenu links — "AI Automation," "Web App Development," "Mobile App Development," "Salesforce Development," "Product Strategy & Design," and "Managed Services & Support" — appear in a dark gray (`#666` or `#555` depending on the level). These are readable for me against the light background; the contrast is sufficient, probably around 5:1. The headings within the mega-menu are clearer still. I appreciate that this dropdown has a solid, light background rather than being transparent over the hero image.

However, the mega-menu also contains descriptive paragraph text and a "View Services" call-to-action link. The paragraph text uses the same `#555` gray as the body text elsewhere on the site. While this technically passes contrast standards, for me personally, after decades of worsening cataracts, that mid-gray on white always reads as "faded." I find myself leaning toward my screen. I can still read it, but it's not comfortable, and on a longer block of text, it would fatigue me quickly.

There's also a "Contact" link in the navigation that appears styled slightly differently — it looks like a button-style link positioned at the far right. On hover, it shifts to a white background with dark text, which actually makes it pop nicely for me.

### Mobile Hamburger Concern

I notice that if I were viewing this on a smaller screen or resized my browser window, the hamburger menu toggle icon (three horizontal lines) appears to use a light gray color (`#ddd`). On pages where the header overlaps a dark hero image, this would be visible. But on interior pages where the background behind the header might be lighter, those nearly-white hamburger lines against a light background would be virtually invisible to me. I would not be able to find the menu at all.

## Finding What LaunchPad Lab Does

### Scrolling Down the Homepage

Below the hero, I encounter a section with the heading "Your Strategic AI Partner" in black text on a white background. Black on white is perfect for me — I can read this effortlessly. The subheading "AI-Powered Digital Solutions for the Modern Enterprise" is also black, and the body paragraph below it is in that same `#555` gray. Again, I can read it, but it requires more effort than the headings.

Further down, there's a section showcasing their services in a card-based layout. Each service — "AI Automation & Agentic AI," "Web Application Development," "Mobile Application Development," "Salesforce Development," "Product Strategy & Design," and "Managed Services & Support" — is presented in a card. Here's where I encounter a significant problem.

**The service cards appear to use a hover-interaction pattern where the descriptive text is initially hidden (set to zero opacity) and only reveals itself when I hover over a specific card.** Before hovering, I see just the service title and perhaps an icon. The body text is literally invisible — not low contrast, but zero contrast, completely transparent. I have to discover, by accident, that hovering over a card reveals more information. For someone like me who relies on being able to scan a page and identify all visible content, this is extremely frustrating. I had no idea additional text existed until my cursor happened to cross one of the cards. This design pattern assumes users will explore interactively, but I navigate by scanning what I can see, and invisible text is, by definition, not scannable.

Each card also has a "Learn More" link, but these links are styled to look like plain body text — `#555` gray, no underline, with just a small arrow icon after them. The arrow icon helps, but the link text itself is indistinguishable from surrounding paragraph text in terms of color or weight. I can't reliably tell what's clickable and what isn't without hovering and watching for cursor changes.

**The card containers themselves are bordered with an extremely light gray (`#CFCFCF` on white), which gives a contrast ratio of roughly 1.56:1.** For me, these borders are essentially invisible. The cards appear to float in an undefined white space without clear boundaries. I can't tell where one card ends and another begins unless I hover and see the interaction effect.

### The Services Page

I click "Services" in the main nav to try to get a clearer picture. The Services page (`/services/`) opens with another hero section — "AI-Centered Digital Product Development" in white text over a background image with a dark gradient overlay. The gradient helps on the left side, but I notice the same issue as the homepage: the overlay doesn't cover the entire image uniformly, so some text areas are harder to read than others.

Below the hero, the services are listed more clearly with headings, descriptions, and "Learn More" links. The headings are in black, the descriptions in `#555` gray on white. I can make out the content here. The "Learn More" links continue to be styled as plain gray text with a small arrow — not underlined, not in a distinctly different color. If the arrow icon weren't there, I genuinely would not know these were links.

I can now confirm: **LaunchPad Lab is a digital product development consultancy based in Chicago. They build custom software — web apps, mobile apps, Salesforce integrations — with a focus on AI.** They serve industries like financial services, healthcare, legal, and education. I've achieved my first goal, but it took more effort than it should have.

### "Problems We Solve" and Stats Sections

Back on the homepage, the "Problems We Solve" section uses icon-based cards. The card borders are again that barely-visible `#CFCFCF`. The stats section ("12+ Years in Business," "730+ Projects," "240+ Clients") uses black text for the large numbers and gray text for the descriptions, with dividing borders in `#bfbfbf` on white — a contrast ratio of only about 1.84:1. I cannot see these dividers at all. The stats read as a run-on block of text without clear visual separation between the three data points.

### Process Section

The "Accelerate Digital Product Speed to Market" section uses a process flow: "Discover," "Deliver," "Release." The step indicators use blue circles and dashed blue connector lines (`#1e60bd`). The blue on white has about 6:1 contrast, which is sufficient for me to follow the flow. The descriptive text under each step is in `#555` gray again — readable but tiring.

## Finding Contact Information

### The Footer CTA

Every page has a call-to-action block near the bottom: "Let's Build Something Great. Get in touch with one of our experts today!" The heading is black on white and completely legible. Below it, there should be a contact form, but I see the message: "Notice: JavaScript is required for this content." The form is rendered by JavaScript (appears to be HubSpot). Since my browser has JavaScript enabled, the form does eventually load — but I should note that the form itself presents a concern.

**The form fields in the CTA sections across the site use a semi-transparent white background (`rgba(255, 255, 255, 0.2)`) with no visible border.** When these forms appear on a blue or dark background (as they do in some CTA blocks), the form fields are nearly indistinguishable from their surroundings. The contrast between the input field and the background is approximately 1.51:1 — far below the 3:1 minimum required for UI components. I literally cannot tell where to click to start typing. I would have to guess where the input fields are based on layout assumptions, and for someone who relies on clear visual boundaries to identify interactive elements, this is a deal-breaker.

### The Contact Page

I navigate to `/contact/` directly. The page opens with "Ready to Build Something Great?" and "Complete the form below to tell us about your project." Again, the form area shows "Notice: JavaScript is required for this content." The HubSpot form loads after a moment. The form itself, once rendered, appears to have its own styling that's separate from the theme's problematic CSS — the HubSpot form inputs have visible borders and adequate label contrast. This is better than the inline CTA forms elsewhere on the site.

Below the form, there's a testimonials section with client quotes. The quote text appears in a readable dark color, and the attribution names and companies are in slightly lighter text but still discernible.

At the bottom of the contact page, I find the information I need:

- **Email**: contact@launchpadlab.com  
- **Phone**: (312) 888-9651  
- **Address**: 2045 W Grand Ave Ste B, PMB 37406, Chicago, Illinois 60612  
- **LinkedIn**: A "Connect" link  

This information is in the footer on every page as well. The footer uses white text on a very dark navy background (`#021C41`), which gives a contrast ratio of about 16.87:1. **The footer is actually the most readable part of the entire site for me.** It's high-contrast, clear, and well-organized. I appreciate this.

However, the footer links have a hover state that reduces opacity to 50%. When I hover over "Contact Us" or any footer link, it becomes significantly harder to read — the effective contrast drops noticeably. It's a counterintuitive design: the act of interacting with a link makes it harder to see.

## What Worked

- **Headings in black on white** throughout the site are excellent for me. H1 and H2 elements are consistently clear.
- **The footer** is high-contrast and contains all essential information (address, phone, email) in a legible layout.
- **Blue buttons** (like "Connect with an Expert") have sufficient contrast and are clearly identifiable as interactive elements due to their distinct shape and fill color.
- **The contact page's direct contact information** (email, phone, address) is presented clearly.
- **The mega-menu** on desktop has a solid background with sufficiently dark text.

## What Did Not Work

- **Hero text over images** is inconsistent — the gradient overlays don't provide uniform contrast, leaving some text areas hard to read.
- **Body text in `#555` gray** is technically sufficient but experientially fatiguing. After reading several paragraphs, my eyes strain.
- **Hover-reveal card content** (service cards with opacity: 0 text) is completely inaccessible to me. I cannot scan content I cannot see.
- **"Learn More" links** styled identically to body text (no underline, same gray color) are unidentifiable as links without hovering.
- **Card boundaries** (`#CFCFCF` borders on white) are invisible to me, making the page layout feel like an undifferentiated wall of content.
- **Section dividers and stat separators** (`#bfbfbf` and `#CFCFCF` borders) are invisible.
- **CTA form inputs** with no border and semi-transparent backgrounds are indistinguishable from their surroundings.
- **Opacity-based hover states** on links make interactive elements harder to read precisely when I'm trying to use them.

## Goal Achievement

| Goal | Achieved? | Difficulty |
|------|-----------|------------|
| Visit the site | Yes | Easy — the site loads and renders |
| Find what LaunchPad Lab does | Yes | Moderate — required visiting multiple sections; hidden card content was a major barrier; body text was tiring to read |
| Find how to contact them | Yes | Moderate — the footer made this possible; the CTA forms were problematic but the direct contact info was clear |

## Would I Stay or Leave?

I would stay long enough to get the information I need, but **I would not enjoy the experience, and I would not linger.** The hidden card text, the invisible borders, and the gray body text all contribute to a sense that this site was designed for people with perfect vision. If I were evaluating LaunchPad Lab as a potential vendor — which is exactly the kind of task I'd do in my role as a marketing director — I would get the basics and then pick up the phone or send an email rather than continue reading through the site. The irony is not lost on me that their FAQ on the Services page explicitly states they "follow WCAG guidelines to ensure digital products are usable by all people, including those with visual...impairments" and mention "thoughtful color contrast" as part of their process. My experience suggests there is room to practice what they preach.

If the site had used darker body text (even just stepping from `#555` to `#333`), underlined or distinctly colored links, visible card borders, and always-visible content instead of hover-reveal patterns, I could have navigated it comfortably and confidently. As it stands, I accomplished my goals but was left with eye strain and a lingering doubt about whether I missed content I simply could not see.
