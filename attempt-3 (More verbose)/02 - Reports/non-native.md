# Accessibility Technical Report: Non-Native English Speaker

**Persona:** Priya Sharma (Non-Native English Speaker, B1/B2 CEFR)  
**Website:** https://launchpadlab.com/  
**Date:** February 16, 2025  
**Testing Focus:** Language accessibility—jargon, idioms, acronyms, and reading level for users with intermediate English proficiency.

---

## Executive Summary

The LaunchPad Lab website presents significant language accessibility barriers for non-native English speakers. Jargon, idioms, unexpanded acronyms, and complex marketing language violate WCAG 2.1 Level AAA success criteria 3.1.3 (Unusual Words), 3.1.4 (Abbreviations), and 3.1.5 (Reading Level). Users with B1/B2 proficiency can complete core tasks (find what the company does, find contact) but require disproportionate effort. Comprehension barriers also undermine trust and willingness to contact.

---

## Issues Identified

### 1. Unusual Words (Jargon) Without Definitions or Explanations

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 3.1.3 Unusual Words (Level AAA) |
| **Severity** | High |
| **Finding** | The site uses industry and marketing jargon without definitions: "AI-centric," "bespoke," "agentic," "agentic AI," "discovery process," "seamless handoff," "cross-functional," "proof of concept," "operational efficiency," "codification," "digital product design." Terms appear in hero, service descriptions, testimonials, and About page. |
| **Impact** | Non-native speakers must guess, look up, or skip. Comprehension fails; users may abandon before understanding the company's purpose. Trust is undermined when key value proposition is opaque. |
| **Fix** | Provide a glossary or expand first use of each term with plain-language equivalent. Example: "AI-centric (focused on artificial intelligence)," "bespoke (custom-built for your needs)," "discovery process (we learn about your business and requirements before building)." Add a plain-language hero summary: "We build websites and mobile apps for businesses. We help you add AI to your products." |
| **WCAG Criterion** | 3.1.3 Unusual Words — "A mechanism is available for identifying specific definitions of words or phrases used in an unusual or restricted way, including idioms and jargon." |

---

### 2. Idioms and Figurative Expressions Without Alternatives

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 3.1.3 Unusual Words (Level AAA) |
| **Severity** | High |
| **Finding** | Marketing copy uses idioms that do not translate: "harness the power," "move the needle," and similar figurative expressions. Idioms assume cultural and linguistic familiarity non-native speakers lack. Translation tools often fail on idioms. |
| **Impact** | Literal interpretation produces nonsense. Users skip or misinterpret key messaging. Value proposition is lost. |
| **Fix** | Replace idioms with literal, direct language. "Harness the power of AI" → "Use AI to improve your business." "Move the needle" → "Get real, measurable results." Audit all marketing copy for figurative expressions; provide plain-language alternatives. |
| **WCAG Criterion** | 3.1.3 Unusual Words — explicitly includes "idioms" as requiring mechanism for identification or explanation. |

---

### 3. Abbreviations (Acronyms) Without Expanded Form

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 3.1.4 Abbreviations (Level AAA) |
| **Severity** | Medium–High |
| **Finding** | Acronyms appear without expansion on first use: ROI, MVP, UAT, UX, AI. Site assumes familiarity. No mechanism (glossary, tooltip, parenthetical) provides expanded form or meaning. |
| **Impact** | Users must guess or look up. ROI and MVP may be inferable for some; UAT is obscure. Time lost; comprehension delayed. Users feel excluded. |
| **Fix** | Expand on first use: "ROI (Return on Investment)," "MVP (Minimum Viable Product)," "UAT (User Acceptance Testing)," "UX (User Experience)." Provide glossary link for repeated acronyms. Ensure programmatic expansion (e.g., `<abbr title="Return on Investment">ROI</abbr>`) where appropriate. |
| **WCAG Criterion** | 3.1.4 Abbreviations — "A mechanism for identifying the expanded form or meaning of abbreviations is available." |

---

### 4. Reading Level Exceeds Lower Secondary Education

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 3.1.5 Reading Level (Level AAA) |
| **Severity** | High |
| **Finding** | Hero, service descriptions, and testimonials use long sentences (20+ words), passive voice, multiple clauses, and abstract concepts. Examples: "Their attention to detail in the discovery process, and their selective choice of questioning is what really stood out to me"; "through what could otherwise become a tumultuous journey of entrepreneurship." Reading level exceeds approximately 7th grade (lower secondary). |
| **Impact** | Non-native speakers read 20–40% more slowly. Long, complex sentences require re-reading 2–3 times. Comprehension drops; fatigue increases. Abandonment risk rises. |
| **Fix** | Rewrite key content in short sentences (under 15 words). One idea per sentence. Use active voice. Replace abstract claims with concrete examples. Provide supplemental plain-language summary or "Simple version" for dense sections. |
| **WCAG Criterion** | 3.1.5 Reading Level — "When text requires reading ability more advanced than the lower secondary education level... supplemental content, or a version that does not require reading ability more advanced than the lower secondary education level, is available." |

---

### 5. Unclear or Inconsistent Contact Labels

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.4 Link Purpose (In Context), 2.4.6 Headings and Labels (Level AA) |
| **Severity** | Medium |
| **Finding** | Primary contact CTA is "Connect with an Expert" rather than "Contact" or "Contact Us." Non-native speakers expect conventional labels. "Connect with an Expert" requires decoding; purpose is not explicit. |
| **Impact** | Users hesitate or search for "Contact" before recognizing the CTA. Cognitive load increases. Contact path is not obvious. |
| **Fix** | Add "Contact" to primary navigation. Use "Contact Us" or "Get in Touch" as primary label. If "Connect with an Expert" is retained for marketing, pair with "Contact" (e.g., "Contact Us — Connect with an Expert"). Ensure footer includes clear "Contact" link. |
| **WCAG Criterion** | 2.4.4 Link Purpose (In Context), 2.4.6 Headings and Labels |

---

### 6. Contact Form Buried Below Testimonials

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.1 Bypass Blocks (Level A), 2.4.6 Headings and Labels |
| **Severity** | Medium |
| **Finding** | Contact page displays five long testimonial blocks above the contact form. Users must scroll extensively to reach the form. Testimonials use same jargon as main copy; they add confusion rather than value for language-struggling users. |
| **Impact** | Users who came to contact must wade through dense, jargon-heavy content. Fatigue increases. Some may abandon. Form completion rate may drop. |
| **Fix** | Move contact form above testimonials. Or add "Skip to contact form" link at top of Contact page. Consider moving testimonials to separate section or below fold with clear heading. |
| **WCAG Criterion** | 2.4.1 Bypass Blocks — "A mechanism is available to bypass blocks of content that are repeated on multiple Web pages." |

---

### 7. No Plain-Language Value Proposition

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 3.1.5 Reading Level (Level AAA), 2.4.6 Headings and Labels |
| **Severity** | High |
| **Finding** | Hero and homepage lack a single, clear, plain-language statement of what the company does. "AI-Centric Digital Product Design & Development" is abstract. Users must visit multiple pages (Services, Work, About) to piece together: they build websites and apps. |
| **Impact** | Core task ("find what they do") requires excessive effort. Users with limited time or patience may leave before understanding. Trust is delayed. |
| **Fix** | Add prominent plain-language summary at top of homepage: "We build websites and mobile apps for businesses. We help you add AI to your products. Contact us to discuss your project." Ensure this appears above the fold. |

---

## Summary Table

| Issue | WCAG Ref | Severity | Priority |
|-------|----------|----------|----------|
| Jargon without definitions | 3.1.3 | High | P0 |
| Idioms without alternatives | 3.1.3 | High | P0 |
| Acronyms without expansion | 3.1.4 | Medium–High | P0 |
| Reading level too high | 3.1.5 | High | P0 |
| No plain-language value proposition | 3.1.5, 2.4.6 | High | P0 |
| Unclear contact labels | 2.4.4, 2.4.6 | Medium | P1 |
| Form buried below testimonials | 2.4.1 | Medium | P1 |

---

## Recommended Remediation Order

1. **Add plain-language hero summary** — One sentence: "We build websites and mobile apps for businesses. We help you add AI to your products."
2. **Expand acronyms on first use** — ROI (Return on Investment), MVP (Minimum Viable Product), UAT (User Acceptance Testing), UX (User Experience).
3. **Replace or explain jargon** — Glossary, tooltips, or inline expansion for: AI-centric, bespoke, agentic, discovery process, seamless handoff, cross-functional, proof of concept.
4. **Replace idioms with literal language** — Audit for "harness the power," "move the needle," etc.; substitute direct equivalents.
5. **Simplify sentence structure** — Short sentences, active voice, one idea per sentence for hero, services, and key CTAs.
6. **Clarify contact path** — Add "Contact" to nav; move form above testimonials or add skip link.
7. **Provide supplemental plain-language version** — Consider "Simple summary" expandable section or alternate page for users who need lower reading level.

---

## References

- [WCAG 2.1 Success Criterion 3.1.3 Unusual Words (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/unusual-words.html)
- [WCAG 2.1 Success Criterion 3.1.4 Abbreviations (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/abbreviations.html)
- [WCAG 2.1 Success Criterion 3.1.5 Reading Level (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/reading-level.html)
- [Plain Language Guidelines](https://www.plainlanguage.gov/guidelines/)
