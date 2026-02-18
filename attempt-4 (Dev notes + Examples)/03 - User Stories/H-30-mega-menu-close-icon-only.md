# H-30: Mega Menu Close Button Is Icon-Only

**Issue ID:** H-30
**Priority:** High
**WCAG Criteria:** 2.5.3 Label in Name (A), 4.1.2 Name, Role, Value (A)
**Affected Personas:** Voice Control

---

## User Story

**As a** voice control user,
**I want** the mega menu close button to have visible text that matches its accessible name,
**so that** I can reliably close the menu by saying "click Close" and have the command work.

---

## Acceptance Criteria

- [ ] The mega menu close button includes visible text reading "Close" (or "Close Menu") alongside or instead of the icon.
- [ ] The visible text matches the `aria-label` value (or the `aria-label` is removed in favor of the visible text).
- [ ] The button is a `<button>` element (not a `<div>` or `<span>`).
- [ ] The button has `type="button"` to prevent unintended form submission.
- [ ] Voice control users can successfully trigger the button by saying "click Close."
- [ ] The button meets the minimum 44×44px touch/click target size.
- [ ] The button is focusable and operable via keyboard (`Enter`/`Space`).

---

## How to Test the Change

### Manual Testing

1. **Voice control test (macOS):** Enable Voice Control (System Settings → Accessibility → Voice Control). Open the mega menu, then say "click Close." Confirm the menu closes.
2. **Voice control test (Windows):** Using Dragon NaturallySpeaking, open the mega menu and say "click Close." Confirm the command works.
3. **Visual inspection:** Open the mega menu. Confirm the close button shows visible text "Close" alongside or near the "X" icon.
4. **Keyboard test:** Tab to the close button. Press `Enter` or `Space`. Confirm the menu closes.
5. **Inspect element:** Verify the element is `<button>`, the `aria-label` matches the visible text, and the element has a minimum 44×44px target area.

### Automated Testing

```javascript
// Check close button has visible text matching aria-label
const closeBtn = document.querySelector('.mega-menu-close, [aria-label="Close"]');
if (closeBtn) {
  const visibleText = closeBtn.textContent.trim();
  const ariaLabel = closeBtn.getAttribute('aria-label');
  console.assert(
    visibleText.toLowerCase().includes('close'),
    'Close button should have visible "Close" text'
  );
  if (ariaLabel) {
    console.assert(
      ariaLabel.toLowerCase().includes(visibleText.toLowerCase()) || visibleText.toLowerCase().includes(ariaLabel.toLowerCase()),
      'aria-label should contain the visible text'
    );
  }
}
```

---

## Developer Notes

### General Approach

Add visible "Close" text to the mega menu close button so that voice control users can target it by name. The visible text must be included in (or match) the accessible name. The simplest approach is to add a visible text label and remove or align the `aria-label`.

### Current State (Problem)

```html
<!-- Icon-only button: voice control can't reliably target it -->
<button class="mega-menu-close" aria-label="Close">
  <svg><!-- X icon --></svg>
</button>
```

The visible label is empty (icon only), but the accessible name is "Close." Per WCAG 2.5.3 Label in Name, the visible label's text must be contained within the accessible name. Since there's no visible text, voice control commands like "click Close" may fail to match.

### Recommended Fix — Option A: Visible Text + Icon

```html
<button class="mega-menu-close" type="button">
  <svg aria-hidden="true" focusable="false"><!-- X icon --></svg>
  <span>Close</span>
</button>
```

```css
.mega-menu-close {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 8px 12px;
  min-width: 44px;
  min-height: 44px;
  background: none;
  border: 1px solid currentColor;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.875rem;
}

.mega-menu-close:focus-visible {
  outline: 3px solid var(--color-focus);
  outline-offset: 2px;
}
```

### Recommended Fix — Option B: Visually Hidden Text (Less Ideal)

If the design absolutely cannot accommodate visible text, use visually hidden text and ensure the `aria-label` matches:

```html
<button class="mega-menu-close" type="button" aria-label="Close menu">
  <svg aria-hidden="true"><!-- X icon --></svg>
  <span class="sr-only">Close menu</span>
</button>
```

```css
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
```

> **Note:** Option B still has reduced voice control reliability. Option A (visible text) is strongly preferred.

### Components / Files to Audit

- Mega menu HTML template (header partial or navigation component)
- Mega menu JavaScript (close button event handler)
- Mega menu CSS (close button styles, positioning)

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **Apple** | Menu close button shows "Close" text alongside the X icon | Voice control users can say "click Close" reliably. |
| **Microsoft** | Mega menu close button has visible "Close" label | Label in Name compliance — visible text matches accessible name. |
| **Salesforce (Lightning)** | Modal/panel close buttons include `sr-only` text "Close" and visible "×" with matching `aria-label="Close"` | Accessible name includes the visible character, plus screen reader text. |
| **W3C APG Dialog Pattern** | Recommends visible "Close" text or at minimum matching the `aria-label` to visible content | Reference specification for the close button pattern. |
