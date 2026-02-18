# C-01: Missing `<main>` Landmark

**Priority:** Critical
**WCAG Criteria:** 1.3.1 Info and Relationships (A), 2.4.1 Bypass Blocks (A)
**Affected Personas:** Screen Reader

---

## User Story

**As a** screen reader user,
**I want** the page to include a `<main>` landmark element wrapping the primary content,
**so that** I can quickly jump to the main content area and efficiently navigate between landmark regions without having to listen through the entire header and navigation.

---

## Acceptance Criteria

- [ ] Every page on the site contains exactly one `<main>` element wrapping the primary content region.
- [ ] The `<main>` element does not wrap the site header, footer, or navigation.
- [ ] Screen readers (NVDA, VoiceOver, JAWS) correctly announce the `<main>` landmark when listing landmarks.
- [ ] The `<main>` element has an `id` attribute (e.g., `id="main-content"`) that the skip navigation link targets.
- [ ] The `<main>` landmark is the first landmark region after the site header/navigation when navigating by landmarks.
- [ ] No nested `<main>` elements exist anywhere in the DOM.

---

## How to Test the Change

### Manual Testing

1. **Screen Reader Landmarks:**
   - Open any page in Chrome with NVDA (or Safari with VoiceOver).
   - Press **D** (NVDA) or use the **Rotor > Landmarks** (VoiceOver) to list all landmarks.
   - Verify "main" appears in the landmark list.
   - Navigate to the main landmark and confirm it contains the primary page content (not header/footer).

2. **DOM Inspection:**
   - Open DevTools (F12) → Elements panel.
   - Search for `<main` — confirm exactly one `<main>` element exists.
   - Verify it wraps only the primary content area.

3. **Accessibility Tree:**
   - In Chrome DevTools, open the Accessibility panel.
   - Verify the `<main>` element appears with role "main" in the accessibility tree.

### Automated Testing

```bash
# Using axe-core CLI
npx @axe-core/cli https://launchpadlab.com --rules landmark-one-main

# Using pa11y
npx pa11y https://launchpadlab.com --standard WCAG2AA
```

```javascript
// Playwright test
test('page has exactly one main landmark', async ({ page }) => {
  await page.goto('https://launchpadlab.com');
  const mainElements = await page.locator('main').count();
  expect(mainElements).toBe(1);
});
```

---

## Developer Notes

### General Approach

Wrap the primary content area of every page template in a `<main>` element. In a WordPress theme, this typically means editing the base template file(s) to add `<main>` around the content output area, excluding the header, footer, and sidebar regions.

### Code Examples

**Before (current state):**

```html
<header class="site-header">...</header>
<div class="page-content">
  <!-- All page content here, no landmark -->
  <section class="hero">...</section>
  <section class="services">...</section>
</div>
<footer class="site-footer">...</footer>
```

**After (fixed):**

```html
<header class="site-header">...</header>
<main id="main-content" role="main">
  <section class="hero">...</section>
  <section class="services">...</section>
</main>
<footer class="site-footer">...</footer>
```

> **Note:** The `role="main"` attribute is included for backward compatibility with older assistive technologies but is redundant with the `<main>` element in modern browsers.

### Components/Files to Audit

- `header.php` — Ensure `<main>` opens after the header closing tag.
- `footer.php` — Ensure `<main>` closes before the footer opening tag.
- `page.php`, `single.php`, `front-page.php`, `index.php` — All base templates should inherit the `<main>` wrapper.
- `archive.php`, `search.php`, `404.php` — Secondary templates also need the landmark.
- Any custom page builder templates or Divi/Elementor layouts.

---

## Examples from Other Sites

| Site | Implementation |
|------|----------------|
| **gov.uk** | Uses `<main id="main-content" role="main">` on every page with a skip link targeting it. |
| **GitHub** | Wraps repository content in `<main id="js-repo-pjax-container">` with a "Skip to content" link. |
| **MDN Web Docs** | Uses `<main id="content">` immediately after the navigation bar. |
| **Apple** | Uses `<main id="main" role="main">` wrapping all content between header and footer. |
