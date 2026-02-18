# Technical Report: Low Vision Persona Accessibility Assessment

**Website:** https://launchpadlab.com/  
**Persona:** Margaret Chen (Low Vision — No Screen Magnifier)  
**Assessment Date:** February 16, 2025  
**Testing Method:** Persona-based evaluation (typography, contrast, zoom/reflow, contact discoverability)

---

## Executive Summary

LaunchPad Lab's website is navigable for users with low vision who rely on browser zoom (125–200%), but several typographic, contrast, and layout issues create unnecessary barriers. The persona (Margaret Chen) successfully completed the task of finding what the company does and how to contact them, but reported significant eye strain and frustration due to small text, thin font weights, low contrast, and contact information buried below testimonials. The site benefits from a clear main headline and readable statistics section, but improvements to base font size, font weight, contrast ratios, and the placement of contact information would substantially improve the experience for users with low vision.

**Key findings:**
- Body text appears below 16px with font weight 300–400, causing strain for low-vision users
- Light gray text on white/light gray backgrounds fails to meet contrast requirements
- Contact page prioritizes testimonials over contact form and direct contact details
- Service cards and footer areas have poor contrast (white on light, gray on gray)
- No skip links to bypass repeated content or reach contact form
- Layout reflow at 150% zoom is acceptable; 200% zoom requires verification

---

## Specific Accessibility Issues

### Critical

#### C1. Body Text Below Minimum Readable Size
| Field | Detail |
|-------|--------|
| **Description** | Body text across the site appears to be 14px or smaller. Low-vision users require at least 16px for comfortable reading without excessive zoom. |
| **Location** | Homepage, About page, Services page, Contact page — body copy, introductory paragraphs, service descriptions |
| **Impact** | Users must zoom to 175% or higher to read comfortably. Increased zoom reduces visible content, increases scrolling, and may cause layout issues at higher levels. |
| **Recommended Fix** | Set base font size to at least 16px (1rem) for body text. Use relative units (`rem`, `em`) so text scales with user zoom preferences. Ensure form labels and helper text are at least 14px. |
| **WCAG** | **1.4.4 Resize Text** (Level AA) — Text can be resized up to 200% without loss of content or functionality; **1.4.8 Visual Presentation** (Level AAA) — Text size and spacing |

---

#### C2. Insufficient Text Contrast (Light Gray on White)
| Field | Detail |
|-------|--------|
| **Description** | Body text and secondary text use light gray (#666 or lighter) on white or light gray backgrounds. Contrast ratio falls below 4.5:1 (WCAG AA for normal text). |
| **Location** | Body text site-wide; footer "Reach Out" section (dark gray on light gray); secondary/helper text |
| **Impact** | Low-vision users cannot distinguish text from background. Requires high contrast mode or excessive zoom. Light gray text is a primary complaint for this persona. |
| **Recommended Fix** | Use dark text (#333 or darker) on white for body text. Ensure minimum 4.5:1 contrast for normal text, 3:1 for large text (18px+ or 14px+ bold). Audit with WebAIM Contrast Checker or similar. |
| **WCAG** | **1.4.3 Contrast (Minimum)** (Level AA) — Text and images of text have contrast ratio of at least 4.5:1 (3:1 for large text) |

---

#### C3. Contact Information Buried Below Long Testimonials
| Field | Detail |
|-------|--------|
| **Description** | The Contact page displays multiple long client testimonials before the contact form and direct contact details (phone, email). Users must scroll through dense quote blocks to reach actionable contact information. |
| **Location** | https://launchpadlab.com/contact/ |
| **Impact** | At 150% zoom, users see less content per viewport. Excessive scrolling is required to find phone and email. Many low-vision users prefer direct contact (phone/email) over forms; burying these details creates a critical barrier. |
| **Recommended Fix** | Place contact form and direct contact details (phone, email, address) above testimonials. Ensure phone number and email are visible without scrolling. Add "Skip to contact form" link. |
| **WCAG** | **2.4.1 Bypass Blocks** (Level A) — Mechanism to bypass repeated blocks; **2.1.1 Keyboard** (Level A) — Content reachable efficiently |

---

### High

#### H1. Thin Font Weight (300–400) for Body Text
| Field | Detail |
|-------|--------|
| **Description** | Body text uses font weight 300–400 (light/regular). Thin fonts are difficult to read for users with low vision and age-related vision decline. |
| **Location** | Body copy site-wide, service descriptions, testimonials |
| **Impact** | Letterforms blend together. Users report eye strain and fatigue. Bolder weights (500–600) significantly improve legibility. |
| **Recommended Fix** | Use font weight 500 (medium) or 600 (semi-bold) for body text. Avoid 300–400 for critical content. |
| **WCAG** | **1.4.8 Visual Presentation** (Level AAA) — Typography; **1.4.4 Resize Text** (Level AA) — Readability when scaled |

---

#### H2. Insufficient Line Height for Body Text
| Field | Detail |
|-------|--------|
| **Description** | Body text in several sections uses line height below 1.5. Tight line spacing makes it harder to track from line to line. |
| **Location** | Body text across homepage, About, Services, Contact |
| **Impact** | Lines "run together" for low-vision users. Increases re-reading and losing place. |
| **Recommended Fix** | Set `line-height` to at least 1.5 (preferably 1.6) for body text. Use `line-height: 1.5` or `1.6` in CSS for body selectors. |
| **WCAG** | **1.4.8 Visual Presentation** (Level AAA) — "Line spacing (leading) is at least space-and-a-half within paragraphs" |

---

#### H3. Poor Contrast in Service Cards and Footer
| Field | Detail |
|-------|--------|
| **Description** | Service cards use white text on colored backgrounds; some colors are too light. Footer "Reach Out" section uses dark gray on light gray. Client logos are faded or low-contrast. |
| **Location** | Services page (service cards), homepage (logo section), footer |
| **Impact** | Users cannot distinguish content. Service boundaries blur. Contact call-to-action in footer is nearly invisible. |
| **Recommended Fix** | Ensure service card text has minimum 4.5:1 contrast against background. Use darker backgrounds or lighter text with sufficient contrast. Make footer contact CTA high-contrast (e.g., dark text on white). Add text labels for client logos. |
| **WCAG** | **1.4.3 Contrast (Minimum)** (Level AA); **1.4.11 Non-text Contrast** (Level AA) — UI components 3:1 against adjacent colors |

---

#### H4. Sticky Header Consumes Excessive Space at Zoom
| Field | Detail |
|-------|--------|
| **Description** | At 150–200% zoom, the sticky header occupies proportionally more vertical space. Users see less main content per viewport. |
| **Location** | All pages (sticky navigation header) |
| **Impact** | Reduces visible content area. Increases scrolling. Users lose context when navigating. |
| **Recommended Fix** | Consider compact or collapsible header at higher zoom levels. Limit header height. Ensure key content is not obscured. Test at 150% and 200% zoom. |
| **WCAG** | **1.4.4 Resize Text** (Level AA) — No loss of functionality when zoomed; **1.4.10 Reflow** (Level AA) — Content reflows appropriately |

---

### Medium

#### M1. No Skip Links
| Field | Detail |
|-------|--------|
| **Description** | No "Skip to main content" or "Skip to contact form" link is present. Users must tab through or scroll past full navigation and hero content. |
| **Location** | All pages |
| **Impact** | Low-vision users who rely on keyboard or structure must traverse unnecessary content. Reduces efficiency when seeking contact information. |
| **Recommended Fix** | Add visible-on-focus "Skip to main content" link at top of each page. On Contact page, add "Skip to contact form" link. |
| **WCAG** | **2.4.1 Bypass Blocks** (Level A) |

---

#### M2. Layout Reflow at 200% Zoom Not Verified
| Field | Detail |
|-------|--------|
| **Description** | At 150% zoom, layout reflow appears acceptable. At 200% zoom (WCAG 1.4.4 requirement), horizontal scrolling or layout breakage may occur. Multi-column sections (services, logos) may not reflow to single column. |
| **Location** | All pages, especially multi-column sections |
| **Impact** | Users who need 200% zoom may encounter horizontal scrolling or overlapping content. |
| **Recommended Fix** | Test at 200% and 400% zoom (equivalent to 320px/256px width). Ensure content reflows without horizontal scrolling. Use responsive breakpoints that accommodate zoomed viewports. |
| **WCAG** | **1.4.4 Resize Text** (Level AA); **1.4.10 Reflow** (Level AA) — Content reflows at 320px width without horizontal scrolling |

---

#### M3. Form Labels and Focus Indicators
| Field | Detail |
|-------|--------|
| **Description** | Contact form labels may use small text. Focus indicators when tabbing through fields must be visible—critical for users who enable high contrast mode. |
| **Location** | Contact page (contact form) |
| **Impact** | Small labels are hard to read. Invisible focus indicators make keyboard navigation difficult. High contrast mode may override colors; focus must remain visible. |
| **Recommended Fix** | Ensure form labels are at least 14px with sufficient contrast. Use visible focus indicators (minimum 3:1 against adjacent colors). Avoid `outline: none` without replacement. |
| **WCAG** | **2.4.7 Focus Visible** (Level AA); **3.3.2 Labels or Instructions** (Level A); **1.4.3 Contrast (Minimum)** (Level AA) |

---

#### M4. Reduced Motion and High Contrast Support
| Field | Detail |
|-------|--------|
| **Description** | Site may not respect `prefers-reduced-motion: reduce`. High contrast mode (Windows High Contrast, `prefers-contrast: high`) may break button styling, focus indicators, or cause content to disappear. |
| **Location** | Site-wide (animations, carousels, auto-playing content, buttons, links) |
| **Impact** | Low-vision users often use high contrast mode in bright environments. Animations can distract. Broken styling in high contrast mode blocks use. |
| **Recommended Fix** | Use `@media (prefers-reduced-motion: reduce)` to disable or reduce animations and auto-playing content. Test with high contrast mode—ensure buttons, links, and focus indicators remain visible. Avoid background images for critical text. |
| **WCAG** | **2.3.3 Animation from Interactions** (Level AAA); **2.2.2 Pause, Stop, Hide** (Level A); **2.4.7 Focus Visible** (Level AA) |

---

### Low

#### L1. Client Logos Without Text Labels
| Field | Detail |
|-------|--------|
| **Description** | Client logos (Harvard, Northwestern, etc.) are displayed as images. At low contrast or when faded, names are hard to identify. No text labels accompany logos. |
| **Location** | Homepage (logo section) |
| **Impact** | Low-vision users cannot identify client names. Reduces value of social proof. |
| **Recommended Fix** | Add visible text labels below or beside logos. Ensure logos have sufficient contrast. Provide `alt` text for screen reader users. |
| **WCAG** | **1.1.1 Non-text Content** (Level A) — Meaningful alt text; **1.4.3 Contrast** (Level AA) |

---

#### L2. Line Length for Body Text
| Field | Detail |
|-------|--------|
| **Description** | Very long lines (full-width text on wide viewports) can make it harder to track from line end to line start. Ideal is 45–75 characters per line. |
| **Location** | Body text on wide viewports |
| **Impact** | Moderate. Long lines increase re-reading. More pronounced when zoomed. |
| **Recommended Fix** | Constrain max-width of text blocks (e.g., `max-width: 65ch` or ~75em). |
| **WCAG** | **1.4.8 Visual Presentation** (Level AAA) |

---

## WCAG Guidelines Referenced

| Guideline | Level | Relevance |
|-----------|-------|------------|
| 1.4.3 Contrast (Minimum) | AA | Body text, service cards, footer |
| 1.4.4 Resize Text | AA | Font size, zoom support, reflow |
| 1.4.8 Visual Presentation | AAA | Font size, weight, line height, line length |
| 1.4.10 Reflow | AA | Layout at 200% zoom, horizontal scrolling |
| 1.4.11 Non-text Contrast | AA | UI components, service cards |
| 2.4.1 Bypass Blocks | A | Skip links, contact placement |
| 2.4.7 Focus Visible | AA | Keyboard focus indicators |
| 2.2.2 Pause, Stop, Hide | A | Auto-playing content |
| 2.3.3 Animation from Interactions | AAA | Reduced motion |
| 3.3.2 Labels or Instructions | A | Form labels |

---

## Priority Recommendations

### P0 (Immediate)
1. **Increase base font size** to at least 16px (1rem) for all body text.
2. **Improve text contrast** — use #333 or darker on white for body text. Audit and fix light gray text.
3. **Move contact form and direct contact details above testimonials** on Contact page. Ensure phone and email visible without scrolling.

### P1 (High)
4. **Increase font weight** to 500+ for body text. Avoid 300–400.
5. **Set line height** to at least 1.5 for body text.
6. **Fix service card and footer contrast** — ensure 4.5:1 minimum for text.
7. **Add "Skip to main content"** and "Skip to contact form" links.

### P2 (Medium)
8. **Verify layout reflow** at 200% zoom. Fix horizontal scrolling if present.
9. **Ensure form labels** and focus indicators meet contrast and visibility requirements.
10. **Implement `prefers-reduced-motion`** support. Test high contrast mode.

### P3 (Low)
11. **Add text labels** for client logos.
12. **Constrain line length** for body text (max-width: 65ch).

---

*This report is based on persona-driven evaluation (Margaret Chen, low vision without screen magnifier) and content analysis of https://launchpadlab.com/. Specific typographic measurements (e.g., exact font-size, contrast ratios) should be verified with developer tools or automated accessibility testing (e.g., axe, Lighthouse, WebAIM Contrast Checker).*
