# Add Missing Industry Categories to "Our Work" Filters

## Priority: High

## User Story
As a prospective client in the logistics/distribution industry, I want to filter case studies by my industry so that I can quickly find relevant examples of the company's work without scanning the entire portfolio.

## Acceptance Criteria
- [ ] Industry filter includes at least: Logistics, Distribution, Supply Chain, Manufacturing, and Transportation
- [ ] Filtering by any new industry returns relevant case studies when they exist
- [ ] Case studies such as Kawasaki and American Truck Business Services are correctly tagged with appropriate industry categories
- [ ] Filter UI remains fully keyboard-accessible and screen-reader friendly
- [ ] Consider adding "All Industries" or "Other" option for edge cases
- [ ] Filter state persists or is clearly indicated when applied (e.g., URL params, visible active state)

## Developer Notes

### General Explanation
The "Our Work" page currently excludes major B2B segments (Logistics, Distribution, Supply Chain, Manufacturing, Transportation). Users in these industries cannot quickly find relevant case studies and must manually scan the entire list, undermining the site's credibility for prospects outside the listed verticals. Add the missing industry categories to the filter, audit existing case studies for correct tagging, and ensure the filter component uses accessible markup.

### Code Examples

**Accessible checkbox group for industry filters:**
```html
<fieldset class="industry-filter" aria-labelledby="industry-filter-legend">
  <legend id="industry-filter-legend">Filter by Industry</legend>
  <div role="group" aria-label="Industry options">
    <label><input type="checkbox" name="industry" value="logistics"> Logistics</label>
    <label><input type="checkbox" name="industry" value="distribution"> Distribution</label>
    <label><input type="checkbox" name="industry" value="supply-chain"> Supply Chain</label>
    <label><input type="checkbox" name="industry" value="manufacturing"> Manufacturing</label>
    <label><input type="checkbox" name="industry" value="transportation"> Transportation</label>
    <label><input type="checkbox" name="industry" value="all"> All Industries</label>
  </div>
</fieldset>
```

**Multi-select with ARIA for compact layouts:**
```html
<div class="industry-filter">
  <label for="industry-select" id="industry-label">Filter by Industry</label>
  <select id="industry-select" 
          name="industry" 
          aria-describedby="industry-hint"
          aria-controls="case-study-list"
          multiple
          size="6">
    <option value="logistics">Logistics</option>
    <option value="distribution">Distribution</option>
    <option value="supply-chain">Supply Chain</option>
    <option value="manufacturing">Manufacturing</option>
    <option value="transportation">Transportation</option>
    <option value="all">All Industries</option>
  </select>
  <span id="industry-hint" class="visually-hidden">Select one or more industries to filter case studies</span>
</div>
```

**CMS / data structure for case study industry tagging:**
```javascript
// Example case study schema with industry array
{
  id: "kawasaki",
  title: "Kawasaki Case Study",
  industries: ["manufacturing", "transportation", "distribution"],
  // ...
}
```

### Components to Audit
- Our Work page (main portfolio/case study listing)
- Industry filter component (dropdown, checkboxes, or pill buttons)
- CMS/content management for case studies (industry taxonomy and tagging)
- Case study card or list item component (ensure industry metadata displays correctly)
- URL/query parameter handling for shareable filtered views

## Examples From Other Sites
- **McKinsey** — Case study portfolio covers diverse industries including retail, insurance, life sciences, banking, healthcare, and manufacturing. Visitors can browse by industry vertical and service area.
- **Accenture** — Organizes case studies through multiple portals with industry filtering. Their Data and Advanced AI section features cases in consumer goods, retail, banking, and public service; Accenture Song focuses on automotive, luxury goods, beauty, and retail.
- **Deloitte** — Case study section highlights work across energy, workforce consulting, manufacturing, consumer goods, life sciences, and cybersecurity. All three firms allow visitors to filter for relevant examples in specific sectors or functional areas.

## References
- Main Report Item 4 (High Priority)
- The "Our Work" page at https://launchpadlab.com/ allows filtering by industry but excludes major B2B segments
- Kawasaki, American Truck Business Services, and similar case studies should be audited for correct industry tagging
