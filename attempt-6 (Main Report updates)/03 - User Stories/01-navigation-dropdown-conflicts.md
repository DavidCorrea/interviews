# Navigation Dropdown Conflicts

## Priority
**High**

## User Story
As a keyboard and mouse user, I want predictable navigation behavior when interacting with top-level menu items, so that I can reliably access the pages I intend without being sent to unexpected destinations.

## Acceptance Criteria

- [ ] Top-level nav items ("Services," "Industries") have a clear visual distinction between the dropdown trigger and the page link
- [ ] Clicking the text link navigates to the parent/overview page consistently
- [ ] Clicking a chevron or dropdown icon opens/closes the dropdown without navigation
- [ ] Repeated clicks produce consistent behavior (no random page navigation)
- [ ] Keyboard users can tab to both the link and the dropdown trigger separately
- [ ] Screen reader users hear clear labels for both the link and the dropdown control
- [ ] Dropdown opens on Enter/Space when focus is on the trigger, not on the link

## How to Test

1. Open https://launchpadlab.com/ and navigate to the main header.
2. Click "Services" once — observe whether a dropdown opens or a page loads.
3. Click "Services" again — verify behavior is identical to step 2.
4. Click "Industries" — repeat the same sequence.
5. Use keyboard only: Tab to "Services," press Enter; note whether navigation or dropdown occurs.
6. Tab to the chevron (if present) and press Enter; verify dropdown opens.
7. Repeat steps 2–6 across multiple browsers (Chrome, Firefox, Safari).
8. Test with a screen reader (VoiceOver or NVDA) to confirm announced behavior matches expectations.

## Developer Notes

### General Explanation
The issue stems from combining the dropdown trigger and the page link into a single interactive element. When both behaviors are wired to the same click target, the browser and/or JavaScript may fire inconsistently or race with each other, causing unpredictable navigation or dropdown state.

**Solution:** Separate the dropdown trigger from the page link. Use a chevron icon (or similar) as the sole dropdown trigger. The text link should navigate to the parent page (e.g., `/services/` or `/industries/`). This follows the WAI-ARIA pattern for disclosure widgets.

### Code Examples

**HTML structure:**
```html
<nav aria-label="Main navigation">
  <ul>
    <li>
      <a href="/services/">Services</a>
      <button type="button" aria-expanded="false" aria-controls="services-menu" aria-haspopup="true">
        <span class="visually-hidden">Toggle Services menu</span>
        <svg aria-hidden="true" role="img"><!-- chevron icon --></svg>
      </button>
      <ul id="services-menu" role="menu" hidden>
        <li><a href="/services/ai-automation-agentforce/" role="menuitem">AI Automation</a></li>
        <li><a href="/services/custom-software/" role="menuitem">Custom Software</a></li>
        <!-- ... -->
      </ul>
    </li>
  </ul>
</nav>
```

**React example:**
```jsx
const NavItem = ({ label, href, children }) => {
  const [expanded, setExpanded] = useState(false);
  const menuId = `${label.toLowerCase().replace(/\s/g, '-')}-menu`;

  return (
    <li>
      <a href={href}>{label}</a>
      <button
        type="button"
        aria-expanded={expanded}
        aria-controls={menuId}
        aria-haspopup="true"
        onClick={() => setExpanded(!expanded)}
      >
        <span className="visually-hidden">Toggle {label} menu</span>
        <ChevronIcon aria-hidden />
      </button>
      <ul id={menuId} role="menu" hidden={!expanded}>
        {children}
      </ul>
    </li>
  );
};
```

**CSS for chevron:**
```css
.nav-item button {
  position: relative;
  padding: 0.5rem;
  background: none;
  border: none;
  cursor: pointer;
}
.nav-item button[aria-expanded="true"] svg {
  transform: rotate(180deg);
}
```

### Components to Audit
- Main header component
- Navigation component
- Menu/dropdown component
- Any global click handlers that might intercept nav events
- Any third-party navigation library

## Examples from Other Sites

- **Stripe.com** — Clean hover dropdowns with clear separation between parent link and submenu. Clicking "Products" navigates to the products overview page; hovering over the dropdown area reveals sub-items without navigation.
- **GitHub.com** — Top nav uses dropdown toggles (chevrons) separate from links. "Product" links to `/features`; the chevron opens the dropdown menu.
