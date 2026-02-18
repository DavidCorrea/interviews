# Remove or Hide Empty Structural Elements from Accessibility Tree

## Priority: Low

## User Story
As a screen reader user, I want empty structural elements to be hidden from the accessibility tree so that I don't encounter meaningless navigation stops while browsing.

## Acceptance Criteria
- [ ] All empty `<li>`, `<p>`, and `<div>` elements that serve no content purpose are either removed or hidden from the accessibility tree
- [ ] Screen reader users do not encounter empty list items or paragraphs when navigating by list or heading
- [ ] Empty elements used for layout/spacing are hidden from assistive technology
- [ ] No meaningless "list item" or "paragraph" announcements for empty content

## Developer Notes

### General Explanation
Empty structural elements (e.g., `<li>`, `<p>`, `<div>`) that are exposed in the accessibility tree create unnecessary stops during screen reader navigation. Users hear "list item" or "paragraph" with no content. Options: remove them entirely, add `aria-hidden="true"`, or use `role="presentation"` / `role="none"`. If empty elements serve layout (e.g., spacers), they should be hidden from assistive technology.

### Code Examples

**Option 1: Remove empty elements**
```html
<!-- Before: empty list item exposed to screen readers -->
<ul>
  <li>Client A</li>
  <li></li>
  <li>Client B</li>
</ul>

<!-- After: remove the empty item -->
<ul>
  <li>Client A</li>
  <li>Client B</li>
</ul>
```

**Option 2: Hide with aria-hidden**
```html
<!-- When element must remain for layout/CSS -->
<li aria-hidden="true"></li>
<p aria-hidden="true"></p>
```

**Option 3: Use role="presentation" or role="none"**
```html
<!-- Removes semantic meaning from the element -->
<li role="presentation"></li>
```

**Note:** `aria-hidden="true"` hides the element and its descendants from the accessibility tree. Use when the element is purely decorative or structural.

### Components to Audit
- Homepage client logos section (empty paragraphs in list items)
- Any list or content component with spacer elements
- Grid/flex layouts that use empty divs for alignment
- Carousel or slider components with placeholder items
- Template-driven content that may render empty containers

## Examples From Other Sites
- **Material UI:** Uses `aria-hidden="true"` on decorative spacer elements and layout divs that have no semantic content
- **Chakra UI:** Hides empty layout wrappers from the accessibility tree; spacer components are marked with `role="presentation"` or `aria-hidden` when they serve only visual purpose

## References
- Main Report Item 17
- WCAG 1.3.1 Info and Relationships
