# Interview: Marcus Webb — Blue-Yellow Color Blind (Tritanopia)

**Persona:** Marcus Webb, 42, small business owner with Tritanopia  
**Site Tested:** https://launchpadlab.com/  
**Goals:** Find what LaunchPad Lab does, find how to contact them  

---

## My Experience

I landed on the LaunchPad Lab homepage and the first thing I noticed was a large hero banner across the top of the page. The background is supposed to be blue—I know that conceptually—but what I actually see is more of a washed-out grayish-pink tone. It doesn't look broken exactly, but it doesn't have the punchy, professional impact I imagine they're going for. The white text on top of it—"AI Innovation. Digital Solutions. Results that Matter."—is still readable because the gray-pink background is dark enough to create contrast with white. So I could read the headline and the description underneath about AI consulting and product development. That told me right away what they do. Good start.

There's a button in the hero area that says "Connect with an Expert." It appears to be a white-outlined or white-filled button on the blue background. For me, it reads fine because the button has clear text and a distinct shape—it looks like a button regardless of the background color. I clicked it and it took me to the contact page. That's a clear win.

### Navigation

The top navigation bar has the items: Services, Technologies, Industries, Our Work, About Us, Insights, and Contact. I could read all of these because they're text-based. However, I noticed that the "Contact" link on the far right seems to be styled differently from the other navigation items—it appears to have a distinct visual treatment, possibly a different background or color to make it stand out as a call to action. For me, whatever color distinction they're using doesn't register the way it's intended. The "Contact" link just looks like a slightly different shade of gray compared to the other links. I was able to find it because it's the last item in the navigation bar and the text clearly says "Contact," but if I were quickly scanning and relying on a color highlight to draw my eye to it, I might gloss over it. The text label saved me here.

When I hovered over "Services," a mega menu dropped down with six service areas: AI Automation, Web App Development, Mobile App Development, Salesforce Development, Product Strategy & Design, and Managed Services & Support. Each had a small icon next to it. The icons are black SVGs on a white background, which works well for me—no color dependency there. There's also a blue "View Services" button in the mega menu dropdown. It looked gray to me, not blue, but it was still clearly a button because of its shape and the text label. I could interact with it.

### Understanding What They Do

Scrolling down the homepage, I came across a section labeled "Your Strategic AI Partner" with a video embed and a description. The text explained that LaunchPad Lab combines product design and development with AI consulting. This section was easy to read—dark text on a light background, good contrast, clear typography. No issues here.

Below that was a section called "Make AI Your Competitive Advantage" with six service cards. Each card has an icon, a heading (like "AI Automation & Agentic AI," "Web Application Development," etc.), a brief description, and a "Learn More" link with an arrow icon. The cards themselves have a blue accent line below the heading, rendered with `border-color: #2363BB`. To me, those lines appear as a muted gray. They're decorative and don't carry essential information, so this isn't a blocker—but I do lose the visual branding effect. The "Learn More" text on each card is accompanied by an arrow icon, which is how I identified them as clickable rather than relying on the blue link color. That arrow icon was critical for me.

Further down, there's a tabbed section called "Ship Game-Changing Digital Products to Market Fast" with tabs for Operational Efficiency, Modern Technology, Customer Engagement, Scalable Solutions, Expansive Resources, and Speed to Market. The active tab appears to have some kind of visual indicator—likely a blue highlight or underline. For me, the distinction between the active tab and inactive tabs was not immediately obvious based on color alone. I had to look more carefully at which tab appeared slightly different in weight or had a preview description visible. The tab component does use proper ARIA roles (`role="tab"`, `aria-selected`), which is good for accessibility tooling, but visually the color-based active indicator didn't pop for me. I ended up relying on which tab's content was displayed to figure out which one was active.

The statistics section—"12+ Years in Business," "730+ Projects," "240+ Clients"—was perfectly accessible. Large black numbers on a light background, with descriptive text below. No color dependency at all. Clear and effective.

### The "Our Signature Approach" Section

There's a section with a dark background (labeled as "dark blue" in the design) that describes their process: Discover, Deliver, Release. For me, the dark blue background renders as a very dark gray, nearly charcoal. The white text on top is perfectly readable. The headings and sub-items (Research & Define, Development, QA Testing, Deploy, Ongoing Support) are all text-based. No issues here at all.

### Case Studies

The case studies carousel was interesting. Each case study card has a colored background—I saw three: one that I'm told is purple (#30327d), one that's blue (#006cfa), and one that's green (#318500). The purple one looked like a dark gray to me, the blue one looked like a lighter gray, and the green one looked distinctly different (I can still perceive green to some degree, though it looks slightly different). The key point is that each case study is differentiated by its company logo (Prosci, CDK Global, Millennium Trust Company), headline text, and the statistics within. I didn't need color to tell them apart. The white text on these colored backgrounds was legible because the backgrounds, even appearing as grays to me, were dark enough to maintain contrast with white text.

However, inside the CDK Global case study, there are two metrics that use an "increase" arrow icon (`increase.svg`) instead of a numerical value, with empty alt text (`alt=""`). Those icons conveyed no information to me—I just saw an arrow with no context. The accompanying text said "Improved Sales Team Alignment" and "Streamlined Discovery & Quoting Process," so I understood the general idea, but the missing icon labels were a gap.

### The Contact Form

At the bottom of the homepage, there's a "Let's Build Something Great" section with a contact form. The form has clear text labels above each field: First Name, Last Name, Company Email, Company, and "How Can We Help You?" Required fields are marked with an asterisk (`*`), not just a color indicator—that's exactly what I need. The form uses Ninja Forms and includes a reCAPTCHA and a Submit button.

I also navigated to the dedicated `/contact` page, which has a similar header ("Ready to Build Something Great?") on the same blue background that appears grayish to me. The page has the same contact form plus three additional contact method cards: Email (contact@launchpadlab.com), Call ((312) 888-9651), and Connect with Us on LinkedIn. Each card has an icon and a text-labeled link. The blue accent lines on these cards appeared gray to me, but the headings and link text were clear. I could use any of these contact methods.

### Footer

The footer has a dark background with white text. It lists their address (2045 W Grand Ave Ste B, Chicago, IL 60612), phone number, and social media links (Facebook, Instagram, LinkedIn). The social media links include both an icon and a text label, which is perfect—I don't need to rely on recognizing the icon color to know what platform it links to.

There's an AgencyReview badge in the footer with a star rating. The star is yellow (#eab308), which to me looks like a very faint, washed-out pinkish-gray. I almost missed it as a star—it blended into the white badge background. But the "10.0" text rating next to it was clear and large, so I understood the rating regardless.

### What Worked Well

- **Text-based navigation:** Every navigation item has a clear text label. I never had to guess what a link was based on color.
- **Headings and structure:** The page is well-organized with clear headings (h1, h2, h3) that let me scan the content structure without relying on color sections.
- **Required field indicators:** The contact form uses asterisks, not just color, to mark required fields.
- **Button text and shapes:** CTAs like "Connect with an Expert," "Learn More," and "Submit" are clearly labeled and shaped as buttons, not just colored text.
- **Icons paired with text:** Navigation menu items and footer social links pair icons with text labels.
- **Arrow icons on links:** The "Learn More" links on service cards include arrow icons, helping me identify them as interactive elements.

### What Didn't Work Well

- **Blue brand elements appear flat:** The entire blue visual identity (#1E60BD, #2363BB, #006cfa) renders as various shades of gray for me. The site loses its visual punch and branded feel. Sections that are supposed to feel distinct (blue hero, blue buttons, blue accent lines) all look gray and blend together.
- **Tab active state is color-dependent:** The active tab in the "Problems We Solve" section relies on a color change to indicate selection. I had difficulty quickly identifying which tab was active.
- **Blue CTA buttons lack non-color emphasis:** The `button-blue-base` buttons (like "View Services" in the mega menu) appear as gray buttons. While the text is readable, they don't visually "pop" as primary calls to action the way they're intended to.
- **Yellow star in rating badge:** The AgencyReview star rating uses yellow, which nearly disappears for me.
- **Case study "increase" icons have empty alt text:** These convey directional information (improvement/increase) without a text alternative.
- **Award badge images have empty alt text:** The Clutch/award badges in the second logo carousel all have `alt=""`, so I get no information about what awards they've received.

### Did I Achieve My Goals?

**Goal 1: Find what LaunchPad Lab does.** Yes. The hero text, the "Your Strategic AI Partner" section, the service cards, and the process section all clearly communicated what they do using text and layout. LaunchPad Lab is a digital product development consultancy that builds AI-powered solutions, web apps, mobile apps, and Salesforce integrations. They've been around since 2012 and have worked with 240+ clients. I got all of this without needing to perceive blue or yellow.

**Goal 2: Find how to contact them.** Yes. The "Contact" link in the navigation was identifiable by text. The hero CTA "Connect with an Expert" took me to the contact page. The contact form has clearly labeled fields. The footer provides an address, phone number, and social links. The contact page additionally provides an email address and phone number as separate cards. Multiple pathways, all text-accessible.

### Would I Have Left the Site?

No. I would not have left. While the blue visual branding is lost on me and some elements are less visually prominent than intended, I was able to accomplish both of my goals. The site relies heavily on text labels, clear headings, and good layout structure, which compensates for the color issues. The tab component gave me the most trouble, but it wasn't a showstopper. Overall, I'd say this site is *usable* for someone with tritanopia, but the visual experience is significantly dulled—the brand's blue identity, which is clearly central to their design, is almost entirely invisible to me.
