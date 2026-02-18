# No Dark Mode Support

## Priority
**Medium**

## User Story
As a user who prefers dark color schemes (e.g., due to eye strain, low-light environments, or system preference), I want the site to respect my `prefers-color-scheme: dark` setting or offer a dark mode toggle, so that I can browse comfortably without excessive brightness.

## Acceptance Criteria

- [ ] Site responds to `prefers-color-scheme: dark` media query
- [ ] Dark mode uses appropriate background and text colors (e.g., dark backgrounds, light text)
- [ ] All color combinations in both light and dark themes meet WCAG AA contrast ratios (4.5:1 for text, 3:1 for UI components)
- [ ] Images, icons, and borders maintain visibility in dark mode
- [ ] Optional: Manual toggle to override system preference (e.g., light/dark/auto)
- [ ] Dark mode is applied consistently across all pages

## How to Test

1. Open https://launchpadlab.com/ in a browser.
2. Set system preference to dark mode: macOS (System Settings > Appearance > Dark), Windows (Settings > Personalization > Colors > Dark).
3. Reload the page — verify the site switches to a dark color scheme.
4. If no change: the site does not support dark mode (current state).
5. Use a contrast checker (e.g., WebAIM Contrast Checker) to verify dark mode colors meet WCAG AA.
6. Test on mobile: enable dark mode on device and verify site behavior.
7. Check all interactive elements (buttons, links, form fields) for visibility in dark mode.

## Developer Notes

### General Explanation
The site has no dark color scheme and does not respect `prefers-color-scheme: dark` media query. Light backgrounds throughout can cause eye strain for users who prefer dark mode, especially in low-light environments.

**Solution:** Implement dark mode using CSS custom properties and `prefers-color-scheme: dark` media query. Ensure all color combinations in both themes meet WCAG AA contrast ratios (4.5:1 for text, 3:1 for UI components).

### Code Examples

**Basic CSS custom properties:**
```css
:root {
  --bg: #ffffff;
  --text: #1a1a1a;
  --text-muted: #666666;
  --accent: #0066cc;
  --border: #e0e0e0;
}

@media (prefers-color-scheme: dark) {
  :root {
    --bg: #1a1a1a;
    --text: #e0e0e0;
    --text-muted: #a0a0a0;
    --accent: #4da6ff;
    --border: #404040;
  }
}

body {
  background-color: var(--bg);
  color: var(--text);
}
```

**With manual toggle (stored in localStorage):**
```html
<button aria-label="Toggle dark mode" id="theme-toggle">Dark mode</button>
```

```javascript
const toggle = document.getElementById('theme-toggle');
const prefersDark = window.matchMedia('(prefers-color-scheme: dark)');

function setTheme(theme) {
  document.documentElement.setAttribute('data-theme', theme);
  localStorage.setItem('theme', theme);
}

function initTheme() {
  const saved = localStorage.getItem('theme');
  if (saved) setTheme(saved);
  else setTheme(prefersDark.matches ? 'dark' : 'light');
}

toggle.addEventListener('click', () => {
  const current = document.documentElement.getAttribute('data-theme');
  setTheme(current === 'dark' ? 'light' : 'dark');
});

initTheme();
```

```css
[data-theme="dark"] {
  --bg: #1a1a1a;
  --text: #e0e0e0;
  /* ... */
}
```

**React example:**
```jsx
const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState(() =>
    localStorage.getItem('theme') || (window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light')
  );

  useEffect(() => {
    document.documentElement.setAttribute('data-theme', theme);
    localStorage.setItem('theme', theme);
  }, [theme]);

  return <ThemeContext.Provider value={{ theme, setTheme }}>{children}</ThemeContext.Provider>;
};
```

### Components to Audit
- Global styles / CSS variables
- All component color definitions
- Images with light backgrounds (may need dark mode variants)
- Form inputs, buttons, links
- Footer, header, navigation

## Examples from Other Sites

- **GitHub.com** — Automatic dark mode based on system preference + manual toggle in settings. Users can choose light, dark, or auto.
- **MDN Web Docs** — Respects system preference. Clean implementation with CSS custom properties.
- **Tailwind CSS docs** — Dark mode toggle with smooth transition. Supports both media query and class-based toggle.
