# M-32: Tabbed Interface Spatial Separation

**Issue ID:** M-32
**Priority:** Medium
**WCAG Criteria:** 1.3.2 Meaningful Sequence (A), 1.4.10 Reflow (AA)
**Affected Personas:** Low Vision Screen Magnifier

---

## User Story

**As a** low-vision user browsing with a screen magnifier at 200%+ zoom,
**I want** the "Problems We Solve" tab labels and their corresponding content to remain visually associated at high magnification,
**so that** I can see which tab is selected and its content without having to pan back and forth across the screen.

---

## Acceptance Criteria

- [ ] At 200% browser zoom (viewport equivalent of 640px), the tab labels and tab content reflow into a stacked (vertical) layout rather than remaining side-by-side.
- [ ] At 300%+ zoom, both the tab labels and the active tab's content are visible within a single scrollable column — no horizontal scrolling required.
- [ ] The visual association between a selected tab and its content is clear at all zoom levels (e.g., the active tab visually connects to its panel via background color, border, or proximity).
- [ ] The tab order remains logical: tab labels come first, followed by the active panel content, at all viewport sizes.
- [ ] The active tab's `aria-selected="true"` and the panel's `aria-labelledby` relationship remain intact regardless of layout changes.
- [ ] No content is clipped, hidden, or overlapping at zoom levels up to 400%.

---

## How to Test the Change

### Manual Testing

1. **Browser zoom test:** On a 1280px monitor, zoom to 200%, 300%, and 400%. Navigate to the "Problems We Solve" section. Confirm the tabs and content stack vertically and are fully readable without horizontal scrolling.
2. **Screen magnifier test:** Using ZoomText, macOS Zoom, or Windows Magnifier at 200%+, navigate to the tabbed section. Confirm you can see the selected tab label and its content without panning horizontally.
3. **Narrow viewport test:** In Chrome DevTools responsive mode, set viewport to 320px wide. Confirm the tabbed interface reflows to a fully vertical layout.
4. **Association test:** At 300% zoom, click different tabs. Confirm you can always tell which tab is active and which content belongs to it (visual connection is clear).
5. **Keyboard test:** At 200%+ zoom, use arrow keys to navigate between tabs. Confirm the active panel content updates and remains visible near the active tab.

### Automated Testing

```javascript
// At narrow viewport, verify tab list and panels stack vertically
await page.setViewportSize({ width: 320, height: 900 });
const tabList = await page.locator('[role="tablist"]').boundingBox();
const firstPanel = await page.locator('[role="tabpanel"]:visible').boundingBox();
console.assert(
  firstPanel.y > tabList.y + tabList.height,
  'Tab panel should be below the tab list at narrow viewport'
);
```

---

## Developer Notes

### General Explanation

The "Problems We Solve" section uses a side-by-side layout: tab labels on the left, tab content (text + image) on the right. At 100% zoom, this works well. But at 200%+ magnification (or on narrow viewports), the user's visible area can only show one "column" at a time. This forces magnifier users to pan left to see which tab is selected, then pan right to read the content — destroying the visual relationship between the tab and its panel.

The fix is to make the layout responsive so that at high zoom levels (or narrow viewports), the tabs stack above their content in a single vertical column.

### Current State (Problem)

```css
.tabs-container {
  display: flex;
  flex-direction: row; /* Side-by-side at all sizes */
}

.tab-list {
  width: 30%;
  flex-shrink: 0;
}

.tab-content {
  width: 70%;
}
```

At 200% zoom on a 1280px monitor (effective 640px), the two columns are squeezed into 192px + 448px — too narrow to read comfortably, and the tab list may overflow.

### Recommended Fix — Responsive Stacking

```css
.tabs-container {
  display: flex;
  flex-direction: column; /* Mobile-first: vertical stack */
}

.tab-list {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  gap: 4px;
}

.tab-content {
  width: 100%;
}

/* Side-by-side only when enough space is available */
@media (min-width: 768px) {
  .tabs-container {
    flex-direction: row;
  }

  .tab-list {
    width: 30%;
    flex-direction: column;
    flex-shrink: 0;
  }

  .tab-content {
    width: 70%;
  }
}
```

### Alternative: Accordion Pattern at Narrow Viewports

Convert the tabbed interface to an accordion at narrow viewports. This is a well-established responsive pattern that naturally pairs labels with content:

```html
<!-- Stacked accordion at narrow viewports -->
<div class="tabs-responsive">
  <!-- Shown at narrow viewports, hidden at wide -->
  <div class="accordion-item">
    <button class="accordion-trigger" aria-expanded="true">
      Digital Transformation
    </button>
    <div class="accordion-panel">
      <p>We help companies modernize...</p>
    </div>
  </div>
  <div class="accordion-item">
    <button class="accordion-trigger" aria-expanded="false">
      AI Integration
    </button>
    <div class="accordion-panel" hidden>
      <p>Leverage artificial intelligence...</p>
    </div>
  </div>
</div>
```

```css
/* Show accordion, hide tabs at narrow viewports */
@media (max-width: 767px) {
  [role="tablist"] { display: none; }
  .accordion-item { display: block; }
}

@media (min-width: 768px) {
  .accordion-item { display: none; }
  [role="tablist"] { display: flex; }
}
```

### Visual Association at All Zoom Levels

Ensure the active tab visually "connects" to its content:

```css
/* Active tab shares background with panel */
[role="tab"][aria-selected="true"] {
  background-color: #f5f5f5;
  border-bottom: none; /* or border merges with panel */
}

[role="tabpanel"] {
  background-color: #f5f5f5;
  border-top: 3px solid var(--color-primary);
}
```

### Components / Files to Audit

- "Problems We Solve" section CSS (flex/grid layout for `.tabs-container`)
- Tab list and tab panel HTML structure
- JavaScript tab switching logic (must work in both horizontal and stacked layouts)
- Any responsive breakpoints that affect this section
- ARIA attributes (`role="tablist"`, `role="tab"`, `role="tabpanel"`, `aria-selected`, `aria-labelledby`)

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **Salesforce Lightning Design System** | Tabs switch from horizontal to vertical stacking below 768px; accordion variant is recommended for mobile | Official design system provides a canonical responsive tabs pattern. |
| **GOV.UK** | Tabs component collapses to an accordion at narrow viewports (tabs-to-accordion pattern) | Content and label are always adjacent, regardless of viewport size. |
| **Material Design (Google)** | Tabs use scrollable tab bar at narrow widths; panel content always appears directly below the tab row | Vertical stacking ensures label-to-content association is maintained. |
| **BBC** | Tabbed content on feature pages reflows to a single column at small screens, with each tab's heading preceding its content | Simple, effective reflow that preserves reading order. |
