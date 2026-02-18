# Issue 14: Fix Hero Text Contrast Over Background Images

**Priority:** Medium
**Location:** Homepage hero, About page hero, Services page hero
**Reported by:** Sam Chen (Dyslexia), Richard Okonkwo (Non-Technical Business Executive)

---

## User Story

**As a** user reading hero section text overlaid on a background image,
**I want** the text to have consistent, high contrast against the background across the entire text area,
**so that** I can read the headline and call-to-action without straining, regardless of the background image's brightness variation.

---

## Problem

Hero sections across the site use white text overlaid on photographic backgrounds with a semi-transparent dark overlay. This creates two problems:

1. **Variable brightness:** Photographs have areas of light and dark. Even with a dark overlay, lighter areas of the photo (e.g., sky, white surfaces, bright reflections) reduce contrast with the white text. A word may be legible over a dark area of the image but illegible where the image is brighter.

2. **Inconsistent contrast ratios:** The current semi-transparent overlay appears to be approximately `rgba(0, 0, 0, 0.3)` to `rgba(0, 0, 0, 0.5)`, which is insufficient over lighter image regions. WCAG AAA requires a 7:1 contrast ratio for normal text and 4.5:1 for large text. The current implementation may meet this over the darkest areas but fail over lighter spots.

Impact:
- **Dyslexic users** already struggle to distinguish letter forms. Reduced contrast makes letters blur together and increases reading fatigue.
- **Non-technical executives** are scanning quickly. If the hero text — often the most important message on the page — is hard to read, the first impression fails and they may leave.

---

## Acceptance Criteria

- [ ] All hero text (H1, subtitle, CTA buttons) maintains a minimum contrast ratio of **7:1** against the effective background at every point across the text area (WCAG AAA for normal text, SC 1.4.6)
- [ ] Large text (18pt+ or 14pt bold) maintains a minimum contrast ratio of **4.5:1** at every point (WCAG AAA for large text)
- [ ] Contrast is achieved through one or more of: increased overlay opacity, a solid background behind the text block, or a text shadow
- [ ] The solution works regardless of which background image is loaded (including CMS-uploaded images that may change)
- [ ] The hero section remains visually appealing — the fix should not completely obscure the background image
- [ ] CTA buttons in the hero maintain proper contrast in both default and hover states
- [ ] The contrast fix is responsive and works on all viewport sizes (the text may reflow, changing which part of the image is behind it)
- [ ] The fix is verified using a contrast analyzer tool sampling at least 5 points across the text area (not just the darkest point)

---

## How to Test

1. **Contrast analyzer — multiple sample points:** Use the [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) or [Colour Contrast Analyser (CCA)](https://www.tpgi.com/color-contrast-checker/) to test the contrast ratio at 5+ points across the hero text area:
   - Top-left of the text block
   - Top-right of the text block
   - Center of the text block
   - Bottom-left
   - Bottom-right
   All points must meet 7:1 for normal text or 4.5:1 for large text
2. **Visual inspection:** View each hero section (Homepage, About, Services) at full viewport width. Squint or blur your vision — if any text becomes unreadable, contrast is insufficient
3. **Image swap test:** If background images are CMS-managed, upload a test image that is predominantly light-colored (e.g., a bright sky photo). Verify the text still meets contrast requirements
4. **Responsive test:** Test at 1440px, 1024px, 768px, and 375px viewports. At each breakpoint, verify contrast remains sufficient (text reflow may position text over different areas of the image)
5. **Dark mode test:** If the site has a dark mode, verify the hero section contrast is maintained in both modes
6. **Browser DevTools:** Use Chrome DevTools' CSS Overview or the built-in contrast ratio tooltip (hover over color values in the Styles panel) to verify computed contrast ratios
7. **Automated scan:** Run axe DevTools or Lighthouse accessibility audit on each hero section. Verify no color contrast violations are flagged

---

## Developer Notes

### Approach

There are three approaches to fixing hero contrast, listed from most robust to least. The recommended approach is a combination of Options 1 and 2.

### Option 1: Increase Overlay Opacity (Minimum Fix)

The simplest fix — increase the dark overlay opacity to ensure sufficient contrast even over the lightest parts of the image:

```css
/* BEFORE — insufficient overlay */
.hero::before {
  content: "";
  position: absolute;
  inset: 0;
  background-color: rgba(0, 0, 0, 0.35);
  z-index: 1;
}

/* AFTER — increased to ensure 7:1 contrast with white text */
.hero::before {
  content: "";
  position: absolute;
  inset: 0;
  background-color: rgba(0, 0, 0, 0.65);
  z-index: 1;
}

.hero__content {
  position: relative;
  z-index: 2;
}
```

To calculate the required opacity: if the lightest pixel in the background image is `rgb(255, 255, 255)` (pure white), then to achieve 7:1 contrast with `#ffffff` text, the overlay needs to darken it to at most `rgb(89, 89, 89)` — which requires an overlay opacity of approximately **0.65**.

Use a gradient overlay instead of a flat color for a more polished look:

```css
.hero::before {
  content: "";
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.70) 0%,
    rgba(0, 0, 0, 0.55) 50%,
    rgba(0, 0, 0, 0.70) 100%
  );
  z-index: 1;
}
```

### Option 2: Solid Background Behind Text Block (Recommended)

Add a semi-opaque background directly behind the text block. This provides guaranteed contrast regardless of the image:

```html
<section class="hero">
  <img class="hero__bg" src="/images/hero-bg.jpg" alt="" role="presentation" />
  <div class="hero__content">
    <div class="hero__text-block">
      <h1>AI Innovation. Digital Solutions. Results that Matter.</h1>
      <p>We build custom software that transforms how your business operates.</p>
      <a href="/contact/" class="btn btn--hero">Get Started</a>
    </div>
  </div>
</section>
```

```css
.hero {
  position: relative;
  min-height: 80vh;
  display: flex;
  align-items: center;
  overflow: hidden;
}

.hero__bg {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: 0;
}

.hero__content {
  position: relative;
  z-index: 2;
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

.hero__text-block {
  background-color: rgba(10, 10, 30, 0.80);
  padding: 2.5rem 3rem;
  border-radius: 16px;
  max-width: 680px;
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
}

.hero__text-block h1 {
  font-size: 2.5rem;
  font-weight: 800;
  color: #ffffff;
  line-height: 1.2;
  margin-bottom: 1rem;
}

.hero__text-block p {
  font-size: 1.25rem;
  color: rgba(255, 255, 255, 0.92);
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.btn--hero {
  display: inline-block;
  padding: 0.875rem 2rem;
  background-color: #2563eb;
  color: #ffffff;
  font-size: 1rem;
  font-weight: 600;
  border-radius: 8px;
  text-decoration: none;
  transition: background-color 0.2s ease;
}

.btn--hero:hover {
  background-color: #3b82f6;
}

.btn--hero:focus-visible {
  outline: 3px solid #93c5fd;
  outline-offset: 2px;
}

@media (max-width: 768px) {
  .hero__text-block {
    padding: 1.5rem;
    border-radius: 12px;
  }

  .hero__text-block h1 {
    font-size: 1.75rem;
  }
}
```

### Option 3: Text Shadow as Enhancement (Supplemental Only)

Text shadow can enhance readability but should not be the sole contrast solution:

```css
.hero__text-block h1,
.hero__text-block p {
  text-shadow:
    0 1px 3px rgba(0, 0, 0, 0.5),
    0 2px 8px rgba(0, 0, 0, 0.3);
}
```

Text shadow alone does **not** count toward WCAG contrast calculations. Use it as a visual enhancement on top of Options 1 or 2, not as a replacement.

### Background Image Accessibility

Ensure the hero background image is properly marked as decorative:

```html
<!-- If using <img> -->
<img src="/images/hero.jpg" alt="" role="presentation" />

<!-- If using CSS background-image -->
<div class="hero" role="img" aria-label="">
  <!-- empty aria-label marks it as decorative -->
</div>

<!-- Better: use aria-hidden on the image container -->
<div class="hero__bg-wrapper" aria-hidden="true">
  <img src="/images/hero.jpg" alt="" />
</div>
```

### Contrast Verification Script

A quick script to check contrast during development:

```javascript
function getContrastRatio(l1, l2) {
  const lighter = Math.max(l1, l2);
  const darker = Math.min(l1, l2);
  return (lighter + 0.05) / (darker + 0.05);
}

function relativeLuminance(r, g, b) {
  const [rs, gs, bs] = [r, g, b].map(c => {
    c = c / 255;
    return c <= 0.03928 ? c / 12.92 : Math.pow((c + 0.055) / 1.055, 2.4);
  });
  return 0.2126 * rs + 0.7152 * gs + 0.0722 * bs;
}

// White text on darkened background
const textLum = relativeLuminance(255, 255, 255);
const bgLum = relativeLuminance(89, 89, 89); // result of 0.65 opacity black over white
const ratio = getContrastRatio(textLum, bgLum);
console.log(`Contrast ratio: ${ratio.toFixed(2)}:1`);
// Target: >= 7.0 for AAA normal text, >= 4.5 for AAA large text
```

### WCAG References

- **WCAG 2.1 SC 1.4.3 (Contrast - Minimum, AA):** 4.5:1 for normal text, 3:1 for large text
- **WCAG 2.1 SC 1.4.6 (Contrast - Enhanced, AAA):** 7:1 for normal text, 4.5:1 for large text — **this is the target**
- **WCAG 2.1 SC 1.4.11 (Non-text Contrast):** 3:1 for UI components and graphical objects (applies to CTA buttons)

### Components to Audit

- **Hero component** — Update overlay opacity and/or add text block background
- **Homepage hero** — Primary fix target
- **About page hero** — Verify and fix
- **Services page hero** — Verify and fix
- **Any other page with text-over-image** — Case study detail pages, industry pages
- **CMS image upload** — If heroes use CMS-uploaded images, the fix must be image-agnostic (don't rely on a specific image's darkness)
- **CTA button contrast** — Verify button colors meet 4.5:1 against the overlay/background

---

## Examples from Other Sites

### Apple (apple.com)
Product hero sections use solid-color or very dark gradient backgrounds behind text. When images are used, Apple either places text on a solid-colored portion of the image or uses an opaque text container. Text is always maximally readable.

### Stripe (stripe.com)
Hero sections use solid dark backgrounds (not photographs) behind text, ensuring perfect contrast. When images appear, they are beside the text — not behind it.

### Airbnb (airbnb.com)
Hero search areas have a solid white card overlaid on the background image. The text is never directly competing with a photographic background. This guarantees contrast.

### Linear (linear.app)
Uses dark, low-variation background images with high-opacity overlays. The text-over-image treatment achieves near-perfect contrast because the backgrounds are carefully selected and the overlays are strong.

### Microsoft (microsoft.com)
Product pages use a combination approach: dark gradient overlays on the text side of hero images, with the image visible on the opposite side. Text always sits on a guaranteed-dark surface.
