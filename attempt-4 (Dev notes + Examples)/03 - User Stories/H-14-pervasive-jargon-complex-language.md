# H-14: Pervasive Jargon and Complex Language

**Issue ID:** H-14
**Priority:** High
**WCAG Criteria:** 3.1.5 Reading Level (AAA), 3.1.3 Unusual Words (AAA), 3.1.4 Abbreviations (AAA)
**Affected Personas:** Cognitive Disability, Non-Native Speaker, Senior Person, Big Company Owner, Skeptical User

---

## User Story

**As a** non-native English speaker evaluating this company's services,
**I want** the website to use plain, clear language and explain technical terms when they appear,
**so that** I can understand the service offerings and make an informed decision without needing a glossary or industry background.

---

## Acceptance Criteria

- [ ] All primary page copy (hero sections, service descriptions, CTAs) scores at or below a Grade 8 reading level on the Flesch-Kincaid scale.
- [ ] Industry jargon terms (e.g., "Agentic AI," "bespoke," "cross-functional") are either replaced with plain-language equivalents or defined inline on first use (e.g., via a parenthetical, tooltip, or linked glossary entry).
- [ ] All abbreviations (ROI, CSAT, MVP, etc.) are expanded on first use on each page (e.g., "return on investment (ROI)").
- [ ] Idioms and figurative phrases (e.g., "ship game-changing products," "harness the power") are replaced with literal, concrete descriptions.
- [ ] A glossary page or section exists for recurring technical terms, linked from the first occurrence of each term.
- [ ] CTA labels use plain, action-oriented language (e.g., "Contact Us" instead of "Let's Build Something Great").
- [ ] Headings describe concrete services or outcomes (e.g., "Custom Software Development" instead of "Digital Solutions").

---

## How to Test the Change

### Manual Testing

1. **Readability analysis:** Paste each page's main body copy into [Hemingway Editor](https://hemingwayapp.com/) or run it through a Flesch-Kincaid tool. Confirm the reading level is Grade 8 or below.
2. **Non-native speaker review:** Ask 2–3 non-native English speakers to read the homepage and services page. Ask them to identify any words or phrases they don't understand. Target: zero unexplained terms.
3. **Abbreviation audit:** Search the rendered page for uppercase abbreviations (ROI, CSAT, MVP, AI). Confirm each is expanded on first use.
4. **Five-second test:** Show the hero section to someone unfamiliar with the tech industry. Ask them what the company does. They should be able to answer concretely.
5. **Jargon highlight test:** Print the page content and highlight every jargon term, idiom, or abbreviation. Each highlighted term should either be replaced or have an adjacent definition.

### Automated Testing

```python
# Python readability check using textstat
import textstat

copy = """
LaunchPad Lab designs, builds, and scales custom web and mobile
applications for growing businesses. Our teams work alongside yours
to modernize operations and reach your customers faster.
"""

score = textstat.flesch_kincaid_grade(copy)
assert score <= 8.0, f"Reading level too high: Grade {score}"
```

```javascript
// Front-end abbreviation check
const body = document.body.innerText;
const abbreviations = ['ROI', 'CSAT', 'MVP', 'KPI', 'SaaS', 'API'];
abbreviations.forEach(abbr => {
  const regex = new RegExp(`\\b${abbr}\\b`);
  if (regex.test(body)) {
    // Check if expanded form appears before the abbreviation
    const expandedPattern = new RegExp(`[a-z].*\\(${abbr}\\)`, 'i');
    if (!expandedPattern.test(body)) {
      console.warn(`Abbreviation "${abbr}" used without expansion`);
    }
  }
});
```

---

## Developer Notes

### General Approach

Conduct a full content audit and rewrite. Replace jargon with plain language, expand abbreviations, and add inline definitions or a glossary for necessary technical terms. This is primarily a content/copywriting task, but developers need to implement the glossary mechanism.

### Current State (Problem)

Examples of problematic copy from the site:

| Current Copy | Problem |
|---|---|
| "Agentic AI" | Undefined industry neologism — meaningless to most readers |
| "bespoke digital products" | "Bespoke" is a rarely-used formal term; "custom" is clearer |
| "cross-functional teams" | Industry jargon; "teams with mixed skills" is plainer |
| "ship game-changing products" | Idiom + hyperbole; say "deliver effective software" instead |
| "harness the power of technology" | Cliche; replace with a concrete statement of what the technology does |
| "ROI," "CSAT" | Abbreviations never expanded on the page |

### Recommended Rewrites

| Before | After |
|---|---|
| "We harness the power of Agentic AI to ship game-changing products." | "We use AI tools to build software that solves real business problems." |
| "Our bespoke digital solutions drive ROI." | "Our custom software helps you save time and increase revenue (return on investment)." |
| "Cross-functional teams deliver CSAT improvements." | "Our teams — designers, developers, and strategists — help you improve customer satisfaction (CSAT)." |

### Implementing a Glossary Tooltip

```html
<!-- Inline definition with <dfn> + <abbr> -->
<p>
  Our teams help you improve
  <dfn><abbr title="Customer Satisfaction Score">CSAT</abbr></dfn>
  by building better digital experiences.
</p>
```

```css
abbr[title] {
  text-decoration: underline dotted;
  cursor: help;
}

/* Tooltip on hover/focus */
abbr[title]:hover::after,
abbr[title]:focus::after {
  content: attr(title);
  position: absolute;
  background: #333;
  color: #fff;
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 0.875rem;
  white-space: nowrap;
  margin-top: 1.5em;
}
```

### Components / Files to Audit

- All page templates: homepage, services, about, contact, case studies
- Hero section content (CMS fields or hardcoded)
- Service card descriptions
- Mega menu descriptions
- CTA button text across all pages
- Meta descriptions and `<title>` tags (often contain jargon too)

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **Basecamp** | Homepage copy reads at ~Grade 6. "Basecamp is a project management tool that helps small teams move faster." | Concrete, no jargon, immediately understandable by anyone. |
| **GOV.UK** | Content design guidelines mandate a Grade 9 or lower reading level; plain English is policy | Government services must be accessible to all literacy levels. |
| **Mailchimp Content Style Guide** | Recommends "Use short words" and "Write for translation" | Designed for a global audience with varying English fluency. |
| **Stripe** | Technical docs define every term on first use; marketing pages use plain language | Balances technical accuracy with accessibility. |
