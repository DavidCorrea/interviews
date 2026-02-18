# Add Unique `aria-label` to Duplicate Banner Landmarks

## Priority: Medium

## User Story
As a screen reader user, I want each banner landmark to have a unique label so that I can distinguish between the site header and other banner regions when navigating by landmarks.

## Acceptance Criteria
- [ ] Each `banner` landmark on the page has a unique `aria-label` attribute
- [ ] Screen reader landmark navigation shows distinct labels (e.g., "Site header" vs "Page introduction") instead of duplicate "banner" entries
- [ ] Landmark structure complies with WCAG 1.3.1 (Info and Relationships)
- [ ] Only one primary `banner` exists per page, or all banners are uniquely identifiable

## Developer Notes

### General Explanation
Every page currently has two `banner` landmarks without unique `aria-label` attributes. Screen reader users navigating by landmarks see "banner" twice with no way to distinguish between the site header and the hero section. Add unique labels to each banner, or restructure so the hero is not a banner landmark.

**Recommended approach:**
1. Add `aria-label="Site header"` to the primary banner (site header/nav)
2. Either remove the `banner` role from the secondary hero section or give it a distinct `aria-label` like `aria-label="Page introduction"`
3. Best practice: only one `banner` per page; consider restructuring so the hero is inside `<main>` instead of being a separate banner

### Code Examples

```html
<!-- Primary site header banner -->
<header role="banner" aria-label="Site header">
  <nav aria-label="Main navigation">
    <!-- Site logo, nav links -->
  </nav>
</header>

<!-- Option A: Hero as distinct banner (if it must remain a banner) -->
<section role="banner" aria-label="Page introduction">
  <h1>Welcome to LaunchPad Lab</h1>
  <!-- Hero content -->
</section>

<!-- Option B: Hero inside main (preferred - single banner per page) -->
<main>
  <section aria-label="Page introduction">
    <h1>Welcome to LaunchPad Lab</h1>
    <!-- Hero content -->
  </section>
  <!-- Rest of page content -->
</main>
```

### Components to Audit
- Site header component
- Hero section component
- Page layout template

## Examples From Other Sites
- **MDN Web Docs:** Uses landmark patterns with unique `aria-label` attributes to distinguish multiple regions of the same type
- **W3C WAI Landmark Tutorial:** Recommends one banner per page and demonstrates proper landmark labeling for screen reader navigation

## References
- Main Report Item 13
- WCAG 1.3.1 Info and Relationships
- Website: https://launchpadlab.com/
