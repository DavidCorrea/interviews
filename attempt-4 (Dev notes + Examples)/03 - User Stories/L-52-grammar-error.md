# L-52: Grammar Error "deliver more better"

**Issue ID:** L-52
**Priority:** Low
**WCAG Criteria:** 3.1.5 Reading Level (AAA)
**Affected Personas:** Non-Native Speaker, Cognitive Disability

---

## User Story

As a **non-native English speaker** visiting the Services mega menu, I want the site copy to use correct grammar so that I can understand the company's offerings without confusion about whether the awkward phrasing is intentional jargon or a mistake.

---

## Acceptance Criteria

- [ ] The phrase "deliver more better" in the Services mega menu description is corrected to grammatically standard English (e.g., "deliver better results," "deliver more value," or "deliver superior outcomes").
- [ ] No other grammatical errors exist in the mega menu description text.
- [ ] The corrected text reads naturally for a non-native English speaker at an intermediate reading level.
- [ ] The fix is deployed across all pages where the mega menu appears (site-wide).

---

## How to Test the Change

### Manual Testing
1. Navigate to [launchpadlab.com](https://launchpadlab.com).
2. Hover over or open the **Services** mega menu in the primary navigation.
3. Read the description text within the mega menu.
4. Confirm the phrase "deliver more better" no longer appears.
5. Confirm the replacement text is grammatically correct and clear.
6. Repeat on at least 3 different pages to verify the mega menu text is consistent site-wide.

### Automated / CI Testing
1. Run a content linter (e.g., `textlint`, `vale`, or `alex`) against the mega menu template or content source.
2. Add a regression test or content lint rule to flag double comparatives (e.g., "more better," "more faster").
3. Example `vale` rule pattern:
   ```yaml
   # .vale/styles/Grammar/DoubleComparative.yml
   extends: existence
   message: "Avoid double comparatives: '%s'"
   level: error
   tokens:
     - 'more better'
     - 'more faster'
     - 'more easier'
   ```

---

## Developer Notes

### General Explanation
This is a simple content fix. The phrase "deliver more better" is a double comparative — a common ESL error that should not appear in production copy. Locate the text in the mega menu template or CMS content field and replace it.

### Where to Look
- **WordPress CMS:** Check the mega menu configuration in **Appearance > Menus** or the custom mega menu plugin/widget settings. The description text may be stored in a menu item's "Description" field.
- **Theme template files:** Search for the string in theme PHP templates:
  ```bash
  grep -r "deliver more better" wp-content/themes/
  ```
- **Database:** If the text is stored in WordPress options or post meta:
  ```sql
  SELECT * FROM wp_options WHERE option_value LIKE '%deliver more better%';
  SELECT * FROM wp_postmeta WHERE meta_value LIKE '%deliver more better%';
  ```

### Code Example
Replace the string wherever found:

```diff
- deliver more better
+ deliver better results
```

Or if in a PHP template:
```php
// Before
<p class="mega-menu-description">We help teams deliver more better products.</p>

// After
<p class="mega-menu-description">We help teams deliver better products, faster.</p>
```

### Components/Files to Audit
- Mega menu template (PHP or plugin config)
- WordPress menu item description fields
- Any hardcoded strings in header template partials
- CMS content fields that feed the navigation

---

## Examples from Other Sites

- **Stripe:** All navigation descriptions use plain, grammatically precise language. E.g., "Explore tools to help you build, test, and launch faster."
- **Mailchimp:** Mega menu descriptions are reviewed by a dedicated content team and adhere to their public [Content Style Guide](https://styleguide.mailchimp.com/).
- **GOV.UK:** The UK government style guide explicitly forbids double comparatives and mandates plain English at a reading age of 9.

---

## Additional Context

This issue is low-severity from a functional standpoint but has outsized impact on **perceived professionalism and trust** — especially for enterprise buyers evaluating the company's attention to detail. A grammar error in the primary navigation is one of the first things visitors encounter.
