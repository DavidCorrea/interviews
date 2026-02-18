# AI-06: Fix Focus Indicators on All Interactive Elements

## Metadata
- **ID:** AI-06
- **Priority:** 1 Critical
- **Personas Affected:** 8 of 16 personas (keyboard users, low vision, motor)
- **WCAG Criteria:** 2.4.7 Focus Visible (AA)
- **Effort:** Small (1–2 hours)

---

## User Story

**As a** keyboard user or someone who navigates without a mouse,

**I want** a clear, visible focus indicator on every interactive element when I tab to it,

**So that** I always know where my focus is and can successfully navigate and use the site.

---

## Acceptance Criteria

- [ ] Every link, button, form field, and interactive element shows a visible focus ring when focused
- [ ] Focus ring has at least 3:1 contrast against the adjacent background
- [ ] Focus ring is at least 2px thick (or equivalent visibility)
- [ ] No interactive element uses `outline: none` or `outline: 0` without a visible replacement
- [ ] Focus ring is visible on both light and dark backgrounds
- [ ] `:focus-visible` is used (or `:focus` with care) so mouse users don't see focus ring on click, but keyboard users do
- [ ] Carousel/slider controls, custom dropdowns, and tab panels have focus indicators

---

## Test Plan

### Keyboard-Only Navigation
1. Unplug mouse (or use keyboard only)
2. Navigate to `https://launchpadlab.com/`
3. Press Tab repeatedly through the entire page
4. **Expected:** Each focusable element (links, buttons, form fields, nav items) shows a visible focus ring
5. Repeat on: About, Services, Contact, Blog
6. **Expected:** No element receives focus without a visible indicator

### Element Checklist
- [ ] Skip link (if present)
- [ ] Logo/home link
- [ ] All navigation menu items
- [ ] All footer links
- [ ] All CTA buttons
- [ ] Contact form: name, email, message, submit button
- [ ] Any "Read more" or "Learn more" links
- [ ] Carousel/slider previous/next buttons
- [ ] Any custom dropdowns or accordions
- [ ] Social media links

### Light and Dark Backgrounds
1. Tab to elements on white/light sections — **Expected:** Focus ring visible (e.g., dark outline)
2. Tab to elements on dark sections (e.g., footer, dark hero) — **Expected:** Focus ring visible (e.g., light outline or high-contrast color)

### Automated Testing
- Run axe DevTools — **Expected:** No "Focus indicators" or "focus-visible" violations
- Use Lighthouse accessibility audit — **Expected:** No focus-related failures

---

## Developer Notes

### Remove Problematic Styles
Search and remove or override:

```css
/* Remove these */
*:focus { outline: none; }
*:focus { outline: 0; }
a:focus { outline: none; }
button:focus { outline: none; }
```

### Add Global Focus Styles
```css
:focus-visible {
  outline: 2px solid #000;
  outline-offset: 2px;
}

/* For dark backgrounds */
.dark-section a:focus-visible,
.dark-section button:focus-visible {
  outline-color: #fff;
  outline-offset: 2px;
}
```

### Alternative: box-shadow
If `outline` causes layout issues:

```css
:focus-visible {
  outline: none;
  box-shadow: 0 0 0 2px #fff, 0 0 0 4px #000;
}
```

### :focus vs :focus-visible
- `:focus-visible` shows focus ring only when focus is from keyboard (or similar) — avoids ring on mouse click
- `:focus` shows ring whenever focused — can look odd when clicking with mouse
- Prefer `:focus-visible` for better UX; provide fallback for older browsers:

```css
:focus {
  outline: 2px solid #000;
  outline-offset: 2px;
}
:focus:not(:focus-visible) {
  outline: none;
}
:focus-visible {
  outline: 2px solid #000;
  outline-offset: 2px;
}
```

### Custom Components
- Ensure custom buttons, tabs, and dropdowns use `tabindex="0"` if not natively focusable
- Add `:focus-visible` styles to all custom interactive elements
- Test carousel controls — they are often custom and may need explicit focus styles

### Files to Modify
- Global CSS (reset, base styles)
- Component styles (buttons, links, form controls)
- Any file with `outline: none` or `outline: 0`

---

## Examples

| Site | Approach |
|------|----------|
| **GitHub.com** | Clear blue focus ring on all interactive elements |
| **Stripe.com** | Visible focus outlines; consistent across components |
| **Adobe.com** | High-contrast focus indicators; blue ring on light, light ring on dark |
| **GOV.UK** | Yellow focus ring; highly visible; follows design system |
