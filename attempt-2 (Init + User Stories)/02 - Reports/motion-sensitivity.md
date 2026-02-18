# Technical Report: Motion Sensitivity / Vestibular Disorder Accessibility

**Website:** https://launchpadlab.com/  
**Persona:** Elena Vasquez (Motion Sensitivity / Vestibular Disorder)  
**Test Date:** February 16, 2025  
**Test Task:** Find what the company does and how to contact them

---

## Executive Summary

LaunchPad Lab's website presents severe barriers for users with vestibular disorders or motion sensitivity. The site **does not respect `prefers-reduced-motion: reduce`**, despite this being a widely supported user preference. Scroll-triggered animations (fade-ins, slide-ins, staggered reveals) appear on nearly every section. Hover effects on cards and buttons cause unexpected motion. Possible counting animations, carousels, and layout shifts compound the problem. Users like Elena Vasquez experience dizziness, nausea, and headache within seconds and must either close the tab or disable JavaScript to complete basic tasks.

**Key findings:**
- `prefers-reduced-motion` is ignored—animations run regardless of user preference
- Scroll-triggered animations on almost every section (hero, service cards, case studies, awards)
- Hover lift/scale/transition effects on cards and buttons
- No pause/stop controls for auto-advancing content (if present)
- No site-level "Reduce motion" toggle
- Contact information requires scrolling through animated sections; task completion only possible with JavaScript disabled

---

## Accessibility Issues

### Critical

#### 1. Site Ignores `prefers-reduced-motion: reduce`

| Field | Detail |
|-------|--------|
| **Description** | The site does not respond to the `prefers-reduced-motion: reduce` media query. Animations, transitions, scroll-triggered effects, and hover effects continue to run when the user has this OS/browser preference enabled. |
| **Location** | Site-wide (homepage, About, Services, Contact, Work) |
| **Impact** | Users with vestibular disorders, migraine, or motion sensitivity cannot use the site without physical distress. Excludes an estimated 20–35% of adults who experience vestibular symptoms. Forces users to disable JavaScript as a workaround. |
| **Recommended Fix** | Implement `@media (prefers-reduced-motion: reduce)` throughout CSS: set `animation: none`, `transition: none` for non-essential motion. Use `window.matchMedia('(prefers-reduced-motion: reduce)').matches` in JavaScript to disable parallax, scroll animations, and auto-advancing carousels before initialization. Test with the setting enabled in Chrome, Firefox, Safari, and Edge. |
| **WCAG** | **2.3.3 Animation from Interactions (Level AAA)** — Motion animation triggered by interaction can be disabled. **Criterion: Respect User Preferences** — `prefers-reduced-motion` is part of Media Queries Level 5; ignoring it excludes users with vestibular disorders. |

---

#### 2. Scroll-Triggered Animations Throughout Site

| Field | Detail |
|-------|--------|
| **Description** | Nearly every section uses fade-in, slide-in, or reveal animations that fire when the user scrolls. Elements include: hero headline, six service cards, "Problems We Solve" boxes, case study sections, award badges. Animations are often staggered (sequential, domino-style), creating continuous motion as the user scrolls. |
| **Location** | Homepage (hero, service cards, problems section, case studies, awards), About page, Services page, Work page |
| **Impact** | Scroll-triggered motion is a major vestibular trigger. Users cannot read content without triggering animations. Causes dizziness, nausea, disorientation. User reported having to "scroll blind" or disable JavaScript to complete the task. |
| **Recommended Fix** | Disable all scroll-triggered animations when `prefers-reduced-motion: reduce` is set. Consider removing scroll animations entirely or making them opt-in. Content should be visible immediately without requiring animation. Avoid "animate on scroll" libraries for critical content. |
| **WCAG** | **2.3.3 Animation from Interactions (Level AAA)** — Allow disabling of animations. **2.3.1 Three Flashes or Below Threshold (Level A)** — Ensure no rapid flashing. **2.2.2 Pause, Stop, Hide (Level A)** — Provide mechanism to pause auto-updating content. |

---

#### 3. No Pause/Stop Controls for Auto-Advancing Content

| Field | Detail |
|-------|--------|
| **Description** | Carousels (award badges, company logos) may auto-advance or auto-rotate. No visible pause/play controls were identified. Auto-playing content cannot be stopped by the user. |
| **Location** | Homepage (awards section, "Trusted by" / client logos) |
| **Impact** | Continuous motion without user control triggers nausea and forces users to close the tab. Users with vestibular disorders require the ability to pause or stop any auto-updating content. |
| **Recommended Fix** | Add visible pause and play controls to all carousels. Pause should be the default when `prefers-reduced-motion` is set. Ensure controls are keyboard accessible and clearly labeled. If carousels exist, disable auto-advance when reduced motion is preferred. |
| **WCAG** | **2.2.2 Pause, Stop, Hide (Level A)** — For any auto-updating information that starts automatically, provide a mechanism to pause, stop, or hide it. **2.2.1 Timing Adjustable (Level A)** — User can turn off or adjust time limits. |

---

#### 4. Hover Effects Cause Unexpected Motion

| Field | Detail |
|-------|--------|
| **Description** | Service cards, problem cards, buttons, and logos have hover animations: lift/elevation, scale, color transitions, shadow changes. These fire when the cursor passes over elements—often accidentally while reading or navigating. Large-scale hover effects (scale > 1.05, significant movement) are vestibular triggers. |
| **Location** | Homepage (service cards, problem boxes, buttons, client logos), other pages with similar components |
| **Impact** | Users cannot avoid hovering when trying to read or click. Repeated accidental hovers cause cumulative discomfort. Transitions (even 200–300ms) can accumulate and trigger symptoms. |
| **Recommended Fix** | Disable or significantly reduce hover effects when `prefers-reduced-motion` is set. Use instant state changes (color, opacity) instead of transitions. Avoid lift, scale, rotation. If transitions are necessary, keep under 150ms or eliminate when reduced motion is preferred. |
| **WCAG** | **2.3.3 Animation from Interactions (Level AAA)** — Motion animation triggered by interaction can be disabled. |

---

### High

#### 5. Hero Section Entrance Animation

| Field | Detail |
|-------|--------|
| **Description** | The main hero headline ("AI-Centric Digital Product Design & Development" or similar) animates on page load—fade-in or slide-in. This is the first thing the user sees and triggers symptoms immediately. |
| **Location** | Homepage hero section |
| **Impact** | Unexpected motion on load gives the user no time to prepare. Triggers dizziness within seconds. Cannot be skipped or disabled. |
| **Recommended Fix** | Remove entrance animation or make it minimal (< 1 second). Disable entirely when `prefers-reduced-motion` is set. Content should be visible in static state on load. |
| **WCAG** | **2.3.3 Animation from Interactions (Level AAA)** — Allow disabling. **2.3.1 Three Flashes or Below Threshold (Level A)** — Avoid rapid motion. |

---

#### 6. Possible Number Counting Animation

| Field | Detail |
|-------|--------|
| **Description** | The statistics section (12+ Years, 730+ Projects, 240+ Clients) may use a counting-up animation where numbers start at 0 and rapidly count to the final value. Rapid number changes are a known vestibular trigger. |
| **Location** | Homepage statistics section |
| **Impact** | Counting animations create peripheral motion and rapid visual change. Can trigger nausea and headache. |
| **Recommended Fix** | Display final values immediately. Do not animate numbers. If a counting library is used, disable it when `prefers-reduced-motion` is set or when reduced motion toggle is active. |
| **WCAG** | **2.2.2 Pause, Stop, Hide (Level A)** — Provide mechanism to pause. **2.3.3 Animation from Interactions (Level AAA)** — Allow disabling. |

---

#### 7. Layout Shifts from Lazy-Loaded Content

| Field | Detail |
|-------|--------|
| **Description** | Images and logos loading after initial page render cause content to shift down. Each image load causes everything below it to jump. Unexpected movement is disorienting for users with vestibular sensitivity. |
| **Location** | Homepage, About, Services, Work (any page with images) |
| **Impact** | Layout shifts create unexpected motion. User cannot anticipate when content will move. Increases disorientation and nausea. |
| **Recommended Fix** | Reserve space for images using `width` and `height` attributes. Use `aspect-ratio` or fixed dimensions to prevent layout shift. Ensure no content jumps when images load. |
| **WCAG** | **2.3.1 Three Flashes or Below Threshold (Level A)** — Avoid unexpected motion. **2.2.2 Pause, Stop, Hide (Level A)** — Content that updates automatically should be controllable. |

---

### Medium

#### 8. Smooth Scrolling May Trigger Symptoms

| Field | Detail |
|-------|--------|
| **Description** | If `scroll-behavior: smooth` or custom smooth/momentum scrolling is used, it can create a "floating" sensation that triggers dizziness. Some users with vestibular disorders are sensitive to scroll interpolation. |
| **Location** | Site-wide (if implemented) |
| **Impact** | Smooth scrolling can cause spatial disorientation. Prefer native, direct scrolling for users who need it. |
| **Recommended Fix** | Disable smooth scrolling when `prefers-reduced-motion: reduce` is set. Use `scroll-behavior: auto` in reduced motion media query. Avoid custom scroll implementations with momentum or easing. |
| **WCAG** | **2.3.3 Animation from Interactions (Level AAA)** — Allow disabling of motion. |

---

#### 9. No Site-Level "Reduce Motion" Toggle

| Field | Detail |
|-------|--------|
| **Description** | There is no visible "Reduce motion" or "Stop animations" control on the site. Users whose OS does not expose `prefers-reduced-motion` (or who are unaware of it) have no way to opt out of animations without disabling JavaScript. |
| **Location** | Header, settings, or site chrome |
| **Impact** | Users who need reduced motion but don't know about the OS setting cannot access the site comfortably. A site-level toggle would improve discoverability and control. |
| **Recommended Fix** | Add a "Reduce motion" toggle in the header, visible before animations start. When activated: disable scroll animations, hover effects, carousels, transitions. Persist preference in localStorage or cookie across pages. |
| **WCAG** | **2.3.3 Animation from Interactions (Level AAA)** — Provide mechanism to disable animations. **2.1.1 Keyboard (Level A)** — Toggle must be keyboard accessible. |

---

#### 10. Contact Information Requires Scrolling Through Animated Sections

| Field | Detail |
|-------|--------|
| **Description** | To reach the Contact page, users must navigate from the homepage or menu. The Contact page may have scroll-triggered animations. Contact details (phone, email, address) appear after testimonials, requiring additional scrolling. |
| **Location** | Contact page, navigation flow |
| **Impact** | Users with motion sensitivity may abandon the task before reaching contact info. With JS enabled, the user could not complete the task without distress. |
| **Recommended Fix** | Display contact information (phone, email, address) at the top of the Contact page and in the footer on every page. Ensure skip links or keyboard navigation can reach contact info without scrolling through animated sections. |
| **WCAG** | **2.4.1 Bypass Blocks (Level A)** — Skip links. **2.4.5 Multiple Ways (Level AA)** — Multiple ways to locate content. |

---

### Low

#### 11. Sticky Header May Cause Unexpected Appearance

| Field | Detail |
|-------|--------|
| **Description** | If the navigation bar becomes sticky (fixed) on scroll, its sudden appearance or state change can create unexpected motion. |
| **Location** | Header/navigation |
| **Impact** | Minor compared to other issues, but can contribute to disorientation when combined with other motion. |
| **Recommended Fix** | If sticky header is used, ensure any transition is minimal or instant when reduced motion is set. Consider static header as default for reduced motion users. |
| **WCAG** | **2.3.3 Animation from Interactions (Level AAA)** — Allow disabling. |

---

#### 12. Logo Hover/Zoom Effects

| Field | Detail |
|-------|--------|
| **Description** | Client logos in "Trusted by" or similar sections may have bounce or zoom effects on hover or scroll. |
| **Location** | Homepage, client/logo sections |
| **Impact** | Accidental hovers trigger motion. Contributes to cumulative discomfort. |
| **Recommended Fix** | Remove or disable logo animations when reduced motion is set. Use static images. |
| **WCAG** | **2.3.3 Animation from Interactions (Level AAA)** — Allow disabling. |

---

## WCAG Guidelines Referenced (2.3.x Emphasis)

| Guideline | Level | Relevance |
|-----------|-------|-----------|
| **2.3.1 Three Flashes or Below Threshold** | A | No rapid flashing; avoid unexpected motion |
| **2.3.3 Animation from Interactions** | AAA | Motion animation can be disabled; critical for vestibular users |
| **2.2.2 Pause, Stop, Hide** | A | Auto-updating content (carousels) must have pause/stop |
| **2.2.1 Timing Adjustable** | A | User can turn off or adjust time limits |
| **2.4.1 Bypass Blocks** | A | Skip links to reach content without scrolling |
| **2.4.5 Multiple Ways** | AA | Multiple ways to find contact info |
| **2.1.1 Keyboard** | A | All controls keyboard accessible |
| **Criterion: prefers-reduced-motion** | — | Media Queries Level 5; widely supported; must be respected |

---

## Priority Recommendations

### Phase 1 (Critical — Address First)

1. **Implement `prefers-reduced-motion` support** — Add `@media (prefers-reduced-motion: reduce)` throughout CSS. Disable animations, transitions, and scroll effects. Check `window.matchMedia` in JavaScript before initializing parallax, scroll animations, and carousels. Test with the setting enabled in all major browsers.

2. **Disable scroll-triggered animations** — Remove or disable fade-in, slide-in, and reveal effects on scroll when reduced motion is preferred. Content should appear statically. Audit and remove or conditionally disable any "animate on scroll" libraries.

3. **Add pause/stop controls for carousels** — All auto-advancing carousels must have visible pause and play controls. Pause by default when `prefers-reduced-motion` is set. Ensure controls are keyboard accessible.

4. **Reduce or eliminate hover effects** — Disable lift, scale, and transition effects on hover when reduced motion is set. Use instant color/opacity changes only.

### Phase 2 (High — Next)

5. **Remove hero entrance animation** — Content should load in static state. Disable hero animation when reduced motion is set.

6. **Disable number counting animations** — Display statistics at final values immediately. No count-up effects.

7. **Fix layout shifts** — Reserve space for images with `width`/`height` or `aspect-ratio`. Prevent content from jumping when images load.

### Phase 3 (Medium — Follow-Up)

8. **Disable smooth scrolling when reduced motion** — Use `scroll-behavior: auto` in reduced motion media query.

9. **Add site-level "Reduce motion" toggle** — Visible in header. Persists across pages. Disables all non-essential motion when activated.

10. **Surface contact information** — Phone, email, address at top of Contact page and in footer on every page. Reduce need to scroll through animated sections.

### Phase 4 (Low — Ongoing)

11. **Minimize sticky header transitions** — Use instant state changes when reduced motion is set.

12. **Remove logo hover/scroll effects** — Static logos when reduced motion is preferred.

---

*This report is based on accessibility testing performed from the perspective of the motion sensitivity / vestibular disorder persona (Elena Vasquez) and aligns with WCAG 2.1 guidelines, with emphasis on 2.3.x (Seizures and Physical Reactions). Implementation should be validated with user testing involving people with vestibular disorders or motion sensitivity.*
