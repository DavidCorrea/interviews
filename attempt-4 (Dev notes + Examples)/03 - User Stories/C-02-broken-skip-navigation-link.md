# C-02: Broken Skip Navigation Link

**Priority:** Critical
**WCAG Criteria:** 2.4.1 Bypass Blocks (A)
**Affected Personas:** Screen Reader, Voice Control, Motor Impairment, Low Vision

---

## User Story

**As a** keyboard or assistive technology user,
**I want** the "Skip to Content" link to correctly move focus to the beginning of the main content area,
**so that** I can bypass the repetitive navigation on every page and get to the content I came for without tabbing through dozens of links.

---

## Acceptance Criteria

- [ ] The skip navigation link's `href` value (e.g., `#main-content`) matches an existing `id` attribute on the `<main>` element.
- [ ] Activating the skip link moves both visual scroll position and keyboard focus to the main content area.
- [ ] The `<main>` element has `tabindex="-1"` so it can receive programmatic focus (if it does not natively receive focus in the target browsers).
- [ ] The skip link is the first focusable element in the DOM (appears before the navigation).
- [ ] The skip link is visually hidden by default but becomes visible on keyboard focus (`:focus`).
- [ ] The skip link text clearly communicates its purpose (e.g., "Skip to main content").

---

## How to Test the Change

### Manual Testing

1. **Keyboard Navigation:**
   - Load any page and press **Tab** once. The skip link should become visible at the top of the viewport.
   - Press **Enter** on the skip link. The page should scroll to the main content and focus should move there.
   - Press **Tab** again — the next focused element should be the first interactive element inside `<main>`, not the navigation.

2. **Screen Reader:**
   - With NVDA/VoiceOver active, the first item announced after page load and initial Tab should be the skip link.
   - Activating it should announce the main content region.

3. **Visual Verification:**
   - Confirm the skip link is invisible until it receives focus.
   - Confirm it disappears when focus moves past it.

### Automated Testing

```javascript
// Playwright test
test('skip link targets existing element and moves focus', async ({ page }) => {
  await page.goto('https://launchpadlab.com');

  // Tab to the skip link
  await page.keyboard.press('Tab');
  const skipLink = page.locator('a[href="#main-content"]');
  await expect(skipLink).toBeFocused();

  // Activate skip link
  await page.keyboard.press('Enter');

  // Verify focus moved to main
  const main = page.locator('main#main-content');
  await expect(main).toBeFocused();
});
```

```bash
# Check that the skip link target exists in the DOM
# axe-core will flag skip links with missing targets
npx @axe-core/cli https://launchpadlab.com --rules skip-link
```

---

## Developer Notes

### General Approach

1. Update the skip link `href` from `#primary` to match the actual `id` on the `<main>` element (e.g., `#main-content`).
2. Ensure the `<main>` element has the corresponding `id` and `tabindex="-1"` for programmatic focus.
3. Style the skip link to be visually hidden but visible on focus.

### Code Examples

**Fix the skip link target:**

```html
<!-- Before (broken) -->
<a class="skip-link" href="#primary">Skip to content</a>
<!-- No element with id="primary" exists -->

<!-- After (fixed) -->
<a class="skip-link" href="#main-content">Skip to main content</a>
<!-- ... -->
<main id="main-content" tabindex="-1">
  <!-- Primary content -->
</main>
```

**Skip link CSS (visually hidden until focused):**

```css
.skip-link {
  position: absolute;
  top: -100%;
  left: 0;
  z-index: 10000;
  padding: 0.75rem 1.5rem;
  background: #1a1a2e;
  color: #ffffff;
  font-size: 1rem;
  font-weight: 600;
  text-decoration: none;
  border-radius: 0 0 4px 0;
  transition: top 0.2s ease;
}

.skip-link:focus {
  top: 0;
  outline: 3px solid #f5a623;
  outline-offset: 2px;
}
```

**Remove residual focus outline on main after skip (optional UX polish):**

```css
main:focus {
  outline: none;
}
```

### Components/Files to Audit

- `header.php` — Location of the skip link markup.
- `style.css` / main stylesheet — Skip link visibility styles.
- All page templates — Ensure `<main id="main-content">` is present (pairs with C-01).

---

## Examples from Other Sites

| Site | Implementation |
|------|----------------|
| **gov.uk** | "Skip to main content" link as the first focusable element, targeting `#main-content`. Styled as a prominent blue bar on focus. |
| **GitHub** | "Skip to content" link appears on focus, targets `#start-of-content` which is a `<div>` with `tabindex="-1"`. |
| **BBC** | Multiple skip links: "Skip to content," "Skip to navigation," each targeting appropriately `id`'d elements. |
| **Wikipedia** | "Jump to content" and "Jump to search" links at the top of every page. |
