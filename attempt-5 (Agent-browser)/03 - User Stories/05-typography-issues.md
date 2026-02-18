# Typography Issues (Text Size, Spacing, All-Caps, Serif Fonts)

**Priority:** High
**Location:** All pages — body text, section labels, hero headings, navigation
**WCAG:** [1.4.8 Visual Presentation (AAA)](https://www.w3.org/WAI/WCAG21/Understanding/visual-presentation), [1.4.12 Text Spacing (AA)](https://www.w3.org/WAI/WCAG21/Understanding/text-spacing), [1.4.4 Resize Text (AA)](https://www.w3.org/WAI/WCAG21/Understanding/resize-text)

---

## User Story

> As a **user with a visual impairment, dyslexia, or reading difficulty**,
> I want **body text to be large enough, well-spaced, and set in a readable typeface without all-caps or italic headings**
> so that **I can read the content comfortably without straining or losing my place.**

---

## Problem

Multiple typography issues compound to reduce readability across the site:

| Issue | Current State | Impact |
|---|---|---|
| **Body text size** | ~16px | Below the recommended 18px minimum for accessibility |
| **Line height** | Standard (~1.5) | Too tight for users with dyslexia or low vision |
| **Section labels** | ALL-CAPS | Harder to read — removes word shape recognition cues |
| **Hero headings** | Serif and/or italic fonts | Serif/italic is harder to read on screens, especially at large sizes on varied backgrounds |
| **Navigation** | All-caps with tight letter-spacing | Reduces legibility and scannability |
| **Letter spacing** | Default or tight | Insufficient for readability, especially in all-caps |

---

## Acceptance Criteria

- [ ] Body text is at least `18px` (`1.125rem`) on all viewports.
- [ ] Line height for body text is at least `1.8`.
- [ ] Letter spacing for body text is at least `0.02em`.
- [ ] Word spacing is at least `0.05em`.
- [ ] No text is set in `text-transform: uppercase` — all labels and headings use sentence case or title case.
- [ ] All headings use a sans-serif font family (e.g., Inter, Helvetica Neue, system-ui).
- [ ] No headings use `font-style: italic` as a design default.
- [ ] Navigation links use sentence case with adequate letter-spacing (`0.05em+`).
- [ ] Text remains readable and does not overflow when user applies custom text spacing via browser settings or assistive tools (WCAG 1.4.12 compliance).
- [ ] All text sizes use relative units (`rem` or `em`), not `px`, so they scale with user font-size preferences.

---

## How to Test

1. **Font size audit:** Inspect body text elements in DevTools. Verify computed font-size is ≥ 18px.
2. **Line height check:** Inspect `line-height` on `<p>`, `<li>`, and other body text. Should be ≥ 1.8.
3. **All-caps search:** Search CSS for `text-transform: uppercase`. Flag and replace every instance.
4. **Font family check:** Inspect headings for serif fonts (`Georgia`, `Times New Roman`, `Playfair Display`, etc.) or italic styling.
5. **WCAG 1.4.12 text spacing override test:**
   - Apply these styles via DevTools or a bookmarklet and verify no content is cut off or overlaps:

   ```css
   * {
     line-height: 1.5 !important;
     letter-spacing: 0.12em !important;
     word-spacing: 0.16em !important;
   }
   p {
     margin-bottom: 2em !important;
   }
   ```

6. **Zoom test:** Zoom the browser to 200 %. Verify all text remains readable, no horizontal scrollbar appears, and no text is clipped.
7. **Screen reader test:** Verify that text-transform: uppercase (if any remains) does not cause screen readers to spell out words letter-by-letter (some screen readers interpret all-caps as acronyms).

---

## Developer Notes

### Global typography reset

Apply these base styles site-wide:

```css
:root {
  --font-body: 'Inter', 'Helvetica Neue', system-ui, -apple-system, sans-serif;
  --font-heading: 'Inter', 'Helvetica Neue', system-ui, -apple-system, sans-serif;

  --text-base: 1.125rem;      /* 18px */
  --text-lg: 1.25rem;         /* 20px */
  --text-xl: 1.5rem;          /* 24px */
  --text-2xl: 2rem;           /* 32px */
  --text-3xl: 2.5rem;         /* 40px */
  --text-4xl: 3rem;           /* 48px */

  --line-height-body: 1.8;
  --line-height-heading: 1.3;

  --letter-spacing-body: 0.02em;
  --letter-spacing-heading: -0.01em;
  --letter-spacing-nav: 0.05em;

  --word-spacing-body: 0.05em;
}

body {
  font-family: var(--font-body);
  font-size: var(--text-base);
  line-height: var(--line-height-body);
  letter-spacing: var(--letter-spacing-body);
  word-spacing: var(--word-spacing-body);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

### Heading styles (sans-serif, no italic, sentence case)

```css
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-heading);
  font-weight: 700;
  font-style: normal;                  /* Never italic */
  text-transform: none;                /* Never uppercase */
  line-height: var(--line-height-heading);
  letter-spacing: var(--letter-spacing-heading);
}

h1 { font-size: var(--text-4xl); }
h2 { font-size: var(--text-2xl); }
h3 { font-size: var(--text-xl); }
h4 { font-size: var(--text-lg); }
```

### Section labels — replace all-caps with sentence case

```css
/* BEFORE — problematic */
.section-label {
  text-transform: uppercase;
  font-size: 0.75rem;
  letter-spacing: 0.1em;
}

/* AFTER — accessible */
.section-label {
  text-transform: none;
  font-size: 0.9375rem;       /* 15px — readable, not tiny */
  font-weight: 600;
  letter-spacing: 0.05em;
  color: var(--color-text-secondary);
}
```

### Navigation — sentence case, better spacing

```css
/* BEFORE — problematic */
.nav-link {
  text-transform: uppercase;
  font-size: 0.8125rem;
  letter-spacing: 0.08em;
}

/* AFTER — accessible */
.nav-link {
  text-transform: none;
  font-size: 1rem;
  font-weight: 500;
  letter-spacing: var(--letter-spacing-nav);
  padding: 0.5rem 1rem;
}
```

### Hero headings — sans-serif, no italic

```css
/* BEFORE — problematic */
.hero h1 {
  font-family: 'Playfair Display', serif;
  font-style: italic;
  font-size: 3.5rem;
}

/* AFTER — accessible */
.hero h1 {
  font-family: var(--font-heading);
  font-style: normal;
  font-weight: 700;
  font-size: clamp(2rem, 5vw, 3.5rem);  /* Fluid, responsive */
  line-height: 1.2;
}
```

### Responsive type scale

```css
@media (max-width: 768px) {
  :root {
    --text-base: 1rem;        /* 16px minimum on small screens */
    --text-4xl: 2rem;
    --text-2xl: 1.5rem;
  }
}
```

### Ensuring WCAG 1.4.12 compliance (Text Spacing)

Content must not be clipped or overlap when users override spacing. Avoid:
- Fixed-height containers with `overflow: hidden` on text
- Relying on exact text wrapping for layout

```css
/* Avoid this */
.card__title {
  height: 48px;
  overflow: hidden;
}

/* Do this instead */
.card__title {
  min-height: 48px;
  overflow: visible;
}
```

### Components to audit

| Component | Page(s) | Issues |
|---|---|---|
| Body paragraphs | All | Font size 16px → 18px, line-height → 1.8 |
| Section labels ("OUR SERVICES", "OUR PROCESS") | All | Remove `text-transform: uppercase`, increase size |
| Hero headlines | Homepage, Services, About | Replace serif/italic with sans-serif normal |
| Navigation links | All (header) | Remove all-caps, increase size and spacing |
| Footer text | All | Increase size and line-height |
| Card titles | /work/ | Check for fixed-height clipping |
| Button text | All | Remove all-caps if present |
| Breadcrumbs / meta text | Case study pages | Increase size from small/grey to readable |

---

## Examples from Other Sites

### Apple (apple.com)
- Uses San Francisco (system sans-serif) throughout.
- Body text is 17–21px with generous line-height.
- Headings are bold sans-serif, never italic.
- No all-caps except very short labels.

### GOV.UK (gov.uk)
- Body text: 19px on desktop.
- Line-height: 1.625 (they aim higher than most).
- All text in sentence case. Zero all-caps.
- Font: GDS Transport (custom sans-serif).
- Style guide: "Do not use bold, italics, or CAPITALS for emphasis."

### Medium (medium.com)
- Reading-optimized typography: 21px body text, 1.8 line-height.
- Sans-serif for UI, serif only for long-form article body (by choice, not default).
- No all-caps except very small UI labels.

### BBC (bbc.com)
- Uses BBC Reith (custom sans-serif) at 15–18px body.
- Generous line-height and letter-spacing.
- All navigation in sentence case.
