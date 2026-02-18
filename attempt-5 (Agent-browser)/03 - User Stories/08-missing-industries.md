# Issue 8: Expand Industry Coverage to Reflect Actual Capabilities

**Priority:** High
**Location:** `/industries/`
**Reported by:** Richard Okonkwo (Non-Technical Business Executive)

---

## User Story

**As a** prospective client whose industry isn't listed on the Industries page,
**I want** to see that LaunchPad Lab serves my industry — or at least acknowledges they work beyond the listed categories,
**so that** I don't dismiss the company as irrelevant and leave the site before making contact.

---

## Problem

The Industries page lists only 9 industries: Financial Services, Private Equity, Healthcare, Insurance, Legal, Real Estate, Education, Non-Profit, and Government. There is no mention of manufacturing, distribution, logistics, supply chain, or food/beverage — despite existing case studies for clients like **Kawasaki** and **American Truck Business Services** that clearly fall outside these categories.

The page body copy claims LaunchPad Lab is "industry-agnostic," but the narrow, curated list contradicts that claim. A visitor from a non-listed industry (e.g., a food distribution CEO needing inventory management software) sees the list, concludes the company doesn't serve their vertical, and leaves — even though LaunchPad Lab has directly relevant experience.

---

## Acceptance Criteria

- [ ] The Industries page includes at least 4 additional industry categories covering: Manufacturing, Logistics/Distribution/Supply Chain, Food & Beverage, and Transportation
- [ ] A visible fallback message appears below or alongside the industry list, such as: "Don't see your industry? We've built solutions across 50+ industries. Tell us about your project."
- [ ] The fallback message includes a CTA linking to the Contact page
- [ ] Any case studies associated with unlisted industries (Kawasaki, American Truck Business Services) are correctly tagged to their actual industry
- [ ] The page no longer makes an "industry-agnostic" claim unless the displayed list actually supports it, or the fallback message bridges the gap
- [ ] On mobile, the expanded list and fallback message remain fully visible and accessible

---

## How to Test

1. **Visual audit:** Navigate to `/industries/` and verify all listed industries are present, including the newly added categories
2. **Fallback message:** Confirm the "Don't see your industry?" message is visible without scrolling past the industry list
3. **CTA functionality:** Click the CTA in the fallback message and verify it navigates to the Contact page (or opens a contact modal)
4. **Case study alignment:** Navigate to the Our Work page and filter by "Manufacturing" or "Logistics" — confirm Kawasaki and American Truck Business Services appear
5. **Cross-reference:** Verify the Industries page text no longer contradicts the listed categories (e.g., don't claim "industry-agnostic" if only 9 industries are shown without a qualifying fallback)
6. **Mobile:** Test on mobile viewports (375px, 390px) to confirm the expanded list and fallback message render correctly
7. **Screen reader:** Use VoiceOver or NVDA to confirm the fallback message and CTA are accessible and announced correctly

---

## Developer Notes

### Approach

The fix involves three changes: (1) expand the industry data to include missing categories, (2) add a fallback/catch-all section after the industry list, and (3) ensure case studies are tagged to the correct industry.

### Expanding the Industry List

If industries are rendered from a data source (CMS or static array), add entries for the missing categories:

```json
[
  { "name": "Financial Services", "slug": "financial-services", "icon": "bank" },
  { "name": "Healthcare", "slug": "healthcare", "icon": "heart-pulse" },
  { "name": "Manufacturing", "slug": "manufacturing", "icon": "factory" },
  { "name": "Logistics & Distribution", "slug": "logistics-distribution", "icon": "truck" },
  { "name": "Food & Beverage", "slug": "food-beverage", "icon": "utensils" },
  { "name": "Transportation", "slug": "transportation", "icon": "route" }
]
```

### Adding the Fallback Section

Place a visually distinct "catch-all" section after the industry grid:

```html
<section class="industry-fallback" aria-label="Other industries">
  <div class="industry-fallback__inner">
    <h2>Don't see your industry?</h2>
    <p>
      We've partnered with companies across <strong>50+ industries</strong> —
      from food distribution to aerospace manufacturing.
      Every business has unique challenges, and we build software to solve them.
    </p>
    <a href="/contact/" class="btn btn--primary">
      Tell Us About Your Project
    </a>
  </div>
</section>
```

```css
.industry-fallback {
  margin-top: 3rem;
  padding: 3rem 2rem;
  background-color: #f0f4f8;
  border-radius: 12px;
  text-align: center;
}

.industry-fallback h2 {
  font-size: 1.75rem;
  font-weight: 700;
  margin-bottom: 1rem;
  color: #1a1a2e;
}

.industry-fallback p {
  font-size: 1.125rem;
  line-height: 1.8;
  max-width: 600px;
  margin: 0 auto 1.5rem;
  color: #4a4a68;
}

.btn--primary {
  display: inline-block;
  padding: 0.875rem 2rem;
  background-color: #2563eb;
  color: #ffffff;
  font-size: 1rem;
  font-weight: 600;
  border-radius: 8px;
  text-decoration: none;
  transition: background-color 0.2s ease;
}

.btn--primary:hover {
  background-color: #1d4ed8;
}

.btn--primary:focus-visible {
  outline: 3px solid #93c5fd;
  outline-offset: 2px;
}
```

### Alternative: Organize by Problem Type

Instead of (or in addition to) listing by industry vertical, consider reorganizing by problem type, which is more inclusive:

```html
<section class="solutions-by-problem">
  <h2>Solutions We Build</h2>
  <div class="solutions-grid">
    <div class="solution-card">
      <h3>Inventory & Supply Chain Management</h3>
      <p>Track stock, automate ordering, and reduce waste across locations.</p>
      <span class="solution-card__industries">
        Used in: Manufacturing, Food & Beverage, Distribution
      </span>
    </div>
    <div class="solution-card">
      <h3>Customer Portals & Self-Service</h3>
      <p>Let your customers manage accounts, place orders, and track status online.</p>
      <span class="solution-card__industries">
        Used in: Financial Services, Insurance, Healthcare
      </span>
    </div>
    <div class="solution-card">
      <h3>Internal Tools & Workflow Automation</h3>
      <p>Replace spreadsheets and manual processes with custom applications.</p>
      <span class="solution-card__industries">
        Used in: Legal, Real Estate, Non-Profit, Government
      </span>
    </div>
  </div>
</section>
```

### Components to Audit

- **Industries page template** — Add new industry entries and fallback section
- **CMS / data source** — Ensure industry taxonomy includes new categories
- **Case study tagging** — Re-tag Kawasaki, American Truck Business Services, and any other case studies to their correct industries
- **Industry filter on `/work/`** — Ensure newly added industry categories appear in the filter dropdown
- **Navigation** — If Industries has a mega-menu or dropdown, update it to include new entries

---

## Examples from Other Sites

### Thoughtbot (thoughtbot.com)
Lists specific industries but includes a prominent section: "We've worked across many industries. Here are a few." — framing the list as a sample, not an exhaustive catalog.

### Pivotal Labs / VMware Tanzu
Organizes by **capability** (modernization, cloud-native, API platforms) rather than industry. Prospects self-select by problem, not vertical.

### Deloitte Digital
Uses a hybrid approach: industry pages exist, but a "See All Industries" link leads to a comprehensive A-Z directory. No visitor is left without a match.

### Toptal
Uses the phrasing: "Trusted by leading brands and startups across every industry" with a rotating set of logos that demonstrate cross-industry breadth.
