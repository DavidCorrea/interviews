# AI-02: Add Skip Links Site-Wide

## Metadata
- **ID:** AI-02
- **Priority:** 1 Critical
- **Personas Affected:** 13 of 16 personas
- **WCAG Criteria:** 2.4.1 Bypass Blocks (A)
- **Effort:** Small (1–2 hours)

---

## User Story

**As a** keyboard or screen reader user visiting LaunchPad Lab,

**I want** a "Skip to main content" link that appears as the first focusable element on every page,

**So that** I can bypass repeated navigation and jump directly to the main content without tabbing through the entire header and menu.

---

## Acceptance Criteria

- [ ] "Skip to main content" link is the first focusable element on every page
- [ ] Skip link is visible when focused (not hidden or invisible)
- [ ] Skip link has high-contrast styling when focused (e.g., dark background, light text)
- [ ] Activating the skip link moves focus to the main content area
- [ ] On the Contact page, a second skip link "Skip to contact form" is present
- [ ] "Skip to contact form" moves focus to the contact form (first form field or form container)
- [ ] Skip links are positioned off-screen until focused (or always visible; off-screen is common)
- [ ] Skip links work on all pages: Home, About, Services, Contact, Blog, etc.

---

## Test Plan

### Keyboard Testing
1. Navigate to `https://launchpadlab.com/` and press Tab once
2. **Expected:** First focused element is the skip link; it becomes visible (e.g., appears at top of viewport)
3. Press Enter to activate the skip link
4. **Expected:** Focus moves to `<main>` or main content; focus ring visible on main or first heading
5. Navigate to `/contact` and press Tab
6. **Expected:** First focus is "Skip to main content"; second focus is "Skip to contact form" (or similar)
7. Activate "Skip to contact form"
8. **Expected:** Focus moves to the contact form (first input or the form itself)

### Screen Reader Testing
1. With VoiceOver or NVDA, load the homepage
2. Navigate by links (VoiceOver: VO+Command+L) — skip link should be first
3. Activate skip link — verify announcement indicates focus moved to main content
4. On Contact page, verify both skip links are announced and functional

### Visual Testing
1. Tab to skip link — verify it appears with clear, high-contrast styling
2. Verify skip link is not visible when not focused (if using off-screen technique)
3. Verify skip link does not cause layout shift when focused

### Cross-Page Testing
- Test on: Home, About, Services, Contact, Blog (if applicable)
- Ensure skip link is present and first on every page template

---

## Developer Notes

### HTML
Add before the `<header>` or first navigation element:

```html
<a href="#main-content" class="skip-link">Skip to main content</a>
```

Ensure `<main>` has the matching ID:

```html
<main id="main-content">
```

On the Contact page, add a second skip link after the first:

```html
<a href="#contact-form" class="skip-link">Skip to contact form</a>
```

And add `id="contact-form"` to the form or its wrapper.

### CSS
```css
.skip-link {
  position: absolute;
  top: -40px;
  left: 0;
  padding: 8px 16px;
  background: #000;
  color: #fff;
  text-decoration: none;
  font-weight: 600;
  z-index: 10000;
  transition: top 0.2s ease;
}

.skip-link:focus {
  top: 0;
  outline: 2px solid #fff;
  outline-offset: 2px;
}
```

### Considerations
- Use `position: absolute` so the link doesn't affect layout when off-screen
- Ensure `z-index` is high enough to appear above header/nav
- Do not use `display: none` or `visibility: hidden` on the skip link — screen readers and keyboard users must be able to focus it
- If using a single-page app (SPA), ensure skip links work after client-side navigation; may need to update `href` or use `focus()` in JS

### Files to Modify
- Global layout/template (e.g., `Layout.tsx`, `_app.tsx`, `header.html`, or base template)
- Contact page template (for second skip link)
- Global CSS or component styles

---

## Examples

| Site | Approach |
|------|----------|
| **GitHub.com** | Visible skip link on Tab; "Skip to content" appears at top |
| **GOV.UK** | Prominent skip links; "Skip to main content" standard across all pages |
| **WebAIM.org** | Skip link as first focusable; well-documented pattern |
| **W3C.org** | Skip to main content; follows WCAG 2.4.1 guidance |
