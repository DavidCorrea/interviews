# Redesign Carousel Navigation with Accessible Controls

## Priority: High

## User Story
As a user with motor or visual impairments, I want the carousel to have large, clearly labeled navigation controls so that I can browse all case studies without struggling with tiny dot buttons.

## Acceptance Criteria
- [ ] Carousel has visible Previous/Next buttons with minimum 44×44px click targets
- [ ] Buttons are clearly labeled (e.g., "Previous slide," "Next slide") for screen readers and sighted users
- [ ] Carousel supports keyboard navigation (arrow keys to move between slides)
- [ ] Auto-rotation can be paused (button or preference)
- [ ] Carousel has appropriate ARIA attributes (role="region", aria-label, aria-roledescription="carousel")
- [ ] Current slide position is announced to screen reader users
- [ ] Dot indicators (if retained) are at least 24×24px and have visible focus states

## Developer Notes

### General Explanation
Small dot indicators are difficult for users with motor impairments (hard to click) and visual impairments (hard to see). Carousels also often lack keyboard support and screen reader announcements. Best practices:

1. **Replace or supplement dots** with large, labeled Previous/Next buttons (min 44×44px).
2. **Add keyboard support** — Arrow keys to navigate; optionally Home/End for first/last slide.
3. **Use ARIA** — `role="region"`, `aria-roledescription="carousel"`, `aria-label`, `aria-live` for slide changes.
4. **Pause auto-rotation** — Provide a pause button; respect `prefers-reduced-motion`.
5. **Consider alternatives** — A static grid or list may be more accessible than a carousel for some content.

### Code Examples

**Accessible carousel structure:**
```html
<section
  class="carousel"
  role="region"
  aria-roledescription="carousel"
  aria-label="Case studies"
>
  <div class="carousel__slides" aria-live="polite">
    <div class="carousel__slide" role="group" aria-roledescription="slide" aria-label="Slide 1 of 4">
      <!-- Slide content -->
    </div>
    <!-- More slides -->
  </div>

  <div class="carousel__controls">
    <button
      type="button"
      class="carousel__btn carousel__btn--prev"
      aria-label="Previous slide"
      disabled
    >
      Previous
    </button>
    <button
      type="button"
      class="carousel__btn carousel__btn--next"
      aria-label="Next slide"
    >
      Next
    </button>
    <button
      type="button"
      class="carousel__btn carousel__btn--pause"
      aria-label="Pause auto-rotation"
    >
      Pause
    </button>
  </div>

  <div class="carousel__dots" role="tablist" aria-label="Slide navigation">
    <button role="tab" aria-selected="true" aria-label="Slide 1">1</button>
    <button role="tab" aria-selected="false" aria-label="Slide 2">2</button>
    <!-- ... -->
  </div>
</section>
```

**Keyboard navigation (JavaScript):**
```javascript
carousel.addEventListener('keydown', (e) => {
  if (e.target.closest('.carousel__slide')) {
    switch (e.key) {
      case 'ArrowLeft':
        e.preventDefault();
        goToPrevSlide();
        break;
      case 'ArrowRight':
        e.preventDefault();
        goToNextSlide();
        break;
      case 'Home':
        e.preventDefault();
        goToSlide(0);
        break;
      case 'End':
        e.preventDefault();
        goToSlide(slides.length - 1);
        break;
    }
  }
});
```

**Respecting reduced motion:**
```css
@media (prefers-reduced-motion: reduce) {
  .carousel {
    --carousel-duration: 0s;
  }
}
```

```javascript
if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
  // Disable auto-rotation
  clearInterval(autoplayInterval);
}
```

**Minimum button size (CSS):**
```css
.carousel__btn {
  min-width: 44px;
  min-height: 44px;
  padding: 12px 20px;
  font-size: 1rem;
}
.carousel__btn:focus-visible {
  outline: 2px solid currentColor;
  outline-offset: 2px;
}
```

### Components to Audit
- Homepage case study carousel
- Any other carousels on the site (testimonials, featured content, etc.)
- Slider or carousel components in shared component library

## Examples From Other Sites
- **W3C WAI Carousel Tutorial** — Provides a complete accessible carousel pattern with ARIA, keyboard support, and pause controls: [W3C WAI-ARIA Authoring Practices - Carousel](https://www.w3.org/WAI/ARIA/apg/patterns/carousel/).
- **BBC** — Uses large Previous/Next buttons, visible labels, and keyboard support; carousels respect reduced motion preferences.
- **gov.uk** — Prefers static content over carousels where possible; when used, carousels have clear labels, large controls, and full keyboard access.

## References
- Main Report Item 3 (High Priority)
- W3C WAI-ARIA Authoring Practices: Carousel Pattern
- Interview feedback: users with wrist discomfort and visual impairments struggled with dot indicators
- High-value content (client case studies with metrics) at risk of being inaccessible
