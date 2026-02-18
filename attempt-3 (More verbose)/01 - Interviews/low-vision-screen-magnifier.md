# Accessibility Interview: Low Vision User (Screen Magnifier)

**Persona:** Elena Vasquez (Low Vision, Screen Magnifier)  
**Website:** https://launchpadlab.com/  
**Date:** February 16, 2025  
**Task:** Find what LaunchPad Lab does and how to contact them.  
**Test Conditions:** Browser zoom at 200%, 300%, and 400%. Primary testing at 300%.

---

## First-Person Narrative

I opened LaunchPad Lab's site because I'm researching AI-focused digital product firms in Chicago. I need to understand what they do and how to reach them. I've used a screen magnifier for eight years—macular degeneration—and I zoom to 250–300% routinely. Sometimes 400% for dense text. I set my browser to 300% and hit the homepage.

**The sticky header ate my viewport.** Right away, I saw the problem. At 300% zoom, the header—logo, Work, Services, About, "Connect with an Expert"—stays fixed at the top. It doesn't shrink. It doesn't collapse when I scroll. It just sits there, taking up what felt like a third of my screen. Maybe more. I'm used to seeing only a small window of the page at once. That's normal. But when a third of that window is a header I've already seen, I'm getting less than half the content I should. I scrolled down to read the hero text. The header followed me. I scrolled again. Same thing. Every scroll, I saw maybe one or two new lines of content. The rest was header. I felt like I was wading through molasses. A digital product firm should know better. At 400%, it was worse. The header consumed nearly 40% of my viewport. I could barely see anything below it.

**Horizontal scrolling appeared almost immediately.** I tried to read the hero section. "AI-Centric Digital Product Design & Development." The text didn't reflow. The layout stayed in multiple columns. I had to scroll horizontally to see the full headline. That's the cardinal sin for magnifier users. I shouldn't have to pan sideways to read. I did it anyway, because I needed the information. But every horizontal scroll is a failure. I lose my place. I forget where I was. I have to reorient. I scrolled right, saw more of the hero. Scrolled left to get back. It's exhausting before I've even started.

**The six service boxes were a maze.** I knew from the structure that there were six services—AI Automation, Web & Mobile Development, Salesforce, Digital Product Strategy, Managed Services, and so on. At 300% zoom, I could see maybe two boxes at a time. At 400%, maybe one and a half. The grid didn't collapse to a single column. It stayed multi-column. I had to scroll horizontally to see the third, fourth, fifth, sixth boxes. I'd read one, pan right, lose context, pan back to remember which one I'd just read. "Am I on AI Automation or Web & Mobile?" I had to check the heading again. The content didn't reflow. WCAG 1.4.10 says content must reflow at 400% zoom. It didn't. I was forced to pan. I documented every instance. Service boxes: horizontal scroll. Statistics section: horizontal scroll. Award badges: horizontal scroll. Client logos: horizontal scroll. It was everywhere.

**I lost context constantly.** When I scrolled down to read the testimonials, the section heading disappeared. I couldn't see it anymore. I was in a block of italic text. "Is this still a testimonial? Or did I scroll into the case studies?" I had to scroll back up to check. No persistent section labels. No sticky subheadings. No way to know where I was. Long pages become disorienting when you only see a sliver at a time. I rely on landmarks. Headings. Clear breaks. This site gave me some of that, but not enough. When the header is eating 30–40% of the viewport and the content doesn't reflow, I'm constantly guessing.

**Finding "Connect with an Expert" was hard.** I knew it was in the nav. But the nav was inside that sticky header. At 300% zoom, I could see the logo and maybe one or two nav items. "Connect with an Expert" might have been off to the right. I had to scroll horizontally within the header to find it. Or maybe it was in a hamburger menu—I'm not sure. The point is, I shouldn't have to hunt. A contact CTA should be obvious. Large. High contrast. Easy to find when zoomed. I eventually found it. I clicked. I landed on the Contact page.

**The Contact page repeated the problems.** Testimonials above the form. Five of them. Long blocks. At 300% zoom, each testimonial took multiple scrolls. The sticky header was still there, still eating my viewport. I scrolled and scrolled. When did the testimonials end? When did the form start? I lost track. I had to scroll down, then back up, to find where the form began. The form itself—when I finally reached it—had labels and fields. But the layout didn't reflow. If there were multiple columns in the form, I'd have had to pan horizontally. I don't remember if I did. I was too tired to notice. I filled out what I could see. Name, email, company, message. I hope I didn't miss anything.

**What I learned about what they do.** Despite everything, I pieced it together. AI-centric digital product design and development. Discovery, strategy, UX research, design, prototyping. Managed services. They've done 730+ projects, 12+ years, 4.8 rating. I got that from the statistics—when I could see them. The service boxes, when I could pan to them. The hero, when I could scroll horizontally to read it. The information was there. I found it. But it cost me.

**What worked.** The headings helped when I could see them. The structure wasn't completely broken. I could eventually find the contact form. The "Connect with an Expert" CTA did lead to contact. The content was there. I didn't give up.

**What didn't work.** The sticky header. The horizontal scrolling. The multi-column grids that refused to reflow. The constant context loss. The small touch targets—I'm not sure I measured them, but the nav items felt cramped. At 300% zoom, everything feels smaller than it is. I need 44×44px minimum. I had misclicks. I had to try again. The contrast—some text was light gray. Harder to see when magnified. Not impossible, but not ideal.

**Would I contact them?** I found the form. I could fill it out. I know what they do. So yes, I might reach out. But I'd do it with frustration. A digital product design firm—one that builds accessible experiences for clients—should support zoom and reflow. Their own site forces horizontal scrolling. Their sticky header blocks a third of my screen. They've either not tested at 200% zoom, or they've ignored the results. That doesn't inspire confidence. If they can't make their own site work for me, what will they do for my project?

**Rating: 1.5 out of 5.** I completed the task. I found what they do. I found how to contact them. But the experience was punishing. Horizontal scrolling is a deal-breaker. The sticky header is a major barrier. Content that doesn't reflow at 400% violates WCAG. I got through because I've had years of practice. A first-time visitor with low vision might not. They might close the tab. They might assume the site is broken. I wouldn't blame them. A 2 would mean it was difficult but tolerable. A 1 would mean I nearly gave up. I'm in between. I made it, but I don't feel welcome. I don't feel considered.

---

## Additional Reflections

**On the sticky header:** This is the thing I want them to fix first. At 300% zoom, it consumed 30–40% of my viewport. Every scroll, I saw less new content than I should. It never shrank. It never collapsed. It just sat there, a constant obstacle. Other sites minimize the header on scroll-down. Or they use a thin bar with just the logo. Or they let it scroll away. LaunchPad Lab's header stays full-size. For magnifier users, that's hostile. Fix it. Shrink it. Collapse it. Or let it scroll off. Give me my viewport back.

**On horizontal scrolling:** I documented every instance. Hero. Service boxes. Statistics. Awards. Client logos. Testimonials. Case studies. The layout doesn't reflow. At 200% zoom, horizontal scrollbars appeared. At 300% and 400%, they were constant. I had to pan to read. I had to pan to see. That's a failure. WCAG 1.4.10 is clear: no horizontal scrolling for text content at 400% zoom. This site fails. The fix is reflow. Single column. Flexible layouts. No fixed widths that cause overflow. It's not that hard. Responsive design should handle this. They've built for desktop and mobile. They need to build for zoom.

**On losing context:** When you see only a sliver of the page, you need landmarks. Section headings that persist. Skip links. Clear labels. "You are here: Services > AI Automation." Something. This site has headings, but they scroll away. When I'm deep in a testimonial block, I don't know if I'm still in testimonials or in case studies. I had to scroll back to check. That's inefficient. That's disorienting. Sticky section labels would help. Or a progress indicator. Or just shorter sections so I don't get lost.

**On touch targets:** I didn't measure precisely, but the nav links felt small. The "Connect with an Expert" button—was it 44×44px? I'm not sure. At 300% zoom, small targets become smaller in relative terms. I need to hit them accurately. I had misclicks. I had to try again. Form fields, buttons, links—they should all meet the minimum. I'd want a proper audit. But from experience, they felt cramped.

**On what would have helped:** Reflow. Single column at 400%. No horizontal scrolling. A header that shrinks or collapses. Persistent section labels. Larger touch targets. Higher contrast. That's the list. Those changes would have transformed my experience. I would have left feeling respected. Instead, I left feeling exhausted and overlooked.

**Final thoughts:** I'm used to sites not being built for me. I've developed strategies. I zoom. I pan when I have to. I scroll back to reorient. I persist. I got through LaunchPad Lab because I've had years of practice. But a first-time visitor with low vision might not. They might assume the site is broken. They might never contact the company. That's a loss for everyone. I hope this feedback helps. Fix the reflow. Fix the header. Make the site work for magnifier users. It's not optional. It's a requirement.

**On testing at different zoom levels:** I tried 200% first. Horizontal scrollbars appeared on the homepage. The hero didn't reflow. I bumped to 300%—my usual working zoom—and it got worse. The header dominated. The service grid stayed in multiple columns. At 400%, I could see maybe one service box at a time, and I still had to pan right to see the others. The layout never adapted. It was as if the site was built for one viewport size and never tested beyond it. A digital product firm should test at 200%, 300%, 400%. They clearly haven't.

**On the statistics and award badges:** I wanted to see the numbers—12+ years, 730+ projects, 4.8 rating. Credibility markers. But the statistics section was in a row. At 300% zoom, I could see maybe two numbers. I had to scroll horizontally to see the rest. Same with the award badges. They were laid out in a grid. I panned. I lost my place. I had to pan back to remember which badge I'd just seen. Visual content that should be scannable became a chore.

**On the hero section specifically:** The headline "AI-Centric Digital Product Design & Development" is important. It tells me what they do. But it didn't fit in my viewport. I had to scroll right to read the full line. The supporting text—whatever was underneath—same problem. The CTA button might have been there. I'm not sure I saw it without panning. The hero should reflow. One column. Full width of my narrow viewport. No horizontal scroll. That's basic.

**On comparison to other sites:** I've used sites that get it right. Government sites. Some banks. They reflow. The header shrinks. I can read everything without panning. LaunchPad Lab isn't the worst—I've seen sites that break completely at 200%—but for a firm that does digital product design, it's embarrassing. They should be the example. Instead, they're the cautionary tale. "Look at LaunchPad Lab. They build AI products. Their own site doesn't work for magnifier users." That's the story.

**On what "good" would look like:** Single column at 400% zoom. No horizontal scrolling. Header that shrinks to 15–20% of viewport or scrolls away. Skip link at the top. Persistent section labels. Touch targets that meet 44×44px. Contrast that holds up when magnified. That's the list. Those changes would have taken my experience from punishing to acceptable. Maybe even good. I would have left thinking, "They considered users like me." Instead, I left thinking, "They didn't."

**One last thing:** I completed the task. I found what they do. I found the contact form. I could have submitted an inquiry. But I'm not sure I will. The experience left a bad taste. If their own site doesn't support zoom and reflow, what does that say about the products they build for clients? I'd want to ask them, in a discovery call, "Do you test for low vision users? Do you test at 300% zoom?" If they say no, I'd have my answer. If they say yes, I'd wonder why their site fails. Either way, the site itself didn't make me feel welcome. Fix it.

**On the emotional toll:** I want to be clear: this isn't just about inconvenience. When a site forces horizontal scrolling and a header blocks half my view, it feels like the site wasn't built for me. It feels like I'm an afterthought. I'm a freelance copy editor. I research companies. I need to access information like everyone else. When I encounter barriers like this, I wonder: did anyone consider users with low vision? Did anyone zoom to 300% and try to use the site? The answer, from my experience, seems to be no. That's disappointing. Especially from a firm that claims to build digital products. Their own site should demonstrate their values. Right now, it doesn't.

**On the Work and Services pages:** I didn't spend much time on the Work page or the full Services page. I knew from the homepage structure what to expect—more grids, more multi-column layouts. If the homepage didn't reflow, those pages wouldn't either. I got the gist from the homepage: they do AI automation, web and mobile development, Salesforce, product strategy, managed services. That was enough. I prioritized finding the contact form. I didn't have the energy to pan through every case study. A site that reflowed would have let me explore. This one didn't.

**On recommending the site:** I would not recommend this site to a colleague with low vision. I'd say: "The information is there, but you'll have to fight for it. Horizontal scrolling everywhere. The header blocks a third of your screen. Content doesn't reflow. If you need to contact them, you can—but bring patience." For an agency that builds digital products, that's a failing grade. They should be the standard. They're not.

**On the client logos section:** I wanted to see who they've worked with—Kawasaki, Harvard, Northwestern, Whirlpool. Social proof matters. But the logos were in a row or grid. At 300% zoom, I could see a few. To see the rest, I had to pan. Again. Another horizontal scroll. Another moment of losing my place. Even visual content—logos, images—was locked behind a layout that didn't adapt. The fix is the same: reflow. Stack the logos vertically if needed. Let me scroll down, not sideways.

**Summary:** I completed the task. I found that LaunchPad Lab does AI-centric digital product design and development—discovery, strategy, UX, design, prototyping, managed services. I found the contact form via "Connect with an Expert." But the journey was punishing. Reflow, header, horizontal scroll—fix those three things, and the site would transform for magnifier users like me.

---

*Interview conducted as Elena Vasquez, low vision (screen magnifier) persona. Task: Find what LaunchPad Lab does and how to contact them. Completed with significant effort. Rating: 1.5/5.*

*— Elena Vasquez*

