# Shorten Accordion Button Accessible Names to Concise Labels

## Priority: Medium

## User Story
As a screen reader user, I want accordion buttons to announce only their topic label (e.g., "Business") so that I can quickly understand what each accordion section contains without hearing a paragraph of text.

## Acceptance Criteria
- [ ] Each accordion button announces only its topic label (e.g., "Business", "IT", "Users") when focused
- [ ] Descriptive content (subtext, bullet lists) is announced only when the panel is expanded
- [ ] Buttons include `aria-expanded="true"` or `aria-expanded="false"` to indicate state
- [ ] Accordion pattern complies with WCAG 2.4.6 (Headings and Labels)
- [ ] Screen reader users can efficiently scan accordion options without being overwhelmed

## Developer Notes

### General Explanation
Accordion buttons on the Services page include entire paragraph content as the accessible name. For example, the "Business" button announces the heading, subtext, and full bullet list. This overwhelms screen reader users who expect a concise label. The button's accessible name should come only from the visible topic label; descriptive content belongs in the expandable panel.

**Key fixes:**
1. Ensure the button's accessible name comes only from the visible label text (e.g., "Business", "IT", "Users")
2. Move descriptive content into the expandable panel, not the button name
3. Use `aria-expanded="true/false"` on the button
4. Prevent child text content from contributing to button name—use `aria-label` if needed, or restructure so description is in the panel

### Code Examples

```html
<!-- Accessible accordion pattern -->
<div class="accordion">
  <h3>
    <button type="button"
            aria-expanded="false"
            aria-controls="panel-business"
            id="accordion-business"
            aria-label="Business">
      Business
    </button>
  </h3>
  <div id="panel-business"
       role="region"
       aria-labelledby="accordion-business"
       hidden>
    <p>Subtext and description here.</p>
    <ul>
      <li>Bullet point 1</li>
      <li>Bullet point 2</li>
    </ul>
  </div>
</div>
```

```html
<!-- If button contains extra text, use aria-label to override -->
<button type="button"
        aria-expanded="false"
        aria-controls="panel-business"
        aria-label="Business">
  <span class="accordion-title">Business</span>
  <span class="accordion-description">Subtext and bullets...</span>
</button>
<!-- Better: move description out of button into panel -->
```

### Components to Audit
- Services page accordion/expandable sections
- Any similar accordion or expandable pattern used elsewhere on the site

## Examples From Other Sites
- **W3C WAI Accordion Pattern:** Demonstrates concise button labels with `aria-expanded` and content in panels
- **GOV.UK Accordion Component:** Uses short, descriptive labels on buttons; full content only in expanded regions
- **Deque University:** Teaches accessible accordion patterns with proper `aria-expanded` and `aria-controls`

## References
- Main Report Item 14
- WCAG 2.4.6 Headings and Labels
- Website: https://launchpadlab.com/
