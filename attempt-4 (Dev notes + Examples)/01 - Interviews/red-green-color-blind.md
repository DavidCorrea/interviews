# Interview: David Kim — Red-Green Color Blindness (Protanopia/Deuteranopia)

**Persona:** David Kim, 45, Operations Director  
**Condition:** Protanopia/Deuteranopia (red-green color blindness)  
**Date:** February 16, 2026  
**Site Evaluated:** https://launchpadlab.com/  
**Goals:** (1) Find what LaunchPad Lab does, (2) Find how to contact them

---

## First Impressions

When I first landed on the LaunchPad Lab homepage, my immediate impression was positive from a structural standpoint. The page loaded with a large hero banner at the top — a bold heading reading "AI Innovation. Digital Solutions. Results that Matter." in white text on what I perceive as a muted, medium-toned background. The background color is actually blue (#1E60BD), which I can distinguish reasonably well from other elements. White text on blue — that works for me. The contrast felt adequate, and I could read the subtext describing what they do without issue.

There's a prominent call-to-action button in the hero: "Connect with an Expert." It's rendered as a white-outlined or white-filled button, which I could identify because of its shape, position directly below the hero copy, and its clear text label. Good — it doesn't rely on color alone to be recognizable as a button.

The navigation bar at the top has the LaunchPad Lab logo on the left and text links across the top: Services, Technologies, Industries, Our Work, About Us, Insights, and Contact. These are all plainly labeled with text. I didn't need to rely on any color cue to find or identify them. However, I noticed that the "Contact" link in the navigation appears to be styled differently from the other items — it seemed to have a visually distinct treatment. Whether it's a different background or a border, I can't be entirely sure what color it is, but its position at the far right and its text label "Contact" made it easy to find regardless.

## Finding What LaunchPad Lab Does

This was straightforward. The hero text immediately told me they help "organizations harness the power of AI through tailored consulting and product development services." Below the hero, a section labeled "Your Strategic AI Partner" with a subheading "AI-Powered Digital Solutions for the Modern Enterprise" gave me a full paragraph about their capabilities. The text was dark on a light background — high contrast, easy to read, no reliance on color for meaning.

Scrolling down, I hit a section called "Make AI Your Competitive Advantage" with six service cards: AI Automation & Agentic AI, Web Application Development, Mobile Application Development, Salesforce Development, Product Strategy & Design, and Managed Services & Support. Each card has an icon, a heading, a brief description, and a "Learn More" link.

Here's where I hit my first concern. Each card has a small decorative colored line (a horizontal rule/accent) below the heading, rendered with `border-color: #2363BB` — a blue color. Blue is generally distinguishable for me, so this decorative element didn't create a barrier. But the cards themselves use a hover interaction. When I hovered over a card, it visually transformed — the background appeared to shift to a darker tone and the text became light. The transition seemed to rely on a color shift to communicate interactivity and the "active" state. For someone who can't distinguish certain color changes, a hover state communicated purely through a subtle color shift could be confusing. However, because the cards are clearly laid out as distinct rectangular elements with clear headings and "Learn More" text, I could still navigate them.

The "Learn More" links within the cards are styled as white text with a right-arrow icon when the card is in its hover/active state, and as black text with a right-arrow icon in the default state. The arrow icon alongside the text helped me identify these as links, which I appreciated. They weren't underlined, though — which is something I'd normally look for.

Further down, there's a "Problems We Solve" tab interface. This is where I had a notable concern. The tabs are listed vertically: Operational Efficiency, Modern Technology, Customer Engagement, Scalable Solutions, Expansive Resources, and Speed to Market. The currently selected tab has an `is-active` class. From what I could tell, the active tab is differentiated from inactive tabs by some visual treatment — likely a color change or background highlight. If the active state is communicated solely through a color shift (for example, from gray text to a blue or green highlight), I might not perceive the difference depending on the specific colors used. I relied on position and the corresponding content panel to the right to understand which tab was selected. Text content changed as I navigated tabs, which gave me a secondary cue, but the tab state itself could be more clearly indicated with a bold font weight, an underline, a border, or an icon.

The stats section ("12+ Years in Business," "730+ Projects," "240+ Clients") was clearly readable — large numbers in a dark color on a light background with descriptive text beneath. No color-dependent information here. Good.

The case study carousel was interesting. Three case studies were presented: Prosci (on a dark purple/blue background, #30327d), CDK Global (on a blue background, #006cfa), and Millennium Trust Company (on a **green** background, #318500). The MTC case study is where I paused. The green (#318500) reads to me as a murky, brownish, olive-like tone. It's not immediately vibrant or easily distinguishable from a dark yellow or brown. The white text on this green background was still readable due to sufficient luminance contrast, but the button at the bottom — a white button with text styled in the same green (#318500) — was less clear. That green text on a white button could look brownish or grayish to me, and it might not pop the way the designers intended.

Additionally, in the CDK case study, there are "increase" arrow icons (`increase.svg`) used to represent improvement metrics, but these icons have **empty alt text** (`alt=""`). The icon likely represents a green upward arrow signifying growth, but since I can't rely on the green color and there's no text alternative, I have no way to understand what metric these arrows represent. The text next to them says "Improved Sales Team Alignment" and "Streamlined Discovery & Quoting Process," but without a numerical value or an accessible label on the icon, the data point feels incomplete.

## Finding How to Contact Them

Finding contact information was easy. I had multiple paths:

1. **Navigation:** The "Contact" link in the main navigation was clearly labeled. I clicked it and arrived at the Contact page.

2. **Homepage CTA:** At the bottom of the homepage, there's a "Let's Build Something Great" section with a contact form embedded right there. The form has labeled fields (First Name, Last Name, Company Email, Company, How Can We Help You?) with text labels above each input. Required fields are marked with an asterisk (*), which is a text-based indicator — good, it doesn't rely on color.

3. **Footer:** The footer contains a "Contact Us" heading with the physical address (2045 W Grand Ave Ste B, PMB 37406, Chicago, Illinois 60612) and phone number ((312) 888-9651) as a clickable link.

On the Contact page itself, the form was the same Ninja Forms-based form. The page header says "Ready to Build Something Great?" with instructional text: "Complete the form below to tell us about your project. We will get in touch with you as soon as possible." Below the form, there are three contact cards: Email (contact@launchpadlab.com), Call ((312) 888-9651), and Connect with Us on LinkedIn. Each card has an icon, a heading, and the actual contact method as a clickable link. The headings and text labels made these unambiguous.

My concern here is about **form validation**. I didn't submit the form, but based on the form configuration, the system uses standard Ninja Forms validation. The error message text ("This is a required field," "Please correct errors before submitting this form") is text-based, which is accessible. However, Ninja Forms typically highlights error fields with a **red border** or changes the field's styling to indicate an error state. If the only indication that a specific field has an error is a red border — without an icon, text message adjacent to the field, or other non-color cue — that would be a barrier for me. I cannot distinguish a red border from a normal dark gray border. The form does have a general error message area (`role="alert"`), which is promising, but per-field error states need more than just color.

Similarly, on successful submission, if the success state is indicated only by a green banner or green checkmark without accompanying text, I'd miss it. The form is configured to "hide complete" and "clear complete," suggesting it shows a success message — but I can't verify whether that message relies on green color coding.

## What Worked Well

- **Text-based navigation:** All navigation items are clearly labeled with text. I never had to rely on color to find a page.
- **Clear headings and hierarchy:** The page uses `<h1>`, `<h2>`, `<h3>` tags appropriately, making the content structure scannable through typography alone.
- **Required field indicators:** The asterisk (*) symbol for required form fields is a non-color cue.
- **Multiple contact methods:** Phone, email, physical address, and a contact form — all clearly labeled.
- **Icons with text labels:** Navigation menu items in the mega menu dropdowns pair icons with text labels (e.g., the icon next to "AI Automation" has the text "AI Automation" in a `<span>`). The icons have `aria-hidden="true"` and empty alt text, deferring to the text label — this is correct usage.
- **Skip to content link:** The page includes `<a class="skip-link screen-reader-text" href="#primary">Skip to content</a>`, which, while primarily a screen reader feature, indicates awareness of accessibility.

## Frustrations and Barriers

1. **Links in body text lack underlines.** Throughout the site, inline links (such as "contact@launchpadlab.com" on the Contact page, or "Learn More" within cards) are not underlined. They appear to be differentiated from surrounding text only by color. Since I can't reliably distinguish link colors from body text colors, I had to rely on context (e.g., knowing that an email address is usually a link) to identify clickable elements. This is my single biggest frustration.

2. **Tab active state may rely on color alone.** The "Problems We Solve" tab component uses an `is-active` class to visually differentiate the selected tab. Without inspecting the code, I couldn't confidently tell which tab was "selected" at a glance — I had to watch the content panel change.

3. **Case study green (#318500) backgrounds.** The Millennium Trust Company case study uses a pure green background that reads as muddy/brownish to me. While the white text atop it remained readable, the green-colored button text on the white CTA button blurred into an ambiguous brownish tone.

4. **Missing alt text on upward-arrow "increase" icons.** In the CDK Global case study, growth metrics use an arrow icon with `alt=""` and no textual stat value, leaving me to guess what improvement is being highlighted.

5. **Form validation uncertainty.** I can't confirm whether field-level validation errors use color alone (e.g., red borders) without text or icon indicators. If they do, I'd have no way to identify which field has an error after a failed submission.

6. **Award badge images lack alt text.** The scrolling award/badge logos section has images with empty `alt=""` attributes. I can see there are badge images from Clutch and other review sites, but I can't determine what specific awards or ratings they represent without meaningful alt text. This isn't color-specific, but it compounds the problem when badges might use red/green color coding for ratings.

## Goal Achievement

| Goal | Achieved? | Notes |
|------|-----------|-------|
| Find what LaunchPad Lab does | **Yes** | Clear from hero text, service cards, and descriptive copy throughout |
| Find how to contact them | **Yes** | Multiple clearly labeled options: nav link, form, footer address/phone, contact page cards |

## Would I Leave the Site?

**No, I would not leave the site.** I was able to achieve both of my goals. The site's overall structure, clear text labels, and content hierarchy allowed me to navigate effectively despite my color vision deficiency. The barriers I encountered were real but not blocking — they added friction rather than completely preventing access. The most significant risk would come if I needed to fill out the contact form and encountered color-only error validation, which could be a real blocker in practice.

That said, the site could be meaningfully improved for people with my condition. Underlining links, adding non-color indicators to tab states and form validation, and providing descriptive alt text for informational images would make the experience smoother and eliminate the guesswork I occasionally had to do.
