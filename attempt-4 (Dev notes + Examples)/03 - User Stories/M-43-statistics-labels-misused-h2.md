# M-43: Statistics Labels Misused as H2

**Issue ID:** M-43
**Priority:** Medium
**WCAG Criteria:** 1.3.1 Info and Relationships (A), 2.4.6 Headings and Labels (AA)
**Affected Personas:** Screen Reader, ADHD, Cognitive Disability

---

## User Story

As a **screen reader user**, I want **heading elements to represent actual content sections, not decorative statistics labels** so that **when I navigate by headings, I find meaningful page structure rather than misleading landmarks like "Years in Business" or "Projects Delivered."**

---

## Acceptance Criteria

- [ ] Statistics labels (e.g., "Years in Business," "Projects Delivered," "Team Members") are no longer coded as `<h2>` elements.
- [ ] Statistics labels use semantically appropriate elements: `<p>`, `<span>`, `<dt>/<dd>`, or `<div>` with appropriate ARIA if needed.
- [ ] The visual appearance of the statistics labels remains unchanged (large/bold styling achieved via CSS classes, not heading tags).
- [ ] The heading hierarchy on affected pages (Homepage, About) remains logical after the change — no orphaned or skipped heading levels.
- [ ] Screen reader heading navigation (e.g., pressing `H` in NVDA/JAWS) no longer surfaces statistics labels.

---

## How to Test the Change

### Manual Testing

1. Open the homepage (and About page) in Chrome.
2. Install the [HeadingsMap browser extension](https://chrome.google.com/webstore/detail/headingsmap/) and open it.
3. Verify the heading outline shows a logical hierarchy without statistics labels appearing as H2 entries.
4. Open NVDA or VoiceOver and press `H` to navigate between headings — confirm statistics labels are skipped.
5. Visually confirm the statistics section looks identical to the previous version (no visual regression).

### Automated Testing

1. Run axe DevTools on the homepage and About page — check for heading hierarchy issues.
2. Run Lighthouse accessibility audit — review heading order warnings.
3. Use a heading audit script:
   ```javascript
   document.querySelectorAll('h1, h2, h3, h4, h5, h6').forEach(h => {
     console.log(`${h.tagName}: "${h.textContent.trim()}"`);
   });
   // Verify no statistics labels appear in the output
   ```

---

## Developer Notes

### General Explanation

Statistics labels like "Years in Business" and "Projects Delivered" are visually styled as large, bold text — which led developers to use `<h2>` tags to achieve that appearance. However, these labels are data descriptions, not section headings. Using heading elements pollutes the document outline and confuses screen reader navigation. The fix is to replace the heading tags with semantically neutral elements and use CSS for visual styling.

### Code Examples

**Before (current):**
```html
<div class="stat">
  <h2>12+</h2>
  <h2>Years in Business</h2>
</div>
<div class="stat">
  <h2>300+</h2>
  <h2>Projects Delivered</h2>
</div>
```

**After — Option A (simple `<p>` with CSS):**
```html
<div class="stat">
  <p class="stat-number">12+</p>
  <p class="stat-label">Years in Business</p>
</div>
```

```css
.stat-number {
  font-size: 3rem;
  font-weight: 700;
  line-height: 1.2;
}

.stat-label {
  font-size: 1.125rem;
  font-weight: 600;
  text-transform: uppercase;
}
```

**After — Option B (description list for better semantics):**
```html
<dl class="statistics">
  <div class="stat">
    <dt class="stat-label">Years in Business</dt>
    <dd class="stat-number">12+</dd>
  </div>
  <div class="stat">
    <dt class="stat-label">Projects Delivered</dt>
    <dd class="stat-number">300+</dd>
  </div>
</dl>
```

**After — Option C (figure/figcaption):**
```html
<figure class="stat" role="group" aria-label="12+ Years in Business">
  <span class="stat-number" aria-hidden="true">12+</span>
  <figcaption class="stat-label">Years in Business</figcaption>
</figure>
```

### Components / Files to Audit

- Homepage statistics section template
- About page statistics section template
- Any reusable "stats" or "counter" component/widget
- WordPress Elementor or Gutenberg counter blocks
- Check for other instances of headings misused for visual styling (inspect heading outline of every page)

---

## Examples from Other Sites

- **Stripe.com:** Displays statistics using `<div>` containers with `<span>` elements for numbers and labels — no heading elements.
- **Salesforce.com:** Statistics sections use a description list (`<dl>/<dt>/<dd>`) pattern, providing semantic meaning without polluting the heading hierarchy.
- **GitHub:** Repository statistics (stars, forks, issues) are presented as `<span>` elements with ARIA labels, not headings.
- **GOV.UK:** Statistics in government dashboards use `<p>` elements with distinct CSS classes, never heading elements, as per their design system guidelines.
