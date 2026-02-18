# H-21: Tab Active State Relies on Color Alone

**Issue ID:** H-21
**Priority:** High
**WCAG Criteria:** 1.4.1 Use of Color (A)
**Affected Personas:** Blue-Yellow Color Blind, Red-Green Color Blind, Situational Contrast

---

## User Story

**As a** color-blind user navigating the "Problems We Solve" section,
**I want** the active tab to be visually distinguished by more than just a color change,
**so that** I can clearly identify which tab is currently selected without relying on color perception.

---

## Acceptance Criteria

- [ ] The active tab has at least one non-color visual indicator in addition to the color change (e.g., underline/bottom border, bold font weight, background fill, or an icon).
- [ ] The active tab's non-color indicator meets a 3:1 contrast ratio against its surrounding area.
- [ ] The inactive tabs are visually distinct from the active tab even when viewed in grayscale.
- [ ] The active tab has `aria-selected="true"` and inactive tabs have `aria-selected="false"`.
- [ ] The tab's selected state is perceivable in Windows High Contrast Mode.

---

## How to Test the Change

### Manual Testing

1. **Grayscale test:** Enable grayscale mode on your OS (macOS: Accessibility → Display → Color Filters → Grayscale; Windows: Color Filters → Grayscale). Navigate to the "Problems We Solve" section and confirm you can identify the active tab.
2. **Color blindness simulation:** Use the Chrome DevTools Rendering panel → "Emulate vision deficiencies" → test Protanopia, Deuteranopia, and Tritanopia. Confirm the active tab remains distinguishable.
3. **High Contrast Mode (Windows):** Enable Windows High Contrast and confirm the active tab has a visible indicator (border, underline, or background).
4. **Keyboard test:** Tab to the tabbed interface and use arrow keys to switch tabs. Confirm the visual indicator moves to the newly active tab.

### Automated Testing

- Capture a screenshot, convert to grayscale, and visually compare active vs inactive tabs.
- Use `axe-core` to verify ARIA tab roles and `aria-selected` state.

```javascript
// Verify aria-selected state
const tabs = document.querySelectorAll('[role="tab"]');
const activeTabs = [...tabs].filter(t => t.getAttribute('aria-selected') === 'true');
console.assert(activeTabs.length === 1, 'Exactly one tab should be selected');
```

---

## Developer Notes

### General Approach

Add a secondary visual indicator (bottom border, background fill, or font weight) to the active tab state so that the selected tab is identifiable without color perception.

### Current State (Problem)

```css
/* Active tab only changes color */
.tab-button.active {
  color: #0066CC; /* Blue text — indistinguishable from inactive for color-blind users */
}

.tab-button {
  color: #555555; /* Default gray text */
  border: none;
  background: none;
}
```

### Recommended Fix

```css
.tab-button {
  color: #555555;
  background: none;
  border: none;
  border-bottom: 3px solid transparent;
  padding-bottom: 8px;
  font-weight: 400;
  transition: border-color 0.2s ease, font-weight 0.2s ease;
}

.tab-button.active,
.tab-button[aria-selected="true"] {
  color: #0066CC;
  border-bottom: 3px solid #0066CC; /* Non-color indicator: visible underline */
  font-weight: 700;                  /* Non-color indicator: bold weight */
}

/* Focus indicator */
.tab-button:focus-visible {
  outline: 3px solid #0066CC;
  outline-offset: 2px;
}

/* High Contrast Mode support */
@media (forced-colors: active) {
  .tab-button.active,
  .tab-button[aria-selected="true"] {
    border-bottom: 3px solid LinkText;
    forced-color-adjust: none;
  }
}
```

### ARIA Markup

```html
<div role="tablist" aria-label="Problems We Solve">
  <button role="tab" aria-selected="true" aria-controls="panel-1" id="tab-1">
    Growth Strategy
  </button>
  <button role="tab" aria-selected="false" aria-controls="panel-2" id="tab-2" tabindex="-1">
    Digital Transformation
  </button>
  <!-- More tabs -->
</div>
```

### Components / Files to Audit

- Tab button CSS (likely in `style.css` or a component stylesheet)
- Tab JavaScript initialization (handles `aria-selected` toggling)
- "Problems We Solve" section HTML template

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **Google Material Design** | Active tab has a bold bottom border (2–3px) plus color change | Two independent cues — visible in grayscale. |
| **GitHub** | Active repo tab uses a bold bottom border + different background | Underline + fill makes the active state obvious without color. |
| **BBC** | Navigation tabs use underline + bold weight for the active state | Multiple non-color cues work across all vision types. |
| **Stripe Docs** | Sidebar active item has a left border + bold text + background highlight | Three redundant indicators ensure universal perception. |
