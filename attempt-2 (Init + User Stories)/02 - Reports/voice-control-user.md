# Technical Report: Voice Control User Accessibility Assessment

**Website:** https://launchpadlab.com/  
**Persona:** Jennifer Torres (Voice Control User — ALS, Voice Control/Dragon NaturallySpeaking)  
**Assessment Date:** February 16, 2025  
**Testing Method:** Persona-based evaluation (voice-only navigation, visible labels, duplicate link text, hover interactions, form labels)

---

## Executive Summary

LaunchPad Lab's website is partially accessible to users who rely on voice control software (Voice Control, Dragon NaturallySpeaking, Windows Speech Recognition) as their primary input method. The persona (Jennifer Torres) successfully completed the task of finding what the company does and how to contact them, but reported significant frustration due to **icon-only buttons with no visible labels**, **multiple "Learn More" links with identical text**, **unclear "Connect" link**, **contact information buried below testimonials**, and **potential form labeling issues**. Voice control users target elements by visible text—saying "click [label]"—so `aria-label` and hidden labels do not help. Every interactive element must have visible, unique text. The site benefits from clearly labeled main navigation (Work, Services, About, Contact) and reachable contact information (email, phone). However, icon-only buttons force users into the "show numbers" fallback, which is slow and disorienting. Duplicate link text causes wrong link activation. These issues violate WCAG 2.4.4 (Link Purpose) and 2.5.3 (Label in Name).

**Key findings:**
- Icon-only buttons (hamburger menu, social icons, carousel arrows) have no visible labels—voice control users cannot target them; must use "show numbers" fallback
- Six or more "Learn More" links with identical text—saying "click Learn more" activates wrong link (WCAG 2.4.4 failure)
- "Connect" link for LinkedIn has unclear purpose—destination not conveyed by visible text
- Contact information (phone, email) buried below testimonials on Contact page
- Form fields may use placeholder-only or floating labels—problematic for dictation
- Main navigation (Work, Services, About, Contact) has visible labels—works for voice
- Hover-only interactions not fully ruled out—voice control users cannot hover

---

## Specific Accessibility Issues

### Critical

#### C1. Icon-Only Buttons Have No Visible Labels
| Field | Detail |
|-------|--------|
| **Description** | Hamburger menu, social media icons (LinkedIn, etc.), carousel arrows, and close buttons display only icons with no visible text. Voice control software matches spoken words to on-screen text. Users say "click [label]." With no visible label, there is nothing to say. Users must use "show numbers" or "show grid" to overlay numbers and say "click 7"—a fallback that is slow, disorienting, and requires mapping numbers to elements. |
| **Location** | Header (mobile/responsive menu toggle), footer (social icons), carousels (previous/next arrows), modals (close button) |
| **Impact** | Voice control users cannot open the navigation menu, activate social links, or control carousels without the show-numbers fallback. This creates significant friction and fatigue. Persona reported using show numbers repeatedly. |
| **Recommended Fix** | Add visible text to every interactive element. For hamburger menu: display "Menu" or "Open menu" next to the icon. For social icons: display "LinkedIn," "Twitter," etc. For carousel arrows: display "Previous" and "Next." For close: display "Close" or "X" with visible text. Icon + text together. Never rely on `aria-label` alone—voice control targets visible text. |
| **WCAG** | **1.1.1 Non-text Content** (Level A) — Text alternatives for non-text content; **2.5.3 Label in Name** (Level A) — Name contains the text presented visually; **4.1.2 Name, Role, Value** (Level A) — For voice control, visible name is critical |

---

#### C2. Multiple "Learn More" Links Without Unique Visible Text
| Field | Detail |
|-------|--------|
| **Description** | Six or more links on the homepage and Services page use the identical visible text "Learn More." Each link refers to a different service (AI Automation, Web Development, Mobile Development, etc.). Voice control users say "click Learn more" to activate a link. The software matches to the first or a random match. The wrong link activates. Users cannot target a specific service. |
| **Location** | Homepage (services section), Services page (service cards) |
| **Impact** | Voice control users cannot reliably navigate to the intended service page. Saying "click Learn more" activates a random link. Persona reported activating Web Development when she wanted AI Automation. Repeated attempts yield same ambiguity. Task completion requires workarounds (reading visible card text instead of clicking). |
| **Recommended Fix** | Use unique, descriptive visible link text for each link: "Learn more about AI Automation & Agentic AI," "Learn more about Web Application Development," "Learn more about Mobile Application Development," etc. The visible text must be unique—`aria-label` alone does not help voice control users. Ensure link purpose is determinable from the visible link text alone. |
| **WCAG** | **2.4.4 Link Purpose (In Context)** (Level A) — The purpose of each link can be determined from the link text alone or from the link text together with its programmatically determined link context; **2.5.3 Label in Name** (Level A) — Visible label must match or be contained in the accessible name |

---

#### C3. "Connect" Link Has Unclear Purpose
| Field | Detail |
|-------|--------|
| **Description** | The LinkedIn link displays only "Connect" as visible text. Voice control users cannot determine that it links to LaunchPad Lab's LinkedIn page. "Connect" could mean many things—connect a device, connect to support, etc. The destination is not conveyed by the visible text. |
| **Location** | Contact page, possibly footer |
| **Impact** | Users who want to reach LinkedIn cannot target the link by saying a meaningful label. Saying "click Connect" may work but provides no context. Users may not know where they are navigating. |
| **Recommended Fix** | Use descriptive visible link text: "Connect with LaunchPad Lab on LinkedIn" or "LaunchPad Lab on LinkedIn." The visible text must convey the destination. Do not rely on `aria-label`—voice control users target visible text. |
| **WCAG** | **2.4.4 Link Purpose (In Context)** (Level A); **2.5.3 Label in Name** (Level A) |

---

#### C4. Contact Information Buried Below Testimonials
| Field | Detail |
|-------|--------|
| **Description** | The Contact page displays multiple long client testimonials before the contact form and direct contact details (phone, email). Voice control users must say "scroll down" repeatedly to reach actionable contact information. Phone and email are not visible without significant scrolling. |
| **Location** | https://launchpadlab.com/contact/ |
| **Impact** | Users seeking quick contact (phone, email) must navigate through dense testimonial content. Many voice control users prefer direct contact over forms—dictating an email or using voice-to-call is faster than form completion. Burying contact details creates a critical barrier. |
| **Recommended Fix** | Place contact form and direct contact details (phone, email, address) above testimonials. Ensure phone number and email are visible without scrolling. Add "Skip to contact form" link as first focusable element on Contact page. |
| **WCAG** | **2.4.1 Bypass Blocks** (Level A) — Mechanism to bypass repeated blocks; **2.1.1 Keyboard** (Level A) — Content reachable efficiently |

---

### High

#### H1. Form Fields May Use Placeholder-Only or Floating Labels
| Field | Detail |
|-------|--------|
| **Description** | Contact form fields may use placeholder text instead of persistent visible labels, or floating labels that disappear or move on focus. Voice control users dictate into fields. They say the label, then dictate the value. If the label is only a placeholder, it may disappear when the field is focused. If the label floats away, the user loses context. |
| **Location** | Contact page (contact form) |
| **Impact** | Users cannot reliably determine what to dictate into each field. "Name," "Email," "Company," "Message"—these must be visible at all times. Placeholder-only or floating labels cause confusion and form abandonment. |
| **Recommended Fix** | Use persistent visible `<label>` elements for every form field. Placeholder can supplement but never replace the label. Labels must remain visible when the field is focused. Use `for`/`id` association so clicking the label focuses the field. |
| **WCAG** | **3.3.2 Labels or Instructions** (Level A); **2.5.3 Label in Name** (Level A); **4.1.2 Name, Role, Value** (Level A) |

---

#### H2. Contact Form May Not Be Keyboard/Voice Accessible
| Field | Detail |
|-------|--------|
| **Description** | Prior assessments reported the contact form may be in an iframe (e.g., HubSpot) or loaded dynamically. Form fields may not be focusable via Tab or targetable by voice. If the form is not in the main DOM or has focus traps, voice control users cannot reach it. |
| **Location** | https://launchpadlab.com/contact/ |
| **Impact** | Users who prefer or require the contact form cannot use it. Voice control relies on focus and activation. If the form is inaccessible, users are blocked from the primary contact CTA. |
| **Recommended Fix** | Ensure the contact form is in the main DOM and all fields are focusable. If in an iframe, ensure the iframe has a descriptive `title` and form fields are reachable. Ensure all fields have visible, persistent labels. Verify form can be completed using only voice (dictation + "click Submit"). |
| **WCAG** | **2.1.1 Keyboard** (Level A); **4.1.2 Name, Role, Value** (Level A) |

---

#### H3. Hover-Only Interactions Not Ruled Out
| Field | Detail |
|-------|--------|
| **Description** | Navigation dropdowns, tooltips, or reveal-on-hover content may exist. Voice control users cannot hover. All functionality must be available via click (or equivalent voice activation). If dropdowns open only on hover, users cannot access submenu items. If tooltips contain critical information and appear only on hover, that information is inaccessible. |
| **Location** | Main navigation, service cards, buttons, custom widgets |
| **Impact** | Users cannot access hover-only content. Menus that require sustained hover are unusable. Tooltips with unique information are lost. |
| **Recommended Fix** | Ensure all dropdowns open on click/focus, not only hover. Support Enter/Space to activate. Provide click/tap as primary trigger. If tooltips contain critical information, also provide it as visible text or ensure tooltip can be triggered by click/focus. |
| **WCAG** | **2.1.1 Keyboard** (Level A); **2.5.3 Label in Name** (Level A) — Ensure no critical functionality requires hover |

---

#### H4. Logo/Home Link May Lack Visible Label
| Field | Detail |
|-------|--------|
| **Description** | The logo or home link may be an image or icon with no visible text. Voice control users say "click LaunchPad Lab" or "click Home" to return to the homepage. If the logo has no visible text—only an image—users cannot target it by voice. |
| **Location** | Header (all pages) |
| **Impact** | Users cannot easily return to the homepage by voice. They may need to use "show numbers" or navigate through the menu. |
| **Recommended Fix** | Ensure the logo link has visible text "LaunchPad Lab" or "Home" next to or within the link. If the logo is an image, add visible text "LaunchPad Lab" as part of the link. |
| **WCAG** | **2.5.3 Label in Name** (Level A); **4.1.2 Name, Role, Value** (Level A) |

---

### Medium

#### M1. Submit Button Visibility and Label
| Field | Detail |
|-------|--------|
| **Description** | The contact form submit button must have visible text such as "Submit," "Send," or "Send message." Voice control users say "click Submit" to activate. If the button shows only an icon or has unclear text, users cannot target it. |
| **Location** | Contact page (contact form) |
| **Impact** | Users may not be able to submit the form by voice if the button lacks a clear, visible label. |
| **Recommended Fix** | Ensure the submit button displays visible text: "Submit," "Send," or "Send message." Avoid icon-only buttons. |
| **WCAG** | **2.5.3 Label in Name** (Level A); **4.1.2 Name, Role, Value** (Level A) |

---

#### M2. Carousel and Dynamic Content Voice Activation
| Field | Detail |
|-------|--------|
| **Description** | Carousels (awards, client logos, case studies) may have previous/next controls that are icon-only. Auto-advancing content may not have pause controls with visible labels. Voice control users cannot advance or pause carousels if controls lack visible text. |
| **Location** | Homepage, Work page, other pages with carousels |
| **Impact** | Users may be unable to control carousel navigation. Auto-advancing content may be distracting or cause motion sensitivity issues. |
| **Recommended Fix** | Provide visible "Previous" and "Next" buttons for carousels. Add visible "Pause" button for auto-advancing content. Ensure all controls have visible labels. |
| **WCAG** | **2.1.1 Keyboard** (Level A); **2.2.2 Pause, Stop, Hide** (Level A); **2.5.3 Label in Name** (Level A) |

---

#### M3. Skip Link Visibility on Focus
| Field | Detail |
|-------|--------|
| **Description** | A "Skip to main content" or "Skip to contact form" link should be the first focusable element. It is typically visually hidden until focused. Voice control users can say "click Skip to main content" if that text is programmatically available. However, if the skip link is not the first focusable element or has no visible/announced text, users may not find it. |
| **Location** | All pages (header) |
| **Impact** | Users must traverse the entire header (logo, nav, social icons) on every page. A skip link would reduce navigation burden. On Contact page, "Skip to contact form" would bypass testimonials. |
| **Recommended Fix** | Add "Skip to main content" as first focusable element on all pages. Add "Skip to contact form" on Contact page. Ensure skip links have visible text when focused (or at least programmatically determinable text that voice control can match). |
| **WCAG** | **2.4.1 Bypass Blocks** (Level A) |

---

### Low

#### L1. Visible Names Matching Accessible Names
| Field | Detail |
|-------|--------|
| **Description** | If visible text says "Contact" but the accessible name is "Contact Us" or "Contact LaunchPad Lab," voice control software may or may not match "click Contact." Inconsistencies between visible and accessible names can cause activation failures. |
| **Location** | Navigation, buttons, links site-wide |
| **Impact** | Users may say the visible text and the wrong element activates, or no element activates. |
| **Recommended Fix** | Ensure visible text matches or is contained in the accessible name. WCAG 2.5.3 (Label in Name) requires the accessible name to contain the visible label text. Avoid `aria-label` that differs from visible text when visible text exists. |
| **WCAG** | **2.5.3 Label in Name** (Level A) |

---

#### L2. Long or Complex Labels
| Field | Detail |
|-------|--------|
| **Description** | Overly long button or link labels (e.g., "Submit your inquiry to our team and we'll get back to you within 24 hours") are harder to say and may not match voice control software's expectations. Short, clear labels work best. |
| **Location** | Buttons, links, form labels |
| **Impact** | Minor. Users may need to abbreviate or repeat. Prefer "Submit" over long phrases. |
| **Recommended Fix** | Use short, clear labels: "Submit," "Contact," "Learn more about [topic]." Avoid jargon or overly long labels. |
| **WCAG** | **2.4.6 Headings and Labels** (Level AA) |

---

## WCAG Guidelines Referenced

| Guideline | Level | Relevance |
|-----------|-------|-----------|
| **1.1.1 Non-text Content** | A | Icon-only buttons need text alternatives; for voice control, visible text is required |
| **2.1.1 Keyboard** | A | All functionality operable; voice control relies on focus and activation |
| **2.4.1 Bypass Blocks** | A | Skip links; contact info not buried |
| **2.4.4 Link Purpose (In Context)** | A | "Learn More," "Connect" links must convey purpose from visible text |
| **2.4.6 Headings and Labels** | AA | Labels describe purpose; short, clear labels |
| **2.5.3 Label in Name** | A | **Critical for voice control** — Visible label text must be contained in the accessible name; users target by visible text |
| **3.3.2 Labels or Instructions** | A | Form labels |
| **4.1.2 Name, Role, Value** | A | For voice control, visible name is critical—aria-label alone is insufficient |

---

## Priority Recommendations

### P0 (Immediate)
1. **Add visible labels to all icon-only buttons** — Hamburger menu: "Menu" or "Open menu." Social icons: "LinkedIn," "Twitter," etc. Carousel arrows: "Previous," "Next." Close: "Close." Icon + text. Never icon-only.
2. **Make "Learn More" links unique** — Visible text must differ: "Learn more about AI Automation," "Learn more about Web Development," etc. Each link targetable by unique spoken phrase.
3. **Fix "Connect" link** — Visible text: "Connect with LaunchPad Lab on LinkedIn" or "LaunchPad Lab on LinkedIn."
4. **Reorganize Contact page** — Place contact form and direct contact details (phone, email) above testimonials. Add "Skip to contact form" link.

### P1 (High)
5. **Ensure form fields have persistent visible labels** — No placeholder-only. No floating labels that disappear on focus. "Name," "Email," "Company," "Message" always visible.
6. **Verify contact form accessibility** — Ensure form is in main DOM, all fields focusable, submit button has visible "Submit" or "Send."
7. **Audit hover-only interactions** — Dropdowns must open on click/focus. No critical content in hover-only tooltips.
8. **Ensure logo/home link has visible label** — "LaunchPad Lab" or "Home" visible and targetable.

### P2 (Medium)
9. **Add skip links** — "Skip to main content" on all pages. "Skip to contact form" on Contact page.
10. **Verify carousel controls** — Visible "Previous," "Next," "Pause" buttons.
11. **Ensure visible names match accessible names** — WCAG 2.5.3 compliance site-wide.

### P3 (Low)
12. **Use short, clear labels** — "Submit" not "Submit your inquiry to our team."
13. **Test with real voice control software** — Dragon NaturallySpeaking, Voice Control (macOS), Windows Speech Recognition. Complete key flows: navigate, open menu, reach contact form, submit.

---

*This report is based on persona-driven evaluation (Jennifer Torres, voice control user with ALS) and content/structure analysis of https://launchpadlab.com/. Voice control users target elements by visible text—aria-label and hidden labels do not help. Testing should be verified with actual voice control software (Dragon, Voice Control, Windows Speech Recognition) to confirm activation behavior and "show numbers" fallback requirements.*
