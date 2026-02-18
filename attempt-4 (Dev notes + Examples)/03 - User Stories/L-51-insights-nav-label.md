# L-51: "Insights" Nav Label Instead of "Blog"

**Issue ID:** L-51
**Priority:** Low
**WCAG Criteria:** 2.4.6 Headings and Labels (AA)
**Affected Personas:** Non-Native Speaker, Senior Person

---

## User Story

As a **non-native English speaker or older user**, I want **the navigation label for the blog section to use a universally understood term** so that **I can find articles and blog posts without having to guess that "Insights" means the company blog.**

---

## Acceptance Criteria

- [ ] The primary navigation link labeled "Insights" is renamed to **"Blog"** (or "Blog & Insights" as a compromise).
- [ ] The link continues to point to `/blog/`.
- [ ] The page heading on the blog landing page matches or aligns with the navigation label.
- [ ] Any other references to "Insights" in the site (footer, mega menu descriptions) are updated for consistency.
- [ ] The URL path remains `/blog/` (no URL change needed).

---

## How to Test the Change

### Manual Testing

1. Open the site and look at the primary navigation.
2. Verify the blog link reads "Blog" (or "Blog & Insights").
3. Click the link and confirm it navigates to `/blog/`.
4. Check the page heading on the blog landing page — verify it aligns with the nav label.
5. Check the footer navigation — verify the label matches.
6. Ask a non-native English speaker: "Where would you click to find articles?" Confirm they can identify the correct link.

### Automated Testing

1. Verify navigation label:
   ```javascript
   const nav = document.querySelector('nav.primary-nav, .main-navigation');
   const blogLink = nav?.querySelector('a[href*="/blog"]');
   console.log('Blog nav label:', blogLink?.textContent.trim());
   // Expected: "Blog" or "Blog & Insights"
   ```
2. Check for consistency across header and footer:
   ```javascript
   const header = document.querySelector('header');
   const footer = document.querySelector('footer');
   const headerLabel = header?.querySelector('a[href*="/blog"]')?.textContent.trim();
   const footerLabel = footer?.querySelector('a[href*="/blog"]')?.textContent.trim();
   console.log(`Header: "${headerLabel}", Footer: "${footerLabel}"`);
   // Both should match
   ```

---

## Developer Notes

### General Explanation

The navigation uses "Insights" as the label for the blog section, but the URL is `/blog/`. "Insights" is a corporate euphemism that non-native English speakers and older users may not associate with blog posts or articles. The mismatch between the label and URL also creates a subtle inconsistency. The fix is simply renaming the navigation item to "Blog" — the universally understood term for this content type. This aligns with WCAG 2.4.6, which requires labels to be descriptive and predictable.

### Code Examples

**WordPress Menu Update (Admin):**
1. Go to Appearance > Menus.
2. Find the "Insights" menu item.
3. Change the Navigation Label from "Insights" to "Blog."
4. Save the menu.

**If the menu is hardcoded in `header.php`:**
```html
<!-- Before -->
<nav class="primary-nav" aria-label="Main navigation">
  <ul>
    <li><a href="/services/">Services</a></li>
    <li><a href="/case-studies/">Case Studies</a></li>
    <li><a href="/blog/">Insights</a></li>
    <li><a href="/about/">About</a></li>
    <li><a href="/contact/">Contact</a></li>
  </ul>
</nav>

<!-- After -->
<nav class="primary-nav" aria-label="Main navigation">
  <ul>
    <li><a href="/services/">Services</a></li>
    <li><a href="/case-studies/">Case Studies</a></li>
    <li><a href="/blog/">Blog</a></li>
    <li><a href="/about/">About</a></li>
    <li><a href="/contact/">Contact</a></li>
  </ul>
</nav>
```

**Also update the footer:**
```html
<!-- Before -->
<a href="/blog/">Insights</a>

<!-- After -->
<a href="/blog/">Blog</a>
```

**Update the blog landing page heading if needed:**
```html
<!-- Before -->
<h1>Insights</h1>

<!-- After -->
<h1>Blog</h1>
<!-- Or: <h1>Blog & Insights</h1> -->
```

**If using mega menu with description:**
```html
<!-- Before -->
<a href="/blog/">
  <span class="menu-title">Insights</span>
  <span class="menu-desc">Thoughts on technology and innovation</span>
</a>

<!-- After -->
<a href="/blog/">
  <span class="menu-title">Blog</span>
  <span class="menu-desc">Articles on software development, AI, and digital products</span>
</a>
```

### Components / Files to Audit

- WordPress admin: Appearance > Menus (primary and footer menus)
- `header.php` — if navigation is hardcoded
- `footer.php` — footer navigation links
- Mega menu component — if the label appears there
- Blog archive page template — page heading
- Any breadcrumbs that reference "Insights"
- SEO: update `<title>` and meta description of the blog landing page if they reference "Insights"

---

## Examples from Other Sites

- **Basecamp.com:** Uses "Blog" in their navigation — simple, clear, universally understood.
- **Stripe.com:** Uses "Blog" as the nav label, pointing to `/blog`.
- **GitHub:** Uses "Blog" in their footer navigation.
- **Atlassian:** Uses "Blog" in their resource navigation rather than "Insights" or "Thought Leadership."
- **Note:** Some enterprise sites use "Resources" as a parent menu containing "Blog," "Whitepapers," and "Webinars" — this is acceptable because it is a clear container label, not a euphemism.
