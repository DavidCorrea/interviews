# Dense Enterprise Language

## Priority
**Medium**

## User Story
As a business user or potential client, I want clear, plain language that explains what LaunchPad Lab does and how they can help, so that I can quickly understand the value proposition without wading through jargon.

## Acceptance Criteria

- [ ] Site-wide language is simplified: shorter sentences, fewer buzzwords
- [ ] Key terms like "digital transformation" and "autonomous digital workforce" are either replaced or explained in plain language
- [ ] Reading level is closer to WCAG AAA target (lower secondary education level, ~Grade 8)
- [ ] Bullet points and scannable content are used where appropriate
- [ ] Bullhorn case study is used as a model for specific, concrete content
- [ ] Persona-specific landing pages (if added) use appropriate tone for each audience
- [ ] No sacrifice of professionalism — tone remains credible and expert

## How to Test

1. Read the homepage hero and main value propositions aloud.
2. Count instances of terms like "digital transformation," "game-changing," "autonomous digital workforce."
3. Run a readability test (e.g., Hemingway Editor, Flesch-Kincaid) on key pages.
4. Compare the Bullhorn case study to other service descriptions — note specificity and clarity.
5. Ask a non-technical colleague to summarize what LaunchPad Lab does after 30 seconds on the site.
6. Check that bullet points and headings make content scannable.
7. Verify that plain-language alternatives exist for complex concepts.

## Developer Notes

### General Explanation
Heavy corporate jargon ("digital transformation," "autonomous digital workforce," "game-changing digital products") alienates non-enterprise users and frustrates business users who want substance. WCAG 2.1 AAA suggests content be written to lower secondary education level (Reading Level, 2.4.8). Dense language also affects cognitive accessibility.

**Solution:** Simplify language site-wide. Use shorter sentences, bullet points, and plain-language alternatives. Model content after the Bullhorn case study, which uses specific, concrete language. Consider persona-specific landing pages with appropriate tone. Maintain professionalism while improving clarity.

### Code Examples

**Before (jargon-heavy):**
```html
<p>
  We deliver game-changing digital products that power your autonomous digital
  workforce and accelerate your digital transformation journey.
</p>
```

**After (plain language):**
```html
<p>
  We build software that automates repetitive work and frees your team to focus
  on what matters. From AI-powered tools to custom applications, we help you
  work smarter.
</p>
```

**Bullet points for scannability:**
```html
<section>
  <h2>What We Do</h2>
  <ul>
    <li>Custom software that fits your workflow</li>
    <li>AI and automation to reduce manual tasks</li>
    <li>Design and development from idea to launch</li>
  </ul>
</section>
```

**Glossary or tooltip for necessary jargon:**
```html
<p>
  We help with <dfn id="digital-transformation">digital transformation</dfn>
  — the process of using technology to improve how your business operates.
</p>
```

**Content guidelines (for CMS/copy):**
- Prefer active voice
- Limit sentences to ~15–20 words
- Use "you" and "we" for a conversational tone
- Replace "leverage" with "use," "utilize" with "use"
- Replace "game-changing" with specific outcomes
- Use the Bullhorn case study as a style guide: specific metrics, clear problem/solution

### Components to Audit
- Homepage hero and value propositions
- Services page descriptions
- Industry/solution page copy
- Case study summaries (ensure they're as specific as Bullhorn)
- Meta descriptions and page titles
- Any marketing or CMS-driven content blocks

## Examples from Other Sites

- **Mailchimp.com** — Clear, friendly, jargon-free language. Explains features in plain terms. Tone is approachable without being unprofessional.
- **Stripe.com** — Technical but plain-spoken. Avoids buzzwords; explains concepts clearly. Good model for a technical audience.
- **Basecamp.com** — Conversational and direct. Short sentences, clear value propositions. No corporate fluff.
