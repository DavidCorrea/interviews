# L-55: Navigation `<nav>` Lacks `aria-label`

**Issue ID:** L-55
**Priority:** Low
**WCAG Criteria:** 1.3.1 Info and Relationships (A), 4.1.2 Name, Role, Value (A)
**Affected Personas:** Screen Reader

---

## User Story

As a **screen reader user**, I want each `<nav>` element on the page to have a unique, descriptive `aria-label` so that I can distinguish between navigation regions (e.g., primary navigation vs. footer navigation) when browsing the landmarks list.

---

## Acceptance Criteria

- [ ] Every `<nav>` element on every page has either an `aria-label` or `aria-labelledby` attribute.
- [ ] Each `aria-label` value is unique within the page (no two `<nav>` elements share the same label).
- [ ] Labels are descriptive and human-readable (e.g., "Primary navigation," "Footer navigation," "Breadcrumb navigation").
- [ ] Screen readers (NVDA, VoiceOver, JAWS) list the navigation landmarks with their distinct labels when the user opens the landmarks/regions list.
- [ ] The fix is applied consistently across all pages site-wide.

---

## How to Test the Change

### Manual Testing
1. Open any page on launchpadlab.com.
2. Open browser DevTools and search for all `<nav>` elements:
   ```javascript
   document.querySelectorAll('nav').forEach(nav => {
     console.log(nav.getAttribute('aria-label') || nav.getAttribute('aria-labelledby') || 'MISSING LABEL');
   });
   ```
3. Verify each `<nav>` has a unique, descriptive label.
4. Test with VoiceOver (macOS):
   - Press `VO + U` to open the Rotor.
   - Navigate to **Landmarks**.
   - Confirm each navigation landmark appears with its unique label (e.g., "Primary navigation, navigation" and "Footer navigation, navigation").
5. Test with NVDA (Windows):
   - Press `D` to jump between landmarks.
   - Confirm each `<nav>` is announced with its label.
6. Repeat on at least 3 different page types (homepage, service page, contact page).

### Automated Testing
1. Run `axe-core`:
   ```bash
   npx @axe-core/cli https://launchpadlab.com --rules landmark-unique
   ```
2. Write a custom assertion:
   ```javascript
   const navs = document.querySelectorAll('nav');
   const labels = new Set();
   navs.forEach(nav => {
     const label = nav.getAttribute('aria-label') || 
                   document.getElementById(nav.getAttribute('aria-labelledby'))?.textContent;
     expect(label).toBeTruthy();
     expect(labels.has(label)).toBe(false); // unique
     labels.add(label);
   });
   ```

---

## Developer Notes

### General Explanation
When a page contains multiple `<nav>` elements (primary nav, footer nav, sidebar nav, breadcrumbs, etc.), screen readers list them all as "navigation" in the landmarks list. Without `aria-label`, users have no way to tell them apart. Adding a unique label to each `<nav>` takes seconds and dramatically improves landmark navigation.

### Code Examples

```html
<!-- BEFORE: unlabeled nav elements -->
<nav>
  <!-- Primary site navigation -->
</nav>
...
<nav>
  <!-- Footer navigation -->
</nav>

<!-- AFTER: labeled nav elements -->
<nav aria-label="Primary">
  <!-- Primary site navigation -->
</nav>
...
<nav aria-label="Footer">
  <!-- Footer navigation -->
</nav>
```

If the `<nav>` already has a visible heading, use `aria-labelledby` instead:
```html
<nav aria-labelledby="footer-nav-heading">
  <h2 id="footer-nav-heading">Quick Links</h2>
  <ul>...</ul>
</nav>
```

### Common `<nav>` Labels by Convention

| Location | Suggested `aria-label` |
|---|---|
| Header primary menu | `"Primary"` |
| Header utility/secondary menu | `"Utility"` |
| Mobile hamburger menu | `"Mobile"` |
| Footer link columns | `"Footer"` |
| Breadcrumb trail | `"Breadcrumb"` |
| Sidebar/in-page nav | `"Sidebar"` or `"On this page"` |

### Components/Files to Audit
- `header.php` — primary `<nav>` element
- `footer.php` — footer `<nav>` element(s)
- Mobile menu template/partial
- Any page-specific `<nav>` elements (breadcrumbs, sidebar navigation)
- WordPress `wp_nav_menu()` calls — add `aria-label` to the `container` args or wrapper element

### WordPress-Specific Implementation
```php
// In header.php or nav template
wp_nav_menu( array(
    'theme_location' => 'primary',
    'container'      => 'nav',
    'container_class'=> 'primary-nav',
    'items_wrap'     => '<ul id="%1$s" class="%2$s" role="menubar">%3$s</ul>',
) );
// Add aria-label to the <nav> wrapper manually or via filter:
```

Or simply add the attribute directly in the template:
```php
<nav aria-label="Primary" class="primary-nav">
  <?php wp_nav_menu( array( 'theme_location' => 'primary', 'container' => false ) ); ?>
</nav>
```

---

## Examples from Other Sites

- **GOV.UK:** Uses `<nav aria-label="Menu">` for the main navigation and `<nav aria-label="Related content">` for sidebar links. Each is uniquely labeled.
- **MDN Web Docs:** Uses `<nav aria-label="Main menu">` and `<nav aria-label="Breadcrumb">` — each landmark is clearly distinguished.
- **Deque University:** Their navigation pattern reference recommends unique `aria-label` values on all `<nav>` elements when more than one exists on a page.

---

## Additional Context

This is one of the simplest accessibility fixes — a single HTML attribute per `<nav>` element — with a meaningful impact on screen reader usability. The [ARIA Landmarks specification](https://www.w3.org/WAI/ARIA/apg/patterns/landmarks/) explicitly calls out the need for unique labels when multiple landmarks of the same type exist on a page.
