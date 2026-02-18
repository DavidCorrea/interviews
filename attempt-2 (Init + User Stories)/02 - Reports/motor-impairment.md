# Technical Report: Motor Impairment Accessibility Assessment

**Website:** https://launchpadlab.com/  
**Persona:** Marcus Okonkwo (Motor Impairment — Essential Tremor, Cerebral Palsy)  
**Assessment Date:** February 16, 2025  
**Testing Method:** Persona-based evaluation (keyboard navigation, focus visibility, target size, skip links, forms, contact discoverability)

---

## Executive Summary

LaunchPad Lab's website is partially accessible to users with motor impairment who rely on keyboard navigation, but several critical barriers create unnecessary friction. The persona (Marcus Okonkwo) successfully completed the task of finding what the company does and how to contact them, primarily using the keyboard. However, he reported significant frustration due to: **no skip link**, **invisible or faint focus indicators**, **small click targets** (under 44×44px) for secondary links and icons, and **contact information buried below testimonials**. The site benefits from logical tab order and keyboard-reachable navigation, but improvements to skip links, focus visibility, target size, and contact page structure are essential for users with limited fine motor control, tremor, or adaptive device use.

**Key findings:**
- No "Skip to main content" or "Skip to contact form" link on any page
- Focus indicators are missing, too faint, or removed (e.g., `outline: none` without replacement)
- "Learn More" links, arrow icons, and secondary CTAs have hit areas under 44×44px
- Contact page displays testimonials before contact form and direct contact details
- Tab order is logical; no keyboard traps identified in primary flows
- Main CTA button and primary nav links are keyboard accessible

---

## Specific Accessibility Issues

### Critical

#### C1. No Skip Link
| Field | Detail |
|-------|--------|
| **Description** | No "Skip to main content" or "Skip to contact form" link is present as the first focusable element. Users must tab through the entire header (logo, nav links, possibly social icons) on every page load. |
| **Location** | All pages (homepage, About, Services, Contact, Work) |
| **Impact** | Users with motor impairment who rely on keyboard or switch scanning must traverse 10+ focusable elements before reaching main content. Increases fatigue, repetition, and time to complete tasks. Critical for users who tab on every page load. |
| **Recommended Fix** | Add a visible-on-focus "Skip to main content" link as the first focusable element. Use `position: absolute` with `left: -9999px` or similar, and `:focus` to bring it into view. Target `#main-content` or `<main>`. On Contact page, add "Skip to contact form" link. |
| **WCAG** | **2.4.1 Bypass Blocks** (Level A) — A mechanism must be provided to bypass blocks of content that are repeated on multiple Web pages. |

---

#### C2. Invisible or Insufficient Focus Indicators
| Field | Detail |
|-------|--------|
| **Description** | Focus indicators on links, buttons, and form controls are either missing, too faint, or removed (e.g., `outline: none` without a visible replacement). User cannot reliably determine where keyboard focus is. |
| **Location** | All interactive elements site-wide — navigation links, buttons, form fields, "Learn More" links, social icons |
| **Impact** | Users with motor impairment rely on visible focus to navigate. Without it, they lose orientation and must tab through the entire page to relocate. Causes disorientation, repeated attempts, and task abandonment. |
| **Recommended Fix** | Ensure every focusable element has a visible focus indicator with at least 3:1 contrast against adjacent colors. Use `outline: 2px solid` or `box-shadow` — never `outline: none` without replacement. Apply consistently: `:focus-visible { outline: 2px solid [color]; outline-offset: 2px; }`. |
| **WCAG** | **2.4.7 Focus Visible** (Level AA) — Any keyboard operable user interface has a mode of operation where the keyboard focus indicator is visible. |

---

#### C3. Click Targets Under 44×44 CSS Pixels
| Field | Detail |
|-------|--------|
| **Description** | "Learn More" links, arrow icons for carousels, secondary CTAs, and possibly some nav items have hit areas smaller than 44×44 CSS pixels. Tightly packed elements increase misclick risk. |
| **Location** | Service cards, case study cards, carousel controls, footer links, secondary navigation |
| **Impact** | Users with tremor, limited fine motor control, or adaptive devices (switch, head pointer) require multiple attempts to activate small targets. Causes frustration, fatigue, and task abandonment. Persona reported missing small links "half the time." |
| **Recommended Fix** | Ensure all interactive elements have a minimum hit area of 44×44 CSS pixels. Use padding to increase hit area without changing visual size. Make entire cards clickable rather than only a small "Learn More" link. Add at least 8px spacing between adjacent targets. |
| **WCAG** | **2.5.5 Target Size** (Level AAA) — The size of the target for pointer inputs is at least 44 by 44 CSS pixels. **2.5.8 Target Size (Minimum)** (Level AA, WCAG 2.2) — At least 24×24px; 44×44px recommended for motor impairment. |

---

#### C4. Contact Information Buried Below Testimonials
| Field | Detail |
|-------|--------|
| **Description** | The Contact page displays multiple long client testimonials before the contact form and direct contact details (phone, email). Users must tab and scroll through dense quote blocks to reach actionable contact information. |
| **Location** | https://launchpadlab.com/contact/ |
| **Impact** | At 10+ tabs per testimonial block, users with motor impairment expend significant effort before reaching the form or contact details. Many prefer direct contact (phone/email) over forms; burying these creates a critical barrier. |
| **Recommended Fix** | Place contact form and direct contact details (phone, email, address) above testimonials. Ensure phone number and email are visible without scrolling. Add "Skip to contact form" link. |
| **WCAG** | **2.4.1 Bypass Blocks** (Level A); **2.1.1 Keyboard** (Level A) — Content reachable efficiently |

---

### High

#### H1. Form Field Hit Areas May Be Insufficient
| Field | Detail |
|-------|--------|
| **Description** | Contact form fields (name, email, company, message) may have small hit areas or tight spacing. Labels may not extend the clickable region. |
| **Location** | Contact page (contact form) |
| **Impact** | Users with tremor or limited precision may accidentally focus adjacent fields or miss the intended input. Increases form completion time and error rate. |
| **Recommended Fix** | Ensure form controls have minimum 44px height. Use `<label for="id">` so clicking the label focuses the field, effectively enlarging the target. Add adequate padding and spacing between fields. |
| **WCAG** | **2.5.5 Target Size** (Level AAA); **3.3.2 Labels or Instructions** (Level A) |

---

#### H2. Navigation Links May Be Under Minimum Target Size
| Field | Detail |
|-------|--------|
| **Description** | Main navigation links (Work, Services, About, Contact) may have hit areas under 44×44px, especially if only the text is clickable and padding is minimal. |
| **Location** | Header navigation |
| **Impact** | Persona reported overshooting and clicking the wrong link when using mouse. Keyboard navigation mitigates this, but switch users and those who occasionally use pointer need adequate targets. |
| **Recommended Fix** | Add padding to nav links to achieve 44px minimum height. Ensure entire link area (including padding) is clickable. |
| **WCAG** | **2.5.5 Target Size** (Level AAA) |

---

#### H3. Carousel and Custom Widget Keyboard Support Not Verified
| Field | Detail |
|-------|--------|
| **Description** | Carousels (awards, client logos, case studies) may lack keyboard-accessible Previous/Next buttons, Arrow key support, or pause controls. Focus management within carousels is unknown. |
| **Location** | Homepage (awards, client logos), Work page, other pages with carousels |
| **Impact** | Users who cannot use mouse may be unable to advance carousels or pause auto-advancing content. Keyboard traps are possible if focus is not managed correctly. |
| **Recommended Fix** | Provide visible, keyboard-focusable Previous/Next buttons. Support Arrow keys for navigation within carousel. Ensure focus is trapped within carousel when active, with Escape to close/exit. Add pause control for auto-advancing carousels. |
| **WCAG** | **2.1.1 Keyboard** (Level A); **2.1.2 No Keyboard Trap** (Level A); **2.2.2 Pause, Stop, Hide** (Level A) |

---

#### H4. Hover-Dependent Interactions Not Fully Ruled Out
| Field | Detail |
|-------|--------|
| **Description** | Navigation dropdowns or submenus may use hover to reveal. Tooltips or reveal-on-hover content may exist. Persona did not encounter critical hover-only content, but comprehensive audit is needed. |
| **Location** | Main navigation, cards, buttons |
| **Impact** | Users with motor impairment cannot reliably sustain hover. Cursor drift triggers wrong menus or closes them before activation. Hover-only content is a barrier. |
| **Recommended Fix** | Ensure all dropdowns open on focus or Enter, not only hover. Support Arrow keys to move between items. Provide click/tap as primary trigger. Ensure no critical information is in hover-only tooltips. |
| **WCAG** | **2.1.1 Keyboard** (Level A); **2.5.3 Label in Name** (Level A) — Ensure hover tooltips don't contain unique critical info |

---

### Medium

#### M1. Focus Order on Initial Load
| Field | Detail |
|-------|--------|
| **Description** | User reported multiple Tab presses before focus became apparent. First focusable element may not be obvious, or focus may start on an element that is off-screen or visually hidden. |
| **Location** | All pages (initial load) |
| **Impact** | Users may believe the page is unresponsive or that keyboard navigation is broken. Adds confusion and delay. |
| **Recommended Fix** | Ensure first focusable element is the skip link (when added) or a logical starting point. Verify no `tabindex="-1"` or `visibility: hidden` elements receive focus. |
| **WCAG** | **2.4.3 Focus Order** (Level A) — Focus order preserves meaning and operability |

---

#### M2. Form Error Handling and Focus Management
| Field | Detail |
|-------|--------|
| **Description** | Contact form validation and error handling were not fully tested. If validation errors occur, focus may not move to the first error. Error messages may not be programmatically associated with fields. |
| **Location** | Contact page (contact form) |
| **Impact** | Users with motor impairment may not notice validation errors. Correcting and resubmitting requires additional navigation. |
| **Recommended Fix** | On validation failure, move focus to the first invalid field. Associate error messages with fields via `aria-describedby` or `aria-errormessage`. Use clear, actionable error text. |
| **WCAG** | **3.3.1 Error Identification** (Level A); **3.3.3 Error Suggestion** (Level AA); **2.4.7 Focus Visible** (Level AA) |

---

#### M3. No Time Limits (Verification)
| Field | Detail |
|-------|--------|
| **Description** | Form session timeout or countdown timers were not observed. If present, they would block users who need extra time to complete forms. |
| **Location** | Contact form, any multi-step flows |
| **Impact** | Users with motor impairment move slowly. Time limits cause stress and task failure. |
| **Recommended Fix** | Do not impose time limits on form completion. If session expiry exists, allow user to extend. Provide warning before expiry. |
| **WCAG** | **2.2.1 Timing Adjustable** (Level A) |

---

### Low

#### L1. Social Icons and Footer Links
| Field | Detail |
|-------|--------|
| **Description** | Social media icons and footer links may have small hit areas. Icon-only buttons require `aria-label` for accessibility. |
| **Location** | Header, footer |
| **Impact** | Minor. Users can tab to them, but small targets increase misclick risk. Icon-only without labels is problematic for voice control users. |
| **Recommended Fix** | Ensure 44×44px minimum. Add visible or `aria-label` text for icon-only buttons. |
| **WCAG** | **2.5.5 Target Size** (Level AAA); **4.1.2 Name, Role, Value** (Level A) |

---

#### L2. Drag-and-Drop
| Field | Detail |
|-------|--------|
| **Description** | No drag-and-drop functionality was identified. If any exists (e.g., reordering, file upload with drag), it would be inaccessible to this persona. |
| **Location** | N/A (none found) |
| **Impact** | None if absent. Critical if present without alternative. |
| **Recommended Fix** | If drag-and-drop is added, provide keyboard alternative (e.g., Move Up/Move Down buttons, click to select then activate). |
| **WCAG** | **2.1.1 Keyboard** (Level A) |

---

## WCAG Guidelines Referenced

| Guideline | Level | Relevance |
|-----------|-------|-----------|
| 2.1.1 Keyboard | A | All functionality operable via keyboard |
| 2.1.2 No Keyboard Trap | A | Focus can escape modals, carousels |
| 2.2.1 Timing Adjustable | A | No form timeouts |
| 2.2.2 Pause, Stop, Hide | A | Carousel pause controls |
| 2.4.1 Bypass Blocks | A | Skip links |
| 2.4.3 Focus Order | A | Logical tab order |
| 2.4.7 Focus Visible | AA | Visible focus indicators |
| 2.5.5 Target Size | AAA | 44×44px minimum |
| 2.5.8 Target Size (Minimum) | AA (2.2) | 24×24px minimum |
| 3.3.1 Error Identification | A | Form validation |
| 3.3.2 Labels or Instructions | A | Form labels |
| 3.3.3 Error Suggestion | AA | Form error messages |
| 4.1.2 Name, Role, Value | A | Icon labels |

---

## Priority Recommendations

### P0 (Immediate)
1. **Add "Skip to main content" link** — First focusable element on every page. Visible on focus. Target main content landmark.
2. **Fix focus indicators** — Ensure every focusable element has a visible focus style (min 3:1 contrast). Never use `outline: none` without replacement.
3. **Increase click target sizes** — All interactive elements to minimum 44×44px. "Learn More" links, arrow icons, form controls.
4. **Reorganize Contact page** — Place contact form and direct contact details (phone, email) above testimonials. Add "Skip to contact form" link.

### P1 (High)
5. **Enlarge form field hit areas** — Minimum 44px height. Ensure labels extend clickable region.
6. **Verify navigation link target size** — Add padding to achieve 44×44px for nav links.
7. **Audit carousels** — Add keyboard-accessible Previous/Next, Arrow key support, pause control. Verify no keyboard traps.
8. **Audit hover-dependent interactions** — Ensure dropdowns open on focus/Enter. No critical content in hover-only tooltips.

### P2 (Medium)
9. **Verify focus order on load** — First focusable element should be skip link. No hidden elements receiving focus.
10. **Improve form error handling** — Move focus to first error. Associate errors with fields. Clear, actionable messages.
11. **Verify no time limits** — No form timeout or session expiry that blocks completion.

### P3 (Low)
12. **Footer and social icons** — 44×44px minimum. `aria-label` for icon-only buttons.
13. **If drag-and-drop added** — Provide keyboard alternative.

---

*This report is based on persona-driven evaluation (Marcus Okonkwo, motor impairment with essential tremor and cerebral palsy) and content analysis of https://launchpadlab.com/. Testing was performed using keyboard-only navigation. Target size measurements should be verified with browser DevTools. Automated testing (e.g., axe, Lighthouse) can supplement these findings.*
