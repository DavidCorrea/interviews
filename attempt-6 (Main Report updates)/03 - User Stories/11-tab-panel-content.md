# Tab Panel Content Accessibility

## Priority
**Medium**

## User Story
As a screen reader user interacting with the homepage tabbed interface, I want only the active tab's content to be exposed in the accessibility tree, so that I am not distracted by hidden content or confused by empty panels.

## Acceptance Criteria

- [ ] Non-selected tabpanels have `hidden` attribute or `aria-hidden="true"`
- [ ] Tab content is contained within `<div role="tabpanel">` elements
- [ ] Tab activation correctly shows/hides panels via `hidden` or `aria-hidden`
- [ ] Only active tab content is exposed in the accessibility tree
- [ ] Tabs follow WAI-ARIA tabs pattern: `tablist`, `tab`, `tabpanel`, `aria-selected`, `aria-controls`, `aria-labelledby`
- [ ] Keyboard navigation works: Arrow keys move between tabs, Tab moves focus into the active panel
- [ ] No empty panels are announced to screen readers

## How to Test

1. Open https://launchpadlab.com/ and locate the tabbed interface on the homepage.
2. Use a screen reader: navigate to the tab list and verify only the active tab is announced as selected.
3. Inspect the accessibility tree (Chrome DevTools > Elements > Accessibility) — verify inactive tabpanels are hidden.
4. Tab through the interface: verify focus moves between tabs, then into the active panel content.
5. Use arrow keys to switch tabs — verify only the active panel's content is visible and exposed.
6. Verify no inactive panel content is visible in the DOM or accessibility tree when not selected.
7. Test with VoiceOver (macOS) and NVDA (Windows) for full coverage.

## Developer Notes

### General Explanation
The homepage tabbed interface exposes all tab content simultaneously in the accessibility tree OR shows empty panels. ARIA tab pattern implementation is incorrect. Screen readers expect only the active tab's content to be exposed; inactive tabs should be hidden.

**Solution:** Follow the WAI-ARIA tabs pattern. Non-selected tabpanels should have `hidden` attribute or `aria-hidden="true"`. Content must be within `tabpanel` elements. Tab activation should show/hide panels correctly.

### Code Examples

**Correct WAI-ARIA tabs pattern:**
```html
<div class="tabs">
  <div role="tablist" aria-label="Content sections">
    <button
      role="tab"
      id="tab-1"
      aria-selected="true"
      aria-controls="panel-1"
      aria-labelledby="tab-1-label"
      tabindex="0"
    >
      <span id="tab-1-label">Section 1</span>
    </button>
    <button
      role="tab"
      id="tab-2"
      aria-selected="false"
      aria-controls="panel-2"
      aria-labelledby="tab-2-label"
      tabindex="-1"
    >
      <span id="tab-2-label">Section 2</span>
    </button>
    <button
      role="tab"
      id="tab-3"
      aria-selected="false"
      aria-controls="panel-3"
      aria-labelledby="tab-3-label"
      tabindex="-1"
    >
      <span id="tab-3-label">Section 3</span>
    </button>
  </div>
  <div
    role="tabpanel"
    id="panel-1"
    aria-labelledby="tab-1-label"
  >
    Content for section 1
  </div>
  <div
    role="tabpanel"
    id="panel-2"
    aria-labelledby="tab-2-label"
    hidden
  >
    Content for section 2
  </div>
  <div
    role="tabpanel"
    id="panel-3"
    aria-labelledby="tab-3-label"
    hidden
  >
    Content for section 3
  </div>
</div>
```

**JavaScript for tab switching:**
```javascript
const tabs = document.querySelectorAll('[role="tab"]');
const panels = document.querySelectorAll('[role="tabpanel"]');

tabs.forEach((tab, index) => {
  tab.addEventListener('click', () => selectTab(index));
  tab.addEventListener('keydown', (e) => {
    if (e.key === 'ArrowRight') selectTab((index + 1) % tabs.length);
    if (e.key === 'ArrowLeft') selectTab((index - 1 + tabs.length) % tabs.length);
  });
});

function selectTab(index) {
  tabs.forEach((t, i) => {
    t.setAttribute('aria-selected', i === index);
    t.setAttribute('tabindex', i === index ? 0 : -1);
  });
  panels.forEach((p, i) => {
    p.hidden = i !== index;
  });
}
```

**React example:**
```jsx
const Tabs = ({ items }) => {
  const [activeIndex, setActiveIndex] = useState(0);

  return (
    <div className="tabs">
      <div role="tablist" aria-label="Content sections">
        {items.map((item, i) => (
          <button
            key={i}
            role="tab"
            id={`tab-${i}`}
            aria-selected={i === activeIndex}
            aria-controls={`panel-${i}`}
            tabIndex={i === activeIndex ? 0 : -1}
            onClick={() => setActiveIndex(i)}
          >
            {item.label}
          </button>
        ))}
      </div>
      {items.map((item, i) => (
        <div
          key={i}
          role="tabpanel"
          id={`panel-${i}`}
          aria-labelledby={`tab-${i}`}
          hidden={i !== activeIndex}
        >
          {item.content}
        </div>
      ))}
    </div>
  );
};
```

### Components to Audit
- Homepage tabbed interface component
- Any tab or accordion components
- Third-party tab libraries (e.g., Radix UI, Reach UI)

## Examples from Other Sites

- **W3C WAI-ARIA Tabs Pattern** — https://www.w3.org/WAI/ARIA/apg/patterns/tabs/ — Official reference implementation with full keyboard support and correct ARIA attributes.
- **Reach UI Tabs** — Accessible tab component that handles focus management, keyboard navigation, and ARIA attributes correctly out of the box.
