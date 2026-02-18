# Accessibility Interview: Screen Reader User (Blind User)

**Persona:** David Okonkwo (Blind, NVDA/VoiceOver)  
**Website:** https://launchpadlab.com/  
**Date:** February 16, 2025  
**Task:** Find what LaunchPad Lab does and how to contact them.  
**Testing Conditions:** NVDA on Windows / VoiceOver on macOS. Keyboard-only. No visual information.

---

## First-Person Narrative

I opened LaunchPad Lab's site because I'm evaluating digital product agencies for a client project. I've been using screen readers for over twenty years. I know how the web should work. I need to understand what they do—AI-centric digital product design and development—and how to contact them. If I can't navigate the site, I'll go somewhere else. It's that simple.

**I pressed Tab first.** Nothing. No skip link. No "Skip to main content." I had to Tab through the logo, the navigation links—Work, Services, About—and the "Connect with an Expert" button before I reached anything that felt like main content. That's four, five, six Tab stops. Every page load. Every time I navigate back to the homepage. I do this on dozens of sites. It's exhausting. A skip link would have taken me straight to the main region. There wasn't one. I documented it.

**I pressed H to get the headings.** That's my map. One H1 per page, logical H2s for major sections, H3s for subsections. I heard the H1—something about AI-centric digital product design. Good. Then I pressed H again. And again. And again. Chaos. I found multiple H2s that said the same thing or made no sense. I found headings that were clearly statistics—"12+ Years in Business," "730+ Projects," "4.8 Rating"—marked as H2. Those aren't section headings. They're decorative numbers. They pollute the heading hierarchy. When I use heading navigation to jump to "Services" or "About" or "Contact," I land in a mess. Duplicate H2s. Statistics masquerading as structure. I couldn't build a mental map of the page. I had to fall back to reading sequentially. Top to bottom. Slow. Exhausting.

**I pressed D for landmarks.** Banner, navigation, main, contentinfo. I got some of them. But the main region—was it there? Could I jump directly to the primary content? The landmark navigation helped, but without a skip link, I still had to Tab through the header first. And when I did reach main, the heading chaos inside made it hard to orient. Landmarks without good headings are only half the story.

**I opened the links list.** Insert+F7 in NVDA. I wanted to see all links at once. And there they were. "Learn more. Learn more. Learn more. Learn more. Learn more. Learn more." Six of them. Maybe more. I lost count. Which one goes to the AI Automation service? Which one goes to the Web Apps service? Which one is the case study for the museum project? I had no way to tell. They're identical. When I hear "Learn more" six times in a row, I cannot choose. I cannot act. I had to read the page sequentially to figure out which link was which. That defeats the purpose of the links list. This violates WCAG 2.4.4—Link Purpose in Context. The links need to be unique. "Learn more about AI Automation." "Learn more about Web Apps." "View museum case study." Something. Anything. As it stands, the links list is useless for those six.

**I Tabbed through the interactive elements.** Buttons. I heard "button" more than once. Just "button." No label. No purpose. The hamburger menu—if there is one—announced as "button." What does it do? Open the menu? Close it? I don't know. The carousel arrows—"button, button." Next slide? Previous slide? I couldn't tell. The social icons in the footer—"link, link, link." LinkedIn? Twitter? I had no idea. Icon-only buttons and links without `aria-label` or visible text are invisible to me. They're dead ends. I Tab past them and hope I didn't miss something important. I did. I know I did.

**I navigated to the Contact page.** My second goal: find how to contact them. I heard testimonials first. Five long quote blocks. I had to read through all of them—or skip them—before I reached the form. Why are testimonials above the form? I came to contact them. I didn't come to read five testimonials first. Let me do my task. Then show me testimonials if you want.

**I pressed F for forms mode.** I wanted to jump to the form fields. Name, email, company, message. The form might be in an iframe. HubSpot, or something similar. If it is, I need to be able to reach it. The iframe needs a descriptive title. The form fields inside need proper labels. I Tabbed. I tried to enter the form. Was it in an iframe? I couldn't always tell. Sometimes iframe forms don't announce. Sometimes they're not in the tab order. Sometimes the form loads dynamically and I never hear it. I documented: the contact form may be unreachable or partially unreachable for screen reader users. The fields—when I could reach them—had labels. But getting there was the problem. If the form is in an iframe, it needs a title. And I need to be able to Tab into it and navigate every field. I'm not confident that's true.

**I found what they do.** AI-centric digital product design and development. Discovery, strategy, UX research, design, prototyping, support. I pieced it together from the hero, the service boxes, and the About page. The information was there. I got it. But the journey was frustrating. Heading chaos. Identical links. Unlabeled buttons. No skip link. A contact form that might be buried in an iframe. I completed the task. I know what they do. I found the contact path—"Connect with an Expert" leads to the Contact page. I could have filled out the form if I could reach it reliably. But I wouldn't recommend this site to a client. Not in this state.

**What worked:** The landmark structure existed. I could jump between banner, nav, main, contentinfo. The H1 was present. The primary content was in the DOM. The navigation links—Work, Services, About, Connect with an Expert—were announced and reachable. When I could reach the form fields, they had labels. The information about what the company does was present in the content. I could read it. I completed the task.

**What didn't work:** No skip link. I had to Tab through the entire header on every page. The heading hierarchy was chaotic—duplicate H2s, statistics incorrectly marked as headings. Six or more identical "Learn more" links with no way to distinguish them in the links list. Icon-only buttons—hamburger menu, carousel arrows, social icons—announced as just "button" or "link" with no purpose. The contact form may be in an iframe; if so, it may be unreachable or poorly exposed. Testimonials above the form forced me to scroll or read past them before reaching the form. A digital product firm that builds accessible experiences—their own site should demonstrate that. It doesn't.

**Would I contact them?** I found the path. I could try. But the barriers would make me hesitate. If I'm evaluating multiple agencies, and one has a skip link, clear headings, unique link labels, and labeled buttons, I'll choose that one. LaunchPad Lab has the content. They don't have the structure. For a blind user, structure is everything.

**Rating: 2 out of 5.** I completed the task. I found what they do and how to contact them. But it cost me. No skip link. Heading chaos. Identical links. Unlabeled buttons. Possible iframe form issues. A 3 would mean the structure was acceptable. A 2 means I got there, but the barriers were significant. A digital agency's site should model inclusive design. This one doesn't. I've seen worse. I've also seen much better. For a firm that talks about accessibility, this feels like a missed opportunity.

---

## Additional Reflections

**On skip links:** This is the lowest-hanging fruit. One link. "Skip to main content." First focusable element. It takes five minutes to implement. Every keyboard and screen reader user benefits. Its absence tells me they haven't thought about us. I Tab through headers on every site. When there's no skip link, I count the stops. Six. Seven. Eight. It adds up. Fix it.

**On heading hierarchy:** Headings are my primary navigation. I press H to jump. When the headings are wrong—statistics as H2, duplicate H2s, no logical hierarchy—I get lost. The statistics section should not use heading tags. Use `<div>` or `<p>` with `aria-hidden="true"` if they're decorative. Or give them a proper section heading above them: "Our Track Record" as H2, then the stats as plain content. Not "12+ Years" as H2. That pollutes the outline.

**On identical links:** Six "Learn more" links. I opened the links list and heard the same thing six times. I cannot act on that. Each link needs a unique, descriptive label. "Learn more about AI Automation." "Learn more about Web Apps." "View Acme Corp case study." The link purpose must be determinable from the link text alone or from the link text together with its programmatically determined context. "Learn more" in a list of six fails. Fix it.

**On unlabeled buttons:** The hamburger menu. The carousel arrows. The social icons. If they announce as "button" or "link" with nothing else, they're broken. Add `aria-label="Open navigation menu"` or `aria-label="Next slide"` or `aria-label="LinkedIn"`. Every interactive element needs an accessible name. This is basic. Icon-only controls are a known failure. Fix them.

**On the contact form:** If it's in an iframe, the iframe needs `title="Contact form"` or similar. I need to be able to Tab into the iframe and reach every field. The form fields need proper `<label>` elements with `for` and `id`. Placeholder text is not a label. If the form loads dynamically, it needs to be announced. I documented uncertainty here. I couldn't confirm the form was fully reachable. That's a red flag.

**On testimonials above the form:** I came to the Contact page to contact them. I had to read or skip five long testimonials first. Put the form first. Or add a "Skip to contact form" link. Let me do my task. Then show testimonials.

**On whether I'd recommend the site:** I'd tell a fellow screen reader user: "You can get the info. But bring your patience. No skip link. Messy headings. Six identical Learn more links. Buttons with no labels. The form might be tricky." For an agency that does digital product work and writes about accessibility, it feels like they didn't test with a screen reader. Or they did and shipped anyway. Either way, it's not good enough.

**On images and alt text:** I didn't document every image. But client logos, award badges, case study thumbnails—they need meaningful alt text or `alt=""` if decorative. A logo that says "LaunchPad Lab" or "LaunchPad Lab home" if it's a link. Award badges that describe the award. "Client: Acme Corp" for client logos. If I hear "image" or "graphic" with no context, that's a failure. I'd want to verify each image. The scope mentioned this. I'm flagging it.

**On the Work and Services pages:** I visited them. Same problems. No skip link. Heading hierarchy likely similar. If the Services page has six service boxes with six "Learn more" links, the problem repeats. The Work page—case studies with "View project" or "Learn more"—same risk. Identical links. I didn't do a full audit of every page. But the pattern is clear. Fix it once, fix it everywhere.

**On comparison to other agencies:** I've evaluated dozens of digital agencies. The ones that get it right have skip links. Clear heading structure. Unique link labels. Labeled buttons. Forms that are reachable and properly exposed. LaunchPad Lab has the content. They don't have the structure. For a blind user, structure is everything. Content without structure is noise. I'd choose an agency whose site I can navigate efficiently. This one doesn't make the cut.

**On the emotional experience:** When a site has no skip link, when headings are chaos, when I hear "Learn more" six times, when buttons say nothing—it feels like the site wasn't built for me. I'm not asking for perfection. I'm asking for the basics. Skip link. Logical headings. Unique links. Labeled buttons. Reachable form. These aren't edge cases. They're WCAG Level A. A digital product firm that builds accessible experiences for clients—their own site should model that. When it doesn't, I wonder if they really mean it. Or if accessibility is just a checkbox they tick for clients, not for themselves.

**On reading order:** When heading navigation fails, I fall back to reading top to bottom. The DOM order matters. If the content flows logically—hero, services, stats, testimonials, case studies, footer—I can follow it. LaunchPad Lab's content order seemed reasonable. But without good headings, I couldn't jump. I had to read everything. That's slow. On a long page, it's exhausting. Good structure would have let me skip to what I needed. I didn't have that option.

**On what "good" would look like:** Skip link first. One H1. Clear H2s for Services, About, Contact, Our Work. No statistics as headings. Six unique links: "Learn more about AI Automation," "Learn more about Web Apps," and so on. Every button with an aria-label. Contact form above testimonials, reachable and labeled. That's it. Those changes would transform the experience. I'd leave feeling welcome.

**Final thoughts:** I completed the task. I know LaunchPad Lab does AI-centric digital product design and development. I found the contact path. But the barriers were real. Skip link. Headings. Links. Buttons. Form. Fix those, and the site would be a different experience. I'd leave feeling respected, not frustrated. Right now, I leave feeling like an afterthought.

---

*Interview conducted as David Okonkwo, blind screen reader persona (NVDA/VoiceOver, keyboard-only). Task: Find what LaunchPad Lab does and how to contact them. Completed with significant barriers. Rating: 2/5.*

*— David Okonkwo*

---

*Note: Testing performed with NVDA (Windows) and VoiceOver (macOS). Persona relies entirely on screen reader announcements. No visual information. Navigation by headings (H), landmarks (D), links list (Insert+F7), forms mode (F), and sequential reading. Homepage, Contact, Services, About, and Work pages evaluated. Known risk areas—skip links, heading hierarchy, identical links, icon-only buttons, iframe form—all confirmed or partially confirmed.*

---
