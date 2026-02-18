# User Story: Surface Consumer Case Studies on Homepage

**Priority:** High  
**Related Finding:** [Finding 2](../main-report.md#finding-2)

## Story
As a potential client who builds consumer-facing products, I want to see consumer and startup case studies prominently displayed on the homepage, so that I can quickly determine this agency has relevant experience for my type of project.

## Context
The homepage case study carousel exclusively features enterprise clients (Millennium Trust, Prosci/Salesforce, CDK Global). The agency's impressive consumer work — Breadcrumb (10M views debut), NextLot ($2B+ platform), Omaha Zoo (25M+ users), Tiny House Listings — is buried in the portfolio page and requires significant scrolling to discover. First impressions are shaped by what's visible on the homepage.

## Acceptance Criteria
- The homepage case study carousel includes at least 2 consumer-facing or startup case studies
- Consumer case studies show consumer-relevant metrics (users, downloads, views) rather than enterprise metrics (ROI, cost reduction)
- The "Our Work" page has a way to filter or surface consumer/startup projects specifically

## How to Test
1. Navigate to homepage
2. Scroll to case studies carousel
3. Confirm at least 2 of the visible case studies are consumer-facing (e.g., Breadcrumb, NextLot, Omaha Zoo)
4. Navigate to "Our Work" page and verify a filter for "Consumer" or "Startup" exists

## Developer Notes

### General Approach
Update the case study carousel data source to include consumer-facing projects. If the carousel is CMS-driven, re-order or tag featured case studies. If hardcoded, update the array/list.

### Components to Audit
- Homepage case study carousel component
- Case study data model (may need a `featured` or `category` field)
- Portfolio page filter/dropdown component

### Code Examples
```jsx
// Update carousel items to include consumer case studies
const featuredCaseStudies = [
  { 
    client: "Breadcrumb", 
    headline: "10 Million Views on App Debut", 
    metric: "10M+ views",
    type: "consumer"
  },
  { 
    client: "Millennium Trust", 
    headline: "Spurring Enterprise Innovation",
    metric: "$1M+ new annual revenue",
    type: "enterprise"
  },
  { 
    client: "NextLot", 
    headline: "Scaled to $2B+ with Custom Auction Platform",
    metric: "$2B+ in transactions",
    type: "consumer"
  },
];
```

For the portfolio filter:
```jsx
<select onChange={handleFilterChange} aria-label="Filter case studies by type">
  <option value="all">All Industries</option>
  <option value="consumer">Consumer & Startups</option>
  <option value="enterprise">Enterprise</option>
  <option value="healthcare">Healthcare</option>
  {/* etc */}
</select>
```

## How Other Sites Achieve This
- **Work & Co** (work.co) — rotates their homepage portfolio between consumer (Ikea) and enterprise (Chase) equally
- **Thoughtbot** (thoughtbot.com) — case study page has clear tags for startup vs enterprise work
- **Ueno** — features consumer-facing work (brand apps, consumer platforms) prominently on landing page
