# Heading Hierarchy Issues

## Priority
**Medium**

## User Story
As a screen reader user who navigates by headings, I want statistics like "Years in Business," "Projects," and "Clients" to be marked as content rather than section headings, so that I can efficiently skim the page structure and find actual sections without wading through inflated heading counts.

## Acceptance Criteria

- [ ] Statistics (Years in Business, Projects, Clients, etc.) are not marked with `<h1>`, `<h2>`, or other heading tags
- [ ] Stats use semantic alternatives: `<p>`, `<span>`, or `<dl>` definition lists
- [ ] Heading hierarchy is logical and sequential (no skipped levels: h1 → h2 → h3)
- [ ] Screen reader heading navigation shows only actual section titles, not stat labels
- [ ] Each page has a single `<h1>` for the main page title
- [ ] All pages have been audited for heading misuse

## How to Test

1. Open https://launchpadlab.com/ and navigate to the homepage.
2. Use a screen reader: enable heading navigation (VoiceOver: VO+U, then "Headings"; NVDA: Insert+F7).
3. Step through headings — verify "Years in Business," "Projects," "Clients" do not appear as headings.
4. Inspect the DOM: search for `<h2>` elements and verify none wrap stat labels.
5. Use browser DevTools or axe DevTools to run an accessibility audit — check for heading-related violations.
6. Repeat on other key pages (About, Services, Our Work, Contact).
7. Verify heading count is reasonable (e.g., homepage should not have 20+ headings).

## Developer Notes

### General Explanation
Statistics like "Years in Business," "Projects," and "Clients" are data labels, not document sections. Using heading tags for them inflates the heading count and confuses users who rely on heading navigation to understand page structure. Screen readers announce "heading level 2" for each, which creates noise and makes it harder to find actual sections.

**Solution:** Replace heading tags on stats with appropriate semantic elements. Reserve headings for actual section titles. Use `<dl>`, `<dt>`, `<dd>` for definition-style data (label + value), or simple `<p>`/`<span>` for inline stats.

### Code Examples

**Before (incorrect):**
```html
<h2>Years in Business</h2>
<p>15</p>
<h2>Projects</h2>
<p>200+</p>
<h2>Clients</h2>
<p>50+</p>
```

**After (correct):**
```html
<dl class="stats">
  <dt>Years in Business</dt>
  <dd>15</dd>
  <dt>Projects</dt>
  <dd>200+</dd>
  <dt>Clients</dt>
  <dd>50+</dd>
</dl>
```

**Alternative with semantic HTML:**
```html
<div class="stats" aria-label="Company statistics">
  <p><span class="stat-label">Years in Business</span> <span class="stat-value">15</span></p>
  <p><span class="stat-label">Projects</span> <span class="stat-value">200+</span></p>
  <p><span class="stat-label">Clients</span> <span class="stat-value">50+</span></p>
</div>
```

**React example:**
```jsx
const Stats = ({ items }) => (
  <dl className="stats" aria-label="Company statistics">
    {items.map(({ label, value }) => (
      <div key={label}>
        <dt>{label}</dt>
        <dd>{value}</dd>
      </div>
    ))}
  </dl>
);
```

### Components to Audit
- Homepage stats section
- Hero or banner components
- About page statistics
- Footer sections
- Any reusable component that displays key metrics
- All page templates

## Examples from Other Sites

- **Gov.uk** — Exemplary heading hierarchy. Section titles use headings; data and statistics use semantic markup. Heading navigation is clean and predictable.
- **MDN Web Docs** — Clean heading structure. Stats and metrics are not headings; document structure is clearly delineated with headings.
