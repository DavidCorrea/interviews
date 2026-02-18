# FAQ Discoverability

## Priority
**Low**

## User Story
As a user scanning the AI Automation and Industries pages, I want FAQ sections to have clear expand/collapse indicators and some answers visible by default, so that I can quickly discover valuable information without having to guess that content is expandable.

## Acceptance Criteria

- [ ] First 1–2 FAQ answers are expanded by default on page load
- [ ] Clear visual expand/collapse indicators (e.g., +/− icons or chevrons) are present
- [ ] Toggle buttons have `aria-expanded="true"` or `aria-expanded="false"` reflecting current state
- [ ] Toggle buttons use `aria-controls` pointing to the ID of the answer content
- [ ] Answer content is in a region controlled by `aria-controls`
- [ ] Collapsed content uses `hidden` attribute or equivalent for screen readers
- [ ] Keyboard users can activate toggle buttons (Enter/Space)
- [ ] Visual indicators have `aria-hidden="true"` so they are not announced redundantly

## How to Test

1. Navigate to the AI Automation page and Industries page on https://launchpadlab.com/.
2. Locate FAQ sections — verify at least the first 1–2 answers are expanded by default.
3. Check for visible expand/collapse indicators (+/− or chevrons) next to each question.
4. Inspect toggle buttons: verify `aria-expanded` and `aria-controls` attributes.
5. Use a screen reader — confirm expanded/collapsed state is announced.
6. Use keyboard only — Tab to each FAQ button, activate with Enter/Space, verify content toggles.
7. Verify collapsed content is not exposed in the accessibility tree when hidden.

## Developer Notes

### General Explanation
FAQ sections on AI Automation and Industries pages are collapsed by default with minimal visual cues for expandability. Users scanning quickly miss valuable information because they don't realize content is hidden behind toggles. Proper ARIA ensures screen reader users understand the interaction model.

**Solution:** Show the first 1–2 FAQ answers expanded by default. Add clear visual expand/collapse indicators (+/− icons or chevrons). Ensure proper ARIA: `aria-expanded="true|false"` on toggle buttons, content in regions controlled by `aria-controls`. Use the `hidden` attribute or `aria-hidden` for collapsed content so it's not read until expanded.

### Code Examples

**Accessible FAQ accordion:**
```html
<div class="faq-list">
  <div class="faq-item">
    <button
      type="button"
      aria-expanded="false"
      aria-controls="faq-1-answer"
      id="faq-1-question"
    >
      What is agentic AI?
      <span class="icon" aria-hidden="true">+</span>
    </button>
    <div id="faq-1-answer" role="region" hidden aria-labelledby="faq-1-question">
      <p>Answer text...</p>
    </div>
  </div>
</div>
```

**JavaScript for toggle:**
```javascript
faqButtons.forEach((button) => {
  button.addEventListener('click', () => {
    const expanded = button.getAttribute('aria-expanded') === 'true';
    const targetId = button.getAttribute('aria-controls');
    const target = document.getElementById(targetId);
    const icon = button.querySelector('.icon');

    button.setAttribute('aria-expanded', !expanded);
    target.hidden = expanded;
    icon.textContent = expanded ? '+' : '−';
  });
});
```

**React FAQ component:**
```jsx
const [expandedIds, setExpandedIds] = useState(new Set([faqs[0]?.id, faqs[1]?.id]));

return (
  <div className="faq-list">
    {faqs.map((faq) => {
      const isExpanded = expandedIds.has(faq.id);
      return (
        <div key={faq.id} className="faq-item">
          <button
            type="button"
            aria-expanded={isExpanded}
            aria-controls={`faq-${faq.id}-answer`}
            onClick={() => {
              setExpandedIds((prev) => {
                const next = new Set(prev);
                if (next.has(faq.id)) next.delete(faq.id);
                else next.add(faq.id);
                return next;
              });
            }}
          >
            {faq.question}
            <span className="icon" aria-hidden="true">
              {isExpanded ? '−' : '+'}
            </span>
          </button>
          <div
            id={`faq-${faq.id}-answer`}
            role="region"
            hidden={!isExpanded}
            aria-labelledby={`faq-${faq.id}-question`}
          >
            <p>{faq.answer}</p>
          </div>
        </div>
      );
    })}
  </div>
);
```

### Components to Audit
- FAQ accordion component on AI Automation page
- FAQ accordion component on Industries page
- Any shared accordion/collapsible component
- CSS for expand/collapse icon visibility

## Examples from Other Sites

- **Stripe.com** — FAQ sections use clean expand/collapse with chevrons. First items often expanded by default. Clear visual affordance.
- **Apple.com Support** — FAQs have clear visual indicators (chevrons) and proper ARIA for expandable content.
- **GOV.UK** — Accordion pattern with explicit "Show" / "Hide" text and proper `aria-expanded` usage.
