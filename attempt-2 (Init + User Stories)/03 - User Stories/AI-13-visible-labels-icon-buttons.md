# AI-13: Visible Labels for Icon-Only Buttons

## User Story

As a **screen reader or voice control user**, I want **all icon-only buttons to display visible text labels**, so that **I can identify and activate them without relying on hidden accessibility attributes**.

## Acceptance Criteria

- [ ] Hamburger menu button displays visible "Menu" text
- [ ] Social icon buttons display visible text (e.g., "LinkedIn", "Twitter")
- [ ] Carousel navigation buttons display visible "Previous" and "Next" text
- [ ] Close buttons display visible "Close" text
- [ ] Every icon button shows visible text next to the icon
- [ ] Voice control user can say "click Menu," "click LinkedIn," "click Next" and correct button activates

## How to Test

1. **Visual test:** Every icon button should display visible text next to the icon
   - Hamburger → "Menu"
   - Social icons → "LinkedIn", "Twitter", etc.
   - Carousel → "Previous", "Next"
   - Close → "Close"

2. **Voice control test:** Use Voice Control (macOS) or Voice Access (Windows)
   - Say "click Menu" → hamburger/menu button activates
   - Say "click LinkedIn" → LinkedIn link/button activates
   - Say "click Next" → carousel next button activates

3. **Screen reader test:** Verify each button is announced with its purpose

## Developer Notes

- Add **visible text** next to each icon — do not rely on `aria-label` alone
- Use layout: `display: inline-flex; align-items: center; gap: 4px;` for icon + text
- Button examples:
  - Hamburger → "Menu"
  - Social icons → "LinkedIn", "Twitter", "GitHub", etc.
  - Carousel → "Previous", "Next"
  - Close → "Close"
- **Do NOT rely on `aria-label` alone** — voice control users need visible text to activate elements
- Consider responsive design: text may be hidden on very small screens, but ensure fallback (e.g., `aria-label` + `sr-only` text for screen readers)

## WCAG References

- **1.1.1 Non-text Content (Level A):** All non-text content that is presented to the user has a text alternative that serves the equivalent purpose.
- **2.5.3 Label in Name (Level A):** For user interface components with labels that include text or images of text, the name contains the text that is presented visually.
- **4.1.2 Name, Role, Value (Level A):** For all user interface components, the name and role can be programmatically determined.

## Priority & Effort

| Priority | Effort Estimate |
|----------|-----------------|
| P2 High | Small–Medium (2–4h) |
