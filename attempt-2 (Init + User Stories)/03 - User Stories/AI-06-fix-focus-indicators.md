# AI-06: Fix Focus Indicators

## Title
Ensure all interactive elements have visible focus indicators with 3:1 contrast

## User Story
As a **keyboard user**, I want **every focusable element to show a clear, visible focus indicator**, so that **I can see where my focus is at all times and navigate the site effectively without a mouse**.

## Acceptance Criteria

- [ ] All focusable elements (links, buttons, form fields, cards) show a visible focus indicator
- [ ] Focus indicator has at least 3:1 contrast against adjacent colors
- [ ] Focus indicator is at least 2px thick
- [ ] No focusable element has `outline: none` without a visible replacement
- [ ] Focus indicators are visible on all pages and components
- [ ] Focus order follows a logical sequence

## How to Test

1. Navigate to `https://launchpadlab.com/`
2. Use **Tab** to move through every focusable element on each page
3. Verify each element shows a visible outline or focus ring when focused
4. Check: links, buttons, form fields, navigation items, cards, and any other interactive elements
5. Verify the focus indicator has 3:1 contrast against adjacent background/foreground colors
6. Test on Home, About, Contact, Blog, and other key pages
7. Ensure no element receives focus without showing a visible indicator

## Developer Notes

- Add global CSS for focus indicators:
  ```css
  :focus-visible {
    outline: 2px solid #000;
    outline-offset: 2px;
  }
  ```
- Use `:focus-visible` (not `:focus`) to avoid drawing outlines on mouse click when not needed
- Remove or replace any `outline: none` declarations—ensure every focusable element has a visible replacement
- For custom-styled focus, ensure 3:1 contrast:
  ```css
  :focus-visible {
    outline: 2px solid #000;
    outline-offset: 2px;
  }
  /* Or for dark backgrounds */
  .dark :focus-visible {
    outline: 2px solid #fff;
    outline-offset: 2px;
  }
  ```
- Test on: links, buttons, form fields (input, select, textarea), cards with click handlers, and custom interactive components

## WCAG References

- **[2.4.7 Focus Visible (Level AA)](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)**: Any keyboard operable user interface has a mode of operation where the keyboard focus indicator is visible.

## Priority & Effort

| Attribute | Value |
|-----------|-------|
| **Priority** | P1 Critical |
| **Effort Estimate** | Small (1–2 hours) |
