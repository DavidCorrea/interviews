# L-57: No Site-Level Accessibility Preferences

**Issue ID:** L-57
**Priority:** Low
**WCAG Criteria:** 1.4.8 Visual Presentation (AAA)
**Affected Personas:** ADHD, Motion Sensitivity

---

## User Story

As a **user with motion sensitivity**, I want the site to offer accessibility preference toggles (such as reduced motion, dark mode, or increased text size) so that I can customize my browsing experience without relying solely on OS-level settings that may not be respected by the site.

---

## Acceptance Criteria

- [ ] A visible accessibility preferences panel or widget is accessible from a persistent location (e.g., site header, footer, or a floating button).
- [ ] The panel includes, at minimum, toggles for:
  - **Reduced motion** — disables all CSS animations and JS-driven motion
  - **Increased text size** — scales body text to a larger base size
  - **High contrast** — increases contrast ratios for text and UI elements
- [ ] User preferences are persisted across page loads (via `localStorage` or cookie).
- [ ] Preferences survive browser sessions (persist beyond tab close).
- [ ] Toggling reduced motion immediately halts all CSS transitions, keyframe animations, and JS-driven motion on the page.
- [ ] The preferences panel itself is fully keyboard accessible and screen reader compatible.
- [ ] The button/trigger to open the preferences panel has a visible label and `aria-label`.

---

## How to Test the Change

### Manual Testing
1. Navigate to launchpadlab.com.
2. Locate the accessibility preferences button/widget (should be visible in the header or as a floating icon).
3. Open the panel and verify all toggles are present and labeled.
4. Toggle **Reduced Motion**:
   - Scroll through the page and confirm AOS animations are disabled.
   - Confirm carousels stop auto-scrolling.
   - Confirm counter animations display final values instantly.
5. Toggle **Increased Text Size**:
   - Confirm body text size increases visibly.
   - Confirm the layout reflows without horizontal scrolling.
6. Toggle **High Contrast**:
   - Confirm text contrast improves (test with a contrast checker tool).
7. Reload the page — confirm preferences persist.
8. Close and reopen the browser — confirm preferences still persist.
9. Test the preferences panel with keyboard only (Tab, Enter, Space, Escape).
10. Test with VoiceOver/NVDA to verify the panel is announced correctly.

### Automated Testing
1. Write integration tests for preference persistence:
   ```javascript
   // Set preference
   localStorage.setItem('a11y-reduced-motion', 'true');
   // Reload
   await page.reload();
   // Verify class is applied
   expect(document.documentElement.classList.contains('reduced-motion')).toBe(true);
   ```
2. Test animation state:
   ```javascript
   // With reduced motion enabled
   const computedStyle = getComputedStyle(document.querySelector('[data-aos]'));
   expect(computedStyle.animation).toBe('none');
   expect(computedStyle.transition).toBe('none 0s ease 0s');
   ```

---

## Developer Notes

### General Explanation
While OS-level `prefers-reduced-motion` and `prefers-color-scheme` media queries are the primary mechanism, not all users know how to configure these settings. Providing site-level controls gives users direct, discoverable control over their experience.

This feature should be implemented as a lightweight preferences panel that applies CSS classes to `<html>` and saves settings to `localStorage`.

### Implementation Approach

**1. Preferences toggle button (always visible):**
```html
<button id="a11y-preferences-toggle"
        aria-label="Accessibility preferences"
        aria-expanded="false"
        aria-controls="a11y-preferences-panel">
  <svg aria-hidden="true"><!-- accessibility icon --></svg>
  <span class="sr-only">Accessibility preferences</span>
</button>
```

**2. Preferences panel:**
```html
<div id="a11y-preferences-panel" role="dialog" aria-label="Accessibility preferences" hidden>
  <h2>Accessibility Preferences</h2>

  <label>
    <input type="checkbox" id="a11y-reduce-motion" />
    Reduce motion
  </label>

  <label>
    <input type="checkbox" id="a11y-increase-text" />
    Increase text size
  </label>

  <label>
    <input type="checkbox" id="a11y-high-contrast" />
    High contrast
  </label>

  <button id="a11y-preferences-close">Close</button>
</div>
```

**3. JavaScript handler:**
```javascript
const PREFS = ['reduce-motion', 'increase-text', 'high-contrast'];

function loadPreferences() {
  PREFS.forEach(pref => {
    const value = localStorage.getItem(`a11y-${pref}`) === 'true';
    document.documentElement.classList.toggle(pref, value);
    const checkbox = document.getElementById(`a11y-${pref}`);
    if (checkbox) checkbox.checked = value;
  });
}

function savePreference(pref, value) {
  localStorage.setItem(`a11y-${pref}`, value);
  document.documentElement.classList.toggle(pref, value);
}

// Initialize on page load
loadPreferences();

PREFS.forEach(pref => {
  const checkbox = document.getElementById(`a11y-${pref}`);
  checkbox?.addEventListener('change', (e) => {
    savePreference(pref, e.target.checked);
  });
});
```

**4. CSS rules:**
```css
/* Reduced motion */
html.reduce-motion *,
html.reduce-motion *::before,
html.reduce-motion *::after {
  animation-duration: 0.01ms !important;
  animation-iteration-count: 1 !important;
  transition-duration: 0.01ms !important;
  scroll-behavior: auto !important;
}

/* Increased text size */
html.increase-text {
  font-size: 125%; /* 20px if base is 16px */
}

/* High contrast */
html.high-contrast {
  --text-color: #000000;
  --bg-color: #FFFFFF;
  --link-color: #0000EE;
}
html.high-contrast body { color: var(--text-color); background: var(--bg-color); }
html.high-contrast a { color: var(--link-color); text-decoration: underline; }
```

### Components/Files to Audit
- Site header template (for button placement)
- Main JavaScript bundle (for preference logic)
- Global CSS (for preference-driven overrides)
- AOS initialization (should check for `reduce-motion` class)
- Carousel/slider initialization (should check for reduced motion)

---

## Examples from Other Sites

- **BBC:** Provides an "Accessibility Help" page and honors `prefers-reduced-motion` universally. Their iPlayer has built-in accessibility controls.
- **GOV.UK:** While relying primarily on OS settings, they ensure all animations respect `prefers-reduced-motion` and provide high-contrast compatibility.
- **Inclusive Design Principles (inclusivedesignprinciples.org):** Offers a dark mode toggle and font size controls directly on the site.
- **A11Y Project:** Includes a prominent dark mode toggle in the header, demonstrating the pattern of user-facing accessibility controls.

---

## Additional Context

This is an enhancement rather than a bug fix. It's classified as Low priority because OS-level settings provide the primary mechanism. However, implementing site-level controls demonstrates a commitment to accessibility and provides a better experience for users who are unaware of OS settings or whose OS settings are not respected by the current site code (see issues C-09, H-23, H-24, H-25, H-26).
