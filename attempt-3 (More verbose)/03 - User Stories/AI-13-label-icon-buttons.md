# AI-13: Add Visible Labels to All Icon-Only Buttons

## Metadata
- **ID:** AI-13
- **Priority:** 2 High
- **Personas Affected:** 4+ of 16 personas
- **WCAG Criteria:** 1.1.1 Non-text Content (A), 2.5.3 Label in Name (A), 4.1.2 Name, Role, Value (A)
- **Effort:** Small–Medium (2–4 hours)

---

## User Story

**As a** screen reader user or someone using voice control,

**I want** every icon-only button (hamburger menu, social icons, carousel arrows, close buttons) to have an accessible name that describes its purpose,

**So that** I know what each button does when I navigate to it, and I can activate the correct one with voice commands like "Click Menu" or "Click Next slide."

---

## Acceptance Criteria

- [ ] Hamburger/menu button has accessible name: "Open menu" or "Menu"
- [ ] Social media links (LinkedIn, Twitter, etc.) have accessible names: "Visit our LinkedIn page," etc.
- [ ] Carousel/slider previous/next buttons: "Previous slide," "Next slide"
- [ ] Close buttons: "Close" or "Close dialog"
- [ ] All icon-only buttons pass axe DevTools — no "button without accessible name" violations
- [ ] Screen reader announces purpose when focusing each button
- [ ] Voice control can target each button by its label (e.g., "Click Menu")

---

## Test Plan

### Screen Reader Navigation
1. Open `https://launchpadlab.com/` with NVDA, VoiceOver, or JAWS
2. Tab to hamburger menu button
3. **Expected:** Announces "Open menu button" or "Menu button" — not just "button"
4. Tab to each social icon
5. **Expected:** "Visit our LinkedIn page link," etc. — not "link" or "LinkedIn logo"
6. Tab to carousel arrows (if present)
7. **Expected:** "Previous slide button," "Next slide button"
8. Open a modal/dialog; tab to close button
9. **Expected:** "Close button" or "Close dialog button"

### Voice Control
1. Enable voice control
2. Say "Click Menu" — **Expected:** Hamburger/menu opens
3. Say "Click Next slide" — **Expected:** Carousel advances
4. Say "Click Close" — **Expected:** Dialog closes
5. Say "Click LinkedIn" or "Click Visit our LinkedIn page" — **Expected:** Correct link activates

### Automated Testing
- Run axe DevTools on full page
- **Expected:** No "button without accessible name" or "link without accessible name" violations
- Fix any "Empty button" or "Image button missing alt text" issues

### Visual Verification
- aria-labels should match what users would naturally say
- "Menu" is more natural than "Navigation toggle" for hamburger
- "Next slide" is clearer than "Next" for carousel

---

## Developer Notes

### Hamburger Menu
```html
<!-- Option 1: aria-label -->
<button aria-label="Open menu" type="button">☰</button>

<!-- Option 2: sr-only text (preferred for flexibility) -->
<button type="button">
  <span class="sr-only">Menu</span>
  <span aria-hidden="true">☰</span>
</button>
```

### Social Links
```html
<a href="https://linkedin.com/company/launchpadlab" aria-label="Visit our LinkedIn page">
  <svg aria-hidden="true">...</svg>
</a>
```

### Carousel Controls
```html
<button aria-label="Previous slide" type="button">←</button>
<button aria-label="Next slide" type="button">→</button>
```

### Close Button
```html
<button aria-label="Close dialog" type="button">×</button>
```

### Screen Reader Only (.sr-only) Class
```css
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
```

### Mark Decorative Icons
- Use `aria-hidden="true"` on the icon SVG/element so screen readers don't announce it
- The button/link's accessible name comes from aria-label or sr-only text

### Components to Audit (LaunchPad Lab)
- [ ] Header/nav hamburger
- [ ] All social icons in header/footer
- [ ] Logo carousel prev/next
- [ ] Testimonial carousel prev/next
- [ ] Modal/dialog close buttons
- [ ] Any "X" or close icon
- [ ] Search toggle (if icon-only)

### Files to Modify
- Header/navigation component
- Footer (social links)
- Carousel/slider components
- Modal/dialog components

---

## Examples

| Site | Approach |
|------|----------|
| **Airbnb.com** | Labeled icon buttons; aria-labels on nav, filters, and actions |
| **Slack.com** | aria-labels on all icon buttons; consistent naming |
| **GitHub.com** | Tooltips + aria-labels; icons have clear purposes |
