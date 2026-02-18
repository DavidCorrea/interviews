# Carousel Broken ARIA

## Priority
**High**

## User Story
As a screen reader user, I want the case studies carousel to announce accurate slide position information (e.g., "slide 1 of 3"), so that I can understand my position within the carousel and navigate it effectively.

## Acceptance Criteria

- [ ] Carousel announces correct slide position (e.g., "slide 1 of 3," "slide 2 of 3")
- [ ] Position text is mathematically consistent (current slide ≤ total slides)
- [ ] Live region updates when slide changes
- [ ] Previous/Next buttons have clear labels (e.g., "Next slide," "Previous slide")
- [ ] Carousel has appropriate `aria-roledescription="carousel"` or equivalent
- [ ] Slide count does not exceed total number of slides
- [ ] No conflicting or stale live region announcements

## How to Test

1. Navigate to the page containing the case studies carousel.
2. Open the browser's accessibility tree (e.g., Chrome DevTools > Elements > Accessibility).
3. Locate the carousel region and its live region / status text.
4. Note the announced slide position (e.g., "slide 5 of 7" or "slide 5 to 7 of 3").
5. Advance the carousel (click Next or use keyboard).
6. Verify the position updates and remains consistent (e.g., "slide 2 of 3").
7. Use a screen reader (VoiceOver or NVDA) to navigate the carousel.
8. Confirm announcements match the visual state and are mathematically correct.
9. Test with different numbers of slides (if editable) to ensure logic scales.

## Developer Notes

### General Explanation
The carousel reports "slide 5 to 7 of 3" — an impossible state that confuses screen reader users. This typically stems from:
- Incorrect indexing (0-based vs 1-based)
- Wrong variable used for current slide or total count
- Multiple live regions or ARIA attributes conflicting
- Carousel library not properly updating ARIA on slide change

**Solution:** Audit the carousel's ARIA implementation. Ensure `aria-label` or the live region text uses the correct current index and total. Fix any off-by-one errors. Verify the carousel library (Swiper, Splide, custom, etc.) supports accessible patterns or add custom ARIA updates.

### Code Examples

**Correct live region pattern:**
```html
<div role="region" aria-roledescription="carousel" aria-label="Case studies">
  <div aria-live="polite" aria-atomic="true" class="visually-hidden">
    Slide 1 of 3
  </div>
  <div class="slides">
    <div role="group" aria-roledescription="slide" aria-label="Slide 1 of 3">
      <!-- slide content -->
    </div>
    <!-- ... -->
  </div>
  <button aria-label="Previous slide">Previous</button>
  <button aria-label="Next slide">Next</button>
</div>
```

**JavaScript to update live region:**
```javascript
function updateCarouselAnnouncement(currentIndex, totalSlides) {
  const liveRegion = document.querySelector('[aria-live="polite"]');
  if (liveRegion) {
    liveRegion.textContent = `Slide ${currentIndex + 1} of ${totalSlides}`;
  }
}

// Call on slide change
carousel.on('slideChange', () => {
  updateCarouselAnnouncement(carousel.activeIndex, carousel.slides.length);
});
```

**React example:**
```jsx
const [currentSlide, setCurrentSlide] = useState(0);
const totalSlides = slides.length;

useEffect(() => {
  const liveRegion = liveRegionRef.current;
  if (liveRegion) {
    liveRegion.textContent = `Slide ${currentSlide + 1} of ${totalSlides}`;
  }
}, [currentSlide, totalSlides]);
```

**Common bug to fix:**
```javascript
// WRONG - may produce "slide 5 to 7 of 3"
ariaLabel = `slide ${startIndex} to ${endIndex} of ${total}`;

// CORRECT
ariaLabel = `slide ${currentIndex + 1} of ${total}`;
```

### Components to Audit
- Carousel/slider component
- Swiper, Splide, or other carousel library configuration
- `aria-roledescription`, `aria-label`, `aria-live` attributes
- Any `status` or `polite` live regions
- Slide change event handlers (ensure they update ARIA)
- Pagination/dots component (ensure they have proper labels)

### Reference
- [W3C WAI Carousel Pattern](https://www.w3.org/WAI/tutorials/carousels/) — Authoritative guidance on accessible carousel implementation.

## Examples from Other Sites

- **W3C WAI Carousel Tutorial** (https://www.w3.org/WAI/tutorials/carousels/) — Shows correct ARIA implementation with live regions, slide labels, and button semantics. Use as the primary reference for fixing this issue.
