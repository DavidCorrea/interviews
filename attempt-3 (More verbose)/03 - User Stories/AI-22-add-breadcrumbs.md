# AI-22: Add Breadcrumbs on Inner Pages

## Metadata
- **ID:** AI-22
- **Priority:** 3 Medium
- **Personas Affected:** 3+ of 16 personas (screen reader, cognitive disability, senior)
- **WCAG Criteria:** 2.4.8 Location (AAA)
- **Effort:** Small–Medium (2–4 hours)

---

## User Story

**As a** user navigating inner pages (About, Services, individual service pages),

**I want** breadcrumb navigation showing my current location in the site hierarchy (e.g., Home > Services > AI Automation),

**So that** I understand where I am, can easily return to parent sections, and don't feel lost in the site structure.

---

## Acceptance Criteria

- [ ] Breadcrumbs appear on all inner pages (not necessarily on homepage)
- [ ] Breadcrumb trail is visible below header, above page heading (h1)
- [ ] Format: Home > Parent Section > Current Page (or similar)
- [ ] Each breadcrumb except the current page is a clickable link
- [ ] Current page is not a link and has `aria-current="page"`
- [ ] Semantic markup: `<nav aria-label="Breadcrumb">` with `<ol>` and `<li>` items
- [ ] Separator (e.g., ">", "/", or chevron) between items — visually and for screen readers
- [ ] Clicking "Home" navigates to homepage
- [ ] JSON-LD BreadcrumbList structured data for SEO (optional but recommended)

---

## Test Plan

### Visual Presence
1. Visit `https://launchpadlab.com/about` (or equivalent inner page)
2. **Expected:** Breadcrumb trail visible below header, above page h1
3. **Expected:** Format similar to "Home > About" or "Home > Services > AI Automation"
4. Visit Services, individual service pages, Work, Case Studies
5. **Expected:** Breadcrumbs on each inner page

### Link Functionality
1. On an inner page, click "Home" in breadcrumbs
2. **Expected:** Navigates to homepage
3. On "Home > Services > AI Automation", click "Services"
4. **Expected:** Navigates to Services index page
5. Current page (e.g., "AI Automation") should NOT be a link

### Semantic Markup
1. Inspect breadcrumb HTML
2. **Expected:** `<nav aria-label="Breadcrumb">` wraps the trail
3. **Expected:** `<ol>` with `<li>` for each item
4. **Expected:** Current page has `aria-current="page"` on the `<li>` or `<span>`
5. **Expected:** Links use `<a href="...">` for non-current items

### Screen Reader Test
1. Enable VoiceOver or NVDA
2. Navigate to a page with breadcrumbs
3. **Expected:** Landmark "Breadcrumb" is announced
4. **Expected:** List structure is announced (e.g., "List with 3 items")
5. **Expected:** Current page is announced as "current page" or similar
6. **Expected:** Each link's purpose is clear from context

### Separator Accessibility
1. Use `aria-hidden="true"` on separator characters (e.g., ">") so screen readers don't announce "greater than"
2. Or use CSS `::before`/`::after` with `content` for visual separators and ensure list items are announced in order
3. **Expected:** Screen reader announces "Home, link. Services, link. AI Automation, current page" — not "Home greater than Services greater than..."

### JSON-LD (Optional)
1. View page source, search for "BreadcrumbList"
2. **Expected:** Valid JSON-LD schema if implemented
3. Test with Google Rich Results Test: https://search.google.com/test/rich-results

---

## Developer Notes

### HTML Structure
```html
<nav aria-label="Breadcrumb">
  <ol>
    <li><a href="/">Home</a></li>
    <li><a href="/services">Services</a></li>
    <li aria-current="page">AI Automation</li>
  </ol>
</nav>
```

### Separator Options
```css
/* Option 1: CSS separator */
.breadcrumb li + li::before {
  content: ">";
  margin: 0 0.5rem;
  color: #666;
}

/* Option 2: Inline with aria-hidden */
<li><span aria-hidden="true">/</span></li>
```

### JSON-LD Structured Data
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    { "@type": "ListItem", "position": 1, "name": "Home", "item": "https://launchpadlab.com/" },
    { "@type": "ListItem", "position": 2, "name": "Services", "item": "https://launchpadlab.com/services" },
    { "@type": "ListItem", "position": 3, "name": "AI Automation" }
  ]
}
</script>
```

### Reusable Component (React/Vue/Generic)
- Accept `items: [{ label, href? }]` — last item has no href
- Render `<nav aria-label="Breadcrumb"><ol>...</ol></nav>`
- Add `aria-current="page"` to last item
- Position: below header, above h1; typically full-width or within content container

### CMS / Framework Integration
- If using CMS: generate breadcrumb from page path or taxonomy
- If using Next.js: use `usePathname()` or router to build trail
- If using WordPress: use breadcrumb plugin (Yoast, Rank Math) with accessible markup

### Placement
- Place below site header, above main content
- Ensure sufficient contrast with background
- Font size: readable but not dominant (e.g., 0.875rem or 14px)

---

## Examples

| Site | Approach |
|------|----------|
| **Amazon.com** | Breadcrumbs on every product page: Home > Category > Subcategory > Product |
| **GOV.UK** | Breadcrumbs on all inner pages; semantic nav; clear hierarchy |
| **MDN Web Docs** | Breadcrumb with semantic markup; aria-label; aria-current |
| **Wikipedia** | Breadcrumb trail at top of articles |
| **Shopify** | Breadcrumbs on collection and product pages |
