# H-27: Contact Form Two-Column Layout Doesn't Reflow

**Issue ID:** H-27
**Priority:** High
**WCAG Criteria:** 1.4.10 Reflow (AA), 1.4.4 Resize Text (AA)
**Affected Personas:** Low Vision Screen Magnifier, Low Vision

---

## User Story

**As a** low-vision user browsing at 200% zoom or higher,
**I want** the contact form to reflow into a single column at high magnification levels,
**so that** I can complete the form without horizontal scrolling or a confusing zigzag reading pattern.

---

## Acceptance Criteria

- [ ] At 200% browser zoom (or viewport width ≤ 320px CSS pixels equivalent), the contact form displays in a single column with full-width fields.
- [ ] No horizontal scrollbar appears at up to 400% zoom on a 1280px-wide monitor.
- [ ] Form fields, labels, and buttons are all readable and usable at 200%, 300%, and 400% zoom.
- [ ] The tab order follows a logical top-to-bottom sequence in the single-column layout.
- [ ] Field labels remain visually associated with their inputs at all zoom levels.
- [ ] The submit button spans the full width of the single-column layout.

---

## How to Test the Change

### Manual Testing

1. **Browser zoom test:** On a 1280px monitor, set browser zoom to 200%, 300%, and 400%. Navigate to the contact form. Confirm single-column layout with no horizontal scroll.
2. **Responsive design mode:** In Chrome DevTools, set viewport to 320px wide. Confirm the form is single-column and fully usable.
3. **Screen magnifier test:** Using ZoomText, macOS Zoom, or Windows Magnifier at 200%+, fill out the contact form. Confirm all fields are reachable without horizontal panning.
4. **Tab order test:** At 200%+ zoom, tab through all form fields. Confirm the order is top-to-bottom (First Name → Last Name → Email → Company → Message → Submit), not left-right zigzag.

### Automated Testing

```javascript
// Check that at narrow viewport, form fields are stacked (single column)
// Puppeteer / Playwright example
await page.setViewportSize({ width: 320, height: 900 });
const fields = await page.$$('.contact-form input, .contact-form textarea');
let prevBottom = 0;
for (const field of fields) {
  const box = await field.boundingBox();
  console.assert(box.y >= prevBottom, 'Fields should stack vertically');
  prevBottom = box.y + box.height;
}
```

---

## Developer Notes

### General Approach

Change the contact form's grid/flex layout to collapse from two columns to one column at a breakpoint that activates at 200% zoom on a standard display (effectively at `max-width: 640px` or the equivalent `@media` query).

### Current State (Problem)

```css
.contact-form .form-row {
  display: flex;
  gap: 20px;
}

.contact-form .form-row .field-half {
  width: 50%;  /* Forces two columns at all sizes */
}
```

### Recommended Fix

```css
.contact-form .form-row {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.contact-form .form-row .field-half {
  flex: 1 1 100%; /* Default: single column (mobile-first) */
}

/* Two columns only when there's enough space */
@media (min-width: 640px) {
  .contact-form .form-row .field-half {
    flex: 1 1 calc(50% - 10px);
  }
}

/* Ensure single column when user zooms to 200%+ */
@media (max-width: 640px) {
  .contact-form .form-row .field-half {
    width: 100%;
    flex-basis: 100%;
  }
}
```

### Alternative: Use CSS Grid with Auto-Fit

```css
.contact-form .form-row {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
}

/* No media query needed — grid auto-collapses when space is insufficient */
```

### Tab Order Verification

Ensure the HTML source order is logical for single-column reading:

```html
<form class="contact-form">
  <div class="form-row">
    <div class="field-half">
      <label for="first-name">First Name</label>
      <input type="text" id="first-name" name="first-name">
    </div>
    <div class="field-half">
      <label for="last-name">Last Name</label>
      <input type="text" id="last-name" name="last-name">
    </div>
  </div>
  <!-- When reflowed to single column: First Name stacks above Last Name -->
  <div class="form-row">
    <div class="field-half">
      <label for="email">Email</label>
      <input type="email" id="email" name="email">
    </div>
    <div class="field-half">
      <label for="company">Company</label>
      <input type="text" id="company" name="company">
    </div>
  </div>
  <div class="form-row">
    <label for="message">Message</label>
    <textarea id="message" name="message"></textarea>
  </div>
  <button type="submit" class="btn btn-primary" style="width: 100%;">Contact Us</button>
</form>
```

### Components / Files to Audit

- Contact form CSS (grid/flex layout rules for `.form-row`, `.field-half`)
- Ninja Forms template overrides (if any)
- Contact page template
- Global responsive breakpoints in the theme

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **GOV.UK** | All forms are single-column by default with generous field widths | No reflow needed — already works at any zoom level. |
| **Stripe** | Contact form uses CSS Grid `auto-fit` with `minmax(300px, 1fr)` | Gracefully collapses without media queries. |
| **Apple** | Support forms are single-column on all devices | Simplest approach — guaranteed reflow compliance. |
| **WCAG Understanding 1.4.10** | Recommends content reflow to 320px CSS pixels without horizontal scroll | The definitive reference for reflow requirements. |
