# Add `main` Landmark to All Pages

## Priority: Critical

## User Story

As a screen reader user, I want the primary content area of every page to be wrapped in a `<main>` landmark so that I can jump directly to the content using landmark navigation.

## Acceptance Criteria

- [ ] Every page has exactly one `<main>` element (or one element with `role="main"`)
- [ ] The main landmark is exposed in the accessibility tree and announced by screen readers
- [ ] The skip-to-content link targets the main landmark (e.g., `href="#primary"` and `<main id="primary">`)
- [ ] The main landmark wraps all primary page content (hero, articles, forms, etc.) but excludes header, footer, and navigation
- [ ] Landmark navigation (e.g., VoiceOver rotor, NVDA landmark list) shows "main" as a distinct region
- [ ] No duplicate `main` landmarks exist on any page

## Developer Notes

### General Explanation

The site currently uses a container with `id="primary"` for the skip-to-content target, but that element is not a `<main>` element and does not have `role="main"`. Screen reader users rely on the main landmark to bypass repeated header/navigation content and jump directly to the primary content. Without it, they must navigate linearly through every page.

**Fix:** Replace the existing `#primary` container with a `<main>` element (or add `role="main"` to the existing element). Ensure the skip-to-content link's `href="#primary"` matches the main landmark's `id`. Only one `<main>` per page is allowed per HTML5 spec.

### Code Examples

**Replace existing container with `<main>`:**

```html
<!-- Before: generic div -->
<div id="primary" class="site-content">
  <!-- page content -->
</div>

<!-- After: semantic main landmark -->
<main id="primary" class="site-content">
  <!-- page content -->
</main>
```

**Skip-to-content link (must match main id):**

```html
<a href="#primary" class="skip-link">Skip to content</a>
```

**React/Next.js layout example:**

```jsx
export default function Layout({ children }) {
  return (
    <>
      <a href="#primary" className="skip-link">Skip to content</a>
      <Header />
      <main id="primary" className="site-content">
        {children}
      </main>
      <Footer />
    </>
  );
}
```

**Alternative (if you cannot change the element):**

```html
<div id="primary" role="main" class="site-content">
  <!-- page content -->
</div>
```

Using the native `<main>` element is preferred over `role="main"` for better semantics and browser support.

### Components to Audit

- Page layout template (base layout component)
- All page templates (homepage, Services, Our Work, About, Contact, etc.)
- Any template that renders the primary content wrapper
- Skip-to-content link component (ensure `href` matches main `id`)

## Examples From Other Sites

- **gov.uk** uses a `<main id="main-content" class="govuk-main-wrapper">` on every page. Their skip link targets `#main-content`. The main landmark is consistently exposed for screen reader landmark navigation.
- **MDN Web Docs** wraps all article and documentation content in `<main>`. Their skip link ("Skip to main content") targets the main landmark, allowing users to bypass the large navigation menu.
- **W3C WAI tutorials** demonstrate the main landmark pattern in their [Page Structure tutorial](https://www.w3.org/WAI/tutorials/page-structure/), showing `<main>` as the primary content region with a skip link.

## References

- [James Okafor Interview — Task 1: First Impressions & Accessibility Structure](../01%20-%20Interviews/james-okafor-interview.md)
- [James Okafor Report — Landmark & Document Structure Issues](../02%20-%20Reports/james-okafor-report.md)
- [Main Report — Item 10: Missing `main` Landmark on All Pages](../main-report.md)
