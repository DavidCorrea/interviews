# M-38: Card Borders Insufficient Contrast (1.56:1)

**Issue ID:** M-38
**Priority:** Medium
**WCAG Criteria:** 1.4.11 Non-text Contrast (AA)
**Affected Personas:** Low Contrast Sensitivity

---

## User Story

As a **user with low contrast sensitivity**, I want **card boundaries to be clearly visible** so that **I can distinguish individual content cards from the background and understand the grouping of related information.**

---

## Acceptance Criteria

- [ ] Card border colors achieve a contrast ratio of at least **3:1** against both the card background and the page background.
- [ ] Current card border color `#CFCFCF` on `#FFFFFF` (1.56:1) is replaced with a color that meets the 3:1 threshold (e.g., `#767676` or darker).
- [ ] The visual design of cards remains clean and not overly heavy — the border should define the boundary without dominating.
- [ ] All card variants across the site (service cards, case study cards, testimonial cards, blog cards) are updated consistently.
- [ ] The fix applies across all breakpoints (mobile, tablet, desktop).

---

## How to Test the Change

### Manual Testing

1. Open any page with card components (Homepage, Services, Case Studies).
2. Use the [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) to measure the contrast between the card border color and the page background (`#FFFFFF`).
3. Confirm the ratio is at least **3:1**.
4. Also check the contrast between the card border and the card's internal background (if different from white).
5. Zoom to 200% and 400% — verify card boundaries remain visible.
6. View the page in grayscale (Chrome DevTools > Rendering > Emulate vision deficiency > Achromatopsia) to confirm borders are still distinguishable.

### Automated Testing

1. Run axe DevTools — specifically check for WCAG 1.4.11 Non-text Contrast violations.
2. Write a script to extract all `.card` border colors and test against adjacent backgrounds:
   ```javascript
   document.querySelectorAll('.card').forEach(card => {
     const border = getComputedStyle(card).borderColor;
     console.log(`Card border: ${border}`);
   });
   ```

---

## Developer Notes

### General Explanation

Card borders at `#CFCFCF` on `#FFFFFF` produce only a 1.56:1 contrast ratio — half the 3:1 minimum required by WCAG 1.4.11 for non-text UI components. Users with reduced contrast sensitivity or in bright environments cannot see the card boundaries, making the cards appear to float without defined edges. The fix is to darken the border color or add a subtle box-shadow as a supplemental boundary indicator.

### Code Examples

**Before (current):**
```css
.card {
  border: 1px solid #CFCFCF; /* 1.56:1 contrast on white — FAIL */
  background: #FFFFFF;
}
```

**After — Option A (darker border):**
```css
.card {
  border: 1px solid #767676; /* 4.54:1 contrast on white — PASS */
  background: #FFFFFF;
}
```

**After — Option B (medium border + shadow for depth):**
```css
.card {
  border: 1px solid #949494; /* 3.03:1 contrast on white — PASS */
  background: #FFFFFF;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12);
}
```

**After — Option C (no border, use shadow only):**
```css
.card {
  border: none;
  background: #FFFFFF;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15); /* Creates visible boundary */
  border-radius: 8px;
}
```

### Components / Files to Audit

- `.card` class and any card variant classes (`.service-card`, `.case-study-card`, `.testimonial-card`, `.blog-card`)
- Global component stylesheet
- Any WordPress block or Elementor widget that renders cards
- Check for border color overrides in section-specific styles

---

## Examples from Other Sites

- **Google Material Design:** Cards use `box-shadow` (elevation) rather than borders to define boundaries, providing consistent visual separation regardless of background color.
- **Shopify Polaris Design System:** Card borders use `#C9CCCF` on `#F6F6F7` (3.1:1+) with an additional subtle shadow for reinforcement.
- **GitHub:** Repository cards use `border: 1px solid #d0d7de` on `#ffffff` (approximately 2.7:1) supplemented with interactive border color changes on hover.
- **Linear.app:** Uses no borders on cards, relying entirely on background color contrast and shadows to create card boundaries, ensuring 3:1+ contrast.
