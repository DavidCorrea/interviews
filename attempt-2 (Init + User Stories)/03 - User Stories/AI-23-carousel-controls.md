# AI-23: Add Visible Pause/Play and Keyboard Controls to Carousels

## User Story

As a **user with a disability or motion sensitivity**, I want **visible pause/play controls and keyboard navigation on all carousels**, so that **I can stop auto-advancing content and navigate slides at my own pace**.

## Acceptance Criteria

- [ ] Visible "Pause" and "Play" buttons on all carousels
- [ ] Visible "Previous" and "Next" buttons with text labels
- [ ] Left/Right Arrow keys navigate between slides
- [ ] Pause button stops auto-advance; Play resumes it
- [ ] When `prefers-reduced-motion` is set, carousel does not auto-advance
- [ ] Screen reader announces slide changes
- [ ] Tab exits carousel to next page element (no keyboard trap)

## How to Test

1. **Tab** to the carousel → confirm focus enters carousel controls
2. Use **Left/Right Arrow keys** → confirm slides change
3. Click or activate **"Pause"** button → confirm auto-advance stops
4. Click or activate **"Play"** button → confirm auto-advance resumes
5. Set **`prefers-reduced-motion: reduce`** in OS or browser → confirm carousel does not auto-advance on load
6. Use a **screen reader** → confirm slide changes are announced (e.g., "Slide 2 of 5")
7. **Tab** through carousel → confirm focus exits to the next logical element on the page (no trap)

## Developer Notes

- Add visible "Pause/Play," "Previous," and "Next" buttons with visible text labels (avoid icon-only)
- Support **Left/Right Arrow keys** for slide navigation
- Pause auto-advance by default when `prefers-reduced-motion: reduce` is set (use `matchMedia`)
- Use `aria-live="polite"` on the slide container for screen reader announcements
- Ensure **no keyboard trap** — Tab should exit carousel to the next focusable element
- Consider `aria-roledescription="carousel"` and `aria-label` for the carousel region
- Ensure buttons have `aria-pressed` for Pause/Play state if using toggle pattern

## WCAG References

- **2.2.2 Pause, Stop, Hide** (Level A): For any auto-updating information that (1) starts automatically and (2) is presented in parallel with other content, there is a mechanism for the user to pause, stop, or hide it.
- **2.1.1 Keyboard** (Level A): All functionality of the content is operable through a keyboard interface.

## Priority & Effort

| Priority | Effort Estimate |
|----------|-----------------|
| P3 Medium | Medium (4–6h) |
