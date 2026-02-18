# H-13: Duplicate/Nested Links on Service Cards

**Issue ID:** H-13
**Priority:** High
**WCAG Criteria:** 4.1.1 Parsing (A), 2.4.4 Link Purpose (In Context) (A)
**Affected Personas:** Low Vision Screen Magnifier, Motor Impairment, Voice Control, Screen Reader

---

## User Story

**As a** screen reader user navigating the services section,
**I want** each service card to have a single, clearly defined link rather than nested or duplicate links to the same destination,
**so that** I hear each service announced once and don't waste time tabbing through redundant interactive elements.

---

## Acceptance Criteria

- [ ] No `<a>` element is nested inside another `<a>` element anywhere on the site (this is invalid HTML per the spec).
- [ ] Each service card produces exactly **one** tab stop (not two) when navigating with the keyboard.
- [ ] The single link's accessible name includes the service name (e.g., "AI Development — Learn more").
- [ ] The entire card surface is clickable (if desired) via a CSS/JS click-delegation pattern rather than an outer `<a>` wrapper.
- [ ] Screen readers announce the service card link once, not twice, when navigating by links or tabbing.
- [ ] Voice control users see one target per card, not two overlapping targets.
- [ ] The fix passes HTML validation (no nested `<a>` warnings in the W3C validator).

---

## How to Test the Change

### Manual Testing

1. **Keyboard tab test:** Tab through the services section. Count the number of tab stops per card. Confirm each card produces exactly one tab stop.
2. **Screen reader link list:** Open the links list in NVDA (`Insert+F7`) or VoiceOver (`VO+U`). Confirm each service appears once, not twice.
3. **HTML validation:** Run the page through the [W3C Markup Validator](https://validator.w3.org/). Confirm no "nested `<a>`" errors.
4. **Voice control test:** Say "click" and check how many targets overlay each service card. There should be exactly one.
5. **Click target test:** Click on the card heading, the card body, and the "Learn More" area. All should navigate to the same service page via the single link.

### Automated Testing

- Run `axe-core`: check for "Nested interactive controls" violations.
- W3C HTML validator — check for "Element `a` not allowed as descendant of element `a`."

```javascript
// Detect nested <a> elements
document.querySelectorAll('a a').forEach(nested => {
  console.error('Nested link found:', nested.href, 'inside', nested.closest('a').href);
});

// Check for duplicate tab stops per card
document.querySelectorAll('.service-card').forEach(card => {
  const links = card.querySelectorAll('a');
  if (links.length > 1) {
    console.warn('Service card has multiple links:', card.querySelector('h3')?.textContent);
  }
});
```

---

## Developer Notes

### General Approach

Remove the nested link structure and implement one of two accessible card patterns: (A) a single link with CSS-expanded click area, or (B) a heading-level link with JavaScript click delegation for the card surface.

### Current State (Problem)

```html
<!-- INVALID: <a> nested inside <a> -->
<a href="/services/ai-development/" class="service-card">
  <h3>AI Development</h3>
  <p>Build intelligent applications with cutting-edge AI.</p>
  <a href="/services/ai-development/" class="learn-more">Learn More</a>  <!-- Nested! -->
</a>
```

This produces:
- Invalid HTML (nested `<a>`)
- Two tab stops for the same destination
- Screen readers announce two links per card
- Voice control shows two overlapping click targets

### Recommended Fix — Option A: Single Link with Expanded Click Area

```html
<div class="service-card">
  <h3>
    <a href="/services/ai-development/">AI Development</a>
  </h3>
  <p>Build intelligent applications with cutting-edge AI.</p>
</div>
```

```css
.service-card {
  position: relative;
}

/* Expand the heading link to cover the entire card */
.service-card h3 a::after {
  content: '';
  position: absolute;
  inset: 0;
}

/* Ensure focus outline wraps the card, not just the text */
.service-card h3 a:focus-visible {
  outline: none;
}

.service-card:has(h3 a:focus-visible) {
  outline: 3px solid #0066CC;
  outline-offset: 2px;
  border-radius: 4px;
}
```

### Recommended Fix — Option B: JavaScript Click Delegation

```html
<div class="service-card" data-href="/services/ai-development/">
  <h3><a href="/services/ai-development/">AI Development</a></h3>
  <p>Build intelligent applications with cutting-edge AI.</p>
</div>
```

```javascript
document.querySelectorAll('.service-card[data-href]').forEach(card => {
  card.style.cursor = 'pointer';
  card.addEventListener('click', (e) => {
    // Don't intercept if user clicked the actual link or is selecting text
    if (e.target.closest('a') || window.getSelection().toString()) return;
    window.location.href = card.dataset.href;
  });
});
```

### Components / Files to Audit

- Service card component template (e.g., `partials/service-card.php`)
- Service card CSS (click area expansion or card-level cursor styles)
- Any JavaScript handling card clicks
- Homepage and Services page templates where cards are rendered

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **Inclusive Components (Heydon Pickering)** | [Card pattern](https://inclusive-components.design/cards/) using heading link + `::after` pseudo-element | One tab stop, entire card clickable, valid HTML. |
| **Smashing Magazine** | Article cards use a single heading link with a `::after` overlay for the full card | Avoids nested links; one focusable element per card. |
| **GitHub** | Repository cards have one link (the repo name) with CSS expanding the click target | Clean single-link pattern with no duplicate tab stops. |
| **UK Design System** | Card components use the heading link pattern with explicit guidance against wrapping cards in `<a>` | Government-grade accessible card implementation. |
