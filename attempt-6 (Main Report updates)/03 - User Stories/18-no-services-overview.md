# No Services Overview Page

## Priority
Medium

## User Story
As a **prospective client exploring services**, I want **a dedicated Services overview page that lists all offerings** with brief descriptions and links to detail pages, so that **I can understand the full scope of options before diving into specific pages**.

## Acceptance Criteria

- [ ] A `/services/` route exists and serves a dedicated overview page
- [ ] The overview page lists all services with brief descriptions
- [ ] Each service has a link to its detail page
- [ ] Services are visually organized (e.g., cards, grid, or categorized list)
- [ ] The main navigation "Services" link navigates to `/services/` (not a random sub-service)
- [ ] Page has a clear H1 (e.g., "Our Services" or "What We Offer")
- [ ] Content is readable and scannable (headings, subheadings, icons optional)
- [ ] Page is keyboard accessible and screen reader friendly

## How to Test

1. Click the main navigation "Services" link.
2. Confirm the URL is `/services/` (or equivalent).
3. Verify the page shows a list/grid of all services (e.g., AI Automation, Web Development, etc.).
4. Confirm each service has a brief description and a link to its detail page.
5. Click each service link and verify it navigates to the correct sub-page.
6. Check that the page has a clear hierarchy (H1, H2s).
7. Use keyboard navigation to tab through all links and verify focus order.

## Developer Notes

### General Explanation
The Services link should lead to a dedicated landing page that summarizes all offerings. This page acts as a hub: users can scan the full list and choose which service to explore in depth. It should not redirect to a random sub-service or drop-down. The overview page should be a first-class route that serves as the primary entry point for services.

### Code Example (HTML Structure)

```html
<main>
  <h1>Our Services</h1>
  <p class="intro">We help businesses build and scale digital products with strategy, design, and development.</p>

  <section aria-labelledby="services-heading">
    <h2 id="services-heading">What We Offer</h2>
    <ul class="services-grid">
      <li>
        <article>
          <h3><a href="/services/ai-automation/">AI Automation</a></h3>
          <p>Streamline workflows and reduce manual tasks with intelligent automation.</p>
          <a href="/services/ai-automation/">Learn more →</a>
        </article>
      </li>
      <li>
        <article>
          <h3><a href="/services/web-development/">Web Development</a></h3>
          <p>Custom web applications built for scalability and performance.</p>
          <a href="/services/web-development/">Learn more →</a>
        </article>
      </li>
      <!-- ... more services -->
    </ul>
  </section>
</main>
```

### React Example

```jsx
const services = [
  { slug: 'ai-automation', title: 'AI Automation', description: '...' },
  { slug: 'web-development', title: 'Web Development', description: '...' },
  // ...
];

function ServicesOverview() {
  return (
    <main>
      <h1>Our Services</h1>
      <section aria-labelledby="services-heading">
        <h2 id="services-heading">What We Offer</h2>
        <ul className="services-grid">
          {services.map((s) => (
            <li key={s.slug}>
              <article>
                <h3><Link to={`/services/${s.slug}/`}>{s.title}</Link></h3>
                <p>{s.description}</p>
                <Link to={`/services/${s.slug}/`}>Learn more →</Link>
              </article>
            </li>
          ))}
        </ul>
      </section>
    </main>
  );
}
```

### Components to Audit

- [ ] Main navigation component (ensure "Services" links to `/services/`)
- [ ] Routing configuration (add `/services/` route)
- [ ] Any existing services pages or data fetching
- [ ] CMS or content source for service metadata

## Examples from Other Sites

- **IBM.com/services** — Clean overview of all service areas (Cloud, AI, Consulting, etc.) with categorized offerings and links to detail pages.
- **Deloitte.com** — Services landing page with categorized offerings (Audit, Consulting, Tax, etc.), each with brief descriptions and links to sub-pages.
- **Accenture.com** — Services page with clear sections and icons for each service type.
