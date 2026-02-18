# Fix Heading Hierarchy — Demote Stat Labels and Handle Tab Panel Headings

## Priority: Medium

## User Story
As a screen reader user, I want the heading hierarchy to reflect the actual document structure so that navigating by headings gives me an accurate outline of page content.

## Acceptance Criteria
- [ ] Stat labels ("Years in Business", "Projects", "Clients") are no longer marked as `h2` headings
- [ ] Headings in inactive tab panels are hidden from the accessibility tree (do not appear in heading navigation when panel is not selected)
- [ ] Heading outline matches the logical document structure
- [ ] Visual styling of stat labels is preserved via CSS, not heading elements
- [ ] Complies with WCAG 1.3.1 (Info and Relationships)

## Developer Notes

### General Explanation
Two issues affect the heading hierarchy:

1. **Stat labels:** "Years in Business", "Projects", "Clients" are marked as `h2` headings, which clutters the heading outline and misrepresents document structure. These are labels, not section headings.

2. **Tab panel headings:** `h3` headings inside inactive tab panels appear in heading navigation even when the panel is not selected, inflating the heading list and confusing users.

**Fixes:**
- Replace `h2` on stat labels with `<p>`, `<span>`, or `<div>` with appropriate visual styling (CSS for size, not heading elements)
- For tab panel headings: hide headings in non-selected panels from the accessibility tree using `aria-hidden="true"` on inactive panels, or dynamically add/remove headings when tabs are selected
- Audit all pages for heading levels used purely for visual styling

### Code Examples

```html
<!-- Stat labels: use semantic elements + CSS, not headings -->
<div class="stats-grid">
  <div class="stat">
    <span class="stat-value">15+</span>
    <p class="stat-label">Years in Business</p>
  </div>
  <div class="stat">
    <span class="stat-value">200+</span>
    <p class="stat-label">Projects</p>
  </div>
  <div class="stat">
    <span class="stat-value">100+</span>
    <p class="stat-label">Clients</p>
  </div>
</div>

/* CSS for visual styling */
.stat-label {
  font-size: 1.25rem;
  font-weight: 600;
  /* Match previous h2 appearance */
}
```

```html
<!-- Tab panels: hide inactive content from accessibility tree -->
<div role="tablist">
  <button role="tab" aria-selected="true" aria-controls="panel-1">Tab 1</button>
  <button role="tab" aria-selected="false" aria-controls="panel-2">Tab 2</button>
</div>
<div role="tabpanel" id="panel-1" aria-hidden="false">
  <h3>Panel 1 Heading</h3>
  <!-- Content visible and in a11y tree -->
</div>
<div role="tabpanel" id="panel-2" aria-hidden="true" hidden>
  <h3 aria-hidden="true">Panel 2 Heading</h3>
  <!-- Content hidden from a11y tree when inactive -->
</div>
```

### Components to Audit
- Homepage stats section
- Tablist/tabpanel component
- Any page using headings for decorative or purely visual purposes

## Examples From Other Sites
- **W3C WAI Tabs Pattern:** Demonstrates hiding inactive tab panel content (including headings) from the accessibility tree
- **Smashing Magazine:** Stats sections use `<p>` or `<span>` with CSS for visual hierarchy, not heading elements
- **CSS-Tricks:** Similar approach for stat blocks—semantic markup with styling, avoiding heading misuse

## References
- Main Report Item 15
- WCAG 1.3.1 Info and Relationships
- Website: https://launchpadlab.com/
