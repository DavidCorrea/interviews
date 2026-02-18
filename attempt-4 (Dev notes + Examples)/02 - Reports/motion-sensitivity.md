# Accessibility Report: Motion Sensitivity / Vestibular Disorder

**Persona**: Taylor Kim — Vestibular disorder, motion sensitivity
**Site**: https://launchpadlab.com/
**Date**: February 16, 2026
**Evaluator Setting**: `prefers-reduced-motion: reduce` enabled in OS/browser

---

## Executive Summary

The LaunchPad Lab website contains numerous motion-based elements — scroll-triggered animations, counting number animations, CSS transitions, hover state animations, and smooth scrolling — the majority of which do **not** respect the `prefers-reduced-motion` user preference. While the logo scroller component correctly checks this media query and disables its animation, all other motion on the site plays unconditionally. The site's main CSS file contains **zero** `@media (prefers-reduced-motion: reduce)` declarations. For users with vestibular disorders, the cumulative motion across the site creates a physically uncomfortable and potentially unusable experience.

---

## Issues Found

### Issue 1: AOS (Animate on Scroll) Library Does Not Respect `prefers-reduced-motion`

**Pages Affected**: All pages (Homepage, Contact, About, Services — confirmed on each)

**Element(s)**:
- Homepage hero text block: `<div class="text-block" data-aos="fade-up" data-aos-duration="1000">` (1-second fade-up)
- Six service cards on homepage: `<li class="card" data-aos="fade-up" data-aos-duration="200">` (200ms fade-up each)
- Contact page hero text: `data-aos="fade-up" data-aos-duration="1000"`
- Contact page cards: `data-aos="fade-up" data-aos-duration="200"` (3 cards)
- About page hero text: `data-aos="fade-up" data-aos-duration="1000"`
- About page image blocks: `data-aos="fade-right"`
- Services page hero text: `data-aos="fade-up" data-aos-duration="1000"`
- Services page image blocks: `data-aos="fade-right"` (multiple)
- Services page cards: `data-aos="fade-up" data-aos-duration="200"` (6 cards)

**Root Cause**: AOS is initialized with `AOS.init()` (no configuration) at the bottom of every page. The AOS library supports a `disable` option that can accept a function or condition to disable animations (e.g., when `prefers-reduced-motion` matches), but this option is not used.

**WCAG Criteria Violated**:
- **2.3.3 Animation from Interactions (Level AAA)** — Motion animation triggered by interaction (scrolling) cannot be disabled by the user.
- **2.3.1 Three Flashes or Below Threshold (Level A)** — While individual animations don't flash, the cumulative rapid-fire triggering of multiple fade-up animations during normal scrolling creates a sustained motion effect.

**Severity**: **Critical**

This is the most pervasive motion issue on the site. Every page has scroll-triggered animations that fire regardless of user preference. For a user with a vestibular disorder, scrolling through any page triggers repeated motion that cannot be avoided, reduced, or disabled.

**Recommended Fix**:
```javascript
// Replace: AOS.init();
// With:
AOS.init({
  disable: window.matchMedia('(prefers-reduced-motion: reduce)').matches
});
```
Alternatively, add a CSS override:
```css
@media (prefers-reduced-motion: reduce) {
  [data-aos] {
    opacity: 1 !important;
    transform: none !important;
    transition: none !important;
  }
}
```

**Impact on User**: Every page visit triggers multiple animations during normal scrolling. Taylor experienced dizziness and vestibular discomfort while scrolling through the homepage and service cards. The motion is unavoidable — the content is hidden until the animation plays.

---

### Issue 2: Statistics Counter Animation Ignores `prefers-reduced-motion`

**Pages Affected**: Homepage (`/`), About page (`/about/`)

**Element(s)**:
- `<section class="stats-wrapper animation-on">` containing:
  - "12+" Years in Business
  - "730+" Projects
  - "240+" Clients

**Root Cause**: The file `stats-animation.js` uses `IntersectionObserver` to detect when the stats section enters the viewport, then animates numbers from 0 to their final value over 2,000 milliseconds using `requestAnimationFrame`. The script checks for the `animation-on` CSS class but does **not** check `prefers-reduced-motion`.

**WCAG Criteria Violated**:
- **2.3.3 Animation from Interactions (Level AAA)** — The counting animation is triggered by scrolling (an interaction) and cannot be disabled.
- **2.2.2 Pause, Stop, Hide (Level A)** — The animation runs for 2 seconds with no mechanism to pause, stop, or hide it.

**Severity**: **Major**

Rapidly changing numbers in a fixed area of the viewport creates a sustained visual disturbance. The animation runs for a full 2 seconds with continuous numeric updates.

**Recommended Fix**:
```javascript
// Add at the start of the DOMContentLoaded handler in stats-animation.js:
if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
  return; // Numbers display at their final values without animation
}
```

**Impact on User**: Taylor had to avert their gaze for ~2 seconds while the numbers counted up, then look back to verify the animation had completed. The rapid numeric changes in a confined area triggered mild dizziness.

---

### Issue 3: CSS Stylesheet Contains No `prefers-reduced-motion` Media Queries

**Pages Affected**: All pages (global stylesheet)

**Element(s)**: The theme stylesheet at `/wp-content/themes/lpl/style.css` defines multiple CSS keyframe animations and transitions:
- `@keyframes fade-in` (opacity 0 to 1)
- `@keyframes slide-in-left` (translateX(-100%) to 0)
- `@keyframes fade-in-right` (translateX(50%) to 0)
- `@keyframes fade-in-left` (translateX(-50%) to 0)
- `@keyframes fade-in-bottom` (translateY(100%) to 0)
- Numerous `transition: all 0.3s ease-in-out` on buttons, links, and interactive elements

**Root Cause**: The stylesheet contains **zero** `@media (prefers-reduced-motion: reduce)` declarations. All CSS animations and transitions run unconditionally.

**WCAG Criteria Violated**:
- **2.3.3 Animation from Interactions (Level AAA)** — CSS animations triggered by interactions (hover, focus, page load) cannot be disabled.

**Severity**: **Major**

While individual CSS transitions (e.g., button hover color change over 0.3s) are minor, the absence of *any* reduced-motion media query in the entire stylesheet indicates a systemic gap. The keyframe animations in particular (`slide-in-left`, `fade-in-bottom`, etc.) involve translation/movement that is problematic for vestibular users.

**Recommended Fix**:
```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```
For a more targeted approach, override specific keyframes and transitions individually.

**Impact on User**: CSS keyframe animations and transitions contribute to the overall motion load. While each is small, they compound across the site experience.

---

### Issue 4: Service Card Hover Animations Not Reducible

**Pages Affected**: Homepage (`/`), Services page (`/services/`), Contact page (`/contact/`)

**Element(s)**:
- `.cards-wrapper.hover-cards-interaction .card:hover` — On hover:
  - Background color transitions to `#1e60bd` (blue)
  - Icon and `h3` heading animate to `opacity: 0`
  - Hidden `.text-block-inner` transitions from `max-height: 0; opacity: 0` to `max-height: 1000px; opacity: 1`
  - Arrow icons swap visibility
- CSS transitions use `cubic-bezier(0.4, 0, 0.2, 1)` easing over 0.2–0.4 seconds

**Root Cause**: The hover state changes involve multiple simultaneous CSS transitions (background-color, opacity, max-height, color, position) with no `prefers-reduced-motion` override. The card effectively "transforms" its entire appearance on hover.

**WCAG Criteria Violated**:
- **2.3.3 Animation from Interactions (Level AAA)** — Hover interaction triggers animation that cannot be disabled.

**Severity**: **Major**

The card hover effect is particularly problematic because it involves the simultaneous disappearance of existing content (icon, heading) and appearance of new content (description text), creating a disorienting "flip" sensation. Users hovering over cards while scanning the page encounter this repeatedly.

**Recommended Fix**:
```css
@media (prefers-reduced-motion: reduce) {
  .cards-wrapper.hover-cards-interaction .card,
  .cards-wrapper.hover-cards-interaction .card h3,
  .cards-wrapper.hover-cards-interaction .card .icon,
  .cards-wrapper.hover-cards-interaction .card .text-block-inner {
    transition: none !important;
  }
}
```

**Impact on User**: Taylor found the card hover transitions disorienting, as the multi-property animation under the cursor created an unexpected and uncontrollable visual shift.

---

### Issue 5: Mega Menu Dropdown Animation

**Pages Affected**: All pages (global navigation)

**Element(s)**:
- `<ul id="mega-menu-menu-1" ... data-effect="fade_up" data-effect-speed="200" data-effect-mobile="slide_right" data-effect-speed-mobile="200">`
- Affects "Services" dropdown and "Industries" dropdown mega menus

**Root Cause**: The Max Mega Menu plugin is configured with `fade_up` animation effect at 200ms. The plugin does not check `prefers-reduced-motion` before applying the dropdown animation.

**WCAG Criteria Violated**:
- **2.3.3 Animation from Interactions (Level AAA)** — Navigation dropdown animation triggered by hover/click cannot be disabled.

**Severity**: **Minor**

The animation is short (200ms) and relatively subtle (fade with upward motion). However, it fires every time the user interacts with the primary navigation, which is frequent during normal browsing.

**Recommended Fix**: Configure the mega menu plugin to use `data-effect="disabled"` or add CSS:
```css
@media (prefers-reduced-motion: reduce) {
  .mega-menu-megamenu,
  .mega-sub-menu {
    transition: none !important;
    animation: none !important;
    opacity: 1 !important;
    transform: none !important;
  }
}
```

**Impact on User**: Mild discomfort from repeated navigation use. Individually tolerable, but contributes to cumulative motion fatigue.

---

### Issue 6: Smooth Scrolling for Anchor Links Ignores `prefers-reduced-motion`

**Pages Affected**: All pages (global behavior)

**Element(s)**:
- Custom JavaScript selecting all `a[href^="#"]` links and applying:
  ```javascript
  targetElement.scrollIntoView({
    behavior: 'smooth',
    block: 'start'
  });
  ```

**Root Cause**: The smooth scroll implementation uses a hardcoded `behavior: 'smooth'` without checking `prefers-reduced-motion`. The JavaScript `scrollIntoView` API does not automatically respect the OS media query preference.

**WCAG Criteria Violated**:
- **2.3.3 Animation from Interactions (Level AAA)** — Smooth scroll animation triggered by clicking an anchor link cannot be disabled.

**Severity**: **Major**

Smooth scrolling causes the entire viewport to move, which is one of the most disorienting motion types for vestibular users. Every anchor link click (including the "Connect with an Expert" CTA on the homepage) triggers a gliding scroll animation.

**Recommended Fix**:
```javascript
const behavior = window.matchMedia('(prefers-reduced-motion: reduce)').matches
  ? 'auto'
  : 'smooth';

targetElement.scrollIntoView({
  behavior: behavior,
  block: 'start'
});
```
Or add a global CSS declaration:
```css
@media (prefers-reduced-motion: reduce) {
  html {
    scroll-behavior: auto !important;
  }
}
```

**Impact on User**: Clicking any anchor link causes the viewport to glide rather than jump, creating a full-page scrolling motion that directly triggers vestibular discomfort.

---

### Issue 7: Case Study Carousel Slide Transitions

**Pages Affected**: Homepage (`/`)

**Element(s)**:
- `<ul class="outcome-slider">` containing Prosci, CDK Global, and Millennium Trust Company case studies
- Powered by tiny-slider library

**Root Cause**: While `autoplay: false` is correctly set (preventing autonomous motion), the slide transition animation when manually navigating between slides is not disabled for `prefers-reduced-motion`.

**WCAG Criteria Violated**:
- **2.3.3 Animation from Interactions (Level AAA)** — Slide transition animation on manual navigation cannot be disabled.

**Severity**: **Minor**

The carousel does not autoplay, which is the correct baseline. The slide transition animation on manual interaction is a lower-severity issue since the user controls when it happens.

**Recommended Fix**: Configure tiny-slider with `speed: 0` when `prefers-reduced-motion: reduce` is detected:
```javascript
var speed = window.matchMedia('(prefers-reduced-motion: reduce)').matches ? 0 : 300;
```

**Impact on User**: Controllable by the user (only fires on manual interaction), but the horizontal sliding motion between case studies can still trigger mild discomfort.

---

## Positive Findings

| Element | Implementation | Notes |
|---------|---------------|-------|
| Logo scroller (client logos) | Checks `prefers-reduced-motion: reduce` via `window.matchMedia()` before enabling infinite scroll animation | Correctly static when preference is set |
| Award logo scroller | Same implementation as client logo scroller | Correctly static when preference is set |
| Wistia video embed | No autoplay parameter; video requires manual click to play | Does not force motion on the user |
| Tiny-slider carousels | `autoplay: false` configured on all carousel instances | No autonomous motion from carousels |
| Skip link | `<a class="skip-link screen-reader-text" href="#primary">Skip to content</a>` present | Standard accessibility feature present |

---

## Summary of Issues

| # | Issue | WCAG Criterion | Severity | Pages Affected |
|---|-------|---------------|----------|----------------|
| 1 | AOS scroll-triggered animations ignore `prefers-reduced-motion` | 2.3.3 (AAA), 2.3.1 (A) | **Critical** | All pages |
| 2 | Stats counter animation ignores `prefers-reduced-motion` | 2.3.3 (AAA), 2.2.2 (A) | **Major** | Homepage, About |
| 3 | CSS stylesheet has zero `prefers-reduced-motion` queries | 2.3.3 (AAA) | **Major** | All pages (global CSS) |
| 4 | Service card hover animations not reducible | 2.3.3 (AAA) | **Major** | Homepage, Services, Contact |
| 5 | Mega menu dropdown animation | 2.3.3 (AAA) | **Minor** | All pages (global nav) |
| 6 | Smooth scrolling ignores `prefers-reduced-motion` | 2.3.3 (AAA) | **Major** | All pages |
| 7 | Case study carousel slide transitions | 2.3.3 (AAA) | **Minor** | Homepage |

**Critical Issues**: 1
**Major Issues**: 4
**Minor Issues**: 2

---

## Recommendations Summary

### Immediate (Critical)
1. **Add `prefers-reduced-motion` check to AOS initialization** — Single line change that eliminates the most pervasive motion issue across the entire site.

### Short-Term (Major)
2. **Add a global `prefers-reduced-motion` media query to the CSS** — A blanket rule that reduces `animation-duration` and `transition-duration` to near-zero for users with the preference set.
3. **Add `prefers-reduced-motion` check to `stats-animation.js`** — Skip the counting animation and display final numbers immediately.
4. **Conditionally set smooth scrolling behavior** — Check the media query before applying `behavior: 'smooth'`.

### Medium-Term (Minor)
5. **Configure mega menu to disable dropdown animation** when `prefers-reduced-motion` is detected.
6. **Set carousel transition speed to 0** for reduced-motion users.

### Systemic Recommendation
The logo scroller implementation demonstrates that the development team understands `prefers-reduced-motion`. The recommended approach is to apply this same pattern consistently across all motion on the site. A global CSS media query (Recommendation #2) would address most issues in a single change. Individual JavaScript-driven animations (AOS, stats counter) require separate checks.
