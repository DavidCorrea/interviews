# 41. Inconsistent Statistics Across Pages

**Priority:** Low
**Location:** Homepage ("12+ Years in Business") vs. About Us page ("13+ Years in Business")
**Reported by:** Margaret Sullivan (AI-Curious Business Executive)

---

## User Story

**As a** detail-oriented insurance executive evaluating LaunchPad Lab as a potential technology partner,
**I want** to see consistent, accurate facts and figures across every page of the site,
**so that** I can trust that the company pays attention to details — a non-negotiable quality in a firm that will handle my business data and processes.

---

## Problem

The Homepage and About Us page display conflicting statistics about LaunchPad Lab's tenure:

- **Homepage:** "12+ Years in Business"
- **About Us page:** "13+ Years in Business"

LaunchPad Lab was founded in 2012, making the correct figure **13+ years** as of 2025 and **14+ years** as of 2026.

### Why This Matters

This may seem minor, but for the target persona — a careful, skeptical executive evaluating a six-figure technology investment — inconsistencies erode trust in a specific way:

1. **Signal of carelessness.** If the website can't keep a founding date consistent, what other details are wrong? Margaret, a 57-year-old company president, has seen vendor relationships fail over missed details. Small errors are a red flag.

2. **Compounding doubt.** This isn't the only credibility issue. When Margaret encounters this inconsistency *after* noticing jargon she doesn't understand, testimonials from industries she doesn't recognize, and no educational resources — it compounds her existing hesitation. Each small issue adds weight to the "I'm not sure about these guys" feeling.

3. **Manual maintenance = future drift.** The root cause is that these statistics are hardcoded as static text. Every year, someone has to remember to update them. In practice, they don't — which is how the homepage fell a year behind. This is a systemic issue, not a one-time typo.

### Other Potential Inconsistencies to Audit

While investigating this issue, audit all instances of statistics, metrics, and facts across the site:

- Number of years in business (every page)
- Number of projects completed
- Number of team members
- Number of clients served
- Any "X+" metrics in hero sections, footers, or stat bars

---

## Acceptance Criteria

### A. Consistency
- [ ] All instances of "years in business" display the same, correct number across the entire site
- [ ] All statistical claims (years, projects, team size, clients) are consistent across all pages where they appear
- [ ] A single source of truth exists for each statistic (not hardcoded in multiple templates)

### B. Dynamic Calculation
- [ ] The "years in business" figure is dynamically calculated from the founding year (2012), not hardcoded
- [ ] The calculation updates automatically — no manual intervention is needed when the calendar year changes
- [ ] The dynamic figure displays correctly in January (when the year rolls over) without needing a deploy

### C. Accuracy
- [ ] The founding year (2012) is stored as a single constant or CMS field
- [ ] The displayed figure rounds correctly (e.g., in March 2026, "14+ years" is correct; it does not prematurely display "15+ years")
- [ ] If other statistics (projects, team size) are displayed, they are sourced from a CMS or database — not hardcoded in HTML

### D. Audit Trail
- [ ] A content audit documents every instance of statistical claims across the site
- [ ] Each statistic is mapped to its source (CMS field, calculated value, or hardcoded — with plan to migrate hardcoded values)

---

## How to Test

### Visual Verification
1. Navigate to the Homepage (`/`)
2. Locate the "years in business" statistic — note the displayed value
3. Navigate to the About Us page (`/about/` or `/about-us/`)
4. Locate the "years in business" statistic — note the displayed value
5. Compare the two values — they **must match**
6. Calculate the expected value: `current year - 2012` → verify the displayed value matches (e.g., in 2026, expect "14+ Years")
7. Search for statistics on all other pages (Services, Contact, footer) — verify consistency

### Code Verification
1. Search the codebase for hardcoded year strings: `"12+"`, `"13+"`, `"14+"`, `"years in business"`, `"years"` near numbers
2. Verify all instances reference a shared constant or dynamic calculation — none should be hardcoded as static strings
3. Verify the founding year constant exists in exactly one location

### Automated Test
1. Write a test that extracts the "years" figure from every page containing it
2. Assert all extracted values are identical
3. Assert the extracted value equals `new Date().getFullYear() - 2012`
4. Run this test as part of the CI/CD pipeline to catch future regressions

### Year Rollover Test
1. Temporarily set the system clock to December 31, 11:59 PM
2. Load the homepage — note the displayed year value
3. Advance the clock to January 1, 12:01 AM
4. Reload the homepage — verify the value increments by 1
5. (Alternatively, test this with a unit test that mocks `Date`)

---

## Developer Notes

### Strategy

Replace all hardcoded year/statistic strings with dynamically calculated values sourced from a single constant. For server-rendered sites, calculate at build time or render time. For client-rendered sections, use JavaScript. Either way, the founding year should be defined exactly once.

### Option 1: JavaScript Dynamic Calculation (Client-Side)

For sites where stats are rendered client-side or need to update without a redeploy:

```html
<div class="stats-bar">
  <div class="stat">
    <span class="stat__number" data-founding-year="2012"></span>
    <span class="stat__label">Years in Business</span>
  </div>
  <div class="stat">
    <span class="stat__number" data-stat="projects">200+</span>
    <span class="stat__label">Projects Delivered</span>
  </div>
  <div class="stat">
    <span class="stat__number" data-stat="team">50+</span>
    <span class="stat__label">Team Members</span>
  </div>
</div>
```

```javascript
function initDynamicStats() {
  document.querySelectorAll('[data-founding-year]').forEach((el) => {
    const foundingYear = parseInt(el.dataset.foundingYear, 10);
    const currentYear = new Date().getFullYear();
    const years = currentYear - foundingYear;
    el.textContent = `${years}+`;
  });
}

document.addEventListener('DOMContentLoaded', initDynamicStats);
```

### Option 2: Server-Side Constant (Build-Time / SSR)

For server-rendered sites (Next.js, Rails, etc.), define the founding year as a constant:

**Next.js / React example:**

```typescript
// lib/constants.ts
export const COMPANY_FOUNDED = 2012;

export function getYearsInBusiness(): number {
  return new Date().getFullYear() - COMPANY_FOUNDED;
}
```

```tsx
// components/StatsBar.tsx
import { getYearsInBusiness, COMPANY_FOUNDED } from '@/lib/constants';

export function StatsBar() {
  const years = getYearsInBusiness();

  return (
    <div className="stats-bar">
      <div className="stat">
        <span className="stat__number">{years}+</span>
        <span className="stat__label">Years in Business</span>
      </div>
    </div>
  );
}
```

**Ruby on Rails example:**

```ruby
# config/initializers/company.rb
COMPANY_FOUNDED = 2012

# app/helpers/application_helper.rb
def years_in_business
  Date.current.year - COMPANY_FOUNDED
end
```

```erb
<!-- app/views/shared/_stats_bar.html.erb -->
<div class="stats-bar">
  <div class="stat">
    <span class="stat__number"><%= years_in_business %>+</span>
    <span class="stat__label">Years in Business</span>
  </div>
</div>
```

### Option 3: CMS-Driven Stats

If using a headless CMS (Contentful, Sanity, etc.), create a "Company Stats" content type:

```json
{
  "contentType": "companyStats",
  "fields": [
    {
      "id": "foundingYear",
      "type": "Integer",
      "name": "Founding Year",
      "required": true
    },
    {
      "id": "projectsCompleted",
      "type": "Integer",
      "name": "Projects Completed",
      "required": true
    },
    {
      "id": "teamSize",
      "type": "Integer",
      "name": "Team Members",
      "required": true
    },
    {
      "id": "clientsServed",
      "type": "Integer",
      "name": "Clients Served",
      "required": true
    }
  ]
}
```

The template then calculates "years in business" from the `foundingYear` field, while other stats are editable by non-developers in the CMS.

### Automated Test (Jest Example)

```javascript
import { getYearsInBusiness, COMPANY_FOUNDED } from '../lib/constants';

describe('Company statistics', () => {
  test('calculates years in business from founding year', () => {
    const expected = new Date().getFullYear() - COMPANY_FOUNDED;
    expect(getYearsInBusiness()).toBe(expected);
  });

  test('founding year is 2012', () => {
    expect(COMPANY_FOUNDED).toBe(2012);
  });

  test('years in business is positive', () => {
    expect(getYearsInBusiness()).toBeGreaterThan(0);
  });
});
```

### End-to-End Consistency Test (Playwright Example)

```javascript
import { test, expect } from '@playwright/test';

const FOUNDING_YEAR = 2012;

test('years in business is consistent across pages', async ({ page }) => {
  const pagesToCheck = ['/', '/about/', '/contact/'];
  const expectedYears = new Date().getFullYear() - FOUNDING_YEAR;
  const yearPattern = new RegExp(`${expectedYears}\\+?\\s*years`, 'i');

  for (const path of pagesToCheck) {
    await page.goto(path);
    const statsText = await page.textContent('body');

    if (statsText.match(/years in business/i)) {
      const statElement = page.locator(':text-matches("\\\\d+\\\\+?\\\\s*Years in Business", "i")');
      if (await statElement.count() > 0) {
        const text = await statElement.first().textContent();
        const displayedYears = parseInt(text.match(/(\d+)/)?.[1] || '0', 10);
        expect(displayedYears).toBe(expectedYears);
      }
    }
  }
});
```

### Content Audit Checklist

Perform a full-site audit for hardcoded statistics:

| Statistic | Homepage | About | Services | Contact | Footer |
|---|---|---|---|---|---|
| Years in business | ✅ Check | ✅ Check | ✅ Check | ✅ Check | ✅ Check |
| Projects completed | ✅ Check | ✅ Check | — | — | ✅ Check |
| Team size | — | ✅ Check | — | — | — |
| Clients served | ✅ Check | ✅ Check | — | — | — |

### WCAG References

- **WCAG 2.1 SC 3.3.1 Error Identification (A):** While primarily about form errors, the principle of accurate information extends to all content — users should be able to trust the information presented
- **WCAG 2.1 SC 1.1.1 Non-text Content (A):** If statistics are displayed as images (infographics), the `alt` text must match the visible number exactly — inconsistencies between visual and alt text compound the problem
- **WCAG 2.1 SC 2.4.6 Headings and Labels (AA):** Statistics should have clear, descriptive labels (e.g., "Years in Business" not just "12+")

### Components to Audit

| Component / Section | Page(s) | What to Fix |
|---|---|---|
| Hero stats bar | Homepage | Replace hardcoded "12+" with dynamic calculation |
| About stats section | About page | Replace hardcoded "13+" with dynamic calculation |
| Footer stats (if any) | All pages | Replace any hardcoded stats with shared constant |
| CMS stat fields | Content management | Create single-source-of-truth fields for all stats |
| Build/deploy pipeline | CI/CD | Add test to verify stat consistency across pages |
| Infographic images (if any) | Any page | Regenerate or use text-based stats instead of images |

---

## Examples from Other Sites

### Stripe (stripe.com)
Stripe's statistics ("Millions of businesses," "135+ currencies") are rendered dynamically. They use a shared data layer that feeds every instance of a metric across the site. When a number changes, it changes everywhere simultaneously.

### Basecamp (basecamp.com)
Basecamp displays "Trusted since 2004" rather than "X years in business" — a static founding year that never needs updating. This is the simplest possible fix: instead of calculating years from a founding date, just display the founding year. "Since 2012" never becomes inaccurate.

### Mailchimp (mailchimp.com)
Their stats section uses a server-rendered component that pulls from a central data store. Each metric (users, emails sent, revenue generated) is fetched once and distributed to every page. They've explicitly avoided hardcoding metrics in templates.

### Gov.uk (gov.uk)
The UK government's design system mandates that all statistics are sourced from a single authoritative dataset. No statistic appears in more than one template — they use includes/partials that render from one source. This eliminates the possibility of inconsistency.

### Key Patterns
1. **Calculate, don't hardcode** — Any date-derived metric should be computed, not typed
2. **Single source of truth** — Define each stat exactly once (constant, CMS field, or API)
3. **Consider "Since YYYY"** — Displaying the founding year ("Since 2012") instead of calculating years eliminates the update problem entirely
4. **Automate testing** — Add a CI test that scrapes all pages for statistics and asserts consistency
5. **Content audit annually** — Even with automation, schedule an annual review of all facts and figures
