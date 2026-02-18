# Issue 12: Fix Confusing and Ambiguous Navigation Labels

**Priority:** Medium
**Location:** Main navigation bar (all pages)
**Reported by:** Jamie Rivera (ADHD), Sam Chen (Dyslexia), Yuki Tanaka (Non-Native English Speaker), Richard Okonkwo (Non-Technical Business Executive)

---

## User Story

**As a** user navigating the LaunchPad Lab website,
**I want** navigation labels that are clear, unambiguous, and visually indicate where I currently am,
**so that** I can quickly find the information I need and always know which page I'm on.

---

## Problem

The main navigation has several compounding issues reported by all four personas:

1. **No active state:** There is no visual indicator showing which page the user is currently viewing. When a user clicks "Services" and lands on the Services page, the "Services" link in the nav looks identical to every other link. Users (especially ADHD and dyslexic users) can't tell if navigation worked.

2. **"Insights" is ambiguous:** Non-native speakers and non-technical users don't know what "Insights" means in this context. Is it analytics? Reports? Thought leadership? The label should be "Blog" or "Articles" — universally understood terms.

3. **"Technologies" is irrelevant:** Non-technical decision-makers (the primary buyer persona) don't care about React, Ruby on Rails, or Python. This label caters to developers, not clients. It takes up primary navigation space without serving the target audience.

4. **"Services" vs. "Technologies" vs. "Industries" is confusing:** Three navigation items that feel conceptually similar. Users aren't sure which one to click to learn what the company does. "What do they do?" could live under any of these three.

5. **No icons or visual differentiation:** All nav items are text-only in the same style. There are no icons, colors, or other visual cues to help users quickly distinguish between items.

---

## Acceptance Criteria

- [ ] The currently active page's navigation link has a visible active state (underline, bold, color change, or background highlight)
- [ ] The active state meets WCAG 2.1 SC 1.4.11 (Non-text Contrast) — 3:1 contrast ratio for the active indicator against adjacent colors
- [ ] "Insights" is renamed to "Blog" (or "Articles")
- [ ] "Technologies" is either removed from primary navigation (moved to footer), renamed to something client-facing (e.g., "How We Build"), or deprioritized as a secondary link
- [ ] Navigation items are visually distinct from each other (via icons, subtitles, or spacing)
- [ ] On hover, each navigation item shows a brief subtitle or description explaining what it leads to
- [ ] The navigation passes keyboard accessibility testing: all items are focusable with `Tab`, activatable with `Enter`, and the active state is announced by screen readers
- [ ] Mobile navigation (hamburger menu) also shows the active state

---

## How to Test

1. **Active state — visual:** Navigate to each page in the site. On each page, check that the corresponding nav link has a visually distinct active state (underline, bold, color, background). Compare to adjacent inactive links
2. **Active state — screen reader:** Using VoiceOver or NVDA, navigate through the nav links. Confirm the current page link is announced as "current page" (via `aria-current="page"`)
3. **Label clarity test:** Show the navigation labels to 3 people unfamiliar with the site. Ask them: "What do you think each link leads to?" If anyone hesitates on a label, it needs improvement
4. **Keyboard test:** Press `Tab` to move through nav items. Confirm each receives a visible focus indicator. Press `Enter` to activate. Confirm navigation works
5. **Hover descriptions:** Hover over each nav item. Confirm a subtitle or tooltip appears with a brief description
6. **Mobile test (375px):** Open the hamburger menu. Confirm the active page is visually highlighted. Confirm all items are tappable with sufficient touch target size (44x44px minimum per WCAG 2.5.8)
7. **Contrast test:** Use a contrast checker to verify the active state indicator has at least 3:1 contrast ratio against the inactive state and the background

---

## Developer Notes

### Approach

The fix involves: (1) adding `aria-current="page"` and visual active styling, (2) renaming ambiguous labels, (3) optionally adding icons and hover descriptions, and (4) restructuring the navigation hierarchy.

### Adding Active State

Use `aria-current="page"` to mark the active link. This provides both semantic meaning for screen readers and a CSS hook for styling:

```html
<nav class="main-nav" aria-label="Main navigation">
  <ul class="main-nav__list">
    <li class="main-nav__item">
      <a href="/services/" class="main-nav__link" aria-current="page">Services</a>
    </li>
    <li class="main-nav__item">
      <a href="/work/" class="main-nav__link">Our Work</a>
    </li>
    <li class="main-nav__item">
      <a href="/industries/" class="main-nav__link">Industries</a>
    </li>
    <li class="main-nav__item">
      <a href="/about/" class="main-nav__link">About</a>
    </li>
    <li class="main-nav__item">
      <a href="/blog/" class="main-nav__link">Blog</a>
    </li>
    <li class="main-nav__item">
      <a href="/contact/" class="main-nav__link main-nav__link--cta">Contact</a>
    </li>
  </ul>
</nav>
```

```css
.main-nav__link {
  position: relative;
  padding: 0.5rem 0;
  color: #374151;
  text-decoration: none;
  font-size: 0.9375rem;
  font-weight: 500;
  transition: color 0.2s ease;
}

.main-nav__link:hover {
  color: #111827;
}

/* Active state — underline indicator */
.main-nav__link[aria-current="page"] {
  color: #2563eb;
  font-weight: 700;
}

.main-nav__link[aria-current="page"]::after {
  content: "";
  position: absolute;
  bottom: -2px;
  left: 0;
  right: 0;
  height: 3px;
  background-color: #2563eb;
  border-radius: 2px;
}

/* Focus state */
.main-nav__link:focus-visible {
  outline: 2px solid #2563eb;
  outline-offset: 4px;
  border-radius: 2px;
}

/* Contact CTA button */
.main-nav__link--cta {
  padding: 0.5rem 1.25rem;
  background-color: #2563eb;
  color: #ffffff;
  border-radius: 6px;
  font-weight: 600;
}

.main-nav__link--cta:hover {
  background-color: #1d4ed8;
  color: #ffffff;
}

.main-nav__link--cta[aria-current="page"] {
  background-color: #1e40af;
  color: #ffffff;
}

.main-nav__link--cta[aria-current="page"]::after {
  display: none; /* CTA uses background change instead of underline */
}
```

### Setting `aria-current` Dynamically

If using a framework (React, Next.js), set `aria-current` based on the current route:

```jsx
// React/Next.js example
import { useRouter } from 'next/router';

function NavLink({ href, children }) {
  const { asPath } = useRouter();
  const isActive = asPath === href || asPath.startsWith(href + '/');

  return (
    <a
      href={href}
      className="main-nav__link"
      aria-current={isActive ? 'page' : undefined}
    >
      {children}
    </a>
  );
}
```

For server-rendered pages, set it in the template:

```erb
<!-- Rails ERB example -->
<a href="/services/"
   class="main-nav__link"
   <%= 'aria-current="page"' if request.path.start_with?('/services') %>>
  Services
</a>
```

### Renaming Labels

| Current Label | New Label | Rationale |
|--------------|-----------|-----------|
| Insights | **Blog** | Universally understood; standard label |
| Technologies | **How We Build** (or move to footer) | Client-facing; explains what the page covers |
| Services | **Services** (keep) | Clear and standard |
| Our Work | **Our Work** (keep) | Clear and standard |
| Industries | **Industries** (keep) | Clear, though consider "Who We Help" |

### Adding Icons (Optional Enhancement)

```html
<a href="/services/" class="main-nav__link" aria-current="page">
  <svg class="main-nav__icon" aria-hidden="true" width="16" height="16">
    <use href="#icon-services" />
  </svg>
  Services
</a>
```

```css
.main-nav__icon {
  width: 1rem;
  height: 1rem;
  flex-shrink: 0;
}

.main-nav__link {
  display: inline-flex;
  align-items: center;
  gap: 0.375rem;
}
```

### Adding Hover Descriptions (Mega-Menu or Tooltip)

```html
<li class="main-nav__item">
  <a href="/services/" class="main-nav__link">
    Services
    <span class="main-nav__subtitle">What we build and how we work</span>
  </a>
</li>
```

```css
.main-nav__subtitle {
  display: block;
  font-size: 0.75rem;
  font-weight: 400;
  color: #9ca3af;
  margin-top: 0.125rem;
}

/* Show only on hover/focus for desktop */
@media (min-width: 769px) {
  .main-nav__subtitle {
    display: none;
  }

  .main-nav__link:hover .main-nav__subtitle,
  .main-nav__link:focus-within .main-nav__subtitle {
    display: block;
  }
}
```

### WCAG References

- **WCAG 2.1 SC 2.4.8 (Location):** A way is available to identify the user's location within a set of web pages — the active state satisfies this
- **WCAG 2.1 SC 1.4.11 (Non-text Contrast):** The active indicator (underline, color change) must have at least 3:1 contrast ratio against adjacent colors
- **WCAG 2.1 SC 2.4.6 (Headings and Labels):** Labels describe topic or purpose — renaming "Insights" to "Blog" makes the label descriptive
- **WCAG 2.1 SC 4.1.2 (Name, Role, Value):** `aria-current="page"` provides the correct state to assistive technology

### Components to Audit

- **Main navigation component** — Add `aria-current="page"`, active styling, and updated labels
- **Mobile navigation / hamburger menu** — Mirror the active state and updated labels
- **Footer navigation** — Move "Technologies" here if removed from main nav; update "Insights" to "Blog"
- **Sitemap** — Update any XML sitemap or HTML sitemap references if URLs change (e.g., `/insights/` → `/blog/`)
- **Internal links** — Search the codebase for any hardcoded links to `/insights/` and update to `/blog/`
- **SEO** — If renaming URLs, add 301 redirects from old paths to new paths

---

## Examples from Other Sites

### Stripe (stripe.com)
The active page link in the nav has a distinct blue color and underline. Other links are gray. The difference is immediately visible.

### GitHub (github.com)
Repository navigation uses an underline + bold active state. The active tab stands out clearly. When using a screen reader, `aria-current="page"` is announced.

### Airbnb (airbnb.com)
Bottom navigation on mobile uses filled icons for the active tab and outline icons for inactive tabs — a clear, universally understood pattern.

### Slack (slack.com)
Navigation items include brief subtitles visible on hover: "Features — See what Slack can do" and "Solutions — For every team and industry." This removes ambiguity from single-word labels.

### UK Government (gov.uk)
Navigation labels are plain, unambiguous words: "Benefits," "Working," "Education." No creative labels. The active link has a bold bottom border in blue.
