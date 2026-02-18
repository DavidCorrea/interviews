# H-15: Body Text Contrast (#555555 on White)

**Issue ID:** H-15
**Priority:** High
**WCAG Criteria:** 1.4.3 Contrast (Minimum) (AA), 1.4.6 Contrast (Enhanced) (AAA)
**Affected Personas:** Dyslexic, Low Contrast Sensitivity, Situational Contrast, Low Vision

---

## User Story

**As a** user with low contrast sensitivity reading the site in a brightly lit environment,
**I want** body text to have strong contrast against the background,
**so that** I can read comfortably without straining my eyes, even under sub-optimal lighting conditions.

---

## Acceptance Criteria

- [ ] All body text (`<p>`, `<li>`, `<span>`, and other prose elements) achieves at least **7:1** contrast ratio against its background to meet WCAG AAA (Enhanced Contrast).
- [ ] The body text color is changed from `#555555` (7.46:1 on white — passes AA but borders AAA) to `#333333` (12.63:1) or darker.
- [ ] The updated color is applied globally through the base typography styles, not per-component overrides.
- [ ] No text element on a white or light background falls below the 4.5:1 AA minimum.
- [ ] The change is verified under simulated bright ambient light conditions (e.g., increased screen brightness + reduced device contrast).
- [ ] The updated color maintains visual harmony with the overall design system (headings, links, buttons).

---

## How to Test the Change

### Manual Testing

1. **Contrast checker:** Use the [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) to verify the new body text color against `#FFFFFF`. Confirm the ratio is ≥ 7:1 (AAA for normal text).
2. **DevTools inspection:** In Chrome DevTools, inspect any `<p>` element. The Styles panel shows the computed contrast ratio next to the color value. Confirm it shows AAA compliance.
3. **Bright environment test:** Turn screen brightness to maximum in a well-lit room. Read a full paragraph of body text. Confirm readability without squinting.
4. **User testing:** Ask a person with low vision or a person over 60 to read a full services page. Measure reading speed and comfort compared to the previous color.
5. **Cross-browser check:** Verify the text color renders consistently across Chrome, Firefox, Safari, and Edge.

### Automated Testing

- Run Lighthouse accessibility audit: confirm no "Background and foreground colors do not have a sufficient contrast ratio" findings for body text.
- Run `axe-core`: check for "Elements must have sufficient color contrast."

```javascript
// Check body text contrast programmatically
document.querySelectorAll('p, li, .entry-content').forEach(el => {
  const color = getComputedStyle(el).color;
  const bg = getComputedStyle(el).backgroundColor;
  // Use a contrast calculation library to verify ratio
  console.log(`Element: ${el.tagName}, Color: ${color}, BG: ${bg}`);
});
```

---

## Developer Notes

### General Approach

Change the body text color from `#555555` to a darker value that comfortably passes WCAG AAA. The recommended value is `#333333` (12.63:1 on white), which provides excellent readability while remaining visually softer than pure black.

### Current State (Problem)

```css
body {
  color: #555555;  /* 7.46:1 on #FFFFFF — passes AA, barely misses AAA */
}
```

While 7.46:1 technically passes WCAG AA (4.5:1), it is marginal for AAA (7:1) and can cause reading fatigue under bright ambient lighting, where effective contrast drops to an estimated 2.5–3.7:1.

### Recommended Fix

```css
body {
  color: #333333;  /* 12.63:1 on #FFFFFF — comfortably passes AAA */
}
```

### Color Options Comparison

| Color | Ratio on #FFF | AA (4.5:1) | AAA (7:1) | Notes |
|---|---|---|---|---|
| `#555555` | 7.46:1 | Pass | Borderline | Current — fatiguing in bright light |
| `#444444` | 9.73:1 | Pass | Pass | Good balance |
| `#333333` | 12.63:1 | Pass | Pass | Recommended — strong readability |
| `#222222` | 15.91:1 | Pass | Pass | Very high contrast; may feel heavy |
| `#000000` | 21:1 | Pass | Pass | Maximum contrast; can cause halation for some users |

### Why Not Pure Black (#000000)?

Pure black on pure white can cause "halation" — a visual effect where text appears to vibrate or shimmer for some users with dyslexia or astigmatism. `#333333` provides strong contrast without this issue.

### Components / Files to Audit

- Base `body` color declaration in the main stylesheet
- Any component-level overrides that explicitly set `color: #555555`
- Typography SCSS/CSS variables (e.g., `$text-color`, `--color-body`)
- WordPress theme Customizer settings if color is configurable

---

## Examples from Other Sites

| Site | Body Text Color | Ratio on White | Why It Works |
|---|---|---|---|
| **Apple** | `#1d1d1f` | 17.45:1 | Near-black with excellent readability; no halation. |
| **Stripe** | `#425466` | 6.81:1 (on #F6F9FC) | Optimized for their light gray background. |
| **GOV.UK** | `#0b0c0c` | 19.78:1 | Government standard — maximum readability for all users. |
| **Medium** | `rgba(41,41,41,1)` (#292929) | 14.72:1 | Designed for long-form reading comfort. |
