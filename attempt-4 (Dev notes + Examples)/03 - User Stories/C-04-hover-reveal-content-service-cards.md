# C-04: Hover-Reveal Content on Service Cards

**Priority:** Critical
**WCAG Criteria:** 1.4.3 Contrast (Minimum) (AA), 1.3.1 Info and Relationships (A), 2.1.1 Keyboard (A), 1.4.13 Content on Hover or Focus (AA)
**Affected Personas:** Low Contrast Sensitivity, Motor Impairment, Voice Control, Situational Contrast

---

## User Story

**As a** keyboard user, voice control user, or someone using a device without a mouse,
**I want** service card descriptions and links to be visible and accessible without requiring a mouse hover,
**so that** I can read the full card content and interact with the links regardless of my input method.

---

## Acceptance Criteria

- [ ] Service card descriptions and "Learn More" links are visible by default (not hidden at `opacity: 0`).
- [ ] All content within service cards is accessible to keyboard users via standard Tab navigation.
- [ ] If a hover/focus reveal pattern is retained, keyboard focus on any element within the card also triggers the content reveal (matching hover behavior).
- [ ] Revealed content remains visible while the pointer is over the content or while any child element has focus (per WCAG 1.4.13).
- [ ] Users can dismiss the revealed content without moving focus (e.g., pressing Escape).
- [ ] All text within service cards meets the 4.5:1 minimum contrast ratio at all times (not just on hover).
- [ ] Voice control users can see and target the "Learn More" links without triggering hover first.

---

## How to Test the Change

### Manual Testing

1. **Keyboard Navigation:**
   - Tab through the service cards section.
   - Verify that when a card or its link receives focus, all card content becomes visible.
   - Confirm focus can move between cards without content disappearing unexpectedly.

2. **Mouse Hover (if reveal is retained):**
   - Hover over a card — content reveals.
   - Move the mouse over the revealed content — it stays visible.
   - Move the mouse away — content dismisses.
   - Press Escape while hovering — content dismisses.

3. **Voice Control:**
   - With Voice Control (macOS) or Dragon NaturallySpeaking active, verify the "Learn More" links are visible and targetable by saying "Click Learn More."

4. **Contrast Check:**
   - Use a contrast picker tool (e.g., Colour Contrast Analyser) to measure text contrast in both default and revealed states.

### Automated Testing

```javascript
// Playwright test — card content visible without hover
test('service card content is visible without hover', async ({ page }) => {
  await page.goto('https://launchpadlab.com');

  const cards = page.locator('.service-card');
  const firstCardDescription = cards.first().locator('.service-card-description, .card-overlay p');

  // Check visibility without hover
  await expect(firstCardDescription).toBeVisible();

  // Check opacity is not 0
  const opacity = await firstCardDescription.evaluate(el =>
    window.getComputedStyle(el).opacity
  );
  expect(Number(opacity)).toBeGreaterThan(0);
});
```

---

## Developer Notes

### General Approach

The best approach is to make all card content visible by default, then optionally enhance with a subtle hover effect (e.g., background color shift, slight elevation). If the design requires a reveal pattern, ensure it triggers on both `:hover` and `:focus-within`.

### Code Examples

**Option A: Always-visible content (recommended):**

```css
/* Before — hidden by default */
.service-card .card-overlay {
  opacity: 0;
  transition: opacity 0.3s ease;
}
.service-card:hover .card-overlay {
  opacity: 1;
}

/* After — always visible */
.service-card .card-overlay {
  opacity: 1;
}

/* Optional: subtle hover enhancement */
.service-card:hover .card-overlay,
.service-card:focus-within .card-overlay {
  background-color: rgba(0, 0, 0, 0.75); /* slightly darker overlay on interaction */
}
```

**Option B: Reveal on hover AND focus-within (if design requires reveal):**

```css
.service-card .card-overlay {
  opacity: 0;
  transition: opacity 0.3s ease;
}

/* Trigger on hover, focus-within, AND a class for JS Escape dismiss */
.service-card:hover .card-overlay,
.service-card:focus-within .card-overlay {
  opacity: 1;
}
```

```javascript
// Dismiss on Escape (per WCAG 1.4.13)
document.querySelectorAll('.service-card').forEach(card => {
  card.addEventListener('keydown', (e) => {
    if (e.key === 'Escape') {
      card.blur();
    }
  });
});
```

**Ensure links are always in the accessibility tree:**

```html
<!-- Before — link hidden from AT when opacity: 0 -->
<a href="/services/web-development" class="learn-more" style="opacity: 0;">
  Learn More
</a>

<!-- After — link always accessible -->
<a href="/services/web-development" class="learn-more">
  Learn More<span class="sr-only"> about Web Development</span>
</a>
```

### Components/Files to Audit

- `.service-card` CSS in the main stylesheet — opacity and transition rules.
- Service card HTML template (page builder module or PHP template).
- Any JavaScript that adds hover listeners to cards.
- `_service-cards.scss` or equivalent Sass partial if using a preprocessor.

---

## Examples from Other Sites

| Site | Implementation |
|------|----------------|
| **Stripe** | Feature cards always show title, description, and link text. Hover adds a subtle elevation shadow — no content is hidden. |
| **Shopify** | Service/feature cards show all content by default with hover adding a border color accent. |
| **Google Material Design** | Card component guidelines explicitly state: "Don't hide primary actions; reveal only supplemental actions on hover." |
| **GitHub** | Repository cards always show description and metadata. Hover only affects the card border/shadow. |
