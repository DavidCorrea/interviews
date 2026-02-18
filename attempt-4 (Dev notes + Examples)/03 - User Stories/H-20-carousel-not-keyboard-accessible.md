# H-20: Carousel/Slider Content Not Keyboard Accessible

**Issue ID:** H-20
**Priority:** High
**WCAG Criteria:** 2.1.1 Keyboard (A), 4.1.2 Name, Role, Value (A), 2.5.1 Pointer Gestures (A)
**Affected Personas:** Motor Impairment, Voice Control, Low Vision Screen Magnifier, Senior Person

---

## User Story

**As a** keyboard-only user,
**I want** case study and testimonial carousels to have visible navigation controls I can operate with the keyboard,
**so that** I can browse all carousel content without needing a mouse or touch gestures.

---

## Acceptance Criteria

- [ ] Each carousel renders visible Previous/Next arrow buttons that are focusable and operable via keyboard (`Enter`/`Space`).
- [ ] Each carousel renders dot indicators or a slide counter (e.g., "2 of 5") that communicates the current position.
- [ ] Arrow keys (`←` / `→`) navigate between slides when the carousel has focus.
- [ ] The carousel container has `role="region"` and an `aria-label` (e.g., `aria-label="Case study carousel"`).
- [ ] Each slide has `role="tabpanel"` or `role="group"` with `aria-roledescription="slide"` and `aria-label="Slide X of Y"`.
- [ ] Focus is managed: when navigating to a new slide, focus moves to the new slide content.
- [ ] The carousel does not auto-advance. If it does, a visible Pause button is present and keyboard-accessible.
- [ ] All carousel content is accessible without requiring click-and-drag or swipe gestures.

---

## How to Test the Change

### Manual Testing

1. **Keyboard navigation:** Tab to the carousel. Use `Enter`/`Space` on arrow buttons and `←`/`→` keys to navigate slides. Confirm all slides are reachable.
2. **Screen reader test:** Using NVDA or VoiceOver, navigate to the carousel. Confirm it announces its role, label, current slide position, and slide content.
3. **Voice control test:** Say "click Next" or "click Previous" using Dragon NaturallySpeaking or Voice Control. Confirm the carousel responds correctly.
4. **No-mouse test:** Unplug the mouse entirely. Attempt to access every slide in each carousel using only the keyboard. Confirm success.
5. **Magnification test:** At 200%+ zoom, confirm arrow buttons and dot indicators remain visible and do not overflow off-screen.

### Automated Testing

- Run `axe-core`: Confirm no "Interactive controls must be focusable" or "ARIA roles" violations related to the carousel.
- Check for keyboard event handlers:

```javascript
// Verify arrow buttons exist and are focusable
const carousels = document.querySelectorAll('.tns-outer, .carousel');
carousels.forEach(c => {
  const prev = c.querySelector('[aria-label*="previous"], .tns-prev');
  const next = c.querySelector('[aria-label*="next"], .tns-next');
  console.assert(prev && prev.tabIndex >= 0, 'Missing focusable Previous button');
  console.assert(next && next.tabIndex >= 0, 'Missing focusable Next button');
});
```

---

## Developer Notes

### General Approach

Re-initialize the Tiny Slider (tns) instances with `controls: true` and `nav: true`, then add ARIA attributes for the carousel pattern. Alternatively, implement the [W3C Carousel (Auto-Rotating) pattern](https://www.w3.org/WAI/ARIA/apg/patterns/carousel/).

### Current State (Problem)

```javascript
tns({
  container: '.case-study-slider',
  items: 1,
  controls: false,   // No arrow buttons
  nav: false,         // No dot indicators
  mouseDrag: true,    // Mouse-only interaction
  // No keyboard handling
});
```

### Recommended Fix

```javascript
const slider = tns({
  container: '.case-study-slider',
  items: 1,
  controls: true,
  controlsText: ['← Previous', 'Next →'],
  nav: true,
  mouseDrag: true,
  arrowKeys: true,  // Enable left/right arrow key navigation
  autoplay: false,
});
```

### Adding ARIA Attributes

```html
<div class="carousel" role="region" aria-label="Case study carousel" aria-roledescription="carousel">
  <div class="carousel-controls">
    <button class="carousel-prev" aria-label="Previous slide">←</button>
    <span class="carousel-counter" aria-live="polite">Slide 1 of 5</span>
    <button class="carousel-next" aria-label="Next slide">→</button>
  </div>
  <div class="carousel-track">
    <div role="group" aria-roledescription="slide" aria-label="Slide 1 of 5">
      <!-- Slide content -->
    </div>
    <!-- More slides -->
  </div>
</div>
```

### Styling the Controls

```css
.tns-controls button {
  background: var(--color-primary);
  color: #fff;
  border: 2px solid transparent;
  border-radius: 50%;
  width: 44px;   /* Minimum touch target size */
  height: 44px;
  cursor: pointer;
  font-size: 1.25rem;
}

.tns-controls button:focus-visible {
  outline: 3px solid var(--color-focus);
  outline-offset: 2px;
}

.tns-nav button {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  border: 2px solid var(--color-primary);
  background: transparent;
  margin: 0 4px;
}

.tns-nav button.tns-nav-active {
  background: var(--color-primary);
}
```

### Components / Files to Audit

- Tiny Slider initialization script (e.g., `main.js`, `carousel.js`, or inline `<script>`)
- Case study carousel template partial
- Testimonial carousel template partial
- Related CSS for `.tns-outer`, `.tns-controls`, `.tns-nav`

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **Apple** | Product carousels have visible arrow buttons + dot indicators, all keyboard accessible | Controls are prominent, operable by all input methods. |
| **GOV.UK** | Step-by-step navigation replaces carousels with expandable sections | Removes the carousel pattern entirely in favor of a more accessible alternative. |
| **Airbnb** | Listing carousels have prominent left/right arrows with `aria-label`s and keyboard support | Follows the W3C carousel pattern closely. |
| **W3C APG** | [Carousel example](https://www.w3.org/WAI/ARIA/apg/patterns/carousel/) | Reference implementation of the accessible carousel pattern. |
