# Interview: David Okonkwo (Screen Reader User Persona)

**Date:** February 16, 2025  
**Website:** https://launchpadlab.com/  
**Task:** Find what LaunchPad Lab does and how to contact them  
**Persona:** David Okonkwo, 45, Chicago — blind user, 20+ years with NVDA/VoiceOver, keyboard-only navigation

---

## First Impressions

I opened the site and the first thing I heard was the page title: "AI-Centric Digital Product Design & Development | LaunchPad Lab." Good—at least I know where I am.

I pressed Tab. "Skip to content, link." Excellent. They have a skip link. I activated it and landed past the navigation. That's one thing done right—many sites don't have this.

Then I pressed H to get the heading structure. First heading: "Heading level 1, AI Innovation. Digital Solutions. Results that Matter." Okay, that's the main message. I pressed H again. "Heading level 2, Your Strategic AI Partner." Then "Heading level 2, AI-Powered Digital Solutions for the Modern Enterprise." Two H2s in a row? I kept going. "Heading level 2, Driving ROI with AI." "Heading level 2, Make AI Your Competitive Advantage." Then a bunch of H3s—AI Automation, Web Development, Mobile Development, Salesforce, and so on.

> "Every section seems to have two H2 headings. I'm hearing the same thing twice. It's like someone designed the page for sighted users who see a big title and a subtitle—but for me, it's just noise."

I pressed D to check landmarks. I expected to hear banner, navigation, main, contentinfo. The structure wasn't clear. I couldn't jump directly to main content using landmarks the way I normally would.

---

## Navigation by Headings, Landmarks, Links

**Headings:** The hierarchy is messy. I heard "Heading level 2, Years in Business," "Heading level 2, Projects," "Heading level 2, Clients." Those are statistics, not section headings. Why are they in the heading structure? When I press H to skim the page, I expect headings to tell me what sections exist. "12+ Years in Business" as an H2 makes no sense—it's a number, not a section.

> "I use headings to understand the page. When I hear 'Heading level 2, Years in Business,' I think there's a section about that. Then I realize it's just a stat. It breaks my mental model."

**Landmarks:** I couldn't identify clear regions. No distinct "main" or "navigation" announcements. I had to read sequentially in places where I'd normally jump. Without landmarks, I'm stuck tabbing or reading line by line.

**Links:** I pulled up the links list (Insert+F7 in NVDA). "Learn More." "Learn More." "Learn More." Six of them in a row. Which service does each one go to? I had no idea. I had to tab to each link and read the surrounding context to figure it out. That defeats the purpose of efficient navigation.

> "When every link says 'Learn More,' the links list is useless. I need unique, descriptive labels. 'Learn more about AI Automation'—that's what I need to hear."

---

## How I Tried to Find What the Company Does

I used the headings to orient myself. From the H3s I gathered they offer: AI Automation & Agentic AI, Web Application Development, Mobile Application Development, Salesforce Development, Product Strategy & Design, Managed Services & Support. So they're a digital product development firm—web, mobile, Salesforce, AI.

I also heard statistics: 12+ years in business, 730+ projects, 240+ clients. And case study names: Prosci, CDK Global, Millennium Trust Company. So they work with enterprises.

I clicked through to the Services page. Same heading issues—duplicate H2s, unclear structure. But the content was there. I got the gist: they build custom software, implement AI, do discovery and delivery.

> "I figured out what they do. But I had to work for it. The structure made it harder than it should have been."

---

## How I Tried to Find Contact Information

I saw "Connect with an Expert" in the nav—that sounded like a contact link. I activated it. New page: "Contact Us | LaunchPad Lab."

I pressed H. "Heading level 1, Ready to Build Something Great?" Then "Heading level 2, Reach Out." "Heading level 2, Ready to Build Something Great?"—the same text as the H1. Why repeat it?

I tabbed through. I found "Link, contact@launchpadlab.com." Good. "Link, (312) 888-9651." Good. "Link, Connect." Connect to what? I assumed LinkedIn, but "Connect" by itself is useless. It should say "Connect with LaunchPad Lab on LinkedIn."

The page said "Complete the form below." I pressed F to jump to form elements. Nothing. I tabbed through the entire page. No form fields. No inputs, no textareas, no submit button.

> "The page tells me to complete a form. I never found it. Either it doesn't exist, or it's not keyboard accessible. That's a critical failure."

I had the email and phone, so I could contact them. But if someone prefers the form—or if the form is the primary CTA—they're blocked.

---

## Pain Points

**Duplicate headings:** Almost every section has two H2s. "Problems We Solve" followed by "Ship Game-Changing Digital Products to Market Fast." Same section, two headings. It doubles the heading count and confuses navigation.

**Statistics as headings:** "12+ Years in Business," "730+ Projects," "240+ Clients" should not be H2s. They're data points. Put them in a list or div. Headings are for structure.

**Unlabeled links:** Six or more "Learn More" links with no context. "Connect" for LinkedIn with no destination. When I use the links list, I can't distinguish them.

**Missing or inaccessible form:** The contact page references a form. I never encountered one. If it exists, it's not reachable by keyboard or not properly exposed to screen readers.

**Unclear landmarks:** No clear main, nav, or contentinfo regions. I couldn't jump by landmarks.

**Generic link text:** "Learn More" and "Connect" without context. WCAG 2.4.4 says link purpose must be determinable from the link text alone or with context. "Learn More" fails that.

---

## What Worked Well

**Skip link:** "Skip to content" exists and works. I used it immediately. Many sites don't have this.

**Page titles:** Each page has a descriptive title. "Contact Us | LaunchPad Lab," "About Our Digital Product Firm in Chicago." Good.

**Contact info reachable:** I found the email and phone by tabbing. They're links, so I could activate them. The information is there.

**Client logos:** The case study and client logos appear to have alt text (Prosci, CDK Global, etc.). I could identify them.

**Content is present:** The text content is there. I could read what the company does. The problem is structure and labeling, not missing content.

---

## Overall Rating

**2 out of 5**

I completed the task. I know what LaunchPad Lab does (AI-focused digital product development, web/mobile/Salesforce) and I found their contact info (email, phone). But the experience was frustrating. Duplicate headings, unlabeled links, a form I couldn't find, and unclear landmarks made navigation inefficient. As someone who evaluates sites for accessibility, I'd flag this for significant improvements.

> "The content is there. The structure and labeling are not. Fix the headings, fix the links, fix the form—and this could be a much better experience. These aren't hard fixes. They're basic accessibility."

---

## Summary

David Okonkwo (blind screen reader user) completed the task of finding what LaunchPad Lab does and how to contact them. He relied on heading navigation (H key), landmark navigation (D key), and link/button navigation. The skip link worked. He identified the company's services from headings and content. He found email and phone on the Contact page. Major barriers: duplicate H2 headings, statistics incorrectly marked as headings, multiple "Learn More" links with no context, a contact form that was not located or not keyboard accessible, and unclear landmark structure. Improvements to heading hierarchy, link labels, form accessibility, and ARIA landmarks would substantially improve the experience for screen reader users.
