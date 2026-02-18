# C-07: Navigation Collapses to Tiny Unlabeled Hamburger

**Priority:** Critical
**WCAG Criteria:** 4.1.2 Name, Role, Value (A), 2.1.1 Keyboard (A), 1.4.4 Resize Text (AA)
**Affected Personas:** Voice Control, Low Vision, Senior Person, Cognitive Disability, Motor Impairment

---

## User Story

**As a** user with low vision, using voice control, or navigating by keyboard on a zoomed-in or mobile viewport,
**I want** the hamburger menu toggle to be a properly labeled, focusable button with the correct ARIA attributes,
**so that** I can discover, target, and activate the navigation menu using any input method.

---

## Acceptance Criteria

- [ ] The hamburger toggle is a `<button>` element (not a `<div>` or `<span>`).
- [ ] The button has a descriptive `aria-label` (e.g., `aria-label="Open main menu"`).
- [ ] The button has `aria-expanded="false"` when the menu is closed and `aria-expanded="true"` when open.
- [ ] The button has `aria-controls` pointing to the `id` of the navigation menu container.
- [ ] The button is keyboard focusable and can be activated with Enter or Space.
- [ ] The button has a visible focus indicator when focused via keyboard.
- [ ] The button's tap/click target is at least 44×44 CSS pixels.
- [ ] The button is visible and usable at 200% zoom and on viewports as narrow as 320px.
- [ ] Voice control users can activate the button by saying "Click Open main menu" or "Click Menu."
- [ ] When the mobile menu opens, focus moves into the menu. When it closes, focus returns to the hamburger button.

---

## How to Test the Change

### Manual Testing

1. **DOM Inspection:**
   - Resize viewport to 768px or below (or zoom to 150%+).
   - Open DevTools → Inspect the hamburger icon.
   - Verify it is a `<button>` element with `aria-label`, `aria-expanded`, and `aria-controls`.

2. **Keyboard Interaction:**
   - Tab to the hamburger button — verify focus indicator appears.
   - Press Enter or Space — menu should open, `aria-expanded` should change to `"true"`.
   - Press Escape — menu should close, focus returns to the button.

3. **Screen Reader:**
   - Navigate to the button — it should announce "Open main menu, collapsed, button."
   - Activate it — it should announce "Open main menu, expanded, button."

4. **Voice Control:**
   - Say "Click Menu" or "Click Open main menu" — button should activate.

5. **Tap Target Size:**
   - On a mobile device or emulator, verify the button is easily tappable (at least 44×44px).

### Automated Testing

```javascript
// Playwright test
test('hamburger menu is an accessible button', async ({ page }) => {
  await page.setViewportSize({ width: 375, height: 812 });
  await page.goto('https://launchpadlab.com');

  const hamburger = page.locator('#burgerBtn, [aria-label*="menu" i]');
  // Verify it's a button
  const tagName = await hamburger.evaluate(el => el.tagName.toLowerCase());
  expect(tagName).toBe('button');

  // Verify ARIA attributes
  await expect(hamburger).toHaveAttribute('aria-label', /menu/i);
  await expect(hamburger).toHaveAttribute('aria-expanded', 'false');

  // Verify minimum size
  const box = await hamburger.boundingBox();
  expect(box.width).toBeGreaterThanOrEqual(44);
  expect(box.height).toBeGreaterThanOrEqual(44);

  // Toggle and verify state change
  await hamburger.click();
  await expect(hamburger).toHaveAttribute('aria-expanded', 'true');
});
```

---

## Developer Notes

### General Approach

Replace the `<div id="burgerBtn">` with a semantic `<button>` element. Add proper ARIA attributes and keyboard event handling. Ensure the button meets minimum touch target size guidelines.

### Code Examples

**Before (current state):**

```html
<div id="burgerBtn">
  <span></span>
  <span></span>
  <span></span>
</div>
```

**After (fixed):**

```html
<button
  id="burgerBtn"
  type="button"
  aria-label="Open main menu"
  aria-expanded="false"
  aria-controls="primary-navigation"
  class="hamburger-btn"
>
  <span class="hamburger-line"></span>
  <span class="hamburger-line"></span>
  <span class="hamburger-line"></span>
</button>

<nav id="primary-navigation" aria-label="Primary navigation" hidden>
  <!-- Mobile navigation content -->
</nav>
```

**CSS for button reset and sizing:**

```css
.hamburger-btn {
  /* Reset button styles */
  background: none;
  border: none;
  cursor: pointer;
  padding: 0;

  /* Minimum touch target */
  min-width: 44px;
  min-height: 44px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 5px;
}

.hamburger-btn:focus-visible {
  outline: 3px solid #f5a623;
  outline-offset: 3px;
  border-radius: 4px;
}

.hamburger-line {
  display: block;
  width: 24px;
  height: 3px;
  background-color: currentColor;
  border-radius: 2px;
  transition: transform 0.3s ease;
}
```

**JavaScript for toggle behavior:**

```javascript
const burgerBtn = document.getElementById('burgerBtn');
const mobileNav = document.getElementById('primary-navigation');

burgerBtn.addEventListener('click', () => {
  const isOpen = burgerBtn.getAttribute('aria-expanded') === 'true';

  burgerBtn.setAttribute('aria-expanded', String(!isOpen));
  burgerBtn.setAttribute('aria-label', isOpen ? 'Open main menu' : 'Close main menu');
  mobileNav.hidden = isOpen;

  if (!isOpen) {
    // Focus the first link in the menu when opening
    const firstLink = mobileNav.querySelector('a, button');
    firstLink?.focus();
  }
});

// Close on Escape
mobileNav.addEventListener('keydown', (e) => {
  if (e.key === 'Escape') {
    burgerBtn.setAttribute('aria-expanded', 'false');
    burgerBtn.setAttribute('aria-label', 'Open main menu');
    mobileNav.hidden = true;
    burgerBtn.focus();
  }
});
```

### Components/Files to Audit

- `header.php` — The `#burgerBtn` markup.
- Main JavaScript file — The click handler for `#burgerBtn`.
- Mobile navigation CSS — Display/hide logic for the menu panel.
- Any media queries that control when the hamburger appears.

---

## Examples from Other Sites

| Site | Implementation |
|------|----------------|
| **gov.uk** | `<button aria-label="Show navigation menu" aria-expanded="false">Menu</button>` — includes visible "Menu" text next to the icon. |
| **Airbnb** | `<button aria-label="Main navigation menu" aria-expanded="false">` with 48×48px touch target. |
| **GitHub Mobile** | `<button aria-label="Toggle navigation" aria-expanded="false">` with animated hamburger-to-X transition. |
| **Bootstrap 5** | Navbar toggler uses `<button class="navbar-toggler" aria-controls="navContent" aria-expanded="false" aria-label="Toggle navigation">`. |
