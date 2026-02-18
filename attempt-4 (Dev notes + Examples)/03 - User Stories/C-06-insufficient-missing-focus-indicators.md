# C-06: Insufficient/Missing Visible Focus Indicators

**Priority:** Critical
**WCAG Criteria:** 2.4.7 Focus Visible (AA), 2.4.11 Focus Not Obscured (AA), 1.4.11 Non-text Contrast (AA)
**Affected Personas:** Motor Impairment, ADHD, Low Vision

---

## User Story

**As a** keyboard user or someone navigating without a mouse,
**I want** a clearly visible focus indicator on every interactive element — links, buttons, form inputs, and menu items,
**so that** I can always see which element is currently active and navigate the site confidently.

---

## Acceptance Criteria

- [ ] Every interactive element (links, buttons, inputs, selects, textareas, nav items) has a custom `:focus-visible` style.
- [ ] The focus indicator has at least 3:1 contrast ratio against the background it appears on.
- [ ] Focus indicators are visible on both light and dark background sections (hero, footer, blue sections).
- [ ] The focus ring is at least 2px wide and offset enough to not be obscured by the element's border.
- [ ] The browser's default `outline: none` or `outline: 0` is NOT applied globally without a replacement focus style.
- [ ] Focus indicators are visible for mouse-click users only when using `:focus-visible` (not `:focus`) to avoid unnecessary outlines on mouse clicks.
- [ ] No interactive element is fully obscured by another element when it receives focus.

---

## How to Test the Change

### Manual Testing

1. **Keyboard Walkthrough:**
   - Start at the top of any page and Tab through every interactive element.
   - Verify a visible focus ring appears on each element.
   - Pay special attention to: hero section links, navigation items, footer links, form inputs, CTA buttons.

2. **Contrast Verification:**
   - On the blue hero section, Tab to a link — verify the focus ring is visible against the blue background.
   - In the dark footer, Tab to a link — verify visibility against the dark background.
   - On white content sections, Tab to a link — verify the focus ring contrasts with white.

3. **Focus-visible vs Focus:**
   - Click a button with a mouse — no focus ring should appear (using `:focus-visible`).
   - Tab to the same button — focus ring should appear.

### Automated Testing

```javascript
// Playwright test — verify focus indicators exist
test('all interactive elements have visible focus indicators', async ({ page }) => {
  await page.goto('https://launchpadlab.com');

  const interactiveSelectors = ['a[href]', 'button', 'input', 'textarea', 'select', '[tabindex="0"]'];

  for (const selector of interactiveSelectors) {
    const elements = await page.locator(selector).all();
    for (const el of elements.slice(0, 5)) { // Test first 5 of each type
      await el.focus();
      const outlineStyle = await el.evaluate(element => {
        const styles = window.getComputedStyle(element);
        return {
          outline: styles.outline,
          outlineWidth: styles.outlineWidth,
          boxShadow: styles.boxShadow,
        };
      });
      // Verify some focus indicator exists (outline or box-shadow)
      const hasFocusIndicator =
        outlineStyle.outlineWidth !== '0px' ||
        outlineStyle.boxShadow !== 'none';
      expect(hasFocusIndicator).toBe(true);
    }
  }
});
```

---

## Developer Notes

### General Approach

Create a global `:focus-visible` style that works across all backgrounds. Use a "double ring" technique (dark outline + light offset) or a high-contrast single ring that adapts to different sections. Remove any `outline: none` or `outline: 0` resets that aren't paired with a replacement.

### Code Examples

**Global focus style (double-ring technique):**

```css
/* Remove any existing outline suppression */
/* DELETE these if they exist in the codebase: */
/* *:focus { outline: none; } */
/* a:focus { outline: 0; } */

/* Global focus-visible style — works on any background */
:focus-visible {
  outline: 3px solid #1a73e8;        /* Blue ring */
  outline-offset: 2px;
  box-shadow: 0 0 0 6px rgba(255, 255, 255, 0.8); /* White outer halo */
}

/* High-contrast alternative for dark sections */
.hero :focus-visible,
.site-footer :focus-visible,
.bg-dark :focus-visible {
  outline-color: #f5a623;            /* Gold ring on dark backgrounds */
  box-shadow: 0 0 0 6px rgba(0, 0, 0, 0.5);
}
```

**Form input focus:**

```css
input:focus-visible,
textarea:focus-visible,
select:focus-visible {
  outline: 3px solid #1a73e8;
  outline-offset: 0;
  border-color: #1a73e8;
  box-shadow: 0 0 0 3px rgba(26, 115, 232, 0.3);
}
```

**Button focus:**

```css
.btn:focus-visible,
button:focus-visible {
  outline: 3px solid #1a73e8;
  outline-offset: 3px;
}
```

**Search and remove global outline suppression:**

```css
/* FIND AND REMOVE any of these patterns: */
*:focus { outline: none; }
a:focus { outline: 0; }
button:focus { outline: none; }
input:focus { outline: none; }
```

### Components/Files to Audit

- Global stylesheet / reset CSS — search for `outline: none`, `outline: 0`.
- Any CSS framework reset (e.g., normalize.css, reset.css).
- `_buttons.scss`, `_forms.scss`, `_links.scss` — component-level focus overrides.
- Navigation CSS — ensure mega menu items have focus styles.
- Hero section CSS — focus styles on CTAs over images.
- Footer CSS — focus styles on links against dark background.

---

## Examples from Other Sites

| Site | Implementation |
|------|----------------|
| **gov.uk** | Bold 3px yellow (#ffdd00) focus ring with a 3px dark underline — visible on all backgrounds. |
| **GitHub** | Blue focus ring (`box-shadow: 0 0 0 3px rgba(3, 102, 214, 0.3)`) on all interactive elements. |
| **Google** | Blue focus ring with white offset on dark surfaces. Uses `:focus-visible` to suppress rings on mouse clicks. |
| **BBC** | High-contrast focus ring that adapts color based on section background. |
