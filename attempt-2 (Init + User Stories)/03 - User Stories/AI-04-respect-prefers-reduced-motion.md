# AI-04: Respect prefers-reduced-motion

## Title
Implement `prefers-reduced-motion` support to disable all non-essential animations

## User Story
As a **user with vestibular disorders or motion sensitivity**, I want **animations and motion effects to be disabled when I have "Reduce Motion" enabled in my OS**, so that **I can use the site without experiencing dizziness, nausea, or disorientation**.

## Acceptance Criteria

- [ ] When "Reduce Motion" is enabled in OS settings, scroll-triggered animations are disabled
- [ ] Hover transitions are disabled or reduced to near-instant
- [ ] Auto-advancing carousels do not auto-advance
- [ ] Content appears statically without animation
- [ ] A visible "Reduce Motion" toggle is available in the header (optional enhancement)
- [ ] Toggle preference persists via localStorage when implemented

## How to Test

1. Enable "Reduce Motion" in OS settings:
   - **macOS**: System Preferences → Accessibility → Display → Reduce motion
   - **Windows**: Settings → Ease of Access → Display → Show animations
2. Reload `https://launchpadlab.com/`
3. Verify no scroll animations (e.g., AOS, GSAP) trigger when scrolling
4. Verify no hover transitions (or they are near-instant)
5. Verify auto-advancing carousels do not auto-advance
6. Verify content appears statically
7. If "Reduce Motion" toggle exists in header, test that it works and persists across page loads

## Developer Notes

- Add global CSS for reduced motion:
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
- In JavaScript, check before initializing scroll libraries:
  ```js
  if (!window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
    // Initialize AOS, GSAP, scroll animations, etc.
  }
  ```
- Disable auto-advance on carousels when reduced motion is preferred
- Add a visible "Reduce Motion" toggle in the header that:
  - Sets a flag in localStorage
  - Applies reduced-motion styles/behavior when active
  - Persists across page loads

## WCAG References

- **[2.3.3 Animation from Interactions (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/animation-from-interactions.html)**: Motion animation triggered by interaction can be disabled, unless the animation is essential to the functionality or the information being conveyed.
- **[2.2.2 Pause, Stop, Hide (Level A)](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)**: For any moving, blinking or scrolling information that (1) starts automatically, (2) lasts more than five seconds, and (3) is presented in parallel with other content, there is a mechanism for the user to pause, stop, or hide it.

## Priority & Effort

| Attribute | Value |
|-----------|-------|
| **Priority** | P1 Critical |
| **Effort Estimate** | Medium (4–8 hours) |
