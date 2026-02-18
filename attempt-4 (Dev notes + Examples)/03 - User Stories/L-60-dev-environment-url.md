# L-60: Dev Environment URL in Production

**Issue ID:** L-60
**Priority:** Low
**WCAG Criteria:** N/A (trust/quality concern)
**Affected Personas:** Skeptical User

---

## User Story

As a **skeptical prospective client** evaluating the company's technical competence, I want all site assets to load from the production domain so that I don't see development environment URLs that undermine my confidence in the company's attention to detail and deployment practices.

---

## Acceptance Criteria

- [ ] No image, script, stylesheet, or other asset on the production site references `dev-launchpadlab.pantheonsite.io` or any other non-production domain.
- [ ] All asset URLs use the canonical production domain (`launchpadlab.com`), relative paths, or a properly configured CDN.
- [ ] A search of the full page source (all pages) returns zero matches for `dev-`, `staging-`, `.pantheonsite.io`, or any other development/staging hostname.
- [ ] The fix covers all pages site-wide — homepage, services, about, contact, blog posts, and case studies.
- [ ] Images previously served from the dev URL load correctly from the production URL with no broken images.

---

## How to Test the Change

### Manual Testing
1. Navigate to launchpadlab.com.
2. Open DevTools → **Network** tab.
3. Reload the page and filter by **Img** (images).
4. Inspect every image request — confirm none reference `dev-launchpadlab.pantheonsite.io`.
5. Repeat on at least 5 pages: homepage, a service page, about, contact, and a blog post.
6. Right-click any suspected image and select **Open image in new tab** — verify the URL is the production domain.
7. View page source (`Ctrl+U`) and search for `pantheonsite.io` — should return zero results.

### Automated Testing
1. Crawl the site and check all asset URLs:
   ```bash
   # Using wget to spider and grep for dev URLs
   wget --spider -r -l 3 https://launchpadlab.com 2>&1 | grep -i "pantheonsite"
   ```
2. Write a CI test:
   ```javascript
   // Playwright example
   const response = await page.goto('https://launchpadlab.com');
   const html = await page.content();
   expect(html).not.toContain('pantheonsite.io');
   expect(html).not.toContain('dev-launchpadlab');

   // Check all image sources
   const imgSrcs = await page.$$eval('img', imgs => imgs.map(i => i.src));
   imgSrcs.forEach(src => {
     expect(src).not.toContain('pantheonsite.io');
   });
   ```
3. Add a deployment check/lint rule that scans rendered HTML for non-production hostnames before promoting to production.

---

## Developer Notes

### General Explanation
At least one image on the production site loads from `dev-launchpadlab.pantheonsite.io` — a Pantheon development environment URL. This is a deployment hygiene issue: the image was likely uploaded in the dev environment and its absolute URL was stored in the WordPress database, then carried through to production without being updated.

### Where to Look

**1. WordPress database — search for hardcoded dev URLs:**
```sql
-- Find all occurrences in post content
SELECT ID, post_title, post_content
FROM wp_posts
WHERE post_content LIKE '%dev-launchpadlab.pantheonsite.io%';

-- Find all occurrences in post meta (ACF fields, etc.)
SELECT post_id, meta_key, meta_value
FROM wp_postmeta
WHERE meta_value LIKE '%dev-launchpadlab.pantheonsite.io%';

-- Find all occurrences in options
SELECT option_name, option_value
FROM wp_options
WHERE option_value LIKE '%dev-launchpadlab.pantheonsite.io%';
```

**2. Search-and-replace the database:**
```bash
# Using WP-CLI (recommended for Pantheon sites)
wp search-replace 'dev-launchpadlab.pantheonsite.io' 'launchpadlab.com' --all-tables --dry-run
# Review output, then run without --dry-run:
wp search-replace 'dev-launchpadlab.pantheonsite.io' 'launchpadlab.com' --all-tables
```

**3. Theme files — search for hardcoded URLs:**
```bash
grep -rn "dev-launchpadlab" wp-content/themes/
grep -rn "pantheonsite.io" wp-content/themes/
```

**4. Pantheon-specific configuration:**
Ensure `wp-config.php` or a Pantheon `settings.php` file sets the correct `WP_HOME` and `WP_SITEURL` for the production environment:
```php
// wp-config.php or environment-specific config
if (defined('PANTHEON_ENVIRONMENT') && PANTHEON_ENVIRONMENT === 'live') {
    define('WP_HOME', 'https://launchpadlab.com');
    define('WP_SITEURL', 'https://launchpadlab.com');
}
```

### Prevention
Add a deployment step or CI rule to catch dev URLs before they reach production:
```bash
# Pre-deployment check
wp db search 'pantheonsite.io' --all-tables | grep -c 'pantheonsite'
# If count > 0, fail the deployment
```

### Components/Files to Audit
- WordPress `wp_posts` table (post content)
- WordPress `wp_postmeta` table (custom fields, ACF values)
- WordPress `wp_options` table (widget content, theme settings)
- Theme template files (hardcoded image paths)
- Any custom plugin settings storing asset URLs
- Pantheon `wp-config.php` environment configuration

---

## Examples from Other Sites

- **Stripe:** Uses a dedicated CDN (`b.stripecdn.com`) for all production assets. No staging references appear in production HTML.
- **Shopify:** Has automated deployment pipelines that run a URL validation step, rejecting deployments containing non-production hostnames.
- **WordPress VIP:** Enforces environment-specific URL rewriting at the platform level, ensuring database-stored URLs are always rewritten to match the current environment's domain.

---

## Additional Context

This issue often surfaces when using Pantheon's multidev workflow, where content is created in dev/staging environments and the database is promoted to production. The `wp search-replace` command is the standard fix. Consider adding this as a recurring deployment step to prevent future regressions.
