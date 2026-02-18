# User Story: Pricing Transparency for Self-Qualification

**Priority:** Medium  
**Related Finding:** [Finding 5](../main-report.md#5-no-pricing-information-or-budget-expectations)

## Story
As a potential client with budget constraints, I want some indication of pricing ranges or engagement tiers, so that I can self-qualify before reaching out and set appropriate expectations.

## Context
The entire site lacks any pricing indicators — no ranges, tiers, or starting-at figures. Budget-conscious prospects (startup founders, small businesses) cannot determine if the agency is within their price range without initiating contact. This may deter users who assume the agency is out of their budget, even when offerings like the free AI Opportunity Workshop exist.

## Acceptance Criteria
- A pricing FAQ entry exists on the Services page or a dedicated Pricing page addressing "How much does it cost?"
- At minimum, engagement tier descriptions are provided (e.g., "Discovery: starts at $X," "MVP Build: $X-$Y range")
- The free AI Opportunity Workshop is more prominently surfaced as a zero-cost starting point
- Budget expectations are set without requiring a form submission

## How to Test
1. Navigate to the site as a first-time visitor
2. Search for pricing-related information without submitting a contact form
3. Confirm pricing context is available within 3 clicks of the homepage
4. Verify the free workshop is visible on the Services page and/or homepage

## Developer Notes

### General Approach
Add a pricing FAQ section or a lightweight pricing page. Alternatively, add pricing context to the existing Services page FAQ accordion. No complex backend needed — this is content.

### Components to Audit
- Services page FAQ accordion
- Contact page (could add "What to expect" section)
- Homepage (surface the free workshop more prominently)
- Navigation menu (consider adding "Pricing" link)

### Code Examples
```jsx
// FAQ accordion entry
<AccordionItem>
  <AccordionHeader>How much does it cost to work with LaunchPad Lab?</AccordionHeader>
  <AccordionContent>
    <p>Every project is different, but here are some typical engagement ranges:</p>
    <ul>
      <li><strong>AI Opportunity Workshop:</strong> Free — a no-commitment session to explore your needs</li>
      <li><strong>Discovery & Strategy:</strong> Typically 2-4 weeks</li>
      <li><strong>MVP Build:</strong> 6-12 weeks, with budgets varying based on complexity</li>
      <li><strong>Full Product Development:</strong> 3-6+ months</li>
    </ul>
    <p>
      <a href="/contact">Reach out</a> to discuss your specific project and we'll 
      provide a tailored estimate.
    </p>
  </AccordionContent>
</AccordionItem>
```

## How Other Sites Achieve This
- **Toptal** (toptal.com) — shows hourly rate ranges by skill level
- **Thoughtbot** (thoughtbot.com) — has a dedicated "Hiring" page with transparent engagement models and typical investment ranges
- **Scalable Path** — shows project budget ranges on their pricing page
