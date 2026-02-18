# C-10: Auto-Scrolling Logo Carousels with No Pause Control

**Priority:** Critical
**WCAG Criteria:** 2.2.2 Pause, Stop, Hide (A)
**Affected Personas:** ADHD, Dyslexic, Low Vision Screen Magnifier, Low Vision, Motor Impairment, Senior Person, Skeptical User, Voice Control

---

## User Story

**As a** user who is distracted by continuous motion or who needs more time to read content,
**I want** the auto-scrolling logo carousels to have a visible pause/stop button and to respect my reduced-motion system preference,
**so that** I can stop the distracting motion and read the logos at my own pace.

---

## Acceptance Criteria

- [ ] Each auto-scrolling carousel has a clearly visible pause/play toggle button.
- [ ] The pause button has an accessible name (e.g., `aria-label="Pause logo carousel"`) and updates its label when toggled (e.g., "Play logo carousel").
- [ ] When paused, the carousel completely stops — no residual motion or drift.
- [ ] When `prefers-reduced-motion: reduce` is active, the carousel is paused by default (static display).
- [ ] Users can manually start the carousel even with reduced-motion active (if they choose).
- [ ] The carousel content is accessible without the scrolling animation — users can see all logos via manual navigation (arrows or dots) or a static grid layout.
- [ ] The pause state persists as long as the user is on the page (doesn't auto-resume after a timeout).
- [ ] The carousel does not auto-scroll faster than the user can reasonably read (if animation is active).

---

## How to Test the Change

### Manual Testing

1. **Pause Button:**
   - Navigate to a page with the logo carousel.
   - Verify a pause button is visible near the carousel.
   - Click the pause button — carousel should stop immediately.
   - Click again — carousel should resume.
   - Verify the button label/icon changes between pause and play states.

2. **Keyboard Access:**
   - Tab to the pause button — verify it has a focus indicator.
   - Press Enter or Space — verify it toggles the carousel.

3. **Reduced Motion:**
   - Enable `prefers-reduced-motion: reduce` in system settings.
   - Reload the page — carousel should be paused by default.
   - Logos should be visible in a static arrangement.

4. **Screen Reader:**
   - Navigate to the pause button — verify it announces "Pause logo carousel, button."
   - Activate it — verify it announces "Play logo carousel, button."

### Automated Testing

```javascript
// Playwright test
test('logo carousel has pause control', async ({ page }) => {
  await page.goto('https://launchpadlab.com');

  // Find carousel pause button
  const pauseBtn = page.locator('[aria-label*="ause" i]').first();
  await expect(pauseBtn).toBeVisible();

  // Activate pause
  await pauseBtn.click();
  const label = await pauseBtn.getAttribute('aria-label');
  expect(label?.toLowerCase()).toContain('play');
});

test('carousel is static when prefers-reduced-motion is set', async ({ browser }) => {
  const context = await browser.newContext({ reducedMotion: 'reduce' });
  const page = await context.newPage();
  await page.goto('https://launchpadlab.com');

  // Check that carousel animation is paused
  const carousel = page.locator('.logo-marquee, .logo-carousel, .clients-marquee').first();
  const animationState = await carousel.evaluate(el => {
    const s = window.getComputedStyle(el);
    return s.animationPlayState || s.getPropertyValue('animation-play-state');
  });
  expect(animationState).toBe('paused');

  await context.close();
});
```

---

## Developer Notes

### General Approach

Add a visible pause/play toggle button to the logo carousel. Modify the animation to respect `prefers-reduced-motion`. If the carousel uses CSS `@keyframes` animation for infinite scrolling, toggle it by setting `animation-play-state: paused`. If it uses JavaScript, call the appropriate stop method.

### Code Examples

**HTML: Add pause button:**

```html
<section class="logo-carousel-section" aria-label="Our clients">
  <button
    class="carousel-pause-btn"
    aria-label="Pause logo carousel"
    type="button"
  >
    <svg aria-hidden="true" class="icon-pause" width="20" height="20">
      <rect x="4" y="2" width="4" height="16" fill="currentColor"/>
      <rect x="12" y="2" width="4" height="16" fill="currentColor"/>
    </svg>
    <svg aria-hidden="true" class="icon-play" width="20" height="20" hidden>
      <polygon points="4,2 18,10 4,18" fill="currentColor"/>
    </svg>
  </button>

  <div class="logo-marquee" role="marquee" aria-live="off">
    <!-- Logo images -->
  </div>
</section>
```

**CSS: Respect reduced motion + pause state:**

```css
.logo-marquee {
  animation: scroll-logos 30s linear infinite;
}

/* Pause when class is toggled */
.logo-marquee.is-paused {
  animation-play-state: paused;
}

/* Pause by default for reduced motion */
@media (prefers-reduced-motion: reduce) {
  .logo-marquee {
    animation: none;
    /* Show logos in a static grid instead */
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 2rem;
  }
}

/* Pause button styling */
.carousel-pause-btn {
  position: absolute;
  top: 0.5rem;
  right: 0.5rem;
  z-index: 10;
  background: rgba(0, 0, 0, 0.6);
  color: white;
  border: 2px solid white;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.carousel-pause-btn:focus-visible {
  outline: 3px solid #f5a623;
  outline-offset: 2px;
}
```

**JavaScript: Toggle logic:**

```javascript
document.querySelectorAll('.carousel-pause-btn').forEach(btn => {
  const marquee = btn.closest('.logo-carousel-section').querySelector('.logo-marquee');
  const iconPause = btn.querySelector('.icon-pause');
  const iconPlay = btn.querySelector('.icon-play');

  // Respect prefers-reduced-motion on init
  const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)');
  if (prefersReducedMotion.matches) {
    marquee.classList.add('is-paused');
    btn.setAttribute('aria-label', 'Play logo carousel');
    iconPause.hidden = true;
    iconPlay.hidden = false;
  }

  btn.addEventListener('click', () => {
    const isPaused = marquee.classList.toggle('is-paused');
    btn.setAttribute('aria-label', isPaused ? 'Play logo carousel' : 'Pause logo carousel');
    iconPause.hidden = isPaused;
    iconPlay.hidden = !isPaused;
  });
});
```

### Components/Files to Audit

- Logo carousel/marquee HTML template or page builder block.
- Carousel CSS — `@keyframes` animation for scrolling.
- Carousel JavaScript initialization (if using a JS library like Swiper, Slick, etc.).
- All pages with client logo sections (homepage, case studies, about).

---

## Examples from Other Sites

| Site | Implementation |
|------|----------------|
| **W3C WAI Carousel Tutorial** | Reference implementation with play/pause, previous/next controls, and `prefers-reduced-motion` support. |
| **Shopify** | Partner logo section uses a static grid layout — no auto-scrolling at all. |
| **Salesforce** | Client logo carousel includes visible pause/play button and stops on hover. |
| **Microsoft** | Logo strips use a static layout or very slow scroll with a prominent pause button. |
