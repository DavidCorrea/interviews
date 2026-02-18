# Provide Unique Accessible Names for All "Learn More" Links

## Priority: Critical

## User Story

As a screen reader user, I want every "Learn More" link to have a unique, descriptive accessible name so that I can distinguish between them when navigating by link list.

## Acceptance Criteria

- [ ] Every "Learn More" link has a unique accessible name that identifies the destination or context (e.g., "Learn more about AI Automation")
- [ ] Every "View Case Study" link has a unique accessible name (e.g., "View case study: [Client Name]")
- [ ] Link list navigation (VoiceOver links rotor, NVDA links list) shows distinct names for each link
- [ ] The fix is applied across homepage service cards, Services page, case study listings, and any card patterns
- [ ] Visible link text may remain "Learn More" if an accessible name is provided via `aria-label` or `aria-labelledby`
- [ ] No two links on the same page share an identical accessible name when they lead to different destinations

## Developer Notes

### General Explanation

The site has 8+ links all labeled "Learn More" with no distinguishing context. Screen reader users often navigate by link list to move quickly through a page. When every link announces "Learn More," this technique becomes useless — users cannot tell which service or case study each link leads to. Violates WCAG 2.4.4 (Link Purpose in Context).

**Three approaches** (choose based on design constraints):

- **Option A:** Change visible link text to "Learn more about [Service Name]" — best for SEO and clarity.
- **Option B:** Keep "Learn More" visible but add `aria-label="Learn more about [Service Name]"` — preserves design.
- **Option C:** Use `aria-labelledby` referencing the parent card's heading + the link — programmatic association.

Apply the same logic to "View Case Study" links.

### Code Examples

**Option A: Change visible link text**

```html
<div class="service-card">
  <h3>AI Automation</h3>
  <p>Description...</p>
  <a href="/services/ai-automation">Learn more about AI Automation</a>
</div>
```

**Option B: `aria-label` (keeps "Learn More" visible)**

```html
<div class="service-card">
  <h3>AI Automation</h3>
  <p>Description...</p>
  <a href="/services/ai-automation" aria-label="Learn more about AI Automation">
    Learn More
  </a>
</div>
```

**Option C: `aria-labelledby` (references heading)**

```html
<div class="service-card">
  <h3 id="ai-automation-heading">AI Automation</h3>
  <p>Description...</p>
  <a href="/services/ai-automation" aria-labelledby="ai-automation-heading learn-more-ai">
    <span id="learn-more-ai">Learn More</span>
  </a>
</div>
```

**React component example (Option B):**

```jsx
function ServiceCard({ title, description, href }) {
  return (
    <div className="service-card">
      <h3>{title}</h3>
      <p>{description}</p>
      <a href={href} aria-label={`Learn more about ${title}`}>
        Learn More
      </a>
    </div>
  );
}
```

**"View Case Study" links:**

```html
<!-- Before -->
<a href="/work/client-xyz">View Case Study</a>

<!-- After (Option A) -->
<a href="/work/client-xyz">View case study: Client XYZ</a>

<!-- After (Option B) -->
<a href="/work/client-xyz" aria-label="View case study: Client XYZ">View Case Study</a>
```

### Components to Audit

- Homepage service cards
- Services page (service cards, service sections)
- Case study listings (Our Work page, homepage carousel)
- Any card patterns or reusable link components
- Blog post cards, team member cards, or similar patterns with generic CTAs

## Examples From Other Sites

- **Deque University** provides examples of link purpose in context in their [WCAG 2.4.4 guidance](https://dequeuniversity.com/rules/axe/link-name). They recommend either descriptive visible text or `aria-label` when the link purpose is not clear from context alone.
- **Apple's accessibility patterns** use descriptive link names throughout their product pages. Service and feature links include the product or feature name in the accessible name (e.g., "Learn more about iPhone" rather than "Learn more").
- **BBC** uses unique link names for similar link types. Their article cards and section links include the article or section title in the accessible name, ensuring link list navigation is usable.

## References

- [James Okafor Interview — Task 2: Understanding What They Do](../01%20-%20Interviews/james-okafor-interview.md)
- [James Okafor Report — Link Accessibility Issues](../02%20-%20Reports/james-okafor-report.md)
- [Main Report — Item 11: Ambiguous Repeated "Learn More" Link Names for Screen Readers](../main-report.md)
