# Carousel Arrow Controls

**Priority:** Medium

## User Story

As a user navigating carousels on the website, I want visible previous/next arrow buttons in addition to dot indicators, so that I can easily move between slides regardless of my input method or motor ability.

## Acceptance Criteria

- [ ] All carousels (homepage case studies, contact page testimonials) have visible previous/next arrow buttons
- [ ] Arrow buttons meet the minimum 44x44 CSS pixel touch target size
- [ ] Dot indicators also meet the minimum 44x44 CSS pixel touch target size
- [ ] Keyboard users can navigate between slides using left/right arrow keys when the carousel is focused
- [ ] Arrow buttons have descriptive `aria-label` attributes (e.g., "Previous slide," "Next slide")
- [ ] Arrows visually indicate disabled state when at the first or last slide (if not looping)
- [ ] Carousel navigation works on both desktop and mobile

## How to Test

1. Navigate to the homepage and locate the case studies carousel
2. Verify visible left/right arrow buttons are present
3. Click the arrows — confirm slides change correctly
4. Tab to the carousel controls — verify arrow buttons are focusable and keyboard-operable
5. Use DevTools to measure arrow button dimensions — confirm at least 44x44px
6. Use a screen reader — verify arrow buttons announce their purpose ("Previous slide," "Next slide")
7. Test on mobile — confirm arrows are visible and tappable
8. Repeat on the Contact page testimonials carousel

## Developer Notes

### General Approach

Add `<button>` elements for previous/next navigation to all carousel components. Ensure they are placed within the carousel wrapper and styled to be clearly visible. Support keyboard arrow key navigation when the carousel has focus.

### Code Example

```html
<div class="carousel" role="region" aria-label="Case studies" aria-roledescription="carousel">
  <div class="carousel-controls">
    <button class="carousel-prev" aria-label="Previous slide">
      <svg aria-hidden="true" viewBox="0 0 24 24"><path d="M15 18l-6-6 6-6"/></svg>
    </button>
    <button class="carousel-next" aria-label="Next slide">
      <svg aria-hidden="true" viewBox="0 0 24 24"><path d="M9 6l6 6-6 6"/></svg>
    </button>
  </div>
  <div class="carousel-track" aria-live="polite">
    <!-- slides -->
  </div>
  <div class="carousel-dots" role="tablist">
    <!-- dot buttons -->
  </div>
</div>
```

```css
.carousel-prev,
.carousel-next {
  min-width: 44px;
  min-height: 44px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: none;
  border-radius: 50%;
  background: rgba(0, 0, 0, 0.5);
  color: white;
  cursor: pointer;
}

.carousel-prev:focus-visible,
.carousel-next:focus-visible {
  outline: 2px solid #005fcc;
  outline-offset: 2px;
}

.carousel-prev:disabled,
.carousel-next:disabled {
  opacity: 0.3;
  cursor: not-allowed;
}
```

```javascript
carousel.addEventListener('keydown', (e) => {
  if (e.key === 'ArrowLeft') {
    e.preventDefault();
    goToPreviousSlide();
  } else if (e.key === 'ArrowRight') {
    e.preventDefault();
    goToNextSlide();
  }
});
```

### Components to Audit

- Homepage case studies carousel component
- Contact page testimonials carousel component
- Any shared carousel/slider library used (Swiper, Splide, Embla, or custom)
- Carousel CSS for dot button sizing

## Examples from Other Sites

- **Airbnb.com** — Listing image carousels have large, clearly visible left/right arrow buttons alongside dot indicators. Arrows are circular with good contrast and generous touch targets.
- **Amazon.com** — Product image carousels use large chevron buttons on both sides. The buttons have clear hover states and keyboard support.
- **W3C WAI Carousel Tutorial** (w3.org/WAI/tutorials/carousels/) — The canonical reference for accessible carousel implementation. Includes arrow buttons, proper ARIA, and keyboard navigation patterns.
- **Etsy.com** — Product carousels have arrow navigation with smooth transitions and proper focus management.
