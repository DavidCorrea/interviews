# Provide Plain-Language Alternatives for Technical Jargon

## Priority: Medium

## User Story

As a non-technical business executive visiting the site, I want technical terms to be accompanied by plain-language explanations so that I can understand the services being offered without needing a technology background.

## Acceptance Criteria

- [ ] Every instance of the following terms has an inline plain-language explanation or tooltip: "agentic AI," "sprint," "UAT," "stack," "UI/UX," "CSAT," "codification," "prompts," "data pipelines," "full digital product lifecycle"
- [ ] Tooltips are keyboard-accessible (triggered by Tab + Enter/Space, not just mouse hover)
- [ ] Tooltips use proper ARIA attributes (`role="tooltip"`, `aria-describedby`)
- [ ] Tooltip text is concise (one sentence or less)
- [ ] A non-technical user can read any page on the site and understand the service offerings without external research
- [ ] No new jargon is introduced without a corresponding explanation
- [ ] Tooltips/explanations are visually indicated (e.g., dotted underline) so users know they can interact with the term

## Developer Notes

### General Explanation

The site uses technical terminology that is standard within the software industry but opaque to the target audience (C-suite executives, business owners, operations leaders). There are two complementary approaches:

1. **Inline parenthetical explanations** — Add a brief clarification directly after the term. Best for terms used only once or twice.
2. **Glossary tooltip component** — Create a reusable component that wraps jargon in a tooltip. Best for terms used repeatedly across pages.

A hybrid approach is recommended: use inline explanations for one-off usage, and tooltips for recurring terms.

### Term Definitions

| Term | Plain-Language Definition |
|------|--------------------------|
| Agentic AI | AI software that can complete tasks on its own, like a digital assistant that follows your rules |
| Sprint | A two-week work cycle where the team builds, tests, and shows you progress |
| UAT | User acceptance testing — when you try the product to confirm it works the way you need |
| Stack | The collection of software tools and systems your company uses |
| UI/UX | How the product looks (UI) and how easy it is to use (UX) |
| CSAT | Customer satisfaction score — a measure of how happy your customers are |
| Codification | Turning expert knowledge into repeatable steps that software can follow |
| Prompts | Instructions you give to AI to tell it what to do |
| Data pipelines | Automated systems that move data from one place to another |
| Full digital product lifecycle | The entire process of building software, from idea to launch to ongoing updates |

### Code Examples

**Accessible tooltip component (HTML + CSS + JS):**

```html
<span class="jargon-term" tabindex="0" aria-describedby="tooltip-agentic-ai">
  agentic AI
  <span id="tooltip-agentic-ai" role="tooltip" class="jargon-tooltip">
    AI software that can complete tasks on its own, like a digital assistant that follows your rules
  </span>
</span>
```

```css
.jargon-term {
  position: relative;
  border-bottom: 1px dotted #666;
  cursor: help;
}

.jargon-tooltip {
  display: none;
  position: absolute;
  bottom: 100%;
  left: 50%;
  transform: translateX(-50%);
  background: #333;
  color: #fff;
  padding: 8px 12px;
  border-radius: 4px;
  font-size: 14px;
  line-height: 1.4;
  white-space: nowrap;
  max-width: 300px;
  white-space: normal;
  z-index: 10;
}

.jargon-term:hover .jargon-tooltip,
.jargon-term:focus .jargon-tooltip {
  display: block;
}
```

**React component version:**

```jsx
function JargonTerm({ term, definition, children }) {
  const tooltipId = `tooltip-${term.replace(/\s+/g, '-').toLowerCase()}`;

  return (
    <span
      className="jargon-term"
      tabIndex={0}
      aria-describedby={tooltipId}
    >
      {children}
      <span id={tooltipId} role="tooltip" className="jargon-tooltip">
        {definition}
      </span>
    </span>
  );
}
```

### Components to Audit

- AI Automation page (heaviest jargon density)
- Services dropdown/mega-menu description
- Homepage service cards and descriptions
- About Us page
- All individual service pages (Web App Development, Mobile App Development, etc.)
- Case study pages (may reference technical terms in project descriptions)
- Insights/blog pages (if they use terms without definition)

## Examples From Other Sites

- **Salesforce Trailhead** uses a "learning" approach — technical terms are always introduced with a one-sentence definition before being used in context. Their glossary is searchable and cross-linked.
- **IBM** provides contextual help icons next to technical terms in their product pages. Clicking the icon reveals a plain-language explanation in a popover.
- **gov.uk** is the gold standard for plain language. Their style guide explicitly forbids jargon and requires all government digital services to use language that a general audience can understand. Every term is written for a reading age of 9.
- **Stripe** uses technical terms only when necessary and always provides context. For example, instead of "API," they often write "a way for your software to talk to Stripe" on non-developer pages.

## References

- [Margaret Chen Interview — Tasks 1 & 2](../01%20-%20Interviews/margaret-chen-interview.md)
- [Margaret Chen Report — Content Clarity Issues](../02%20-%20Reports/margaret-chen-report.md)
- [Main Report — Item 5: Technical Jargon Without Plain-Language Explanations](../main-report.md)
