# About Us Duplicate Content

## Priority
**High**

## User Story
As a visitor researching LaunchPad Lab, I want a dedicated About Us page with unique content about the team, history, and mission, so that I can make an informed decision about working with the company.

## Acceptance Criteria

- [ ] The route `/about/` serves content that is distinct from the homepage (`/`)
- [ ] About page includes unique H1 (e.g., "About LaunchPad Lab" or "Our Team")
- [ ] Page contains at least: team bios, company history/founding story, and mission/values
- [ ] No duplicate hero, services list, carousel, or contact form identical to homepage
- [ ] Page is crawlable and indexable with unique meta description
- [ ] Screen readers and users navigating to `/about/` receive meaningful, differentiated content
- [ ] Breadcrumb or nav indicates user is on "About" page

## How to Test

1. Navigate to https://launchpadlab.com/
2. Note the H1, hero section, and main content blocks.
3. Navigate to https://launchpadlab.com/about/
4. Compare content: H1, hero, services list, carousel, contact form.
5. Verify the About page has unique content: team section, history, mission/values.
6. Use a screen reader to confirm the About page announces different content than the homepage.
7. Check page source: ensure meta description and title are unique for `/about/`.
8. Verify the "About" link in navigation correctly routes to `/about/`.

## Developer Notes

### General Explanation
The About page currently appears to render the same template or component as the homepage, resulting in identical content. This creates a poor user experience, SEO issues, and accessibility problems (users expect different content when navigating to a different URL).

**Solution:** Create a dedicated About Us page template with unique content. Populate it with team bios, company history, founding story, and mission/values. Ensure the routing system serves this template for `/about/` and does not reuse the homepage template.

### Code Examples

**Route configuration (Next.js example):**
```js
// pages/about.js or app/about/page.js
export default function AboutPage() {
  return (
    <Layout>
      <AboutHero />
      <TeamSection />
      <CompanyHistory />
      <MissionValues />
      <ContactCTA /> {/* Optional, different from homepage form */}
    </Layout>
  );
}
```

**Content structure:**
```html
<main>
  <h1>About LaunchPad Lab</h1>
  <section aria-labelledby="our-story-heading">
    <h2 id="our-story-heading">Our Story</h2>
    <p>Founded in [year], LaunchPad Lab started with...</p>
  </section>
  <section aria-labelledby="team-heading">
    <h2 id="team-heading">Our Team</h2>
    <ul>
      <li>
        <h3>Jane Doe</h3>
        <p>Role, bio...</p>
      </li>
    </ul>
  </section>
  <section aria-labelledby="mission-heading">
    <h2 id="mission-heading">Mission & Values</h2>
    <ul>
      <li>Value 1</li>
      <li>Value 2</li>
    </ul>
  </section>
</main>
```

**CMS/Content check:**
- Ensure `/about/` is not mapped to the same page ID or template as `/`
- Add dedicated fields for About page content in your CMS

### Components to Audit
- Page routing configuration
- Template selection logic
- Homepage component (ensure it's not reused for About)
- CMS page mappings
- Any shared layout that might override page content

## Examples from Other Sites

- **Thoughtbot.com** — Dedicated about page with team photos and bios, company values, history, and a clear narrative about who they are and what they believe.
- **Basecamp.com** — Clear about page with company story, team, and philosophy. Content is distinct from the homepage and product pages.
