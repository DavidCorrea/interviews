# Case Study Filtering & Discovery

## Priority
**Medium**

## User Story
As a visitor browsing the Our Work page, I want to filter case studies by service type, technology, company size, and search by keyword, so that I can quickly find relevant examples without scrolling through 50+ items.

## Acceptance Criteria

- [ ] Multi-faceted filtering is available: by service type, technology, company size, and industry
- [ ] A search function allows keyword search across case study titles and descriptions
- [ ] Pagination or "Load more" is implemented to limit initial cognitive load
- [ ] Optionally: 6–8 highlighted case studies featured at top with "View all" option
- [ ] Filter state is clear (e.g., "Showing 12 of 54 case studies" or active filter chips)
- [ ] Filters are keyboard accessible and screen reader friendly
- [ ] URL updates with filter state for shareable/bookmarkable links (optional)

## How to Test

1. Open https://launchpadlab.com/ and navigate to the Our Work page.
2. Verify filtering options beyond "Industries" dropdown exist (e.g., service type, technology).
3. Search for a keyword (e.g., "healthcare") — verify results update.
4. Apply multiple filters — verify results narrow correctly.
5. Verify pagination or "Load more" is present (not all 50+ items at once).
6. Test with keyboard: tab through filters, use search field.
7. Test with screen reader: verify filter labels and result counts are announced.

## Developer Notes

### General Explanation
The Our Work page lists 50+ case studies with only an Industries dropdown filter. No search, pagination, or filtering by service type, technology, or company size. This creates cognitive overload and makes it difficult for users to find relevant examples.

**Solution:** Add multi-faceted filtering (by service type, technology, company size). Implement pagination or "load more." Consider featuring 6–8 highlighted case studies with an option to view all. Add a search function.

### Code Examples

**Filter UI structure:**
```html
<div class="case-study-filters" role="search" aria-label="Filter case studies">
  <input type="search" placeholder="Search case studies..." aria-label="Search by keyword" />
  <select aria-label="Filter by industry">
    <option value="">All Industries</option>
    <option value="healthcare">Healthcare</option>
    <option value="fintech">Fintech</option>
  </select>
  <select aria-label="Filter by service type">
    <option value="">All Services</option>
    <option value="custom-software">Custom Software</option>
    <option value="ai-automation">AI Automation</option>
  </select>
  <select aria-label="Filter by technology">
    <option value="">All Technologies</option>
    <option value="react">React</option>
    <option value="salesforce">Salesforce</option>
  </select>
  <select aria-label="Filter by company size">
    <option value="">All Sizes</option>
    <option value="startup">Startup</option>
    <option value="mid-market">Mid-market</option>
    <option value="enterprise">Enterprise</option>
  </select>
</div>
<p class="results-count" aria-live="polite">Showing 12 of 54 case studies</p>
```

**React example:**
```jsx
const CaseStudyFilters = ({ caseStudies, onFilter }) => {
  const [search, setSearch] = useState('');
  const [industry, setIndustry] = useState('');
  const [serviceType, setServiceType] = useState('');
  const [technology, setTechnology] = useState('');

  const filtered = useMemo(() => {
    return caseStudies.filter(cs => {
      const matchSearch = !search || cs.title.toLowerCase().includes(search.toLowerCase());
      const matchIndustry = !industry || cs.industry === industry;
      const matchService = !serviceType || cs.serviceType === serviceType;
      const matchTech = !technology || cs.technologies?.includes(technology);
      return matchSearch && matchIndustry && matchService && matchTech;
    });
  }, [caseStudies, search, industry, serviceType, technology]);

  return (
    <>
      <div role="search" aria-label="Filter case studies">
        <input type="search" value={search} onChange={e => setSearch(e.target.value)} />
        <select value={industry} onChange={e => setIndustry(e.target.value)}>...</select>
        <select value={serviceType} onChange={e => setServiceType(e.target.value)}>...</select>
        <select value={technology} onChange={e => setTechnology(e.target.value)}>...</select>
      </div>
      <p aria-live="polite">Showing {filtered.length} of {caseStudies.length} case studies</p>
      <CaseStudyGrid items={filtered} />
    </>
  );
};
```

**Pagination:**
```jsx
const [page, setPage] = useState(1);
const PAGE_SIZE = 12;
const paginatedItems = filtered.slice(0, page * PAGE_SIZE);

return (
  <>
    <CaseStudyGrid items={paginatedItems} />
    {paginatedItems.length < filtered.length && (
      <button onClick={() => setPage(p => p + 1)}>Load more</button>
    )}
  </>
);
```

### Components to Audit
- Our Work page template
- Case study listing component
- Filter component
- CMS/data structure for case studies (ensure metadata: industry, service type, technology, company size)

## Examples from Other Sites

- **Accenture.com case studies** — Filterable by industry, capability, industry, and technology. Clear filter chips and result counts.
- **McKinsey.com insights** — Search + filter + tags. Comprehensive discovery experience for large content sets.
