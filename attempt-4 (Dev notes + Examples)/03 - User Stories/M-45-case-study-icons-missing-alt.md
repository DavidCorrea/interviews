# M-45: "Case Study Increase" Icons Missing Alt Text

**Issue ID:** M-45
**Priority:** Medium
**WCAG Criteria:** 1.1.1 Non-text Content (A)
**Affected Personas:** Screen Reader, Blue-Yellow Color Blind, Red-Green Color Blind

---

## User Story

As a **screen reader user or color-blind user**, I want **directional/trend icons in case study statistics to have descriptive alt text** so that **I can understand whether a metric increased or decreased, without relying on the icon's visual appearance or color.**

---

## Acceptance Criteria

- [ ] All arrow/trend icons within case study stat blocks have meaningful `alt` text (e.g., `alt="increase"`, `alt="decrease"`, or `alt="growth"`).
- [ ] The alt text conveys the direction/trend the icon represents (not "arrow icon" or "green arrow").
- [ ] The trend information is also communicated through adjacent text (not solely through the icon) — e.g., "Revenue increased by 45%."
- [ ] Icons that are purely decorative duplicates of information already in text are marked `alt=""` and `aria-hidden="true"`.
- [ ] The solution works for both `<img>` icons and inline SVG icons.

---

## How to Test the Change

### Manual Testing

1. Navigate to the Case Studies page (or any page with case study statistics).
2. Open DevTools and inspect each trend/arrow icon within stat blocks.
3. Verify each has meaningful `alt` text (for `<img>`) or `aria-label` (for SVG/icon fonts).
4. Use VoiceOver or NVDA to navigate through the statistics — confirm the trend direction is announced.
5. View the page in grayscale (DevTools > Rendering > Emulate: Achromatopsia) — confirm the trend is understandable without color.

### Automated Testing

1. Run axe DevTools on pages with case study stats — check for missing alt text on images.
2. Audit script:
   ```javascript
   document.querySelectorAll('.case-study-stat img, .stat-icon').forEach(icon => {
     const alt = icon.getAttribute('alt');
     const ariaLabel = icon.getAttribute('aria-label');
     console.log(`Icon: ${icon.src || 'SVG'}, alt="${alt}", aria-label="${ariaLabel}"`);
   });
   ```
3. Run `pa11y` on case study pages.

---

## Developer Notes

### General Explanation

Arrow/increase icons in case study statistics convey directional meaning (a metric went up or down). Using `alt=""` on these icons marks them as decorative, but they carry information that is not available elsewhere in the surrounding text. The fix is to add meaningful alt text to the icons AND ensure the trend direction is also conveyed in the adjacent text content, providing redundant cues for both screen reader and color-blind users.

### Code Examples

**Before (current):**
```html
<div class="case-study-stat">
  <img src="/icons/arrow-up.svg" alt="">
  <span class="stat-value">45%</span>
  <span class="stat-label">Revenue</span>
</div>
```

**After — Option A (alt text on img):**
```html
<div class="case-study-stat">
  <img src="/icons/arrow-up.svg" alt="Increased">
  <span class="stat-value">45%</span>
  <span class="stat-label">Revenue increase</span>
</div>
```

**After — Option B (inline SVG with aria-label):**
```html
<div class="case-study-stat">
  <svg aria-label="Increase" role="img" class="trend-icon trend-up">
    <use href="#icon-arrow-up"></use>
  </svg>
  <span class="stat-value">45%</span>
  <span class="stat-label">Revenue</span>
</div>
```

**After — Option C (icon is decorative, text carries meaning):**
```html
<div class="case-study-stat">
  <img src="/icons/arrow-up.svg" alt="" aria-hidden="true">
  <span class="stat-value">
    <span class="visually-hidden">Increased by </span>45%
  </span>
  <span class="stat-label">Revenue</span>
</div>
```

```css
.visually-hidden {
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

**Add non-color cues for color-blind users:**
```css
.trend-up {
  color: #2E7D32; /* Green */
}

.trend-up::before {
  content: "▲ "; /* Visual arrow character as redundant cue */
}

.trend-down {
  color: #C62828; /* Red */
}

.trend-down::before {
  content: "▼ ";
}
```

### Components / Files to Audit

- Case study page template(s)
- Homepage case study carousel/section
- Case study stat/metric component or widget
- Icon assets directory — inventory all trend/arrow icons
- Check if icons are `<img>`, inline SVG, or icon font glyphs

---

## Examples from Other Sites

- **Stripe.com:** Growth metrics on customer stories use text like "45% increase in conversion" without relying on icon alone. Arrow icons include `aria-hidden="true"` since the text is sufficient.
- **HubSpot Case Studies:** Use text labels like "↑ 45% increase" with both a text arrow character and the word "increase" for redundancy.
- **Salesforce Customer Stories:** Statistics include directional text (e.g., "Revenue Up 45%") alongside any visual indicators, making icons purely supplemental.
- **McKinsey.com:** Case study metrics pair colored indicators with explicit text labels ("increase," "decrease," "improvement"), never relying on visual cues alone.
