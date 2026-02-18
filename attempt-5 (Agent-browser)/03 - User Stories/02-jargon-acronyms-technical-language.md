# Pervasive Jargon, Unexplained Acronyms & Technical Language

**Priority:** High
**Location:** All pages — especially Services, Homepage, Industries
**WCAG:** [3.1.3 Unusual Words (AAA)](https://www.w3.org/WAI/WCAG21/Understanding/unusual-words), [3.1.4 Abbreviations (AAA)](https://www.w3.org/WAI/WCAG21/Understanding/abbreviations), [3.1.5 Reading Level (AAA)](https://www.w3.org/WAI/WCAG21/Understanding/reading-level)

---

## User Story

> As a **non-technical decision-maker evaluating software partners**,
> I want **the website to use plain language and explain any technical terms**
> so that **I can understand what LaunchPad Lab does and how it applies to my business without needing a technology background.**

---

## Problem

The site uses extensive technical terminology without definitions. Terms like ROI, CSAT, UAT, UI/UX, CRM, MVP, CI/CD, Agile, Sprint, cross-functional, bespoke, and "agentic AI" appear without explanation. Marketing idioms like "Harness the power of AI" and "Ship game-changing products" assume insider knowledge. The phrase "digital product" is used where "software," "application," or "system" would be clearer.

**Examples of problematic copy:**

- "We build bespoke digital products using Agile methodology with CI/CD pipelines."
- "Harness the power of agentic AI to drive ROI."
- "Our cross-functional teams deliver MVPs in short Sprints."
- "Improving CSAT scores through intuitive UI/UX."

---

## Acceptance Criteria

- [ ] Every acronym is expanded on first use per page (e.g., "Return on Investment (ROI)").
- [ ] The `<abbr>` HTML element with a `title` attribute is used for all acronyms after first expansion.
- [ ] Industry jargon is replaced with plain-language equivalents (see mapping table below).
- [ ] Idioms and figurative phrases are replaced with literal descriptions.
- [ ] "Digital product" is replaced with specific nouns: "software," "web application," "mobile app," or "system."
- [ ] A glossary page or tooltip system is available for unavoidable technical terms.
- [ ] All page copy scores at or below an 8th-grade reading level on the Flesch-Kincaid scale.

---

## How to Test

1. **Plain-language audit:** Read each page aloud. Every time you encounter a term a non-technical CEO might not immediately understand, flag it.
2. **Acronym check:** Search the codebase for uppercase 2–5 letter sequences (e.g., `grep -E '\b[A-Z]{2,5}\b'`). Verify each has an `<abbr>` tag with `title` on first use.
3. **Readability test:** Paste page text into [Hemingway Editor](https://hemingwayapp.com/) — target grade ≤ 8.
4. **Screen reader test:** Use VoiceOver or NVDA. Verify that acronyms are read with their expanded form (the `title` attribute on `<abbr>` provides this).
5. **User test:** Ask someone outside the tech industry to read the homepage and explain what LaunchPad Lab does. If they struggle, the copy needs work.

---

## Developer Notes

### 1. Acronym markup with `<abbr>`

Always expand on first use, then use `<abbr>` for subsequent mentions:

```html
<!-- First use on the page -->
<p>
  We helped increase their Return on Investment
  (<abbr title="Return on Investment">ROI</abbr>) by 40 %.
</p>

<!-- Subsequent uses -->
<p>
  This <abbr title="Return on Investment">ROI</abbr> improvement
  was sustained over 12 months.
</p>
```

### 2. CSS for `<abbr>` elements

Style abbreviations so users know they can interact:

```css
abbr[title] {
  text-decoration: underline dotted;
  text-decoration-color: currentColor;
  text-underline-offset: 0.15em;
  cursor: help;
}

/* Optional tooltip enhancement */
abbr[title]:hover,
abbr[title]:focus {
  position: relative;
}
```

### 3. Tooltip component for technical terms (optional enhancement)

```html
<span class="glossary-term" tabindex="0" role="term" aria-describedby="tip-agile">
  Agile
  <span class="tooltip" id="tip-agile" role="tooltip">
    A project management approach where work is done in short cycles
    (usually 2 weeks) with regular check-ins.
  </span>
</span>
```

```css
.glossary-term {
  position: relative;
  border-bottom: 1px dashed currentColor;
  cursor: help;
}

.glossary-term .tooltip {
  display: none;
  position: absolute;
  bottom: 100%;
  left: 50%;
  transform: translateX(-50%);
  padding: 0.5rem 0.75rem;
  background: #1a1a1a;
  color: #fff;
  font-size: 0.875rem;
  border-radius: 4px;
  white-space: nowrap;
  max-width: 280px;
  white-space: normal;
  z-index: 10;
}

.glossary-term:hover .tooltip,
.glossary-term:focus .tooltip {
  display: block;
}
```

```javascript
// Ensure tooltips are keyboard accessible and dismissable with Escape
document.querySelectorAll('.glossary-term').forEach(term => {
  term.addEventListener('keydown', (e) => {
    if (e.key === 'Escape') {
      term.blur();
    }
  });
});
```

### 4. Jargon-to-plain-language mapping

| Jargon | Plain Language Replacement |
|---|---|
| Digital product | Software / web application / mobile app |
| Bespoke | Custom / custom-built |
| Agentic AI | AI tools that take actions on your behalf |
| Cross-functional | A team with designers, developers, and strategists |
| MVP | A first working version of the software |
| CI/CD | Automated testing and deployment |
| Agile / Sprint | Working in short cycles with regular check-ins |
| ROI | Return on investment — the value gained vs. the cost |
| CSAT | Customer satisfaction score |
| UAT | User acceptance testing — verifying the software meets your needs |
| UI/UX | The look, feel, and ease of use of the software |
| CRM | Customer relationship management system |
| Ship | Release / launch / deliver |
| Harness the power of | Use / take advantage of |
| Game-changing | Effective / high-impact |
| End-to-end | From start to finish |
| Leverage | Use |

### 5. Glossary page (if terms are unavoidable)

Create a `/glossary/` page with definition list markup:

```html
<h1>Glossary</h1>
<dl>
  <dt id="term-agile">Agile</dt>
  <dd>
    A way of managing projects by working in short cycles (usually 2 weeks),
    reviewing progress frequently, and adjusting the plan as you learn more.
  </dd>

  <dt id="term-mvp">MVP (Minimum Viable Product)</dt>
  <dd>
    The simplest working version of your software that lets real users
    try it and give feedback before you build more features.
  </dd>
</dl>
```

### Components to audit

| Component / Section | Page(s) | Key terms to address |
|---|---|---|
| Hero headline + subtext | Homepage | "Digital Solutions," "AI Innovation" |
| Services descriptions | Services | Agile, Sprint, CI/CD, MVP, cross-functional, bespoke |
| Industry pages | Industries | ROI, CSAT, CRM, UAT |
| Case study cards | /work/ | UI/UX, "shipped," "end-to-end" |
| Process section | About, Services | Sprint, Agile, MVP |
| Testimonials | Homepage, About | Any quoted jargon should get a footnote or inline explanation |

---

## Examples from Other Sites

### Basecamp (basecamp.com)
- Avoids almost all technical jargon. Describes features in terms of what the user does, not how the software works.
- Example: "Know what everyone's working on" instead of "Cross-functional team visibility dashboard."

### GOV.UK
- Maintains a strict list of words to avoid: <https://www.gov.uk/guidance/style-guide/a-to-z-of-gov-uk-style>
- Every acronym is expanded on first use. "Do not use jargon. It excludes people."

### Stripe (stripe.com)
- Despite being deeply technical, Stripe explains terms inline: "Accept payments online. Stripe's APIs let you add payment processing to your website or app."
- Technical docs use progressive disclosure: plain summary first, technical detail on click.

### 18F Content Guide (U.S. Government)
- "Don't use formal or long words when easy or short ones will do."
- Guide: <https://content-guide.18f.gov/plain-language/>
