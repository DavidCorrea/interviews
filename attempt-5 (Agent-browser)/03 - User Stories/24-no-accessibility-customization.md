# No Accessibility Customization Options

**Priority:** Low
**Location:** Sitewide
**WCAG:** [1.4.4 Resize Text (AA)](https://www.w3.org/WAI/WCAG21/Understanding/resize-text), [1.4.8 Visual Presentation (AAA)](https://www.w3.org/WAI/WCAG21/Understanding/visual-presentation), [1.4.12 Text Spacing (AA)](https://www.w3.org/WAI/WCAG21/Understanding/text-spacing)

---

## User Story

> As a **user with low vision, dyslexia, or a cognitive disability**,
> I want **on-page controls to adjust text size, line spacing, contrast, and font style**
> so that **I can customize the reading experience to match my needs without relying on browser settings or extensions I may not know about.**

---

## Problem

The LaunchPad Lab website provides no user-facing accessibility controls. Users who need adjusted text sizes, higher contrast, increased line spacing, or a dyslexia-friendly font must:

- Know how to use browser zoom (many users don't).
- Install browser extensions (which may not be available on all devices).
- Modify system accessibility settings (which affect everything, not just this site).

While browsers and operating systems do offer some of these controls, providing site-level customization demonstrates commitment to inclusion and serves users who:

- Are visiting on a shared/public computer with no extensions.
- Are on mobile devices where browser accessibility options are limited.
- Have temporary impairments (eye strain, migraine, bright sunlight).
- Simply prefer a more comfortable reading experience.

---

## Acceptance Criteria

- [ ] An accessibility settings panel/widget is available from every page via a persistent button in the header or floating position.
- [ ] The toggle button has an accessible label (e.g., "Accessibility settings") and uses a recognizable icon (♿ or similar).
- [ ] The panel includes controls for:
  - Text size (increase / decrease / reset)
  - Line height adjustment
  - Letter spacing adjustment
  - High contrast mode
  - Dyslexia-friendly font toggle
- [ ] All controls are keyboard accessible and screen reader–friendly.
- [ ] User preferences persist across page loads (via `localStorage`).
- [ ] The panel can be dismissed with `Escape` and focus returns to the trigger button.
- [ ] No customization breaks the page layout or causes horizontal scrolling.
- [ ] The site still functions normally when all customization options are at their defaults.

---

## How to Test

1. **Widget presence:** Visit every major page. Confirm the accessibility widget button is visible and reachable.
2. **Keyboard test:** `Tab` to the widget button, press `Enter` to open, navigate options with arrow keys or `Tab`, press `Escape` to close. Verify focus management is correct.
3. **Text size test:** Increase text size to maximum. Verify text reflows without horizontal scrolling and no content is clipped.
4. **Contrast test:** Enable high contrast mode. Verify all text meets a minimum 7:1 contrast ratio (AAA) and interactive elements are clearly distinguishable.
5. **Dyslexia font test:** Toggle dyslexia-friendly font. Confirm it applies to body text throughout the page without breaking layout.
6. **Persistence test:** Adjust settings, navigate to another page, and refresh. Confirm settings are preserved.
7. **Screen reader test:** Open the panel with VoiceOver/NVDA. Confirm each control announces its current state (e.g., "Text size: 120%", "High contrast: off").
8. **Reset test:** Click "Reset to defaults". Confirm all settings return to their original values.

---

## Developer Notes

### Strategy

Build a lightweight accessibility preferences panel that modifies CSS custom properties on the `<html>` element. This avoids duplicating stylesheets and leverages the cascade. Store preferences in `localStorage`.

Alternatively, integrate a third-party widget like [UserWay](https://userway.org/) or [AccessiBe](https://accessibe.com/) — though a custom solution offers more control and avoids third-party cookie/privacy concerns.

### Recommended markup

```html
<!-- Trigger button (in header or fixed position) -->
<button
  type="button"
  class="a11y-toggle"
  aria-expanded="false"
  aria-controls="a11y-panel"
  aria-label="Accessibility settings"
>
  <svg aria-hidden="true" width="24" height="24" viewBox="0 0 24 24">
    <path d="M12 2a2 2 0 1 1 0 4 2 2 0 0 1 0-4zm9 7h-6l-1.41
             6.59L16 22h-2l-2-6-2 6H8l2.41-6.41L9 9H3V7h18v2z" />
  </svg>
</button>

<!-- Accessibility panel -->
<div
  id="a11y-panel"
  class="a11y-panel"
  role="dialog"
  aria-labelledby="a11y-panel-title"
  aria-modal="true"
  hidden
>
  <h2 id="a11y-panel-title">Accessibility Settings</h2>

  <div class="a11y-control">
    <label for="text-size">Text Size</label>
    <div class="a11y-range-group">
      <button aria-label="Decrease text size" data-action="decrease" data-target="text-size">−</button>
      <output id="text-size-output">100%</output>
      <button aria-label="Increase text size" data-action="increase" data-target="text-size">+</button>
    </div>
  </div>

  <div class="a11y-control">
    <label for="line-height">Line Height</label>
    <div class="a11y-range-group">
      <button aria-label="Decrease line height" data-action="decrease" data-target="line-height">−</button>
      <output id="line-height-output">1.6</output>
      <button aria-label="Increase line height" data-action="increase" data-target="line-height">+</button>
    </div>
  </div>

  <div class="a11y-control">
    <label for="letter-spacing">Letter Spacing</label>
    <div class="a11y-range-group">
      <button aria-label="Decrease letter spacing" data-action="decrease" data-target="letter-spacing">−</button>
      <output id="letter-spacing-output">Normal</output>
      <button aria-label="Increase letter spacing" data-action="increase" data-target="letter-spacing">+</button>
    </div>
  </div>

  <div class="a11y-control">
    <label>
      <input type="checkbox" id="high-contrast" />
      High Contrast
    </label>
  </div>

  <div class="a11y-control">
    <label>
      <input type="checkbox" id="dyslexia-font" />
      Dyslexia-Friendly Font
    </label>
  </div>

  <button type="button" class="a11y-reset" aria-label="Reset all accessibility settings to defaults">
    Reset to Defaults
  </button>
</div>
```

### CSS — custom properties approach

```css
/* Default values on :root */
:root {
  --a11y-font-size: 1rem;
  --a11y-line-height: 1.6;
  --a11y-letter-spacing: normal;
  --a11y-font-family: "Inter", system-ui, sans-serif;
  --a11y-bg: #ffffff;
  --a11y-text: #1a1a1a;
  --a11y-link: #1a73e8;
}

body {
  font-size: var(--a11y-font-size);
  line-height: var(--a11y-line-height);
  letter-spacing: var(--a11y-letter-spacing);
  font-family: var(--a11y-font-family);
  background-color: var(--a11y-bg);
  color: var(--a11y-text);
}

a {
  color: var(--a11y-link);
}

/* High contrast mode */
html.high-contrast {
  --a11y-bg: #000000;
  --a11y-text: #ffffff;
  --a11y-link: #ffdd57;
}

html.high-contrast img {
  filter: contrast(1.2);
}

html.high-contrast button,
html.high-contrast a {
  outline: 2px solid #ffdd57;
}

/* Dyslexia-friendly font */
html.dyslexia-font {
  --a11y-font-family: "OpenDyslexic", "Comic Sans MS", sans-serif;
  --a11y-letter-spacing: 0.05em;
  --a11y-line-height: 1.8;
}

/* Accessibility panel styles */
.a11y-toggle {
  position: fixed;
  bottom: 1.5rem;
  right: 1.5rem;
  z-index: 9999;
  width: 48px;
  height: 48px;
  border-radius: 50%;
  background: #1a73e8;
  color: #fff;
  border: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
  transition: background 0.2s ease;
}

.a11y-toggle:hover,
.a11y-toggle:focus-visible {
  background: #1558b0;
}

.a11y-toggle:focus-visible {
  outline: 3px solid #ffdd57;
  outline-offset: 3px;
}

.a11y-panel {
  position: fixed;
  bottom: 5rem;
  right: 1.5rem;
  z-index: 9999;
  width: 320px;
  max-height: 80vh;
  overflow-y: auto;
  background: #fff;
  border: 2px solid #333;
  border-radius: 12px;
  padding: 1.5rem;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
}

.a11y-control {
  margin-bottom: 1.25rem;
}

.a11y-control label {
  display: block;
  font-weight: 600;
  margin-bottom: 0.5rem;
  font-size: 0.95rem;
}

.a11y-range-group {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.a11y-range-group button {
  width: 36px;
  height: 36px;
  border: 2px solid #333;
  border-radius: 6px;
  background: #f5f5f5;
  font-size: 1.25rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
}

.a11y-range-group button:focus-visible {
  outline: 3px solid #1a73e8;
  outline-offset: 2px;
}

.a11y-reset {
  width: 100%;
  padding: 0.75rem;
  margin-top: 1rem;
  border: 2px solid #333;
  border-radius: 6px;
  background: #f5f5f5;
  font-weight: 600;
  cursor: pointer;
}
```

### JavaScript — preference management

```js
class A11yPreferences {
  #defaults = {
    fontSize: 100,
    lineHeight: 1.6,
    letterSpacing: 0,
    highContrast: false,
    dyslexiaFont: false,
  };

  constructor() {
    this.prefs = this.#load();
    this.#apply();
    this.#bindEvents();
  }

  #load() {
    try {
      const saved = localStorage.getItem('a11y-prefs');
      return saved ? { ...this.#defaults, ...JSON.parse(saved) } : { ...this.#defaults };
    } catch {
      return { ...this.#defaults };
    }
  }

  #save() {
    localStorage.setItem('a11y-prefs', JSON.stringify(this.prefs));
  }

  #apply() {
    const root = document.documentElement;
    root.style.setProperty('--a11y-font-size', `${this.prefs.fontSize}%`);
    root.style.setProperty('--a11y-line-height', this.prefs.lineHeight);
    root.style.setProperty('--a11y-letter-spacing', `${this.prefs.letterSpacing}em`);
    root.classList.toggle('high-contrast', this.prefs.highContrast);
    root.classList.toggle('dyslexia-font', this.prefs.dyslexiaFont);
    this.#updateOutputs();
  }

  #updateOutputs() {
    const sizeOut = document.getElementById('text-size-output');
    const lhOut = document.getElementById('line-height-output');
    const lsOut = document.getElementById('letter-spacing-output');
    if (sizeOut) sizeOut.textContent = `${this.prefs.fontSize}%`;
    if (lhOut) lhOut.textContent = this.prefs.lineHeight.toFixed(1);
    if (lsOut) lsOut.textContent = this.prefs.letterSpacing === 0
      ? 'Normal' : `${this.prefs.letterSpacing}em`;
  }

  adjustFontSize(delta) {
    this.prefs.fontSize = Math.min(200, Math.max(75, this.prefs.fontSize + delta));
    this.#apply();
    this.#save();
  }

  adjustLineHeight(delta) {
    this.prefs.lineHeight = Math.min(3, Math.max(1, this.prefs.lineHeight + delta));
    this.#apply();
    this.#save();
  }

  adjustLetterSpacing(delta) {
    this.prefs.letterSpacing = Math.min(0.2, Math.max(0, this.prefs.letterSpacing + delta));
    this.#apply();
    this.#save();
  }

  toggleHighContrast() {
    this.prefs.highContrast = !this.prefs.highContrast;
    this.#apply();
    this.#save();
  }

  toggleDyslexiaFont() {
    this.prefs.dyslexiaFont = !this.prefs.dyslexiaFont;
    this.#apply();
    this.#save();
  }

  reset() {
    this.prefs = { ...this.#defaults };
    this.#apply();
    this.#save();
  }

  #bindEvents() {
    const toggle = document.querySelector('.a11y-toggle');
    const panel = document.getElementById('a11y-panel');

    toggle?.addEventListener('click', () => {
      const expanded = toggle.getAttribute('aria-expanded') === 'true';
      toggle.setAttribute('aria-expanded', !expanded);
      panel.hidden = expanded;
      if (!expanded) panel.querySelector('button, input')?.focus();
    });

    document.addEventListener('keydown', (e) => {
      if (e.key === 'Escape' && !panel.hidden) {
        panel.hidden = true;
        toggle.setAttribute('aria-expanded', 'false');
        toggle.focus();
      }
    });
  }
}

document.addEventListener('DOMContentLoaded', () => new A11yPreferences());
```

### Components to audit

| Component / Section | Page(s) | What to fix |
|---|---|---|
| Site header or footer | All pages | Add accessibility widget trigger button |
| Global layout / `<body>` styles | All pages | Use CSS custom properties for themeable values |
| Color palette / design tokens | All pages | Define high-contrast alternatives |
| Font stack | All pages | Include OpenDyslexic as optional font-face |

---

## Examples from Other Sites

### BBC (bbc.co.uk)
- Dedicated accessibility settings page at bbc.co.uk/accessibility.
- Provides guides for adjusting text size, contrast, and using screen readers.
- Content pages use high contrast and large text that adapts to user preferences.

### NNGroup (nngroup.com)
- Offers an accessibility toolbar with font size controls.
- Clean, high-contrast design that works well at any text size.
- Demonstrates that a research/consulting firm can lead by example.

### UserWay Widget (userway.org)
- Third-party accessibility overlay that provides text size, contrast, dyslexia font, cursor size, and line-height controls.
- Easy to integrate (single script tag), though a custom solution offers better privacy and performance.
- Demonstrates the expected feature set for an accessibility panel.
