# User Story: Startup-Inclusive Homepage Messaging

**Priority:** High  
**Related Findings:** [Finding 1](../main-report.md#1-enterprise-centric-messaging-alienates-non-enterprise-users)

## Story
As a startup founder visiting the website, I want to see messaging that acknowledges startups and early-stage companies, so that I feel the agency could be a fit for my needs — not just enterprise clients.

## Context
The homepage and key landing pages currently use enterprise-centric language ("Modern Enterprise," "Digital Transformation," "Operational Efficiency"). This alienates startup founders, solo entrepreneurs, and small business owners who are a real segment of the agency's clientele (evidenced by portfolio work like Breadcrumb, NextLot, Tiny House Listings). No mention of MVPs, startups, product-market fit, or early-stage development exists on the site.

## Acceptance Criteria
- The homepage includes at least one messaging block that speaks to startups/founders
- Key terms like "MVP," "startup," "early-stage," or "product-market fit" appear on the homepage
- The Services page includes startup-relevant framing alongside enterprise messaging
- A dedicated "Startups" landing page or section exists (bonus)

## How to Test
1. Navigate to the homepage as a first-time visitor
2. Without scrolling past the first two screen-lengths, confirm messaging acknowledges non-enterprise users
3. Search the page content for startup-relevant terms
4. Verify the Services page mentions MVP or startup-stage work

## Developer Notes

### General Approach
This is primarily a content/copy change, not a structural change. Update existing CMS content blocks or hardcoded copy. Consider adding a new section or modifying existing section copy.

### Components to Audit
- Homepage hero section (heading + subheading)
- "Your Strategic AI Partner" section copy
- Services page hero tagline
- Navigation menu (consider adding a "Startups" or "For Founders" link under Industries or Services)

### Code Examples
If using a CMS like Contentful (which they use), this is a content update. If hardcoded:

```jsx
// Before
<h2>AI-Powered Digital Solutions for the Modern Enterprise</h2>

// After
<h2>AI-Powered Digital Solutions for Enterprises & Startups</h2>
```

For a new section:
```jsx
<section className="startup-cta">
  <h2>Building Something New?</h2>
  <p>
    From MVPs to scale-ups, we help founders go from idea to launch 
    in as little as 6 weeks. No enterprise budget required.
  </p>
  <a href="/contact" className="cta-button">Tell Us About Your Idea</a>
</section>
```

## How Other Sites Achieve This
- **Vercel** (vercel.com) — has dedicated "Startups" pricing and a "Startup Program" page alongside enterprise offerings
- **Toptal** (toptal.com) — uses dual messaging like "From startups to Fortune 500s" in their hero
- **Thoughtbot** (thoughtbot.com) — explicitly mentions "MVPs" and "startup validation" in services alongside larger project work
