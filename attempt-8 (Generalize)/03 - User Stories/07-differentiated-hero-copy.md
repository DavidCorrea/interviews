# User Story: Differentiated Homepage Hero Copy

**Priority:** Low  
**Related Finding:** [Finding 7](../main-report.md#finding-7)

## Story
As a first-time visitor, I want the homepage headline to communicate a specific, differentiating value proposition, so that I immediately understand what makes this agency unique among the dozens of digital agencies I could visit.

## Context
The current homepage headline "AI Innovation. Digital Solutions. Results that Matter." is perceived as generic. "Results that Matter" in particular is a phrase that could appear on any agency site. The headline misses an opportunity to lead with concrete differentiators the agency actually has — such as the 6-week launch timeline, 730+ completed projects, or AI-first approach with proprietary tools like Mission Control.

## Acceptance Criteria
- The homepage headline contains at least one specific, verifiable claim (a number, timeline, or concrete capability)
- The headline would NOT make sense on a competitor's website without modification
- A/B testing is set up to validate the new headline against the current one (recommended but not required)

## How to Test
1. Read the homepage headline to 5 people unfamiliar with the agency
2. Ask them what makes this agency different from others
3. If they can answer with something specific (not just "they do AI"), the headline succeeds
4. Verify the headline contains at least one concrete differentiator

## Developer Notes

### General Approach
Update the hero heading copy. This is a content change in the CMS or hardcoded template. Consider A/B testing variants.

### Components to Audit
- Homepage hero component (heading + subheading)
- CMS entry for hero content

### Code Examples
```jsx
// Before
<h1>AI Innovation. Digital Solutions. Results that Matter.</h1>

// Option A: Lead with speed
<h1>From Idea to Launch in 6 Weeks. AI-Powered Product Development.</h1>

// Option B: Lead with track record
<h1>730+ Digital Products Built. Yours Could Be Next.</h1>

// Option C: Lead with AI differentiation
<h1>We Don't Just Talk About AI — We Ship It. In 6 Weeks.</h1>
```

## How Other Sites Achieve This
- **Vercel** — "Develop. Preview. Ship." — three words that uniquely describe their workflow, not generic claims
- **Linear** — "Linear is a purpose-built tool for planning and building products" — specific about what they are
- **Basecamp** — "The All-In-One Toolkit for Working Remotely" — specific positioning, not generic quality claims
