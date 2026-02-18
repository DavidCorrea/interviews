# L-61: Inconsistent Stats (12+ vs 13+ Years)

**Issue ID:** L-61
**Priority:** Low
**WCAG Criteria:** N/A (content accuracy concern)
**Affected Personas:** Skeptical User

---

## User Story

As a **skeptical prospective client** comparing LaunchPad Lab against competitors, I want the company's statistics to be consistent across all pages so that I can trust the data being presented and don't question whether the company pays attention to its own content accuracy.

---

## Acceptance Criteria

- [ ] The "years in business" statistic displays the same value on every page where it appears (homepage, about page, and any other location).
- [ ] The value is factually accurate based on the company's actual founding year.
- [ ] If the stat uses a "+" qualifier (e.g., "13+ Years"), the same qualifier format is used everywhere.
- [ ] All other numerical statistics (projects delivered, team members, etc.) are also cross-checked for consistency across pages.
- [ ] A single source of truth exists for statistics values — either a CMS field, a shared template partial, or a constants file — so that updates propagate site-wide automatically.

---

## How to Test the Change

### Manual Testing
1. Navigate to the **homepage** and note the "Years in Business" (or equivalent) statistic.
2. Navigate to the **About page** and note the same statistic.
3. Check any other pages that display company statistics (services pages, case study summaries).
4. Confirm the value is identical everywhere.
5. Verify the number is accurate: if the company was founded in 2012, and it is now 2026, the stat should read "14+ Years" or similar.
6. Cross-check all other stats (projects count, team size, etc.) for cross-page consistency.

### Automated Testing
1. Scrape statistics from multiple pages and compare:
   ```javascript
   // Playwright example
   const pages = ['/', '/about/', '/services/'];
   const stats = {};

   for (const path of pages) {
     await page.goto(`https://launchpadlab.com${path}`);
     const yearsStat = await page.$eval(
       '.stat-years, [data-stat="years"]',
       el => el.textContent.trim()
     ).catch(() => null);
     if (yearsStat) stats[path] = yearsStat;
   }

   const values = Object.values(stats);
   const allSame = values.every(v => v === values[0]);
   expect(allSame).toBe(true);
   ```
2. Add a content lint rule to CI that extracts all numerical statistics from rendered pages and flags mismatches.

---

## Developer Notes

### General Explanation
The homepage displays "12+ Years" while the About page displays "13+ Years in Business." This inconsistency is likely caused by one page being updated while the other was missed. The root cause is having the same data hardcoded in multiple locations rather than pulling from a single source.

### Recommended Fix

**Option A: WordPress ACF options page (single source of truth):**
```php
// In functions.php — register an ACF options page for company stats
if (function_exists('acf_add_options_page')) {
    acf_add_options_page(array(
        'page_title' => 'Company Statistics',
        'menu_title' => 'Company Stats',
        'menu_slug'  => 'company-stats',
    ));
}
```

```php
// In any template — pull from the single source
<span class="stat-value"><?php echo get_field('years_in_business', 'option'); ?>+</span>
<span class="stat-label">Years in Business</span>
```

**Option B: Auto-calculate from founding year:**
```php
<?php
$founding_year = 2012; // Set once
$years = date('Y') - $founding_year;
?>
<span class="stat-value"><?php echo $years; ?>+</span>
<span class="stat-label">Years in Business</span>
```

This approach ensures the number is always correct and never needs manual updating.

**Option C: WordPress shortcode for reuse:**
```php
// In functions.php
function lpl_years_in_business_shortcode() {
    $founding_year = 2012;
    $years = date('Y') - $founding_year;
    return $years . '+';
}
add_shortcode('years_in_business', 'lpl_years_in_business_shortcode');
```

Usage in any page/template: `[years_in_business] Years in Business`

### Components/Files to Audit
- Homepage template (`front-page.php` or equivalent)
- About page template or WordPress page content
- Any template partial rendering statistics (e.g., `stats-section.php`)
- WordPress page content in the block/classic editor (for hardcoded values)
- ACF field groups associated with statistics sections

---

## Examples from Other Sites

- **Thoughtbot:** Uses a single "About" page as the canonical source for all company statistics. The homepage links to it rather than duplicating figures.
- **Basecamp:** Displays a single, dynamically calculated customer count across all marketing pages using a shared data source.
- **Stripe:** Company statistics (processing volume, number of businesses) are maintained in a centralized content system and syndicated to all pages where they appear.

---

## Additional Context

Beyond fixing the immediate inconsistency, the real value is implementing a single source of truth for company statistics. This prevents future drift as the site grows and ensures that when the "years in business" number changes, it updates automatically everywhere. The auto-calculate approach (Option B) is the most future-proof since it never needs manual intervention.
