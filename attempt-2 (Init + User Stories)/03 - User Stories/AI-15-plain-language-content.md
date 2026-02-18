# AI-15: Plain Language Content

## Title
Replace jargon, idioms, and unexpanded acronyms with plain language across the site

## User Story
As a **visitor with limited English proficiency or cognitive differences**, I want **content written in plain, clear language**, so that **I can understand what the company does and offers without confusion or frustration**.

## Acceptance Criteria

- [ ] No unexplained acronyms appear on any page; all acronyms are expanded on first use (e.g., "ROI (Return on Investment)")
- [ ] Jargon terms (e.g., "bespoke," "agentic") are replaced with plain-language alternatives
- [ ] Idioms (e.g., "harness the power") are replaced with direct, literal phrasing
- [ ] Homepage and About page each include a 1–2 sentence plain-language summary at the top
- [ ] A non-native English speaker (B1/B2 level) can understand what the company does within 30 seconds of reading key pages

## How to Test

1. Have a non-native English speaker (B1/B2 proficiency) read the Homepage, About, and Services pages.
2. Time how long it takes for them to understand what the company does (target: ≤ 30 seconds).
3. Ask them to identify any words or phrases they did not understand.
4. Audit all pages for unexplained acronyms and flag any found.
5. Audit all pages for idioms and jargon; verify none remain.

## Developer Notes

- **Content audit:** Replace common jargon:
  - "bespoke" → "custom-made"
  - "agentic" → "AI that works independently"
  - "discovery process" → "we talk with you to understand your needs"
- **Acronyms:** Expand on first use: "ROI (Return on Investment)", "API (Application Programming Interface)"
- **Idioms:** Replace with direct language: "harness the power" → "use"
- Add 1–2 sentence plain-language summary at top of Homepage and About page.

## WCAG References

- **3.1.3 Unusual Words (Level AAA):** A mechanism is available for identifying specific definitions of words or phrases used in an unusual or restricted way.
- **3.1.4 Abbreviations (Level AAA):** A mechanism for identifying the expanded form or meaning of abbreviations is available.
- **3.1.5 Reading Level (Level AAA):** When text requires reading ability more advanced than the lower secondary education level, supplemental content or a version that does not require such reading ability is available.

## Priority
**P2 High**

## Effort Estimate
**Medium (4–8h)**
