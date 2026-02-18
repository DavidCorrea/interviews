# Auto-Playing Carousels & Limited Content Discoverability

**Priority:** High
**Location:** Homepage, About page, Contact page (case studies and testimonials)
**WCAG:** [2.2.2 Pause, Stop, Hide (A)](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide), [1.3.2 Meaningful Sequence (A)](https://www.w3.org/WAI/WCAG21/Understanding/meaningful-sequence), [2.4.7 Focus Visible (AA)](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible)

---

## User Story

> As a **user with ADHD, a cognitive disability, or a motor impairment**,
> I want **carousels to not auto-advance and to provide clear, large navigation controls with a visible slide count**
> so that **I can read content at my own pace without distraction and know how many items are available.**

---

## Problem

The site uses auto-advancing carousels for case studies and testimonials on multiple pages. These carousels have several issues:

1. **Auto-play is distracting.** Content advances on a timer, which is disorienting for users with ADHD or cognitive disabilities, and may cause seizure-prone users to feel discomfort.
2. **Small dot pagination.** The only navigation is tiny dots that are hard to click (especially for users with motor impairments) and convey no information about total content.
3. **Only ~3 items visible.** Users may not realize there are more slides, and valuable content is hidden behind interaction.
4. **No pause/play control.** Users cannot stop the auto-advance, violating WCAG 2.2.2.
5. **Content may be missed entirely.** If a user never interacts with the carousel, they only see the first slide or whatever is animating at the time.

---

## Acceptance Criteria

- [ ] Auto-play is disabled by default on all carousels.
- [ ] A visible Pause/Play button is provided if auto-play is offered as an option.
- [ ] Previous/Next arrow buttons are large (minimum 44×44px touch target) and clearly visible.
- [ ] Arrows are labeled with accessible names (`aria-label="Previous slide"`, `aria-label="Next slide"`).
- [ ] A "Showing X of Y" text indicator is visible (e.g., "2 of 5").
- [ ] The carousel respects `prefers-reduced-motion: reduce` — disabling all transitions and auto-play.
- [ ] Carousel slides are keyboard-navigable (left/right arrow keys when the carousel has focus).
- [ ] The current slide is announced to screen readers when it changes (via `aria-live="polite"` on the slide container or a status region).
- [ ] Each slide's content is accessible — images have `alt` text, text is selectable.
- [ ] On mobile, swipe gestures are supported but are not the only way to navigate.
- [ ] Consider replacing carousels with static grids or stacked cards for testimonials.

---

## How to Test

1. **Auto-play check:** Open the homepage. Does the carousel start advancing on its own? If yes, it fails WCAG 2.2.2 unless a pause button is present.
2. **Pause/Play test:** If auto-play exists, verify a visible Pause/Play button is available and that pressing it stops all motion.
3. **Arrow button size:** Inspect Previous/Next buttons. Verify they are at least 44×44px (use DevTools to measure).
4. **Keyboard navigation:**
   - Tab to the carousel. Verify focus is visible.
   - Press left/right arrow keys. Verify slides change.
   - Verify focus does not get trapped inside the carousel.
5. **Screen reader test:** Navigate the carousel with VoiceOver/NVDA. Verify:
   - The carousel is announced as a region or group.
   - Slide changes are announced (e.g., "Slide 2 of 5").
   - All slide content is readable.
6. **Reduced motion test:** Enable "Reduce motion" in system accessibility settings. Verify the carousel disables auto-play and removes slide transition animations.
7. **Slide count:** Verify a visible "X of Y" indicator is present and updates as slides change.
8. **Content discoverability:** Count total carousel items. If fewer than 6, consider replacing the carousel entirely with a static grid.

---

## Developer Notes

### Recommended carousel markup

```html
<section class="carousel" aria-roledescription="carousel"
         aria-label="Client testimonials">

  <!-- Controls -->
  <div class="carousel__controls">
    <button class="carousel__btn carousel__btn--prev"
            aria-label="Previous slide">
      <svg aria-hidden="true" width="24" height="24" viewBox="0 0 24 24">
        <path d="M15 18l-6-6 6-6" stroke="currentColor"
              stroke-width="2" fill="none"/>
      </svg>
    </button>

    <span class="carousel__count" aria-live="polite">
      <span class="sr-only">Slide</span>
      <span class="carousel__current">1</span>
      of
      <span class="carousel__total">5</span>
    </span>

    <button class="carousel__btn carousel__btn--next"
            aria-label="Next slide">
      <svg aria-hidden="true" width="24" height="24" viewBox="0 0 24 24">
        <path d="M9 6l6 6-6 6" stroke="currentColor"
              stroke-width="2" fill="none"/>
      </svg>
    </button>

    <button class="carousel__btn carousel__btn--pause"
            aria-label="Pause auto-advance"
            aria-pressed="false">
      <svg aria-hidden="true" width="20" height="20" viewBox="0 0 20 20">
        <rect x="4" y="3" width="4" height="14" fill="currentColor"/>
        <rect x="12" y="3" width="4" height="14" fill="currentColor"/>
      </svg>
    </button>
  </div>

  <!-- Slides -->
  <div class="carousel__track" role="group" aria-label="Slides">
    <div class="carousel__slide" role="group"
         aria-roledescription="slide" aria-label="1 of 5">
      <blockquote>
        <p>"LaunchPad Lab helped us build a patient portal that reduced
          appointment no-shows by 35 %."</p>
        <footer>
          <cite>— Jane Smith, CTO at Acme Health</cite>
        </footer>
      </blockquote>
    </div>

    <div class="carousel__slide" role="group"
         aria-roledescription="slide" aria-label="2 of 5"
         hidden>
      <!-- Next slide content -->
    </div>

    <!-- More slides -->
  </div>
</section>
```

### CSS for accessible carousel controls

```css
.carousel {
  position: relative;
  max-width: 64rem;
  margin: 0 auto;
  padding: 2rem 0;
}

.carousel__controls {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.carousel__btn {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 48px;
  height: 48px;                /* Meets 44px minimum touch target */
  border: 2px solid currentColor;
  border-radius: 50%;
  background: transparent;
  color: var(--color-text);
  cursor: pointer;
  transition: background-color 0.2s ease, color 0.2s ease;
}

.carousel__btn:hover {
  background: var(--color-primary);
  border-color: var(--color-primary);
  color: #fff;
}

.carousel__btn:focus-visible {
  outline: 3px solid var(--color-focus-ring);
  outline-offset: 3px;
}

.carousel__count {
  font-size: 1rem;
  font-weight: 600;
  min-width: 4rem;
  text-align: center;
}

/* Slide transitions */
.carousel__slide {
  opacity: 0;
  transition: opacity 0.3s ease;
}

.carousel__slide[aria-current="true"] {
  opacity: 1;
}

.carousel__slide[hidden] {
  display: none;
}

/* Respect reduced motion preferences */
@media (prefers-reduced-motion: reduce) {
  .carousel__slide {
    transition: none;
  }
}
```

### JavaScript for carousel behavior

```javascript
class AccessibleCarousel {
  constructor(el) {
    this.el = el;
    this.slides = [...el.querySelectorAll('.carousel__slide')];
    this.currentIndex = 0;
    this.isPlaying = false;
    this.intervalId = null;

    this.prevBtn = el.querySelector('.carousel__btn--prev');
    this.nextBtn = el.querySelector('.carousel__btn--next');
    this.pauseBtn = el.querySelector('.carousel__btn--pause');
    this.currentDisplay = el.querySelector('.carousel__current');
    this.countRegion = el.querySelector('.carousel__count');

    this.init();
  }

  init() {
    this.prevBtn.addEventListener('click', () => this.prev());
    this.nextBtn.addEventListener('click', () => this.next());
    this.pauseBtn?.addEventListener('click', () => this.togglePlay());

    this.el.addEventListener('keydown', (e) => {
      if (e.key === 'ArrowLeft') { this.prev(); e.preventDefault(); }
      if (e.key === 'ArrowRight') { this.next(); e.preventDefault(); }
    });

    // Pause on hover or focus for accessibility
    this.el.addEventListener('mouseenter', () => this.pause());
    this.el.addEventListener('focusin', () => this.pause());

    // Respect prefers-reduced-motion
    const motionQuery = window.matchMedia('(prefers-reduced-motion: reduce)');
    if (motionQuery.matches) {
      this.isPlaying = false;
    }

    this.showSlide(0);
  }

  showSlide(index) {
    this.slides.forEach((slide, i) => {
      slide.hidden = i !== index;
      slide.removeAttribute('aria-current');
      if (i === index) {
        slide.setAttribute('aria-current', 'true');
      }
    });

    this.currentIndex = index;
    this.currentDisplay.textContent = index + 1;
  }

  next() {
    const nextIndex = (this.currentIndex + 1) % this.slides.length;
    this.showSlide(nextIndex);
  }

  prev() {
    const prevIndex = (this.currentIndex - 1 + this.slides.length)
      % this.slides.length;
    this.showSlide(prevIndex);
  }

  play() {
    this.isPlaying = true;
    this.pauseBtn?.setAttribute('aria-pressed', 'true');
    this.pauseBtn?.setAttribute('aria-label', 'Pause auto-advance');
    this.intervalId = setInterval(() => this.next(), 6000);
  }

  pause() {
    this.isPlaying = false;
    this.pauseBtn?.setAttribute('aria-pressed', 'false');
    this.pauseBtn?.setAttribute('aria-label', 'Play auto-advance');
    clearInterval(this.intervalId);
  }

  togglePlay() {
    this.isPlaying ? this.pause() : this.play();
  }
}

document.querySelectorAll('.carousel').forEach(el => {
  new AccessibleCarousel(el);
});
```

### Alternative: Replace carousel with static grid

If the carousel contains fewer than 6 items, a static grid is simpler and more accessible:

```html
<section aria-labelledby="testimonials-heading">
  <h2 id="testimonials-heading">What Our Clients Say</h2>
  <div class="testimonial-grid">
    <blockquote class="testimonial-card">
      <p>"LaunchPad Lab helped us build a patient portal that
        reduced appointment no-shows by 35 %."</p>
      <footer>
        <cite>— Jane Smith, CTO at Acme Health</cite>
      </footer>
    </blockquote>

    <blockquote class="testimonial-card">
      <p>"They delivered our MVP in 8 weeks, and it's been
        running smoothly for over a year."</p>
      <footer>
        <cite>— John Doe, Founder at FinStart</cite>
      </footer>
    </blockquote>

    <!-- More testimonials -->
  </div>
</section>
```

```css
.testimonial-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
}

.testimonial-card {
  padding: 1.5rem;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  background: #fafafa;
}

.testimonial-card p {
  font-size: 1.125rem;
  line-height: 1.8;
  margin-bottom: 1rem;
}

.testimonial-card cite {
  font-size: 0.9375rem;
  font-style: normal;
  font-weight: 600;
  color: #555;
}
```

### Components to audit

| Component | Page(s) | Issues |
|---|---|---|
| Case study carousel | Homepage | Auto-play, small dots, no arrows, no count |
| Testimonials carousel | Homepage, About | Auto-play, small dots, content hidden |
| Results/stats carousel | Contact page | May auto-play; verify |
| Partner logos slider | About page | If auto-scrolling, needs pause control |

---

## Examples from Other Sites

### GOV.UK
- Does not use carousels at all. Content is always visible in static layouts.
- Their design system documentation explicitly discourages carousels: "Carousels are not accessible, and users often don't interact with them."

### Nielsen Norman Group (nngroup.com)
- Published research showing carousels are largely ignored by users.
- When carousels are used, they recommend: no auto-play, large arrows, visible slide count.
- Article: <https://www.nngroup.com/articles/auto-forwarding/>

### Shopify (shopify.com)
- Product testimonials are displayed in a static grid, not a carousel.
- Featured case studies use large, static cards.

### W3C WAI Carousel Tutorial
- Official guidance for building accessible carousels: <https://www.w3.org/WAI/tutorials/carousels/>
- Recommends: pause button, keyboard navigation, aria-roledescription, and visible slide indicators.

### Airbnb (airbnb.com)
- Uses carousels for listing photos but with large, clearly visible arrows.
- No auto-play.
- Visible "1/8" count in the corner.
- Keyboard navigable with arrow keys.
