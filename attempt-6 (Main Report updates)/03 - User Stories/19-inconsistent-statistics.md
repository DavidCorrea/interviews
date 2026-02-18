# Inconsistent Statistics Across Pages

## Priority
Medium

## User Story
As a **visitor evaluating the company's credibility**, I want **consistent statistics (e.g., years in business) across all pages**, so that **I can trust the information presented and avoid confusion about conflicting data**.

## Acceptance Criteria

- [ ] "Years in business" is identical on Homepage and About page
- [ ] Statistics are sourced from a single data source (config, CMS, or shared component)
- [ ] Years are calculated dynamically from founding date (e.g., `new Date().getFullYear() - 2012`)
- [ ] No hardcoded "12+" or "13+" strings that can drift out of sync
- [ ] Any other stats (e.g., projects completed, clients) are also consistent

## How to Test

1. Open the Homepage and note the "Years in Business" (or equivalent) text.
2. Open the About page and compare.
3. Verify both are identical.
4. If using dynamic calculation, change the system date (or mock) and confirm the year updates.
5. Search the codebase for hardcoded "12+" or "13+" strings and ensure they are removed.

## Developer Notes

### General Explanation
Statistics should be centralized in a single source of truth. For years in business, calculate dynamically from the founding date so the site updates automatically each year. Avoid hardcoding strings like "12+ Years" or "13+ Years" in multiple places—this leads to drift and undermines credibility.

### Code Example (JavaScript)

```javascript
// config/company.js or constants.js
export const FOUNDING_YEAR = 2012;

export function getYearsInBusiness() {
  const currentYear = new Date().getFullYear();
  return currentYear - FOUNDING_YEAR;
}

// Usage: "12+ Years" or "13+ Years" becomes:
// `${getYearsInBusiness()}+ Years in Business`
```

### React Example

```jsx
// config/company.js
export const FOUNDING_YEAR = 2012;

export function getYearsInBusiness() {
  return new Date().getFullYear() - FOUNDING_YEAR;
}

// components/StatsBanner.jsx
import { getYearsInBusiness } from '../config/company';

function StatsBanner() {
  const years = getYearsInBusiness();
  return (
    <p>{years}+ Years in Business</p>
  );
}
```

### CMS Field Example

If using a CMS (e.g., Sanity, Contentful):

- **Option A:** Store `foundingYear` as a number (2012). Use a computed field or template to display: `{{ foundingYear | yearsSince }}`.
- **Option B:** Use a "Years in Business" field that pulls from a single source. Ensure only one place defines this value.

### Components to Audit

- [ ] Homepage hero or stats section
- [ ] About page stats or timeline
- [ ] Footer (if stats appear there)
- [ ] Any shared components displaying company stats
- [ ] CMS schema or content entries

## Examples from Other Sites

- **Automattic.com** — Updates years dynamically; company founding year is used as the source.
- **Most professional firms** — Use dynamic date calculations or a single CMS field for years in business.
- **Stripe.com** — Company stats are centralized and consistent across pages.
