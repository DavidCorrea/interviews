# H-11: Links Visually Indistinguishable from Body Text

**Issue ID:** H-11
**Priority:** High
**WCAG Criteria:** 1.4.1 Use of Color (A)
**Affected Personas:** Low Contrast Sensitivity, Low Vision, Red-Green Color Blind, Situational Contrast

---

## User Story

**As a** color-blind or low-vision user reading body content,
**I want** inline links to be visually distinguishable from surrounding text by more than color alone,
**so that** I can identify clickable elements without relying on color perception or hovering with a mouse.

---

## Acceptance Criteria

- [ ] All inline `<a>` elements within body content have a visible underline (or equivalent non-color indicator such as a bottom border or dotted underline) in their default (non-hover, non-focus) state.
- [ ] The link text color has at least a 3:1 contrast ratio against surrounding body text, **or** a non-color differentiator (underline) is present.
- [ ] The underline/indicator remains visible in Windows High Contrast Mode and when the page is viewed in grayscale.
- [ ] Hover and focus states provide an additional visual change (e.g., color shift, underline removal/thickening, background highlight) to reinforce interactivity.
- [ ] The link styling is applied globally and consistently — no inline links anywhere on the site appear identical to body text.
- [ ] Links are identifiable without mouse interaction (no hover-only indicators).

---

## How to Test the Change

### Manual Testing

1. **Visual scan:** Open any page with body content containing inline links (e.g., About, Services, Blog posts). Without hovering, confirm that every link is visually distinct from surrounding paragraph text.
2. **Grayscale test:** Enable grayscale mode (macOS: Accessibility → Display → Color Filters → Grayscale; Windows: Color Filters → Grayscale). Confirm links remain identifiable.
3. **Color blindness simulation:** Use Chrome DevTools → Rendering → "Emulate vision deficiencies" → test Protanopia, Deuteranopia, and Tritanopia. Confirm links are distinguishable in each mode.
4. **Keyboard-only navigation:** Tab through the page. Confirm focus lands on inline links and a visible focus indicator appears.
5. **High Contrast Mode (Windows):** Enable High Contrast and confirm links are styled distinctly (typically underlined and colored by the system).
6. **Mobile/touch test:** On a mobile device, confirm links are identifiable before tapping (no hover state available).

### Automated Testing

- Run `axe-core` or Lighthouse. Check for "Links must be distinguishable without relying on color" findings.
- Custom CSS audit script:

```javascript
// Check that inline links have underline or distinct visual treatment
document.querySelectorAll('p a, li a, .entry-content a').forEach(link => {
  const styles = getComputedStyle(link);
  const hasUnderline = styles.textDecorationLine.includes('underline');
  const hasBorder = parseFloat(styles.borderBottomWidth) > 0;
  if (!hasUnderline && !hasBorder) {
    console.warn('Link missing visual indicator:', link.href, link.textContent);
  }
});
```

---

## Developer Notes

### General Approach

Add a visible underline to all inline links in their default state. This is the most universally understood link convention and meets WCAG 1.4.1 without requiring any color perception.

### Current State (Problem)

```css
/* Links are styled identically to body text */
a {
  color: #555555;           /* Same as body text */
  text-decoration: none;    /* No underline */
}

a:hover {
  color: #0066CC;           /* Only visible on mouse hover */
}
```

A user who cannot perceive the hover color change — or who is on a touch device — sees no difference between links and body text.

### Recommended Fix

```css
/* Base link styles — always visually distinct */
.entry-content a,
.page-content a,
p a,
li a {
  color: #0066CC;                          /* Distinct from #555555 body text */
  text-decoration: underline;              /* Primary non-color indicator */
  text-underline-offset: 3px;              /* Improve readability */
  text-decoration-thickness: 1.5px;        /* Visible but not heavy */
}

/* Hover: reinforce interactivity */
.entry-content a:hover,
p a:hover,
li a:hover {
  color: #004499;
  text-decoration-thickness: 2.5px;        /* Thicker underline on hover */
}

/* Focus: clear keyboard indicator */
.entry-content a:focus-visible,
p a:focus-visible,
li a:focus-visible {
  outline: 3px solid #0066CC;
  outline-offset: 2px;
  border-radius: 2px;
}

/* High Contrast Mode */
@media (forced-colors: active) {
  .entry-content a,
  p a,
  li a {
    text-decoration: underline;
    forced-color-adjust: auto;
  }
}
```

### Alternative Approach: Dotted Underline

If the design team prefers a subtler look, use a dotted bottom border instead of a full underline:

```css
.entry-content a {
  color: #0066CC;
  text-decoration: none;
  border-bottom: 2px dotted #0066CC;
  padding-bottom: 1px;
}
```

### Components / Files to Audit

- Global stylesheet (e.g., `style.css`, `_typography.scss`, `_links.scss`)
- Any component-level styles that override link `text-decoration` (service pages, blog templates)
- WordPress theme `a` reset styles
- CMS-rendered content blocks (Gutenberg, ACF WYSIWYG fields)

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **GOV.UK** | All body links are underlined by default with a distinct blue color | The UK Government Design System treats underline as mandatory for inline links — the gold standard for link visibility. |
| **Wikipedia** | Links are blue and underlined in all states | Universally recognizable; no color perception needed. |
| **MDN Web Docs** | Links are colored and underlined; hover adds a background highlight | Two independent cues ensure links are always identifiable. |
| **The New York Times** | Inline links use underline; hover changes the underline opacity | Subtle but effective — underline is always present in default state. |
