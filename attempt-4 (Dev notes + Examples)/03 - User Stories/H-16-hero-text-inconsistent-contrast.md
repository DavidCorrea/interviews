# H-16: Hero Text on Photographic Background with Inconsistent Contrast

**Issue ID:** H-16
**Priority:** High
**WCAG Criteria:** 1.4.3 Contrast (Minimum) (AA), 1.4.6 Contrast (Enhanced) (AAA)
**Affected Personas:** Low Contrast Sensitivity, Low Vision, Situational Contrast

---

## User Story

**As a** user with low vision viewing the homepage on a bright screen,
**I want** hero headline and body text to maintain consistent, readable contrast against the background,
**so that** I can read the primary messaging regardless of the viewport size, background image content, or lighting conditions.

---

## Acceptance Criteria

- [ ] All hero text (`<h1>`, `<h2>`, `<p>`) achieves a minimum **4.5:1** contrast ratio against every region of the background it overlaps — not just the darkest area.
- [ ] Large text (18pt+ or 14pt+ bold) achieves a minimum **3:1** contrast ratio per WCAG AA.
- [ ] The background overlay is opaque enough to guarantee consistent contrast regardless of the underlying photograph's content (light sky, faces, etc.).
- [ ] Contrast ratios are tested at multiple viewport widths (320px, 768px, 1024px, 1440px, 1920px) since background images shift with responsive layouts.
- [ ] Text does not overlap areas where the gradient overlay fades to transparent.
- [ ] The fix is tested with at least 3 different hero background images (if images rotate or vary by page) to ensure the overlay works universally.
- [ ] When viewed at maximum screen brightness in direct sunlight, the hero text remains legible.

---

## How to Test the Change

### Manual Testing

1. **Contrast sampling:** Use a color picker tool (e.g., Chrome DevTools eyedropper, Colour Contrast Analyser by TPGi) to sample the text color and the background color at multiple points behind the text. Check the ratio at the lightest background region.
2. **Responsive test:** Resize the browser from 320px to 1920px width. At each breakpoint, confirm the text remains legible and the overlay provides sufficient contrast.
3. **Multiple images test:** If hero images vary by page or rotate, test each image variant. The overlay must work for all of them.
4. **Bright environment test:** View the hero section on a laptop at max brightness in a sunny room. Confirm the headline is readable without squinting.
5. **Screenshot + grayscale:** Take a screenshot of the hero and convert it to grayscale. Confirm the text is still clearly readable.

### Automated Testing

- Use a visual regression tool (e.g., Percy, Chromatic) to capture hero section screenshots at multiple viewports and flag contrast issues.
- Custom contrast sampling script:

```javascript
// Approximate contrast check using canvas
function sampleHeroContrast() {
  const hero = document.querySelector('.hero-section');
  const canvas = document.createElement('canvas');
  const ctx = canvas.getContext('2d');

  // Capture the hero as an image via html2canvas or similar
  // Sample pixels behind text areas and calculate contrast ratios
  console.log('Manual sampling recommended — automated image contrast is approximate.');
}
```

---

## Developer Notes

### General Approach

Strengthen the background overlay so that it provides a guaranteed minimum contrast floor for all text areas. The most reliable approach is a solid or semi-opaque dark overlay rather than a gradient that fades to transparent.

### Current State (Problem)

```css
.hero-section {
  background-image: url('/wp-content/uploads/hero-bg.jpg');
  background-size: cover;
  background-position: center;
}

.hero-overlay {
  background: linear-gradient(
    to right,
    rgba(0, 0, 0, 0.6),    /* Left side: ~4.5:1 for white text */
    rgba(0, 0, 0, 0)         /* Right side: NO overlay — contrast depends on image */
  );
}
```

The gradient fades to fully transparent on the right, meaning text that falls over bright image areas (sky, light clothing, white backgrounds) may have contrast as low as 1.5:1.

### Recommended Fix — Option A: Uniform Semi-Opaque Overlay

```css
.hero-overlay {
  background: rgba(0, 0, 0, 0.65);  /* Uniform overlay — ~7:1 for white text */
}
```

### Recommended Fix — Option B: Gradient That Never Drops Below Minimum

```css
.hero-overlay {
  background: linear-gradient(
    to right,
    rgba(0, 0, 0, 0.7),     /* Left: strong coverage */
    rgba(0, 0, 0, 0.55)      /* Right: still meets 4.5:1 minimum for white text */
  );
}
```

### Recommended Fix — Option C: Text Shadow + Overlay Combo

```css
.hero-section h1,
.hero-section h2,
.hero-section p {
  text-shadow:
    0 1px 3px rgba(0, 0, 0, 0.8),
    0 0 20px rgba(0, 0, 0, 0.5);
}

.hero-overlay {
  background: rgba(0, 0, 0, 0.5);
}
```

### Responsive Considerations

```css
/* Adjust overlay strength at different viewports */
@media (max-width: 768px) {
  .hero-overlay {
    /* On small screens the image crops differently — may need stronger overlay */
    background: rgba(0, 0, 0, 0.7);
  }
}
```

### Contrast Reference Table

| White text (#FFF) on overlay | Approximate Ratio | AA Large (3:1) | AA Normal (4.5:1) | AAA Normal (7:1) |
|---|---|---|---|---|
| `rgba(0,0,0,0.4)` | ~3.6:1 | Pass | Fail | Fail |
| `rgba(0,0,0,0.5)` | ~4.6:1 | Pass | Borderline | Fail |
| `rgba(0,0,0,0.6)` | ~6.2:1 | Pass | Pass | Fail |
| `rgba(0,0,0,0.65)` | ~7.0:1 | Pass | Pass | Borderline |
| `rgba(0,0,0,0.7)` | ~8.2:1 | Pass | Pass | Pass |

### Components / Files to Audit

- Hero section template (e.g., `partials/hero.php`, `components/Hero`)
- Hero CSS (overlay gradient, text-shadow, background-image)
- Any page-specific hero background images (homepage, services, about, contact)
- WordPress Customizer or ACF fields that allow editors to change hero images

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **Apple** | Dark, uniform overlay on hero images with white text; no gradient fade-to-transparent | Consistent contrast regardless of image content. |
| **Airbnb** | Hero text is placed on a solid-color block overlapping the image edge | Text never sits directly on an uncontrolled photo area. |
| **Spotify** | Uses duotone image effects that guarantee a dark enough color range for overlaid text | Image treatment itself ensures contrast, not just an overlay. |
| **gov.uk** | Avoids text on images entirely; uses solid backgrounds for text areas | The most foolproof approach — removes the contrast variability entirely. |
