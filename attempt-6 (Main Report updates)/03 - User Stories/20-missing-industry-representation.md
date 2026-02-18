# Missing Industry Representation

## Priority
Medium

## User Story
As a **visitor from logistics, supply chain, manufacturing, or transportation**, I want **to see my industry represented or relevant business challenges addressed**, so that **I can determine if the company has experience relevant to my sector**.

## Acceptance Criteria

- [ ] Industries page either includes operations-heavy sectors (logistics, supply chain, manufacturing, transportation) OR clearly explains why the site is organized by challenge
- [ ] Site content is consistent with "industry-agnostic" claim (no contradiction)
- [ ] Case studies or examples from adjacent industries are highlighted where applicable
- [ ] If industries are listed, the list is comprehensive or clearly scoped
- [ ] Messaging is clear and does not overclaim or misrepresent

## How to Test

1. Navigate to the Industries page.
2. Confirm the list of industries shown.
3. If industries are listed: verify whether logistics, supply chain, manufacturing, or transportation appear.
4. If not: check if the page explains the approach (e.g., challenge-based vs. vertical-based).
5. Cross-check homepage and About page for "industry-agnostic" or similar claims.
6. Ensure no conflicting messaging between industries page and other marketing copy.

## Developer Notes

### General Explanation
The site claims "industry-agnostic" but the Industries page lists only 9 industries. Operations-heavy sectors (logistics, supply chain, manufacturing, transportation) are absent. Two approaches:

1. **Expand:** Add industry pages for missing sectors, with relevant case studies or adjacent industries.
2. **Restructure:** Organize around business challenges (e.g., "Operations Optimization," "Compliance & Regulatory") rather than vertical names. This aligns with "industry-agnostic" and avoids implying limited coverage.

### Option A: Expand Industries

```html
<!-- Add new industry cards or sections -->
<section>
  <h2>Industries We Serve</h2>
  <ul>
    <li>Healthcare</li>
    <li>Financial Services</li>
    <li>Logistics & Supply Chain</li>
    <li>Manufacturing</li>
    <li>Transportation</li>
    <li>Retail & E-commerce</li>
    <!-- ... -->
  </ul>
</section>
```

### Option B: Challenge-Based Structure

```html
<section>
  <h2>Business Challenges We Solve</h2>
  <p>We work across industries. Our approach is tailored to your business challenges, not limited by vertical.</p>
  <ul>
    <li><strong>Operations Optimization</strong> — Streamline workflows, reduce manual tasks.</li>
    <li><strong>Compliance & Regulatory</strong> — Meet industry standards and reporting.</li>
    <li><strong>Digital Transformation</strong> — Modernize legacy systems.</li>
    <li><strong>Data & Analytics</strong> — Turn data into insights.</li>
  </ul>
</section>
```

### Messaging Alignment

- If "industry-agnostic": Use challenge-based language. Avoid implying only certain industries are served.
- If listing industries: Add operations-heavy sectors or clearly state "sample industries" (e.g., "Industries we've worked with include...").

### Components to Audit

- [ ] Industries page content and structure
- [ ] Homepage and About page copy (industry claims)
- [ ] Case studies or portfolio filtering
- [ ] CMS or content source for industry data

## Examples from Other Sites

- **Accenture.com** — Comprehensive industry list with dedicated pages for each sector (including Manufacturing, Logistics, etc.).
- **PwC.com** — Industries organized by sector with cross-industry themes; clear messaging about breadth.
- **McKinsey.com** — Industry pages plus cross-cutting themes (e.g., Operations, Digital) that span industries.
