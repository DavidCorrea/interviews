# Accessibility Interview: Voice Control User

**Persona:** Marcus Webb (ALS, Voice Control / Dragon NaturallySpeaking)  
**Website:** https://launchpadlab.com/  
**Date:** February 16, 2025  
**Task:** Find what LaunchPad Lab does and how to contact them.  
**Testing Conditions:** Voice-only navigation. No keyboard or mouse. Commands: "Click [label]," "Scroll down," "Show numbers."

---

## First-Person Narrative

I'm Marcus. I'm 52, I live in Chicago, and I have ALS. I've used voice control for five years. I can't use a keyboard or mouse anymore. I speak. That's it. I say "Click Contact" and it works—if there's one Contact link. I say "Click Learn More" and it breaks—there are six of them. I'm researching digital product agencies for a project at my organization. I opened LaunchPad Lab's site because I'd heard they're AI-focused. I need to find what they do and how to contact them. All by voice. If I can't, I'll find another agency. It's that simple.

**I said "Click Connect with an Expert."** That worked. One link. Unique label. The system found it. I landed on the Contact page. Good. I could get there. But I wanted to understand their services first. I said "Click Services." It worked. I saw their navigation—Work, Services, About, Connect with an Expert. Those are unique. I can target them. That's the baseline. I'm not asking for miracles. I'm asking for labels I can speak.

**Then I hit the "Learn More" wall.** I scrolled down. I saw six service boxes. AI Strategy. Product Development. Web Apps. AI Automation. UX Research. Something else. Each one had a link. I said "Click Learn More." The system said "Which one?" Or it clicked the first one. I don't remember which. I said it again. "Click Learn More." Same thing. Which one? I wanted to learn more about AI Automation. I had no way to say that. The link text was just "Learn More." Six times. Identical. I couldn't distinguish them. I had to fall back to "Show numbers." The system overlaid numbers on every interactive element. I counted. Learn More 1, Learn More 2, Learn More 3, Learn More 4, Learn More 5, Learn More 6. I said "Click Learn More 3." I hoped that was the right one. It wasn't. I got Product Development. I wanted AI Automation. I had to try again. "Click Learn More 5." Maybe. I shouldn't have to guess. I shouldn't have to count. Each link should have a unique label. "Learn more about AI Automation." "Learn more about Product Development." I could say that. The system could find it. As it stands, "Learn More" six times is a barrier. I documented it.

**The hamburger menu.** I don't know if there's a hamburger menu on desktop. On mobile, there usually is. I didn't test mobile. But I've seen this pattern everywhere. A button. An icon. Three lines. No text. I say "Click" and there's nothing to say. "Click button"? The system might find it. But "button" could be anything. The carousel arrows—same problem. Left arrow. Right arrow. No visible label. I said "Click Next." Nothing. I said "Click Previous." Nothing. Maybe they have aria-labels. Maybe they don't. If they do, and the label is "Next slide," I'd have to say "Click Next slide." I didn't know that. I saw an arrow. I would say "Click arrow." That doesn't work. Icon-only buttons are dead ends. I cannot speak a command that targets them. I had to use "Show numbers" again. I found a number. I said "Click 47" or whatever. The carousel moved. I'd activated something. But I shouldn't have to overlay numbers on the entire page just to click a carousel arrow. Give it a label. "Next slide." "Previous slide." Visible or not—I need something to say.

**The social icons.** Footer. LinkedIn. Twitter. Maybe others. I saw icons. No text. I said "Click LinkedIn." Nothing. I said "Click Twitter." Nothing. The links might have aria-labels. If they do, and the label is "Follow us on LinkedIn," I'd have to say that. I didn't know. I said "Click LinkedIn" because that's what I see. Or what I'd expect. If the accessible name doesn't match what I'd say, the command fails. Accessible names must match visible text. If there's no visible text, the accessible name must be something I'd naturally say. "LinkedIn." "Twitter." Not "Social media link 1." I couldn't reach the social icons by voice. I gave up. They're not critical for my task. But they're there. They're unusable. I documented them.

**The contact form.** I got there. "Connect with an Expert" worked. I landed on the Contact page. Testimonials first. Five long blocks. I had to scroll past them. Or say "Scroll down" five times. I wanted the form. I didn't want to read testimonials. Let me do my task. Then show me testimonials. I scrolled. I found the form. Name. Email. Company. A dropdown. Message. I said "Click Name." It worked. The field focused. I said "Click Email." It worked. The labels were there. They matched. I could speak them. Good. I said "Click Submit" or "Click Send" or whatever the button said. I don't remember the exact text. If the button said "Submit" and had aria-label="Send form," I would have said "Click Submit." The system might not have found it. The accessible name would be "Send form." I'd have to say "Click Send form." I didn't know that. I got lucky. Or the button used its visible text. I'm not sure. I documented: verify that the submit button's accessible name matches its visible text. Mismatches cause failed commands. I've seen it on other sites. "Click Submit" does nothing. "Click Send form" works. I had to discover that by trial and error. Labels should match what you see.

**What they do.** I pieced it together. AI-centric digital product design and development. Discovery. Strategy. UX research. Design. Prototyping. Support. I got it from the hero, the service boxes, and scrolling. The information was there. I could read it. Voice control lets me scroll. It lets me read. It lets me click—when the labels work. The content was accessible. The structure wasn't always.

**What didn't work.** Six identical "Learn More" links. I said "Click Learn More" and the wrong one activated—or the system asked which one. I had to use "Show numbers." That's a fallback. It's not a solution. I shouldn't need to overlay numbers on the page to distinguish links. Unique labels are required. Icon-only buttons—carousel arrows, social icons, possibly a hamburger menu—had no speakable label. I couldn't click them by name. I had to use "Show numbers" or skip them entirely. Accessible name mismatches—I didn't confirm every one, but the persona doc warned about them. Buttons that say "Submit" but have aria-label="Send form" break "Click Submit." I need consistency. Hover-dependent content—I can't trigger hover by voice. If dropdowns or tooltips only appear on hover, they're inaccessible. I didn't encounter obvious hover traps. But the risk is there. Everything must be reachable by focus and click.

**Would I contact them?** I found the path. "Connect with an Expert" worked. The form was reachable. I could have filled it out. But the journey was frustrating. "Learn More" six times. Icon-only buttons. Having to use "Show numbers" as a crutch. A digital product design firm—one that builds AI-centric experiences—should know that voice control users exist. We're not edge cases. Dragon, Voice Control on Mac, Windows Speech Recognition—millions of people use these tools. If their own site has six identical "Learn More" links and icon-only buttons with no labels, what does that say about the products they build? I'd hesitate. I'd look at other agencies. One with unique link labels and labeled buttons would get my business first.

**Rating: 2 out of 5.** I completed the task. I found what they do and how to contact them. But it cost me. I had to use "Show numbers" to distinguish "Learn More" links. I couldn't click carousel arrows or social icons by name. I might have hit an accessible name mismatch on the submit button—I'm not sure. A 3 would mean the labels were mostly unique and icon-only elements were labeled. A 2 means I got there, but I had to work around the design. I shouldn't have to count "Learn More 3" to reach the right service. I shouldn't have to overlay numbers to click an arrow. A digital agency's site should model inclusive design. This one doesn't. Not for voice control.

---

## Additional Reflections

**On "Show numbers" as a fallback:** When labels are duplicated or missing, voice control overlays numbers. I say "Click 23" and it works. But it's a design failure. I shouldn't need it. Unique, descriptive labels make "Show numbers" unnecessary. Every time I have to use it, the site has failed me. Document it. Fix it.

**On identical links:** Six "Learn More" links. I said "Click Learn More" and got "Which one?" or the wrong one. Each link needs a unique label. "Learn more about AI Strategy." "Learn more about Product Development." "View Acme Corp case study." I could say that. The system could find it. "Learn more" six times is a barrier. It violates WCAG 2.4.4. Fix it.

**On icon-only buttons:** Hamburger menu. Social icons. Carousel arrows. No visible text. I cannot say "Click" anything. They need aria-labels or visible labels. "Open navigation menu." "Next slide." "Previous slide." "LinkedIn." "Twitter." Every interactive element must have a speakable name. Icon-only controls are a known failure. Fix them.

**On accessible name vs. visible text:** If a button shows "Submit" but has aria-label="Send form," I say "Click Submit." It may not work. I have to discover "Send form" by trial and error. Labels should match what I see. WCAG 2.5.3—Label in Name—requires it. Fix mismatches.

**On hover:** I cannot trigger hover by voice. Menus that open on hover. Content revealed on hover. Tooltips. All inaccessible. Everything must be reachable by focus and click. No hover-only interactions.

**On the emotional experience:** When I say "Click Learn More" and the wrong link activates, when I can't click an arrow because it has no label, when I have to overlay numbers on the whole page—it feels like the site wasn't built for me. I'm not asking for perfection. I'm asking for unique labels and labeled buttons. These aren't edge cases. They're WCAG Level A. A digital product firm that builds accessible experiences—their own site should model that.

**On what "good" would look like:** Six unique links: "Learn more about AI Strategy," "Learn more about Product Development," and so on. Every button with a speakable label—carousel arrows, social icons, hamburger menu. Accessible names that match visible text. No need for "Show numbers." That's it. Those changes would transform my experience. I'd leave feeling welcome.

**Final thoughts:** I completed the task. I know LaunchPad Lab does AI-centric digital product design and development. I found the contact path. But the barriers were real. Identical links. Icon-only buttons. Accessible name mismatches. I had to use "Show numbers" as a crutch. Fix those, and the site would be a different experience for voice control users. Right now, I leave feeling like an afterthought.

---

*Interview conducted as Marcus Webb, voice control persona (ALS, Dragon NaturallySpeaking / Voice Control). Task: Find what LaunchPad Lab does and how to contact them. Completed with voice only. Rating: 2/5.*

*— Marcus Webb*

---

*Note: Testing performed with voice commands only. No keyboard or mouse used. Persona relies on "Click [label]," "Scroll down," "Show numbers" fallback. Every interactive element must have a unique, speakable, visible label—or an accessible name that matches what the user would say. Identical links, icon-only buttons, and accessible name mismatches are critical barriers.*
