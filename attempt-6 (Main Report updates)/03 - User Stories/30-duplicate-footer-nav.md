# Duplicate Footer Navigation

## Priority
**Low**

## User Story
As a screen reader user, I want the header and footer navigation to be clearly differentiated, so that when I encounter the same links twice I understand which landmark I am in and can skip redundant content if desired.

## Acceptance Criteria

- [ ] Header `<nav>` has `aria-label="Main navigation"` (or equivalent descriptive label)
- [ ] Footer `<nav>` has `aria-label="Footer navigation"` (or equivalent descriptive label)
- [ ] Labels are unique and descriptive — not generic like "Navigation"
- [ ] Screen reader users can distinguish between the two nav landmarks when navigating by landmarks
- [ ] No duplicate or conflicting `aria-label` values between header and footer nav
- [ ] If multiple navs exist in header/footer, each has a distinct label

## How to Test

1. Navigate to https://launchpadlab.com/.
2. Inspect the header — locate the `<nav>` element and verify it has `aria-label`.
3. Inspect the footer — locate the `<nav>` element and verify it has a different `aria-label`.
4. Use a screen reader's landmark navigation (e.g., VoiceOver rotor, NVDA landmark list).
5. Verify "Main navigation" and "Footer navigation" (or similar) appear as distinct landmarks.
6. Navigate between landmarks — confirm the labels are announced and distinguishable.
7. Check that no other `<nav>` elements lack `aria-label` when multiple navs exist on the page.

## Developer Notes

### General Explanation
The footer has navigation that mirrors the header nav. Two `<nav>` elements lack `aria-label` differentiation. Screen readers encounter the same links twice and cannot easily distinguish which landmark they are in. Adding unique `aria-label` values helps users understand context and skip redundant content.

**Solution:** Add `aria-label` to both `<nav>` elements. Use descriptive, unique labels such as "Main navigation" for the header and "Footer navigation" for the footer. This follows WAI-ARIA Authoring Practices for multiple navigation landmarks.

### Code Examples

**Header and footer with distinct labels:**
```html
<header>
  <nav aria-label="Main navigation">
    <ul>
      <li><a href="/services">Services</a></li>
      <li><a href="/about">About</a></li>
      <li><a href="/contact">Contact</a></li>
    </ul>
  </nav>
</header>

<main>
  <!-- page content -->
</main>

<footer>
  <nav aria-label="Footer navigation">
    <ul>
      <li><a href="/services">Services</a></li>
      <li><a href="/about">About</a></li>
      <li><a href="/contact">Contact</a></li>
    </ul>
  </nav>
</footer>
```

**React layout:**
```jsx
<>
  <header>
    <nav aria-label="Main navigation">
      <NavigationLinks />
    </nav>
  </header>
  <main>{children}</main>
  <footer>
    <nav aria-label="Footer navigation">
      <NavigationLinks />
    </nav>
  </footer>
</>
```

**Alternative labels (choose based on content):**
```html
<nav aria-label="Primary navigation">...</nav>
<nav aria-label="Site footer links">...</nav>
```

**When multiple navs exist in one region:**
```html
<footer>
  <nav aria-label="Footer services">
    <a href="/services">Services</a>
  </nav>
  <nav aria-label="Footer company">
    <a href="/about">About</a>
    <a href="/contact">Contact</a>
  </nav>
</footer>
```

### Components to Audit
- Header component
- Footer component
- Shared navigation component (used in both header and footer)
- Layout/wrapper components that render header and footer

## Examples from Other Sites

- **BBC.com** — Clearly labeled navigation landmarks: "Main navigation," "Footer navigation," etc. Screen reader users can distinguish between them.
- **GitHub.com** — Different `aria-label` values for header and footer navs. Follows WAI-ARIA best practices.
- **GOV.UK** — Uses descriptive `aria-label` for all navigation regions to avoid ambiguity.
