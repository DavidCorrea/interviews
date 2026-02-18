# Technical Report: Senior Person (65+) Accessibility Assessment

**Website:** https://launchpadlab.com/  
**Persona:** Robert Henderson (72, Retired School Administrator — Desktop, Mouse, Reading Glasses)  
**Assessment Date:** February 16, 2025  
**Testing Method:** Persona-based evaluation (navigation discoverability, typography, form labels, contact placement, familiarity with modern patterns)

---

## Executive Summary

LaunchPad Lab's website is partially accessible to older adults (65+) with mild vision and cognitive constraints. The persona (Robert Henderson) successfully completed the task of finding what the company does and how to contact them, but reported significant frustration due to small text, thin fonts, an unfamiliar hamburger menu that was initially overlooked, contact information buried below testimonials, and form labels that may rely on placeholders. The site benefits from a clear main headline, logical menu structure (once discovered), and reachable contact details (email, phone). However, typographic choices, navigation patterns, and content hierarchy create substantial barriers for users who prefer traditional layouts, explicit labels, and familiar conventions.

**Key findings:**
- Hamburger menu may be overlooked or misunderstood by users unfamiliar with modern UI patterns
- "Connect with an Expert" used instead of familiar "Contact" label
- Body text below 16px with thin font weight (300–400) causes strain
- Contact information and form buried below long testimonials
- Form may use placeholder-only labels; persistent labels preferred
- No clear "Cancel," "Back," or confirmation for form submission
- Jargon ("AI-centric," "digital product design") may require interpretation

---

## Specific Accessibility Issues

### Critical

#### C1. Hamburger Menu Not Discoverable or Understandable
| Field | Detail |
|-------|--------|
| **Description** | The main navigation may be hidden behind a hamburger menu (three horizontal lines icon). Older adults unfamiliar with this pattern may overlook it or not understand that it opens a menu. The icon has no visible "Menu" label. |
| **Location** | All pages (navigation header) |
| **Impact** | Users cannot find the main navigation. They may assume the site has no menu or that they are on the wrong page. Critical for wayfinding—users cannot reach About, Services, Contact without discovering the menu. |
| **Recommended Fix** | Add a visible "Menu" label next to the hamburger icon. Alternatively, use always-visible text-based navigation on desktop. Ensure the menu is discoverable without prior knowledge of hamburger conventions. Test with users 65+ who are unfamiliar with the pattern. |
| **WCAG** | **2.4.6 Headings and Labels** (Level AA) — Labels describe purpose; **4.1.2 Name, Role, Value** (Level A) — Icon-only buttons need accessible names |

---

#### C2. Body Text Below Minimum Readable Size
| Field | Detail |
|-------|--------|
| **Description** | Body text across the site appears to be 14px or smaller. Older adults with age-related vision decline require at least 16px for comfortable reading without excessive zoom. |
| **Location** | Homepage, About page, Services page, Contact page — body copy, introductory paragraphs, service descriptions |
| **Impact** | Users must zoom to read comfortably. Increased zoom reduces visible content, increases scrolling, and may cause layout issues. Thin fonts compound the problem—letterforms blend together. |
| **Recommended Fix** | Set base font size to at least 16px (1rem) for body text. Use relative units (`rem`, `em`) so text scales with user zoom preferences. Use font weight 400+ (preferably 500) for body text. |
| **WCAG** | **1.4.4 Resize Text** (Level AA) — Text can be resized up to 200% without loss of content or functionality; **1.4.8 Visual Presentation** (Level AAA) — Text size |

---

#### C3. Contact Information Buried Below Long Testimonials
| Field | Detail |
|-------|--------|
| **Description** | The Contact page displays multiple long client testimonials before the contact form and direct contact details (phone, email). Users must scroll through dense quote blocks to reach actionable contact information. |
| **Location** | https://launchpadlab.com/contact/ |
| **Impact** | Older adults who prefer to call or email must scroll extensively. At increased zoom levels, less content is visible per viewport—scrolling burden increases. Many older users avoid forms; burying phone and email creates a critical barrier. |
| **Recommended Fix** | Place contact form and direct contact details (phone, email, address) above testimonials. Ensure phone number and email are visible without scrolling. Add "Skip to contact form" link. |
| **WCAG** | **2.4.1 Bypass Blocks** (Level A) — Mechanism to bypass repeated blocks |

---

### High

#### H1. "Connect with an Expert" Instead of "Contact"
| Field | Detail |
|-------|--------|
| **Description** | The primary contact link in navigation uses "Connect with an Expert" rather than the familiar "Contact" label. Older adults expect explicit, standard terminology. |
| **Location** | Main navigation (all pages) |
| **Impact** | Users may not recognize this as the contact link. "Connect" could mean social media, newsletter signup, or something else. Uncertainty causes hesitation and may prevent users from reaching the contact page. |
| **Recommended Fix** | Use "Contact" as the primary label. If "Connect with an Expert" is desired for branding, use it as secondary text: "Contact — Connect with an Expert." Ensure the link purpose is immediately clear. |
| **WCAG** | **2.4.4 Link Purpose (In Context)** (Level A) — Purpose determinable from link text; **2.4.6 Headings and Labels** (Level AA) |

---

#### H2. Insufficient Text Contrast (Light Gray on White)
| Field | Detail |
|-------|--------|
| **Description** | Body text and secondary text use light gray (#666 or lighter) on white or light gray backgrounds. Contrast ratio may fall below 4.5:1 (WCAG AA for normal text). |
| **Location** | Body text site-wide; footer; secondary/helper text |
| **Impact** | Users with mild vision decline cannot distinguish text from background. Thin fonts compound the problem. Requires high contrast mode or excessive zoom. |
| **Recommended Fix** | Use dark text (#333 or darker) on white for body text. Ensure minimum 4.5:1 contrast for normal text, 3:1 for large text. Audit with WebAIM Contrast Checker. |
| **WCAG** | **1.4.3 Contrast (Minimum)** (Level AA) |

---

#### H3. Form Labels May Rely on Placeholders
| Field | Detail |
|-------|--------|
| **Description** | The contact form may use placeholder text as the only label for fields. Placeholders disappear when the user types, leaving no persistent indication of what each field requires. |
| **Location** | https://launchpadlab.com/contact/ (contact form) |
| **Impact** | Older adults need visible, persistent labels. Placeholder-only labels cause confusion—users forget what goes in each field. Required vs. optional is unclear. Increases form abandonment and errors. |
| **Recommended Fix** | Use visible labels above or beside each field. Do not rely on placeholders alone. Clearly indicate required fields (e.g., "Required" or asterisk with legend). Ensure labels are associated with inputs via `for`/`id` or `aria-label`. |
| **WCAG** | **3.3.2 Labels or Instructions** (Level A); **2.4.6 Headings and Labels** (Level AA) |

---

#### H4. Thin Font Weight (300–400) for Body Text
| Field | Detail |
|-------|--------|
| **Description** | Body text uses font weight 300–400 (light/regular). Thin fonts are difficult to read for users with age-related vision decline. |
| **Location** | Body copy site-wide, service descriptions, testimonials |
| **Impact** | Letterforms blend together. Users report eye strain and fatigue. Bolder weights (500–600) significantly improve legibility for older readers. |
| **Recommended Fix** | Use font weight 500 (medium) or 600 (semi-bold) for body text. Avoid 300–400 for critical content. |
| **WCAG** | **1.4.8 Visual Presentation** (Level AAA) — Typography |

---

#### H5. No Clear "Cancel," "Back," or Form Confirmation
| Field | Detail |
|-------|--------|
| **Description** | The contact form may lack a visible "Cancel" or "Back" option. Users are uncertain what happens after submission—is there a confirmation? Can they undo? |
| **Location** | Contact page (contact form) |
| **Impact** | Older adults worry about making irreversible mistakes. Fear of accidental submission or "breaking" the site causes hesitation. Lack of confirmation increases anxiety. |
| **Recommended Fix** | Provide a "Cancel" or "Back" link/button. After submission, show a clear success message (e.g., "Thank you. We'll be in touch within 24 hours."). Avoid irreversible actions without clear confirmation. |
| **WCAG** | **3.3.4 Error Prevention (Legal, Financial, Data)** (Level AA) — For critical forms; best practice for all forms |

---

### Medium

#### M1. Click Target Size May Be Below 44×44px
| Field | Detail |
|-------|--------|
| **Description** | Interactive elements (links, buttons, form controls) may be smaller than 44×44 CSS pixels. Users with mild tremor or reduced motor precision struggle with small targets. |
| **Location** | Navigation links, footer links, form buttons, "Learn More" links |
| **Impact** | Misclicks, double-clicks, frustration. Users may accidentally activate the wrong link when targets are close together. |
| **Recommended Fix** | Ensure all interactive elements have a minimum 44×44px click target. Add adequate spacing between links and buttons to reduce misclicks. |
| **WCAG** | **2.5.5 Target Size** (Level AAA) — 44×44px minimum |

---

#### M2. Jargon and Unfamiliar Terminology
| Field | Detail |
|-------|--------|
| **Description** | Terms like "AI-centric," "digital product design," "discovery process," "MVP," "entrepreneurship journey" may require interpretation. Older adults prefer plain language. |
| **Location** | Homepage, About page, Services page, Contact page testimonials |
| **Impact** | Users must re-read and infer meaning. Slows comprehension. Some users may give up or feel excluded. |
| **Recommended Fix** | Use plain language. Provide a simple summary: "We build websites and apps for businesses." Define or avoid jargon. Have content reviewed for clarity by non-experts. |
| **WCAG** | **2.4.6 Headings and Labels** (Level AA) — Labels describe purpose; **3.1.5 Reading Level** (Level AAA) — Plain language |

---

#### M3. No Skip Links
| Field | Detail |
|-------|--------|
| **Description** | No "Skip to main content" or "Skip to contact form" link is present. Users must tab through or scroll past full navigation and hero content. |
| **Location** | All pages |
| **Impact** | Older adults who use keyboard or prefer structured navigation must traverse unnecessary content. Reduces efficiency when seeking contact information. |
| **Recommended Fix** | Add visible-on-focus "Skip to main content" link at top of each page. On Contact page, add "Skip to contact form" link. |
| **WCAG** | **2.4.1 Bypass Blocks** (Level A) |

---

#### M4. Auto-Playing or Rapid Animations
| Field | Detail |
|-------|--------|
| **Description** | Carousels, auto-advancing content, or rapid animations may be present. Older adults find these distracting or overwhelming. |
| **Location** | Homepage, possibly other pages |
| **Impact** | Slower processing speed; content that changes before user can absorb it. May cause disorientation. |
| **Recommended Fix** | Provide pause/stop controls for auto-playing content. Respect `prefers-reduced-motion: reduce`. Use `@media (prefers-reduced-motion: reduce)` to disable or reduce animations. |
| **WCAG** | **2.2.2 Pause, Stop, Hide** (Level A); **2.3.3 Animation from Interactions** (Level AAA) |

---

### Low

#### L1. Generic "Learn More" Links
| Field | Detail |
|-------|--------|
| **Description** | Multiple links use the identical text "Learn More" with no additional context. Each link refers to a different service. |
| **Location** | Homepage (services section), Services page |
| **Impact** | Users cannot distinguish links when scanning. Must read surrounding context. Moderate impact for this persona. |
| **Recommended Fix** | Use unique, descriptive link text: "Learn more about AI Automation," "Learn more about Web Development," etc. |
| **WCAG** | **2.4.4 Link Purpose (In Context)** (Level A) |

---

#### L2. No Accessibility Statement
| Field | Detail |
|-------|--------|
| **Description** | No accessibility statement or policy is linked. Users cannot easily report accessibility issues. |
| **Location** | Footer, site-wide |
| **Impact** | Minor. Older adults may want to know the site's commitment to accessibility and how to report problems. |
| **Recommended Fix** | Add an accessibility statement page. Link from footer. Include contact information for accessibility feedback. |
| **WCAG** | Best practice |

---

## WCAG Guidelines Referenced

| Guideline | Level | Relevance |
|-----------|-------|------------|
| **1.4.3 Contrast (Minimum)** | AA | Body text, light gray on white |
| **1.4.4 Resize Text** | AA | Font size, zoom support |
| **1.4.8 Visual Presentation** | AAA | Font size, weight, typography |
| **2.4.1 Bypass Blocks** | A | Skip links, contact placement |
| **2.4.4 Link Purpose (In Context)** | A | "Connect with an Expert," "Learn More" |
| **2.4.6 Headings and Labels** | AA | Form labels, navigation labels |
| **2.5.5 Target Size** | AAA | Click target size |
| **2.2.2 Pause, Stop, Hide** | A | Auto-playing content |
| **2.3.3 Animation from Interactions** | AAA | Reduced motion |
| **3.3.2 Labels or Instructions** | A | Form labels |
| **3.3.4 Error Prevention** | AA | Form confirmation, cancel option |
| **4.1.2 Name, Role, Value** | A | Hamburger menu, icon-only buttons |

---

## Priority Recommendations

### P0 (Immediate)
1. **Make navigation discoverable** — Add "Menu" label next to hamburger icon, or use always-visible text navigation on desktop. Ensure users 65+ can find the menu without prior knowledge.
2. **Increase base font size** to at least 16px (1rem) for all body text. Use font weight 500+ for body copy.
3. **Move contact form and direct contact details above testimonials** on Contact page. Ensure phone and email visible without scrolling.

### P1 (High)
4. **Use "Contact" as primary navigation label** — Replace or supplement "Connect with an Expert" with "Contact."
5. **Improve text contrast** — Use #333 or darker on white for body text. Audit light gray text.
6. **Add persistent form labels** — Visible labels above or beside fields. Do not rely on placeholders alone. Indicate required fields clearly.
7. **Add form confirmation and cancel option** — Show success message after submission. Provide "Cancel" or "Back" button.

### P2 (Medium)
8. **Ensure click targets are 44×44px minimum** — Audit navigation links, buttons, form controls.
9. **Add skip links** — "Skip to main content" and "Skip to contact form."
10. **Use plain language** — Simplify jargon. Add clear summary: "We build websites and apps for businesses."
11. **Implement prefers-reduced-motion** — Disable or reduce animations for users who prefer reduced motion.

### P3 (Low)
12. **Make "Learn More" links unique** — Add context to each link.
13. **Add accessibility statement** — Link from footer with contact for accessibility feedback.

---

*This report is based on persona-driven evaluation (Robert Henderson, senior person 65+) and content/structure analysis of https://launchpadlab.com/. Testing was simulated by embodying the persona's pace, caution, and preferences. Verification with live user testing involving older adults (65+) is strongly recommended.*
