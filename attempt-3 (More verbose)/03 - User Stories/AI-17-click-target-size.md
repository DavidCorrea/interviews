# AI-17: Ensure Click Targets at Least 44x44px

## Metadata
- **ID:** AI-17
- **Priority:** 2 High
- **Personas Affected:** 3+ of 16 personas (motor impairment, senior, touch users)
- **WCAG Criteria:** 2.5.5 Target Size (AAA), 2.5.8 Target Size (Minimum) (AA — WCAG 2.2)
- **Effort:** Medium (3–6 hours)

---

## User Story

**As a** user with motor impairment, tremor, or someone using a touch device,

**I want** all clickable elements (links, buttons, icons) to have a minimum touch target of 44x44 pixels,

**So that** I can reliably activate them on the first try without accidentally clicking adjacent elements.

---

## Acceptance Criteria

- [ ] All interactive elements have a minimum hit area of 44x44px
- [ ] "Learn More" links, arrow icons, and nav links meet the 44x44px minimum
- [ ] Entire cards are clickable when the card is the primary interactive element
- [ ] Adjacent clickable elements have at least 8px spacing between them
- [ ] Padding (not just margin) is used to increase hit area where needed
- [ ] Targets remain usable with "large cursor" or "large pointer" system setting
- [ ] On touch devices, every target can be hit on first try without zooming

---

## Test Plan

### DevTools Measurement
1. Open `https://launchpadlab.com/` in Chrome or Firefox
2. Use DevTools to inspect each interactive element:
   - Nav links
   - "Learn More" links
   - Arrow icons (carousel, etc.)
   - Buttons
   - Social icons
   - Card links
3. **Expected:** Computed hit area (including padding) is at least 44x44px
4. Use "Inspect" → check computed `padding`, `min-width`, `min-height`

### Large Cursor Test
1. Enable "Large cursor" or "Large pointer" in OS accessibility settings
2. Navigate the site
3. **Expected:** All targets are still easily clickable
4. **Expected:** No targets are obscured or too small for the larger cursor

### Spacing Between Targets
1. Identify adjacent clickable elements (e.g., nav items, icon buttons)
2. **Expected:** At least 8px gap between their hit areas
3. Measure with DevTools or ruler tool

### Touch Device Test
1. Use a touch device (phone/tablet) or Chrome DevTools device emulation
2. Tap each interactive element
3. **Expected:** Can hit every target on first try without zooming
4. **Expected:** No accidental taps on wrong element due to proximity

### Components to Measure
- [ ] Header nav links
- [ ] Hamburger menu button
- [ ] "Learn More" / "Read More" links
- [ ] Carousel prev/next arrows
- [ ] Card links (entire card or just text?)
- [ ] Footer links
- [ ] Social icons
- [ ] CTA buttons
- [ ] Form submit buttons

---

## Developer Notes

### Small Links
Add padding to increase hit area without changing visual size of text:

```css
a {
  padding: 12px 16px;
  display: inline-block;
  min-height: 44px;
  min-width: 44px;
  /* Or use line-height + padding to reach 44px */
}
```

### Card-Based Layouts
Make entire card a click target:

```html
<!-- Option 1: Link wraps entire card -->
<a href="/case-study/1" class="card-link">
  <div class="card">
    <h3>Project Name</h3>
    <p>Description...</p>
  </div>
</a>

/* Option 2: CSS pseudo-element overlay */
.card {
  position: relative;
}
.card::after {
  content: '';
  position: absolute;
  inset: 0;
}
.card-link { position: relative; z-index: 1; }
```

### Nav Links
```css
.nav a {
  padding: 12px 16px;
  min-height: 44px;
  display: inline-flex;
  align-items: center;
}
```

### Icon Buttons
```css
.icon-button {
  min-width: 44px;
  min-height: 44px;
  padding: 10px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}
```

### Spacing Between Targets
```css
.nav {
  gap: 8px; /* or more */
}
.button-group {
  gap: 8px;
}
```

### Use min-height and min-width on Buttons
```css
button, .btn {
  min-height: 44px;
  min-width: 44px;
  padding: 12px 24px;
}
```

### Components to Audit (LaunchPad Lab)
- [ ] Header navigation
- [ ] "Learn More" links in service cards
- [ ] Carousel arrows
- [ ] Footer links
- [ ] Social icons
- [ ] CTA buttons
- [ ] Any icon-only buttons

---

## Examples

| Site | Approach |
|------|----------|
| **Apple.com** | Large touch targets; generous padding on nav and CTAs |
| **Google Material Design** | 48dp (≈48px) minimum touch target guideline |
| **iOS Human Interface Guidelines** | 44pt minimum for touch targets |
