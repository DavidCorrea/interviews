# Increase Click Target Size on Service Card "Learn More" Links

## Priority: High

## User Story
As a user with motor impairments or reduced dexterity, I want the "Learn More" links on service cards to have adequately sized click targets so that I can navigate to service details without difficulty.

## Acceptance Criteria
- [ ] All "Learn More" links (or equivalent CTAs) on service cards meet minimum 24×24px click target size (WCAG 2.2 minimum)
- [ ] Click targets meet recommended 44×44px size where feasible
- [ ] Entire card is clickable OR link has sufficient padding to create adequate hit area
- [ ] Link text is readable (minimum 16px or equivalent for body text)
- [ ] Focus indicators are visible when navigating via keyboard
- [ ] No loss of functionality; users can still navigate to service detail pages

## Developer Notes

### General Explanation
WCAG 2.2 Success Criterion 2.5.8 (Target Size) requires touch targets to be at least 24×24 CSS pixels. Best practice recommends 44×44px for primary interactive elements. Small text and small click targets create barriers for users with motor impairments, wrist discomfort, and those using touch devices or progressive lenses.

**Strategies:**
1. Make the entire card clickable — wrap card content in a single `<a>` or use a card with `onClick` and proper keyboard support.
2. Increase link padding — use `padding` to expand the hit area without changing visual size.
3. Increase font size — ensure link text is at least 16px (or 1rem) for readability.

### Code Examples

**Making the entire card clickable (semantic approach):**
```html
<a href="/services/automation" class="service-card" style="display: block; text-decoration: none; color: inherit;">
  <div class="service-card__content">
    <h3>AI Automation</h3>
    <p>Streamline your workflows...</p>
    <span class="service-card__cta">Learn More</span>
  </div>
</a>
```

**Expanding hit area with padding (link-only approach):**
```html
<div class="service-card">
  <h3>AI Automation</h3>
  <p>Streamline your workflows...</p>
  <a href="/services/automation" class="service-card__link">
    Learn More
  </a>
</div>

<style>
.service-card__link {
  display: inline-block;
  padding: 12px 24px;  /* Creates ~44px min height with 16px text */
  font-size: 1rem;    /* 16px base */
  min-height: 44px;
  min-width: 44px;
  line-height: 1.25;
  /* Ensure focus indicator is visible */
  outline: 2px solid currentColor;
  outline-offset: 2px;
}
.service-card__link:focus-visible {
  outline: 2px solid #0066cc;
}
</style>
```

**Card as button/link with proper semantics:**
```html
<article class="service-card">
  <a href="/services/automation" class="service-card__link" aria-label="Learn more about AI Automation">
    <span class="service-card__link-focus">Learn More</span>
  </a>
  <!-- Or use ::after pseudo-element to create overlay hit area -->
</article>

<style>
.service-card {
  position: relative;
}
.service-card__link::after {
  content: '';
  position: absolute;
  inset: 0;
  /* Entire card becomes clickable */
}
.service-card__link {
  min-height: 44px;
  min-width: 44px;
  padding: 12px 20px;
}
</style>
```

### Components to Audit
- Homepage service cards
- Any similar card pattern across the site (e.g., case study cards, feature cards)
- Cards with "Learn More," "Read More," or similar CTA links

## Examples From Other Sites
- **Apple** — Service and product cards use large clickable areas; entire card surfaces are often interactive with clear focus states.
- **Google Material Design** — Guidelines specify 48×48dp minimum touch targets; cards are designed with full-surface tap targets.
- **Atlassian** — Design system recommends 44×44px minimum for interactive elements; card components use expanded hit areas and full-card clickability.

## References
- Main Report Item 2 (High Priority)
- WCAG 2.2 Success Criterion 2.5.8 (Target Size)
- Interview feedback: users with wrist discomfort and progressive lenses reported difficulty clicking "Learn More" links
- Primary CTAs driving users into service offerings
