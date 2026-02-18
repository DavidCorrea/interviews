# No Mobile Navigation

## Priority
**Medium**

## User Story
As a mobile user visiting the site, I want a hamburger menu or responsive toggle for navigation when the screen is narrow, so that I can access all menu items without overflow or horizontal scrolling.

## Acceptance Criteria

- [ ] A hamburger menu or responsive toggle is implemented for viewports below ~768px
- [ ] The toggle button is keyboard accessible (focusable, activatable with Enter/Space)
- [ ] The toggle has `aria-label="Menu"` or `aria-expanded` to indicate state
- [ ] The mobile drawer/menu traps focus when open (focus management)
- [ ] Focus returns to the toggle button when the menu is closed
- [ ] All seven top-level nav items are accessible within the mobile menu
- [ ] The menu can be closed by activating the toggle again or tapping outside (optional)
- [ ] No horizontal overflow of nav items on small screens

## How to Test

1. Open https://launchpadlab.com/ in a browser.
2. Resize the viewport to mobile width (< 768px) or use DevTools device emulation.
3. Verify a hamburger menu or similar toggle appears.
4. Click/tap the toggle — verify the menu opens and all nav items are visible.
5. Use keyboard only: Tab to the toggle, press Enter — verify menu opens.
6. Tab through menu items — verify focus is trapped within the menu.
7. Close the menu — verify focus returns to the toggle.
8. Test with a screen reader: verify `aria-expanded` and `aria-label` are announced correctly.
9. Test on real mobile devices (iOS Safari, Android Chrome).

## Developer Notes

### General Explanation
Seven top-level nav items with no hamburger menu or responsive toggle detected. Items likely overflow on mobile screens, making navigation difficult or impossible for mobile users.

**Solution:** Implement a responsive hamburger menu for viewports below ~768px. Ensure the toggle button is keyboard-accessible, labeled with `aria-label="Menu"` or `aria-expanded`. The mobile drawer should trap focus when open.

### Code Examples

**Accessible hamburger menu button:**
```html
<button
  type="button"
  aria-label="Menu"
  aria-expanded="false"
  aria-controls="mobile-nav"
  aria-haspopup="true"
  id="menu-toggle"
>
  <span class="hamburger-icon" aria-hidden="true">
    <span class="line"></span>
    <span class="line"></span>
    <span class="line"></span>
  </span>
</button>
<nav id="mobile-nav" aria-label="Mobile navigation" hidden>
  <ul>
    <li><a href="/services/">Services</a></li>
    <li><a href="/industries/">Industries</a></li>
    <!-- ... -->
  </ul>
</nav>
```

**JavaScript for toggle and focus trap:**
```javascript
const toggle = document.getElementById('menu-toggle');
const nav = document.getElementById('mobile-nav');
const focusableElements = nav.querySelectorAll('a, button');

toggle.addEventListener('click', () => {
  const isOpen = nav.hidden;
  nav.hidden = !isOpen;
  toggle.setAttribute('aria-expanded', isOpen);

  if (isOpen) {
    focusableElements[0]?.focus();
    document.addEventListener('keydown', trapFocus);
  } else {
    document.removeEventListener('keydown', trapFocus);
    toggle.focus();
  }
});

function trapFocus(e) {
  if (e.key !== 'Tab') return;
  const first = focusableElements[0];
  const last = focusableElements[focusableElements.length - 1];

  if (e.shiftKey) {
    if (document.activeElement === first) {
      e.preventDefault();
      last.focus();
    }
  } else {
    if (document.activeElement === last) {
      e.preventDefault();
      first.focus();
    }
  }
}
```

**React example:**
```jsx
const MobileNav = () => {
  const [isOpen, setIsOpen] = useState(false);
  const navRef = useRef(null);

  useEffect(() => {
    if (isOpen) {
      const focusable = navRef.current?.querySelectorAll('a, button');
      focusable?.[0]?.focus();
    }
  }, [isOpen]);

  return (
    <>
      <button
        type="button"
        aria-label="Menu"
        aria-expanded={isOpen}
        aria-controls="mobile-nav"
        onClick={() => setIsOpen(!isOpen)}
      >
        <HamburgerIcon />
      </button>
      <nav id="mobile-nav" ref={navRef} hidden={!isOpen}>
        <ul>
          <li><a href="/services/">Services</a></li>
          <li><a href="/industries/">Industries</a></li>
          {/* ... */}
        </ul>
      </nav>
    </>
  );
};
```

**CSS for responsive breakpoint:**
```css
@media (min-width: 768px) {
  .menu-toggle {
    display: none;
  }
  #mobile-nav {
    display: flex;
    hidden: unset;
  }
}

@media (max-width: 767px) {
  .desktop-nav {
    display: none;
  }
  .menu-toggle {
    display: block;
  }
}
```

### Components to Audit
- Main header component
- Navigation component
- Responsive breakpoints
- Any third-party navigation library

## Examples from Other Sites

- **Apple.com** — Hamburger menu on mobile, full nav on desktop. Clean transition between breakpoints. Focus trap in mobile menu.
- **Stripe.com** — Clean responsive nav transition. Hamburger on mobile with accessible drawer.
