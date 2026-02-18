# Replace Vague Marketing Language with Specific, Outcome-Oriented Copy

## Priority: Low

## User Story
As a non-technical business executive, I want the website to use specific, outcome-oriented language instead of vague industry buzzwords so that I can understand exactly what the company is offering without feeling talked-at.

## Acceptance Criteria
- [ ] No instances of "bespoke," "agile," "cross-functional," "synergy," "leverage," or similar buzzwords appear in marketing copy without clear, concrete explanation
- [ ] Each service offering describes a specific outcome or deliverable the user receives (e.g., "custom-built for your business" instead of "bespoke")
- [ ] A non-technical reviewer can read the homepage, service pages, and About Us page and explain in plain language what the company does
- [ ] Navigation dropdown descriptions use concrete language that answers "what do I get?" rather than abstract terminology
- [ ] Copy passes a readability check: no more than 2 industry jargon terms per page without immediate clarification

## Developer Notes

### General Explanation
Terms like "bespoke," "agile," and "cross-functional teams" are used in ways that sound like marketing-speak to non-technical users. While these terms don't prevent task completion, they add low-level friction and reduce the sense that the company is speaking directly to the user's needs. The fix is to audit all marketing copy and replace vague buzzwords with specific, concrete descriptions of what the user gets.

**Replacement guidelines:**
- "Bespoke" → "custom-built for your business"
- "Agile" → "we work in short cycles and show you progress every two weeks"
- "Cross-functional teams" → "a team of designers, developers, and strategists working together"
- "Synergy" → describe the specific benefit (e.g., "your team and ours work as one unit")
- "Leverage" → "use" or "apply" with a concrete example

### Code Examples
Content changes are primary; below are component template examples where text lives:

```html
<!-- Before: vague buzzword -->
<p>We deliver bespoke solutions with agile, cross-functional teams.</p>

<!-- After: specific, outcome-oriented -->
<p>We build custom software for your business. Our team of designers, developers, and strategists work together in two-week cycles, so you see progress regularly and can adjust as we go.</p>
```

```jsx
// Example: Service page hero component
// Before
<h1>Bespoke Digital Solutions</h1>
<p>Leverage our agile methodology and cross-functional expertise.</p>

// After
<h1>Custom Software Built for Your Business</h1>
<p>We design, build, and launch digital products. You get a dedicated team that works in short sprints and shows you progress every two weeks.</p>
```

### Components to Audit
- Homepage hero and value proposition sections
- All service pages (e.g., Product Strategy, Design, Development, etc.)
- About Us page
- Navigation dropdown descriptions
- Case study summaries and service blurbs
- Footer or CTA copy

## Examples From Other Sites

- **Basecamp** — Uses plain, direct language throughout. Their product pages describe exactly what you get ("Message boards," "To-dos," "Schedule") without jargon. They avoid "synergy" and "leverage" in favor of simple verbs and concrete nouns.

- **Stripe** — Stripe's marketing copy explains complex payment infrastructure in plain terms. Instead of "leverage our API," they say "accept payments and manage subscriptions online." Technical concepts are introduced only when necessary and always with clear context.

- **Mailchimp** — Mailchimp famously uses approachable, conversational copy. Their service descriptions focus on outcomes ("Send better emails," "Get your business online") rather than methodology buzzwords. They speak to small business owners who may have no technical background.

## References
- Main Report Item 8 (Low Priority): Vague marketing language ("bespoke," "agile," "cross-functional teams") adds low-level friction for non-technical users
- Interview findings: Non-technical business executives reported feeling "talked-at" rather than spoken to directly
