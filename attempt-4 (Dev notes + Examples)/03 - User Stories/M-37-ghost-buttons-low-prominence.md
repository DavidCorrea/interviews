# M-37: Ghost/Outline Buttons Have Low Visual Prominence

**Issue ID:** M-37
**Priority:** Medium
**WCAG Criteria:** 1.4.11 Non-text Contrast (AA)
**Affected Personas:** Low Vision, Situational Contrast

---

## User Story

As a **user with low vision or in a high-glare environment**, I want **CTA buttons to be clearly distinguishable as interactive elements** so that **I can identify where to click without straining to see thin, low-contrast outlines against colored backgrounds.**

---

## Acceptance Criteria

- [ ] All ghost/outline button borders have a contrast ratio of at least **3:1** against their adjacent background color.
- [ ] Button borders are at least **2px** wide (up from 1px) to increase visual weight.
- [ ] Ghost buttons include at least one additional visual affordance beyond the border (e.g., a subtle background fill, drop shadow, icon, or increased font weight).
- [ ] The hover/focus state of ghost buttons provides a clear visual change (e.g., background fill, border color shift).
- [ ] Buttons pass the "squint test" — still identifiable as buttons when the page is viewed at arm's length or with blurred vision.

---

## How to Test the Change

### Manual Testing

1. Open the homepage and any page with ghost/outline CTAs.
2. Use the [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) or DevTools to measure the contrast ratio between the button border color and the adjacent background.
3. Confirm the ratio is at least 3:1.
4. Verify the border width is at least 2px via DevTools computed styles.
5. Zoom to 200% and 400% — confirm buttons remain clearly visible and identifiable.
6. Test in bright ambient light (e.g., near a window) to simulate situational contrast loss.

### Automated Testing

1. Run axe DevTools — check for Non-text Contrast (1.4.11) flags on button elements.
2. Contrast-audit script example:
   ```javascript
   // Pseudocode — check button border contrast
   document.querySelectorAll('.btn-outline, .ghost-btn').forEach(btn => {
     const borderColor = getComputedStyle(btn).borderColor;
     const bgColor = getComputedStyle(btn.parentElement).backgroundColor;
     console.log(`Border: ${borderColor}, BG: ${bgColor}`);
     // Feed into a contrast ratio calculator
   });
   ```

---

## Developer Notes

### General Explanation

Ghost buttons (outline-only, transparent background) are a popular design pattern, but the 1px white border on a colored background creates very low visual prominence. Users with low vision or in bright environments may not see the button at all. The fix is to increase border width, ensure border contrast meets 3:1, and optionally add a subtle background fill.

### Code Examples

**Before (current):**
```css
.btn-outline {
  background: transparent;
  border: 1px solid #FFFFFF;
  color: #FFFFFF;
}
```

**After (fixed):**
```css
.btn-outline {
  background: rgba(255, 255, 255, 0.1); /* Subtle fill for visual weight */
  border: 2px solid #FFFFFF;
  color: #FFFFFF;
  font-weight: 600;
}

.btn-outline:hover,
.btn-outline:focus-visible {
  background: rgba(255, 255, 255, 0.25);
  border-color: #FFFFFF;
}
```

**On light backgrounds, use a dark border:**
```css
.light-bg .btn-outline {
  border: 2px solid #333333; /* 3:1+ on white */
  color: #333333;
  background: rgba(0, 0, 0, 0.04);
}
```

**Alternative — convert ghost buttons to filled buttons for primary CTAs:**
```css
/* Replace ghost with filled for high-priority actions */
.btn-primary {
  background: #1A73E8;
  border: 2px solid #1A73E8;
  color: #FFFFFF;
}
```

### Components / Files to Audit

- Button component CSS (`.btn-outline`, `.ghost-btn`, or equivalent class names)
- Hero sections where ghost buttons overlay background images/colors
- CTA sections in the footer and mid-page callout areas
- Check for WordPress theme Customizer button style settings

---

## Examples from Other Sites

- **Stripe.com:** Uses ghost buttons sparingly and only on dark backgrounds where white borders provide strong contrast. Primary CTAs always use filled backgrounds.
- **Shopify.com:** Ghost buttons use a 2px border with high-contrast colors and include an arrow icon as an additional visual affordance.
- **Atlassian Design System:** Explicitly documents that "subtle" (ghost) buttons should only be used for tertiary actions and recommends filled buttons for primary and secondary CTAs.
- **Material Design (Google):** "Outlined" buttons use a 1px border but require a minimum contrast ratio of 3:1 and pair with filled "contained" buttons for primary actions.
