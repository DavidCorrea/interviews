# AI-23: Add Carousel Pause Controls and Keyboard Support

## Metadata
- **ID:** AI-23
- **Priority:** 3 Medium
- **Personas Affected:** 4+ of 16 personas (motion sensitivity, vestibular, keyboard, screen reader)
- **WCAG Criteria:** 2.2.2 Pause, Stop, Hide (A), 2.1.1 Keyboard (A)
- **Effort:** Medium (4–6 hours)

---

## User Story

**As a** user who is sensitive to motion, prefers keyboard navigation, or uses a screen reader,

**I want** carousels to have visible pause/play controls, respect reduced motion preferences, and support keyboard navigation,

**So that** I can stop auto-advancing content, navigate slides with keyboard, and understand slide changes without being disoriented.

---

## Acceptance Criteria

- [ ] Pause button visible when carousel is auto-advancing
- [ ] Play button visible when carousel is paused
- [ ] Clicking pause stops auto-advance; clicking play resumes it
- [ ] When `prefers-reduced-motion: reduce` is set, carousel does NOT auto-advance by default
- [ ] Previous/Next arrow buttons are keyboard focusable (Tab)
- [ ] Arrow Left/Right keys navigate between slides when carousel has focus
- [ ] Slide changes are announced to screen readers (e.g., "Slide 2 of 5")
- [ ] No keyboard trap: Tab moves out of carousel to next page element
- [ ] Focus management: when changing slides, focus moves to new slide content or stays on controls
- [ ] Slide indicators (dots) are focusable and keyboard-activatable

---

## Test Plan

### Pause/Play Controls
1. Visit `https://launchpadlab.com/` and locate any carousel (hero, testimonials, case studies)
2. **Expected:** Pause button (⏸) visible when carousel is auto-advancing
3. Click pause
4. **Expected:** Carousel stops; button changes to Play (▶)
5. Click play
6. **Expected:** Carousel resumes auto-advance; button changes to Pause

### Reduced Motion
1. Enable reduced motion in OS:
   - macOS: System Preferences → Accessibility → Display → Reduce motion
   - Windows: Settings → Ease of Access → Display → Show animations
2. Reload page with carousel
3. **Expected:** Carousel does NOT auto-advance by default
4. **Expected:** User can manually advance with arrows or dots
5. **Expected:** Pause/play may still be present but carousel starts paused

### Keyboard Focus
1. Tab to the carousel region
2. **Expected:** Previous/Next arrow buttons receive focus in tab order
3. **Expected:** Focus visible (outline or ring)
4. Tab through: Previous → Next → Pause/Play → Dots (if present)
5. **Expected:** Tab eventually exits carousel to next page element (no trap)

### Arrow Key Navigation
1. Focus on carousel (click or Tab to it)
2. Press Arrow Right
3. **Expected:** Advances to next slide
4. Press Arrow Left
5. **Expected:** Goes to previous slide
6. On first slide, Arrow Left: wrap to last or no-op (document behavior)
7. On last slide, Arrow Right: wrap to first or no-op (document behavior)

### Screen Reader Announcements
1. Enable VoiceOver or NVDA
2. Navigate to carousel
3. **Expected:** Carousel region has `role="region"` and `aria-label="Carousel"` or similar
4. When slide changes (auto or manual)
5. **Expected:** Live region announces "Slide 2 of 5" or equivalent
6. Use `aria-live="polite"` and `aria-atomic="true"` for announcement

### No Keyboard Trap
1. Tab into carousel
2. Continue Tabbing
3. **Expected:** Focus eventually leaves carousel (e.g., to next link, button, or main content)
4. **Fail:** Focus cycles only within carousel indefinitely

---

## Developer Notes

### Pause/Play Button
```html
<button type="button" aria-label="Pause carousel" id="carousel-pause">
  <span aria-hidden="true">⏸</span>
</button>
<!-- When paused, switch to: -->
<button type="button" aria-label="Play carousel" id="carousel-play">
  <span aria-hidden="true">▶</span>
</button>
```

```javascript
const pauseBtn = document.getElementById('carousel-pause');
const playBtn = document.getElementById('carousel-play');
let autoAdvanceInterval;

function startAutoAdvance() {
  autoAdvanceInterval = setInterval(goToNextSlide, 5000);
  pauseBtn.hidden = false;
  playBtn.hidden = true;
}
function stopAutoAdvance() {
  clearInterval(autoAdvanceInterval);
  pauseBtn.hidden = true;
  playBtn.hidden = false;
}

if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
  // Do NOT auto-advance
} else {
  startAutoAdvance();
}
```

### Arrow Buttons
```html
<button type="button" aria-label="Previous slide">←</button>
<button type="button" aria-label="Next slide">→</button>
```
Ensure both are in tab order and have visible focus styles.

### Arrow Key Handler
```javascript
carousel.addEventListener('keydown', (e) => {
  if (e.key === 'ArrowLeft') {
    e.preventDefault();
    goToPrevSlide();
  } else if (e.key === 'ArrowRight') {
    e.preventDefault();
    goToNextSlide();
  }
});
```

### Live Region for Announcements
```html
<div aria-live="polite" aria-atomic="true" class="sr-only" id="carousel-announcer">
  Slide 2 of 5
</div>
```
Update `#carousel-announcer` text when slide changes.

### Tab Order
- Ensure Tab moves: Previous → Next → Pause/Play → Dots → (exit)
- Use `tabindex="-1"` on slide content if it shouldn't be in tab order
- Do NOT use `tabindex="0"` on every slide — only interactive elements

### W3C Carousel Pattern
Reference: https://www.w3.org/WAI/tutorials/carousels/
- Includes structure, roles, and keyboard behavior
- Consider using a library (e.g., Embla, Swiper) with accessibility built-in

---

## Examples

| Site | Approach |
|------|----------|
| **GOV.UK** | Carousel with pause/play; keyboard support; reduced motion respected |
| **Shopify Polaris** | Carousel component with accessible controls and keyboard nav |
| **W3C Carousel Tutorial** | Full pattern: pause, arrows, dots, live region, no trap |
| **Bootstrap Carousel** | Pause/play, arrows; requires additional keyboard and ARIA work |
