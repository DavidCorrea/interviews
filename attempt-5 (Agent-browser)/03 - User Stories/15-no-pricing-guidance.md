# 15. Add Pricing Guidance to Help Prospects Self-Qualify

**Priority:** Medium
**Location:** Sitewide — absent from all pages
**Reported by:** Richard Okonkwo (Non-Technical Business Executive)

---

## User Story

**As a** non-technical business executive evaluating software agencies under time pressure,
**I want** to see directional pricing or budget expectations on the website
**so that** I can quickly determine whether LaunchPad Lab is within my budget range before investing time in a sales conversation.

---

## Acceptance Criteria

- [ ] A FAQ entry addressing pricing exists on at least one page (Services, Contact, or a dedicated FAQ section)
- [ ] The pricing guidance includes a directional range (e.g., "Projects typically start at $X" or "range from $X to $Y")
- [ ] The language clarifies that pricing is project-dependent and offers factors that influence cost (scope, timeline, complexity)
- [ ] A CTA links from the pricing FAQ to the contact form for a custom estimate
- [ ] The pricing information is written in plain language without jargon (no "SOW," "T&M," "retainer" without explanation)
- [ ] The FAQ entry is visible without requiring user interaction (not buried behind collapsed accordion items)
- [ ] The content passes readability checks at an 8th-grade reading level

---

## How to Test

1. **Navigate** to the Services page, Industries page, and Contact page
2. **Search** for any mention of pricing, cost, budget, or investment — confirm the FAQ entry is present on at least one of these pages
3. **Read the pricing FAQ entry** — verify it includes a directional range and factors that influence cost
4. **Verify plain language** — confirm no unexplained jargon (run through [Hemingway Editor](https://hemingwayapp.com/) to check readability grade)
5. **Click the CTA** in the pricing section — verify it navigates to the contact form or scrolls to it
6. **Check visibility** — confirm the pricing FAQ is expanded by default or otherwise visible without additional clicks
7. **Test on mobile** — verify the pricing information is accessible and readable on small screens
8. **Screen reader test** — navigate to the pricing section using VoiceOver (macOS) or NVDA (Windows) and confirm the content is announced clearly

---

## Developer Notes

### Approach

Add a pricing/investment FAQ entry to the Services page and/or Contact page. The content should provide enough information for prospects to self-qualify without committing to exact prices (which vary by project). Consider adding a dedicated "What to Expect" or "Investment" section on the Services page above the existing FAQ accordion.

### Option A: Add to Existing FAQ Accordion

If the Services page already uses an accordion for FAQs, add a new entry and ensure it's expanded by default (see Issue #18 for related guidance).

```html
<section class="faq-section" aria-labelledby="faq-heading">
  <h2 id="faq-heading">Frequently Asked Questions</h2>

  <details class="faq-item" open>
    <summary>
      <h3>How much does a custom software project cost?</h3>
    </summary>
    <div class="faq-answer">
      <p>
        Every project is different, but here's what you can expect:
      </p>
      <ul>
        <li><strong>Small projects</strong> (MVP, prototype, or single feature): starting around <strong>$50,000–$150,000</strong></li>
        <li><strong>Mid-size projects</strong> (full web or mobile application): typically <strong>$150,000–$500,000</strong></li>
        <li><strong>Large or ongoing engagements</strong> (enterprise platforms, long-term partnership): <strong>$500,000+</strong></li>
      </ul>
      <p>
        Cost depends on <strong>scope</strong> (how many features), <strong>complexity</strong> (integrations, data migration, compliance requirements), and <strong>timeline</strong> (how quickly you need it).
      </p>
      <p>
        <a href="/contact/" class="cta-link">Get a free estimate</a> — tell us about your project and we'll provide a ballpark within 2 business days.
      </p>
    </div>
  </details>
</section>
```

### Option B: Standalone Investment Section (Higher Visibility)

Place a dedicated section higher on the Services or Contact page, outside the FAQ accordion, for maximum visibility.

```html
<section class="investment-section" aria-labelledby="investment-heading">
  <h2 id="investment-heading">What to Expect: Investment & Timeline</h2>

  <div class="investment-grid">
    <div class="investment-card">
      <h3>Starting Projects</h3>
      <p class="price-range">$50K – $150K</p>
      <p>MVPs, prototypes, and single-feature applications to validate your idea quickly.</p>
    </div>

    <div class="investment-card">
      <h3>Full Applications</h3>
      <p class="price-range">$150K – $500K</p>
      <p>Complete web or mobile applications with multiple features, integrations, and user roles.</p>
    </div>

    <div class="investment-card">
      <h3>Enterprise Platforms</h3>
      <p class="price-range">$500K+</p>
      <p>Large-scale platforms, ongoing development partnerships, and complex enterprise systems.</p>
    </div>
  </div>

  <p class="investment-note">
    These ranges are directional — your project may be higher or lower depending on scope, complexity, and timeline.
    <a href="/contact/">Contact us for a free, no-obligation estimate.</a>
  </p>
</section>
```

### CSS for Investment Cards

```css
.investment-section {
  padding: 4rem 2rem;
  background-color: #f8f9fa;
}

.investment-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
  margin: 2rem 0;
}

.investment-card {
  background: #ffffff;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 2rem;
  text-align: center;
}

.investment-card h3 {
  font-size: 1.25rem;
  margin-bottom: 0.5rem;
  color: #333333;
}

.price-range {
  font-size: 1.75rem;
  font-weight: 700;
  color: #1a73e8;
  margin-bottom: 1rem;
}

.investment-note {
  font-size: 1rem;
  line-height: 1.8;
  color: #555555;
  text-align: center;
  margin-top: 1.5rem;
}
```

### Components to Audit

- **Services page** — FAQ section at the bottom; consider adding an Investment section above it
- **Contact page** — Add a brief pricing note near the contact form to set expectations
- **Industries page** — FAQ section at the bottom
- **Homepage** — Consider a brief mention in the "Why LaunchPad Lab" or stats section
- **Navigation** — Consider whether a "Pricing" or "What to Expect" nav item would reduce bounce rate

### WCAG References

- **WCAG 2.1 SC 3.1.5 Reading Level (AAA):** Content should be written at a lower secondary education reading level, or supplementary content should be provided
- **WCAG 2.1 SC 2.4.6 Headings and Labels (AA):** Headings describe topic or purpose — pricing headings should clearly indicate the section contains cost information

---

## Examples from Other Sites

### Thoughtbot (thoughtbot.com)
Includes a dedicated "Hire Us" page with transparent information about engagement models, team composition, and pricing structure. They state weekly rates and typical project durations, helping prospects self-qualify before the first call.

### Pivotal Labs (now VMware Tanzu Labs)
Historically published pricing transparently (e.g., "$X per developer per week") which built trust and attracted right-fit clients. Their directness about cost was a competitive differentiator.

### Basecamp (basecamp.com)
While a product company (not a consultancy), Basecamp's pricing page is a gold standard for clarity — one price, explained simply, with an FAQ addressing every common objection. The approach of "answer every question before they ask" applies directly.

### Toptal (toptal.com)
Provides talent-rate ranges by role and seniority on their website. While the model is different, the principle of giving prospects enough information to self-qualify before committing to a call is the same.

### Key Pattern
The most effective agency pricing pages share these traits:
1. **Directional ranges** — not exact quotes, but enough to filter out mismatches
2. **Factors that influence cost** — so the prospect understands _why_ there's a range
3. **Clear CTA** — "Get a custom estimate" paired with the pricing info
4. **No jargon** — "project" not "engagement," "cost" not "investment"
