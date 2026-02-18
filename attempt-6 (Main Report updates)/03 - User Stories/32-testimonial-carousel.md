# Testimonial Carousel

## Priority
**Low**

## User Story
As a potential client visiting the Contact page, I want to see multiple testimonials at once (or filter by industry), so that I can quickly find social proof from companies similar to mine and build confidence before reaching out.

## Acceptance Criteria

- [ ] Contact page displays 2–3 testimonials at once (grid or multi-slide view) OR uses a dedicated testimonials page with filtering
- [ ] Testimonials include recognizable company names or diverse client types
- [ ] If filtering exists, users can filter by industry, company size, or use case
- [ ] Carousel (if retained) is fully keyboard navigable (Tab, Arrow keys, Enter/Space)
- [ ] Carousel has proper ARIA: `aria-roledescription="carousel"`, `aria-label`, slide position announcements
- [ ] Dot navigation has descriptive labels (see User Story 31)
- [ ] No auto-advance without pause/stop control, or auto-advance is disabled by default for accessibility

## How to Test

1. Navigate to the Contact page on https://launchpadlab.com/.
2. Locate the testimonials section.
3. Verify 2–3 testimonials are visible at once (or a grid layout).
4. If filtering exists, test industry/company filters.
5. Use keyboard only — Tab through carousel controls, use Arrow keys if supported, activate with Enter/Space.
6. Use a screen reader — verify carousel structure and slide content are announced.
7. Check that testimonials include recognizable or diverse client references.
8. If auto-advance exists, verify there is a pause button or that it can be disabled.

## Developer Notes

### General Explanation
The Contact page testimonials carousel shows one quote at a time with dot navigation only. Testimonials are from unrecognizable companies. There is no filtering by industry. Users may not find relevant social proof, and the single-slide carousel limits discoverability. Displaying multiple testimonials or adding filtering improves engagement and accessibility.

**Solution:** Display 2–3 testimonials at once using a grid or multi-slide carousel. Add testimonials from diverse, recognizable client types. Consider a dedicated testimonials page with industry/use case filters. Ensure the carousel is keyboard navigable with proper ARIA. Avoid auto-advance without user control.

### Code Examples

**Grid layout (no carousel):**
```html
<section aria-label="Client testimonials">
  <div class="testimonials-grid">
    <blockquote class="testimonial">
      <p>"Quote text..."</p>
      <cite>— Jane Doe, CEO, Acme Corp</cite>
    </blockquote>
    <blockquote class="testimonial">
      <p>"Quote text..."</p>
      <cite>— John Smith, CTO, TechCo</cite>
    </blockquote>
    <blockquote class="testimonial">
      <p>"Quote text..."</p>
      <cite>— Sarah Lee, Director, Global Inc</cite>
    </blockquote>
  </div>
</section>
```

**CSS for 2–3 column grid:**
```css
.testimonials-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1.5rem;
}
```

**Multi-slide carousel (2–3 visible):**
```jsx
<div role="region" aria-roledescription="carousel" aria-label="Client testimonials">
  <div className="slides-container" style={{ display: 'grid', gridTemplateColumns: 'repeat(3, 1fr)' }}>
    {visibleSlides.map((testimonial) => (
      <blockquote key={testimonial.id} className="testimonial">
        <p>{testimonial.quote}</p>
        <cite>{testimonial.author}, {testimonial.company}</cite>
      </blockquote>
    ))}
  </div>
  <div className="carousel-controls">
    <button aria-label="Previous testimonials">Previous</button>
    <button aria-label="Next testimonials">Next</button>
  </div>
</div>
```

**Filtering by industry:**
```jsx
const [industryFilter, setIndustryFilter] = useState('all');

const filteredTestimonials = testimonials.filter(
  (t) => industryFilter === 'all' || t.industry === industryFilter
);

<>
  <div role="group" aria-label="Filter testimonials">
    <button onClick={() => setIndustryFilter('all')}>All</button>
    <button onClick={() => setIndustryFilter('finance')}>Financial Services</button>
    <button onClick={() => setIndustryFilter('healthcare')}>Healthcare</button>
    <button onClick={() => setIndustryFilter('technology')}>Technology</button>
  </div>
  <div className="testimonials-grid">
    {filteredTestimonials.map((t) => (
      <blockquote key={t.id}>...</blockquote>
    ))}
  </div>
</>
```

**Keyboard navigation for carousel:**
```javascript
carouselEl.addEventListener('keydown', (e) => {
  if (e.key === 'ArrowLeft') {
    e.preventDefault();
    goToPrevSlide();
  } else if (e.key === 'ArrowRight') {
    e.preventDefault();
    goToNextSlide();
  }
});
```

### Components to Audit
- Contact page testimonials section
- Testimonial carousel component
- Carousel library (Swiper, Splide, etc.) configuration
- Testimonial data source (ensure diverse, recognizable clients)
- Any filtering UI for testimonials

## Examples from Other Sites

- **Shopify.com** — Testimonials/case studies use a grid layout with industry filters. Users can find relevant social proof quickly.
- **Slack.com** — Testimonials organized by company size and industry. Clear categorization and multiple visible at once.
- **HubSpot.com** — Customer stories page with filtering and grid display. Easy to browse and filter.
- **Stripe.com** — Customer quotes often displayed in a grid or multi-column layout rather than single-slide carousel.
