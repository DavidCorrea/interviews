# C-05: Mega Menu Hover-Only Activation

**Priority:** Critical
**WCAG Criteria:** 2.1.1 Keyboard (A), 2.1.2 No Keyboard Trap (A), 2.5.1 Pointer Gestures (A)
**Affected Personas:** Motor Impairment, Low Vision Screen Magnifier, Voice Control, Senior Person, ADHD, Cognitive Disability

---

## User Story

**As a** keyboard user, screen magnifier user, or voice control user,
**I want** the navigation dropdown menus to open and close reliably via keyboard, click, and focus interactions — not just mouse hover,
**so that** I can access all navigation options regardless of my input device or assistive technology.

---

## Acceptance Criteria

- [ ] Top-level menu items with submenus can be activated by keyboard (Enter or Space) to toggle the dropdown open/closed.
- [ ] Arrow keys (Down/Up) navigate between submenu items when the dropdown is open.
- [ ] Pressing Escape closes the open dropdown and returns focus to the parent menu item.
- [ ] Tab moves focus to the next top-level menu item (closing the current dropdown if open).
- [ ] The dropdown remains open while any element within it has focus (no 300ms timeout that closes it while a user is still interacting).
- [ ] The parent menu item has `aria-expanded="true"` when the dropdown is open and `aria-expanded="false"` when closed.
- [ ] The submenu container has `role="menu"` or `role="region"` and submenu items use `role="menuitem"` (or equivalent navigation pattern).
- [ ] Mouse hover still works as before for mouse users (progressive enhancement).
- [ ] Screen magnifier users who pan away and back within 3 seconds find the menu still open.

---

## How to Test the Change

### Manual Testing

1. **Keyboard Navigation:**
   - Tab to the first nav item with a dropdown (e.g., "Services").
   - Press **Enter** or **Space** — dropdown should open.
   - Press **Down Arrow** — focus should move to the first submenu item.
   - Press **Up/Down Arrow** — focus should move through submenu items.
   - Press **Escape** — dropdown closes, focus returns to "Services."
   - Press **Tab** — focus moves to the next top-level item.

2. **Screen Reader:**
   - Navigate to "Services" — it should announce "Services, expanded" or "Services, collapsed" based on state.
   - Enter the submenu — items should be announced as menu items.

3. **Voice Control:**
   - Say "Click Services" — dropdown should open.
   - Say "Click [submenu item name]" — should navigate to that item.

4. **Screen Magnifier:**
   - Zoom to 300%, hover to open a dropdown.
   - Pan the viewport away from the menu to read a submenu item, then pan back — menu should still be open.

### Automated Testing

```javascript
// Playwright test
test('mega menu opens and navigates by keyboard', async ({ page }) => {
  await page.goto('https://launchpadlab.com');

  // Find the "Services" nav item
  const servicesLink = page.locator('nav a:has-text("Services")').first();
  await servicesLink.focus();

  // Open dropdown with Enter
  await page.keyboard.press('Enter');

  // Check aria-expanded
  const expanded = await servicesLink.getAttribute('aria-expanded');
  expect(expanded).toBe('true');

  // Navigate to first submenu item
  await page.keyboard.press('ArrowDown');
  const focused = await page.evaluate(() => document.activeElement?.textContent?.trim());
  expect(focused).toBeTruthy();

  // Close with Escape
  await page.keyboard.press('Escape');
  const collapsed = await servicesLink.getAttribute('aria-expanded');
  expect(collapsed).toBe('false');
});
```

---

## Developer Notes

### General Approach

Replace the `hover_intent`-only activation with a disclosure pattern: top-level items act as toggle buttons that open/close submenus on click, Enter, or Space. Hover can remain as a progressive enhancement. Implement WAI-ARIA menu/menubar pattern or the simpler disclosure navigation pattern.

### Code Examples

**HTML structure with ARIA:**

```html
<nav aria-label="Primary navigation">
  <ul role="menubar">
    <li role="none">
      <button
        role="menuitem"
        aria-haspopup="true"
        aria-expanded="false"
        id="services-btn"
      >
        Services
      </button>
      <ul role="menu" aria-labelledby="services-btn" hidden>
        <li role="none">
          <a role="menuitem" href="/services/web-development">Web Development</a>
        </li>
        <li role="none">
          <a role="menuitem" href="/services/mobile-apps">Mobile Apps</a>
        </li>
        <!-- more items -->
      </ul>
    </li>
    <!-- more top-level items -->
  </ul>
</nav>
```

**JavaScript for keyboard interaction:**

```javascript
class MegaMenu {
  constructor(nav) {
    this.nav = nav;
    this.triggers = nav.querySelectorAll('[aria-haspopup="true"]');
    this.init();
  }

  init() {
    this.triggers.forEach(trigger => {
      const submenu = trigger.nextElementSibling;
      const items = submenu.querySelectorAll('[role="menuitem"]');

      // Toggle on click/Enter/Space
      trigger.addEventListener('click', () => this.toggle(trigger, submenu));
      trigger.addEventListener('keydown', (e) => {
        if (e.key === 'ArrowDown') {
          e.preventDefault();
          this.open(trigger, submenu);
          items[0]?.focus();
        }
        if (e.key === 'Escape') {
          this.close(trigger, submenu);
          trigger.focus();
        }
      });

      // Arrow key navigation within submenu
      items.forEach((item, index) => {
        item.addEventListener('keydown', (e) => {
          if (e.key === 'ArrowDown') {
            e.preventDefault();
            items[(index + 1) % items.length].focus();
          }
          if (e.key === 'ArrowUp') {
            e.preventDefault();
            items[(index - 1 + items.length) % items.length].focus();
          }
          if (e.key === 'Escape') {
            this.close(trigger, submenu);
            trigger.focus();
          }
        });
      });

      // Close when focus leaves the menu entirely
      submenu.addEventListener('focusout', (e) => {
        if (!submenu.contains(e.relatedTarget) && e.relatedTarget !== trigger) {
          this.close(trigger, submenu);
        }
      });
    });
  }

  toggle(trigger, submenu) {
    const isOpen = trigger.getAttribute('aria-expanded') === 'true';
    isOpen ? this.close(trigger, submenu) : this.open(trigger, submenu);
  }

  open(trigger, submenu) {
    trigger.setAttribute('aria-expanded', 'true');
    submenu.hidden = false;
  }

  close(trigger, submenu) {
    trigger.setAttribute('aria-expanded', 'false');
    submenu.hidden = true;
  }
}
```

### Components/Files to Audit

- Primary navigation HTML template (`header.php` or nav partial).
- `hover_intent` JavaScript initialization — replace or augment with keyboard support.
- Navigation CSS — ensure dropdown visibility is not solely tied to `:hover` states.
- Any third-party mega menu plugin (e.g., UberMenu, Max Mega Menu) — check its accessibility settings.

---

## Examples from Other Sites

| Site | Implementation |
|------|----------------|
| **Microsoft.com** | Mega menu opens on click (not hover). Uses `aria-expanded`, arrow key navigation, and Escape to close. |
| **W3C WAI** | Navigation follows the disclosure pattern. Dropdowns open on click/Enter and close on Escape/blur. |
| **GitHub** | Navigation dropdowns open on click. Arrow keys navigate submenu items. Escape closes and returns focus. |
| **Deque University** | Uses the WAI-ARIA menubar pattern with full keyboard support as a reference implementation. |
