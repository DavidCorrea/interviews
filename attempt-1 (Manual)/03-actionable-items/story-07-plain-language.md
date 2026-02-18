# Story 07: Simplify Language and Define Jargon

## User Story

**As a** user who is not a technology expert (senior, non-native English speaker, person with cognitive disability),
**I want** the site to use plain, simple language and explain any technical terms,
**So that** I can understand what the company does and how to engage with them.

## Description

The site uses extensive business jargon ("agentic," "bespoke," "cross-functional"), undefined acronyms (ROI, UAT, UI/UX, CSAT), metaphorical language ("harness the power," "unlock growth"), and long, complex sentences (20+ words with multiple clauses). Six different user groups reported confusion, frustration, or inability to understand the site's core message.

## Acceptance Criteria

- [ ] The main homepage headline clearly states what the company does in plain English
- [ ] All acronyms are spelled out on first use (e.g., "ROI (Return on Investment)")
- [ ] Jargon terms are replaced with plain alternatives (e.g., "bespoke" → "custom-made," "deploy" → "launch")
- [ ] No sentence exceeds 20 words
- [ ] Dense paragraphs are replaced with bullet-point lists where possible
- [ ] Content reads at a Grade 8 reading level or below (verified with a readability tool)
- [ ] Each page or major section includes a TLDR/summary sentence at the top

## Testing Instructions

1. **Readability tool:** Run homepage and key service page copy through a readability analyzer (e.g., Hemingway App, readable.com) — verify Grade 8 or below reading level
2. **Acronym search:** Search the site for common acronyms (ROI, UAT, UI/UX, CSAT, CRM) — each should be spelled out on first use per page
3. **Jargon audit:** Search for flagged terms ("bespoke," "agentic," "leverage," "harness," "cross-functional," "seamless handoff") — verify they are replaced or explained
4. **User test:** Ask a non-technical person to read the homepage and explain what the company does in their own words — they should be able to answer clearly
5. **Sentence length:** Spot-check 10 paragraphs across the site — no sentence should exceed 20 words

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | Critical |
| **Complexity** | High |
| **WCAG Criteria** | 3.1.3 (Unusual Words), 3.1.5 (Reading Level) |
| **Affected Users** | Seniors, cognitive disability, non-native English speakers, stressed users, ADHD, dyslexic users |

## Source Reports

- Senior User Report
- Cognitive Disability Report
- Non-Native English Speaker Report
- Stressed User Report
- ADHD User Report
- Dyslexic User Report
