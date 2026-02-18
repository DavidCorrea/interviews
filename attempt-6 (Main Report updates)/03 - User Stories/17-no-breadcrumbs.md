# No Breadcrumb Navigation

## Priority
Medium

## User Story
As a **user who has navigated deep into the site** (e.g., Services > AI Automation), I want **breadcrumb navigation to show my current location** within the site hierarchy, so that **I can understand where I am and easily navigate back to parent sections without losing context**.

## Acceptance Criteria

- [ ] Breadcrumb navigation appears on all interior pages (not on homepage)
- [ ] Breadcrumb uses semantic `<nav aria-label="Breadcrumb">` with `<ol>` list structure
- [ ] Each breadcrumb item is a link except the current page (last item)
- [ ] Current page uses `aria-current="page"` on the last item
- [ ] Breadcrumb trail follows the actual site hierarchy (e.g., Home > Services > AI Automation)
- [ ] Schema.org `BreadcrumbList` structured data is present for SEO and assistive tech
- [ ] Breadcrumb links are keyboard accessible and focusable
- [ ] Breadcrumb is visually distinct and readable (sufficient contrast)

## How to Test

1. Navigate to **Home** > **Services** > **AI Automation** (or any sub-page).
2. Verify a breadcrumb appears near the top of the page (typically below header).
3. Confirm the trail reads: Home > Services > AI Automation (or equivalent).
4. Use keyboard only: Tab to each breadcrumb link and verify focus is visible.
5. Click each link and confirm it navigates to the correct parent page.
6. Inspect the page source and run a validator for `BreadcrumbList` schema.
7. Use a screen reader and confirm the breadcrumb announces the current path.

## Developer Notes

### General Explanation
Breadcrumbs provide a clear navigation path for users who have drilled down into the site. They should be implemented as a semantic list with proper ARIA attributes. The current page should not be a link (it is the destination). Use `aria-current="page"` on the last item for assistive technology users.

### Code Example

```html
<nav aria-label="Breadcrumb">
  <ol>
    <li><a href="/">Home</a></li>
    <li><a href="/services/">Services</a></li>
    <li aria-current="page">AI Automation</li>
  </ol>
</nav>
```

### Schema.org BreadcrumbList

```json
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    {
      "@type": "ListItem",
      "position": 1,
      "name": "Home",
      "item": "https://launchpadlab.com/"
    },
    {
      "@type": "ListItem",
      "position": 2,
      "name": "Services",
      "item": "https://launchpadlab.com/services/"
    },
    {
      "@type": "ListItem",
      "position": 3,
      "name": "AI Automation"
    }
  ]
}
```

### React Example

```jsx
import { useLocation } from 'react-router-dom';

function Breadcrumb({ items }) {
  return (
    <nav aria-label="Breadcrumb">
      <ol>
        {items.map((item, index) => (
          <li key={item.path}>
            {index < items.length - 1 ? (
              <a href={item.path}>{item.label}</a>
            ) : (
              <span aria-current="page">{item.label}</span>
            )}
          </li>
        ))}
      </ol>
    </nav>
  );
}
```

### Components to Audit

- [ ] Page layout components (where breadcrumb should be rendered)
- [ ] Routing configuration (to derive breadcrumb path from URL)
- [ ] Header/navigation components
- [ ] Any existing breadcrumb utilities or components

## Examples from Other Sites

- **Amazon.com** — Breadcrumbs on all product and category pages (e.g., Electronics > Computers > Laptops). Clear trail with clickable parent links.
- **Microsoft.com docs** — Full breadcrumb trail in documentation (e.g., Docs > Azure > Compute > Virtual Machines). Consistent placement and styling.
- **W3C WAI** — Breadcrumb pattern documented in their design patterns section.
