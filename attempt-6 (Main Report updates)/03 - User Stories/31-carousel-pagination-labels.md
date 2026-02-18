# Carousel Pagination Labels

## Priority
**Low**

## User Story
As a screen reader user navigating a carousel, I want pagination buttons to have descriptive labels that indicate the content of each slide, so that I can jump directly to the slide I want without cycling through all of them.

## Acceptance Criteria

- [ ] Each carousel pagination button has a descriptive `aria-label` (e.g., "Slide 1: Millennium Trust Company case study")
- [ ] Labels reflect the actual content of each slide (client name, topic, etc.)
- [ ] Current slide button has `aria-current="true"` or equivalent
- [ ] Labels are updated dynamically if carousel content changes (e.g., filtered case studies)
- [ ] Pagination buttons are keyboard focusable and activatable
- [ ] Screen reader announces slide content when focusing pagination, not just "Carousel Page 1"

## How to Test

1. Navigate to a page with a case studies or content carousel on https://launchpadlab.com/.
2. Locate the carousel pagination (dots or numbered buttons).
3. Inspect each pagination button — verify `aria-label` includes slide content description.
4. Use a screen reader — focus each pagination button and confirm descriptive labels are announced.
5. Verify the active/current slide button has `aria-current="true"`.
6. If carousel content is filterable, change filters and verify labels update.
7. Use keyboard — Tab to pagination buttons, activate with Enter/Space, verify correct slide is shown.

## Developer Notes

### General Explanation
Carousel pagination buttons are labeled generically ("Carousel Page 1") without describing slide content. Users cannot determine what's on each slide without cycling through. Descriptive labels allow screen reader users to jump directly to relevant content and understand the carousel structure.

**Solution:** Add descriptive labels to pagination buttons. Example: `aria-label="Slide 1: Millennium Trust Company case study"`. Use slide metadata (client name, title, etc.) to build labels. Update labels dynamically if carousel content changes. Ensure the current slide has `aria-current="true"`.

### Code Examples

**Basic pagination with descriptive labels:**
```html
<div role="group" aria-label="Case studies carousel">
  <div class="slides">
    <div id="slide-1" role="group" aria-roledescription="slide">
      <!-- Millennium Trust Company content -->
    </div>
    <div id="slide-2" role="group" aria-roledescription="slide">
      <!-- Prosci content -->
    </div>
  </div>
  <div class="pagination" role="tablist" aria-label="Slide navigation">
    <button
      role="tab"
      aria-selected="true"
      aria-label="Slide 1: Millennium Trust Company case study"
      aria-controls="slide-1"
    >
      1
    </button>
    <button
      role="tab"
      aria-selected="false"
      aria-label="Slide 2: Prosci case study"
      aria-controls="slide-2"
    >
      2
    </button>
  </div>
</div>
```

**Using `aria-current` instead of `aria-selected` (simpler pattern):**
```html
<button aria-label="Slide 1: Millennium Trust Company case study" aria-current="true">
  1
</button>
<button aria-label="Slide 2: Prosci case study">
  2
</button>
```

**React — dynamic labels from slide data:**
```jsx
const slides = [
  { id: 1, client: 'Millennium Trust Company', type: 'case study' },
  { id: 2, client: 'Prosci', type: 'case study' },
];

<div className="pagination" role="tablist">
  {slides.map((slide, index) => (
    <button
      key={slide.id}
      role="tab"
      aria-selected={index === currentSlide}
      aria-label={`Slide ${index + 1}: ${slide.client} ${slide.type}`}
      aria-controls={`slide-${slide.id}`}
      onClick={() => goToSlide(index)}
    >
      {index + 1}
    </button>
  ))}
</div>
```

**JavaScript for dynamic label updates:**
```javascript
function updatePaginationLabels(slides, currentIndex) {
  const buttons = document.querySelectorAll('.pagination button');
  buttons.forEach((btn, i) => {
    const slide = slides[i];
    btn.setAttribute(
      'aria-label',
      `Slide ${i + 1}: ${slide.clientName} case study`
    );
    btn.setAttribute('aria-current', i === currentIndex ? 'true' : 'false');
  });
}
```

### Components to Audit
- Case studies carousel component
- Carousel pagination/dots component
- Swiper, Splide, or other carousel library pagination config
- Any component that renders carousel navigation buttons

## Examples from Other Sites

- **W3C WAI Carousel Pattern** — Authoritative examples with descriptive pagination labels. Each dot/tab describes slide content.
- **Airbnb.com** — Carousel dots with descriptive hover text and accessible labels for listing images.
- **Apple.com** — Product carousels often use descriptive labels for each slide in pagination.
