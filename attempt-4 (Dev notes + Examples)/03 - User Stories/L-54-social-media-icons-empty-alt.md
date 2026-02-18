# L-54: Social Media Icons Have Empty Alt Text

**Issue ID:** L-54
**Priority:** Low
**WCAG Criteria:** 1.1.1 Non-text Content (A)
**Affected Personas:** Screen Reader (mitigated by adjacent text labels)

---

## User Story

As a **screen reader user**, I want social media icons to have descriptive alt text so that I can identify each platform's icon independently, even when adjacent visible text labels are not present or are separated in the accessibility tree.

---

## Acceptance Criteria

- [ ] Each social media icon `<img>` has a meaningful `alt` attribute describing the platform (e.g., `alt="LinkedIn"`, `alt="Twitter"`, `alt="Facebook"`).
- [ ] If the icon is inside a link that already has an accessible name via visible text, the icon `alt` may remain empty (`alt=""`) to avoid redundant announcements — but this must be verified per-instance.
- [ ] If the icon is the **only content** inside a link, the `alt` text MUST include both the platform name and the action (e.g., `alt="Visit LaunchPad Lab on LinkedIn"`).
- [ ] Screen readers announce each social media link with a clear, non-redundant label.
- [ ] No social media link is announced as simply "link" or "image" without context.

---

## How to Test the Change

### Manual Testing
1. Navigate to the site footer (and header, if social icons exist there).
2. Inspect each social media icon with browser DevTools:
   - Verify `alt` attributes are present and descriptive.
3. Test with VoiceOver (macOS):
   - Use `VO + Right Arrow` to navigate to the social media icons in the footer.
   - Each link should announce the platform name (e.g., "Visit LaunchPad Lab on LinkedIn, link").
   - No link should announce as "image, link" or "link" alone.
4. Test with NVDA (Windows):
   - Press `K` to jump between links in the footer.
   - Verify each social link has a meaningful announcement.
5. Tab through the social icon links with a keyboard and confirm the accessible name in the accessibility tree (DevTools > Accessibility tab).

### Automated Testing
1. Run `axe-core` or Lighthouse accessibility audit:
   ```bash
   npx @axe-core/cli https://launchpadlab.com --tags wcag2a
   ```
2. Write a DOM test to assert non-empty alt text on icon-only links:
   ```javascript
   const socialLinks = document.querySelectorAll('footer .social-icons a');
   socialLinks.forEach(link => {
     const img = link.querySelector('img');
     const visibleText = link.textContent.trim();
     if (!visibleText && img) {
       expect(img.getAttribute('alt')).not.toBe('');
       expect(img.getAttribute('alt')).toBeTruthy();
     }
   });
   ```

---

## Developer Notes

### General Explanation
Social media icon images currently use `alt=""`, which marks them as decorative. This is acceptable **only** if the parent `<a>` link has visible text or an `aria-label` that provides the accessible name. If the icon is the sole content of the link, the link becomes unnamed for screen readers.

The safest approach is to use `aria-label` on the parent link and keep `alt=""` on the icon — this avoids duplication while ensuring the link itself is always named.

### Recommended Pattern

```html
<!-- BEFORE: icon-only link with empty alt -->
<a href="https://linkedin.com/company/launchpadlab">
  <img src="/icons/linkedin.svg" alt="">
</a>

<!-- AFTER (Option A): aria-label on link, decorative icon -->
<a href="https://linkedin.com/company/launchpadlab"
   aria-label="Visit LaunchPad Lab on LinkedIn">
  <img src="/icons/linkedin.svg" alt="">
</a>

<!-- AFTER (Option B): meaningful alt on icon -->
<a href="https://linkedin.com/company/launchpadlab">
  <img src="/icons/linkedin.svg" alt="Visit LaunchPad Lab on LinkedIn">
</a>

<!-- AFTER (Option C): visually hidden text + decorative icon -->
<a href="https://linkedin.com/company/launchpadlab">
  <img src="/icons/linkedin.svg" alt="">
  <span class="sr-only">Visit LaunchPad Lab on LinkedIn</span>
</a>
```

If icons are inline SVGs rather than `<img>` tags:
```html
<a href="https://linkedin.com/company/launchpadlab"
   aria-label="Visit LaunchPad Lab on LinkedIn">
  <svg aria-hidden="true" focusable="false"><!-- icon --></svg>
</a>
```

### Components/Files to Audit
- Footer template (`footer.php` or template partial)
- Header social icons (if present)
- Any widget rendering social media links
- WordPress Social Icons block or custom shortcode
- CSS for `.sr-only` / `.visually-hidden` utility class (ensure it exists)

---

## Examples from Other Sites

- **GitHub:** Social/footer links use `aria-label` on the `<a>` element with `aria-hidden="true"` on the SVG icon. Example: `<a aria-label="GitHub on Twitter" href="..."><svg aria-hidden="true">...</svg></a>`.
- **Shopify:** Footer social links use visually hidden `<span>` text inside the link alongside a decorative SVG.
- **A11Y Project:** Their social links follow the exact pattern of `aria-label` on the link + `aria-hidden` on the icon, serving as a reference implementation.

---

## Additional Context

The report notes this issue is **mitigated** by adjacent visible text labels. However, the icons should still be properly handled in the accessibility tree to be robust. If visible text labels are ever removed (e.g., in a redesign), the links would become completely inaccessible. Fixing this now is a preventive measure.
