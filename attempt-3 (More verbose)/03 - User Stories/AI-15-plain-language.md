# AI-15: Replace Jargon with Plain Language

## Metadata
- **ID:** AI-15
- **Priority:** 2 High
- **Personas Affected:** 5+ of 16 personas
- **WCAG Criteria:** 3.1.3 Unusual Words (AAA), 3.1.4 Abbreviations (AAA), 3.1.5 Reading Level (AAA)
- **Effort:** Medium (4–8 hours)

---

## User Story

**As a** non-native English speaker, person with cognitive disability, senior user, or general visitor,

**I want** the website copy to use plain language instead of jargon, acronyms, and idioms,

**So that** I can quickly understand what LaunchPad Lab does and how they can help me, without needing to look up unfamiliar terms.

---

## Acceptance Criteria

- [ ] All acronyms (ROI, MVP, UAT, etc.) are expanded on first use
- [ ] Jargon terms replaced with plain equivalents: "bespoke" → "custom," "agentic" → "AI that acts on your behalf"
- [ ] Idioms removed or replaced: "harness the power" → "use" or "leverage"
- [ ] Hero/summary text explains the company in one clear sentence
- [ ] Reading level targets 8th grade or lower (Flesch-Kincaid Grade Level)
- [ ] No unexplained technical terms (e.g., "AI-centric," "discovery process" without context)
- [ ] A non-technical person can read and explain what the company does in their own words

---

## Test Plan

### Readability Tools
1. Copy homepage and key page content into Hemingway Editor or similar
2. **Expected:** Grade 8 or lower reading level
3. Run through WebFX Readability Tool or similar
4. **Expected:** No "complex" or "very complex" sentences without simplification

### Acronym Audit
1. Search site for: ROI, MVP, UAT, API, UX, UI, etc.
2. **Expected:** Each acronym expanded on first use: "Return on Investment (ROI)" or use `<abbr title="Return on Investment">ROI</abbr>`
3. Check that expansion appears before the acronym in the same section/page

### Jargon Audit
1. Create list of jargon terms from content audit
2. **Expected:** Each has a plain replacement or is explained in context
3. Terms to check: "AI-centric," "bespoke," "agentic," "discovery process," "seamless handoff," "leverage," "synergy"

### User Testing
1. Ask a non-technical person (friend, colleague) to read the homepage
2. Ask: "What does this company do?"
3. **Expected:** They can explain in 1–2 sentences without confusion
4. Note any terms they ask about or stumble over

### Idiom Check
1. Search for: "harness," "cutting edge," "best-in-class," "game-changer," "low-hanging fruit"
2. **Expected:** Replaced with direct, literal language where possible

---

## Developer Notes

### Content Audit Spreadsheet
Create a spreadsheet with columns:
- **Term** | **Location (URL + section)** | **Plain Replacement** | **Status**

Example:
| Term | Location | Replacement | Status |
|------|----------|-------------|--------|
| bespoke | Homepage hero | custom | Done |
| agentic AI | Services | AI that acts on your behalf | Done |
| discovery process | About | research phase | Done |

### Hero Plain-Language Summary
**Before:** "We're an AI-centric digital product studio..."
**After:** "We build websites, mobile apps, and AI tools for businesses."

### Replacement Guide
| Jargon | Plain Equivalent |
|--------|------------------|
| bespoke | custom |
| agentic AI | AI that acts on your behalf |
| discovery process | research phase |
| seamless handoff | smooth transition between teams |
| AI-centric | focused on AI |
| harness the power | use |
| leverage | use |
| synergy | working together |

### Acronym Markup
```html
<abbr title="Return on Investment">ROI</abbr>
<abbr title="Minimum Viable Product">MVP</abbr>
<abbr title="User Acceptance Testing">UAT</abbr>
```

First use in body: "Return on Investment (ROI)" — then use ROI alone or with abbr.

### Consider a Glossary Page
- Link from first use of technical terms: "See our glossary"
- Or use `<dfn>` for definitions inline

### Files to Modify
- Homepage copy
- Services/About pages
- Contact page
- Any landing pages or case studies
- Meta descriptions and OG tags (for consistency)

---

## Examples

| Site | Approach |
|------|----------|
| **GOV.UK** | Plain language standard; "Start here" instead of "Begin"; no jargon |
| **Mailchimp Content Style Guide** | Plain language guidelines; avoid jargon; write for clarity |
| **Basecamp.com** | Simple, direct copy; no corporate speak; conversational tone |
