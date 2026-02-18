# Accessibility Technical Report: Motion Sensitivity (Vestibular Disorder)

**Persona:** Sam Okonkwo (Motion Sensitivity / Vestibular Disorder)  
**Website:** https://launchpadlab.com/  
**Date:** February 16, 2025  
**Testing Focus:** Motion, animation, `prefers-reduced-motion` support, and vestibular accessibility.

---

## Executive Summary

The LaunchPad Lab website presents critical accessibility barriers for users with vestibular disorders and motion sensitivity. The site does **not** respect `prefers-reduced-motion: reduce`. Scroll-triggered animations (fade-ins, slide-ins, staggered reveals) fire on every scroll. Hover effects (lift, scale, shadow transitions) trigger on interactive elements. Users experience dizziness, nausea, and headaches while attempting to complete basic tasks. Severity ranges from High to Critical. WCAG 2.1 Success Criteria 2.3.3 (Animation from Interactions), 2.2.2 (Pause, Stop, Hide), and 2.3.1 (Three Flashes or Below Threshold) are violated or at risk.

---

## Issues Identified

### 1. `prefers-reduced-motion` Not Respected

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.3.3 Animation from Interactions (Level AAA) |
| **Severity** | Critical |
| **Finding** | The site ignores the `prefers-reduced-motion: reduce` media query. Scroll-triggered animations, hover effects, and other motion continue unchanged when the user has the OS/browser preference set. |
| **Impact** | Users with vestibular disorders cannot use the site without triggering physical symptoms. The site explicitly disregards a well-established accessibility preference. |
| **Fix** | Implement `@media (prefers-reduced-motion: reduce)` in CSS to disable or simplify animations. For JavaScript-driven animations (scroll observers, Intersection Observer), check `window.matchMedia('(prefers-reduced-motion: reduce)').matches` before applying motion. Replace animated reveals with instant content display. |
| **WCAG Criterion** | 2.3.3 Animation from Interactions — "Motion animation triggered by interaction can be disabled" |

---

### 2. Scroll-Triggered Animations (Fade-ins, Slide-ins)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.3.3 Animation from Interactions, 2.2.2 Pause, Stop, Hide |
| **Severity** | Critical |
| **Finding** | Content animates into view on scroll. Hero, client logos, services, statistics, testimonials, case studies—each section triggers fade-in, slide-in, or similar effects as the user scrolls. Motion occurs on every scroll action. |
| **Impact** | Vestibular conflict: visual motion conflicts with stationary body. Triggers dizziness, vertigo, nausea. Users cannot read or navigate without repeatedly triggering motion. Scrolling becomes a barrier. |
| **Fix** | Disable scroll-triggered animations when `prefers-reduced-motion` is set. Use `visibility` and `opacity: 1` without transitions. Content appears instantly when in viewport. For all users, consider reducing motion density or providing a site-level "Reduce motion" toggle. |
| **WCAG Criterion** | 2.3.3, 2.2.2 |

---

### 3. Staggered Reveals

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.3.3 Animation from Interactions |
| **Severity** | High |
| **Finding** | Multiple elements animate in sequence (e.g., six service boxes, statistics, award badges). Staggered timing prolongs motion. |
| **Impact** | Prolonged motion amplifies symptoms. Single fade is problematic; six elements fading one after another is six times worse. Users report needing to look away or close eyes. |
| **Fix** | When `prefers-reduced-motion` is set, show all elements instantly. No stagger. Eliminate `animation-delay` and sequential triggers. |
| **WCAG Criterion** | 2.3.3 |

---

### 4. Hover Effects (Lift, Scale, Shadow)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.3.3 Animation from Interactions |
| **Severity** | High |
| **Finding** | Service boxes, cards, and buttons use hover effects: lift (transform: translateY), scale (transform: scale), shadow transitions. Six service boxes each have hover-triggered motion. |
| **Impact** | Users must hover to discover interactivity, but each hover triggers motion. Medium severity per interaction; cumulative effect across many elements causes headache and nausea. Keyboard users may avoid hover but can still accidentally trigger via focus + mouse movement. |
| **Fix** | When `prefers-reduced-motion` is set, replace motion-based hover with static state changes: color change, underline, border. Remove `transform` and `box-shadow` transitions. Ensure focus states are visible without motion. |
| **WCAG Criterion** | 2.3.3 |

---

### 5. No Pause, Stop, or Hide Controls

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.2.2 Pause, Stop, Hide (Level A) |
| **Severity** | High |
| **Finding** | No site-level control to pause, stop, or reduce animations. No "Reduce motion" toggle, setting, or link. |
| **Impact** | Users cannot disable motion even when `prefers-reduced-motion` is ignored (e.g., in environments where the preference cannot be set). No escape. |
| **Fix** | Add a "Reduce motion" or "Accessibility" toggle in the site header or footer. When enabled, disable all non-essential animations. Persist preference (e.g., localStorage). Honor `prefers-reduced-motion` as default; toggle provides override for edge cases. |
| **WCAG Criterion** | 2.2.2 Pause, Stop, Hide — "For any moving, blinking or scrolling information that (1) starts automatically, (2) lasts more than five seconds, and (3) is presented in parallel with other content, there is a mechanism for the user to pause, stop, or hide it" |

---

### 6. Parallax Effects (If Present)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.3.3 Animation from Interactions |
| **Severity** | High |
| **Finding** | Hero section and full-width visuals may use parallax (layered motion at different scroll speeds). Creates depth illusion through motion. |
| **Impact** | Layered motion causes severe disorientation. Vestibular system cannot reconcile with reality. Users report feeling as if the room is tilting. |
| **Fix** | Disable parallax when `prefers-reduced-motion` is set. Use static background. No layered scroll effects. |
| **WCAG Criterion** | 2.3.3 |

---

### 7. Auto-Advancing Carousels (If Present)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.2.2 Pause, Stop, Hide |
| **Severity** | Critical (if present) |
| **Finding** | Client logos, testimonials, or case studies may use auto-advancing carousels. User reported no confirmed carousel; if present, would be among the worst triggers. |
| **Impact** | Continuous, uncontrollable motion. Users cannot pause. Must endure or leave. Nausea within seconds. |
| **Fix** | Provide pause/play control. Auto-advance only when user has not interacted. When `prefers-reduced-motion` is set, disable auto-advance entirely; show static content or require manual advance. |
| **WCAG Criterion** | 2.2.2 |

---

### 8. Three Flashes or Below Threshold (Risk)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.3.1 Three Flashes or Below Threshold (Level A) |
| **Severity** | To be verified |
| **Finding** | Rapid transitions, repeated hover effects, or flashing elements could approach 3 flashes per second. Staggered reveals with short delays may create flash-like effect. |
| **Impact** | Can trigger seizures in users with photosensitive epilepsy. Vestibular users also report headache from rapid, repeated motion. |
| **Fix** | Ensure no content flashes more than 3 times per second. Avoid rapid transitions. When `prefers-reduced-motion` is set, eliminate all flashing and rapid motion. |
| **WCAG Criterion** | 2.3.1 Three Flashes or Below Threshold |

---

## Summary Table

| Issue | WCAG Ref | Severity | Priority |
|-------|----------|----------|----------|
| `prefers-reduced-motion` ignored | 2.3.3 | Critical | P0 |
| Scroll-triggered animations | 2.3.3, 2.2.2 | Critical | P0 |
| Staggered reveals | 2.3.3 | High | P0 |
| Hover effects (lift, scale, shadow) | 2.3.3 | High | P1 |
| No pause/stop controls | 2.2.2 | High | P1 |
| Parallax effects | 2.3.3 | High | P1 |
| Auto-advancing carousels | 2.2.2 | Critical (if present) | P0 |
| Three flashes risk | 2.3.1 | To verify | P2 |

---

## Recommended Remediation Order

1. **Implement `prefers-reduced-motion` support** — Critical. Add CSS media query and JavaScript checks. Disable or simplify all animations when preference is set.
2. **Disable scroll-triggered animations** — Content appears instantly when in viewport. No fade, slide, or stagger.
3. **Replace motion-based hover effects** — Use color, underline, or border changes. No transform or shadow transitions.
4. **Add site-level "Reduce motion" toggle** — Provide user control. Persist preference.
5. **Disable parallax** when `prefers-reduced-motion` is set.
6. **Verify carousels** — If present, add pause control; disable auto-advance when preference is set.
7. **Audit for 2.3.1** — Ensure no content flashes more than 3 times per second.

---

## Impact on Task Completion

**Task:** Find what LaunchPad Lab does and how to contact them.

**Result:** Task completable but with significant physical discomfort. User reported dizziness, nausea, and headache. Completed task by enduring symptoms; would have abandoned earlier if not for evaluation context. Users with more severe vestibular sensitivity may not complete the task. The site is a barrier for this population.

---

## References

- [WCAG 2.1 Success Criterion 2.3.3 Animation from Interactions (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/animation-from-interactions.html)
- [WCAG 2.1 Success Criterion 2.2.2 Pause, Stop, Hide (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)
- [WCAG 2.1 Success Criterion 2.3.1 Three Flashes or Below Threshold (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/three-flashes-or-below-threshold.html)
- [MDN: prefers-reduced-motion](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion)
- [Vestibular Disorders Association](https://vestibular.org/)
