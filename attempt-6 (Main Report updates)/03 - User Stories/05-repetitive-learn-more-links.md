# Repetitive "Learn More" Links

## Priority
**High**

## User Story
As a screen reader user, I want each "Learn More" link to have unique, descriptive text, so that I can understand where each link leads without additional context.

## Acceptance Criteria

- [ ] No two "Learn More" links on the Services page (or site-wide) have identical, non-differentiated text
- [ ] Each link either has unique visible text (e.g., "Learn more about AI Automation") or a unique `aria-label`
- [ ] Link purpose is determinable from the link text alone (WCAG 2.4.4)
- [ ] Screen reader users hear distinct labels for each link (e.g., "Learn more about AI Automation, link")
- [ ] Links remain visually consistent if desired (e.g., all can still say "Learn More" visually with `aria-label` for screen readers, or all can use descriptive text)
- [ ] No link reads only "Learn More" when announced by a screen reader without additional context

## How to Test

1. Navigate to the Services page (https://launchpadlab.com/services/ or equivalent).
2. Identify all "Learn More" links (use browser DevTools or "Find in page").
3. Use a screen reader (VoiceOver or NVDA) to tab through each link.
4. Verify each link announces a unique purpose (e.g., "Learn more about AI Automation").
5. If using `aria-label`, inspect the element and confirm the label is unique and descriptive.
6. Run an automated accessibility test (e.g., axe DevTools) and check for "Link purpose" violations.
7. Test with "Links list" or "Form controls" view in a screen reader — ensure each entry is distinguishable.

## Developer Notes

### General Explanation
When multiple links share the same generic text ("Learn More"), screen reader users navigating by links hear "Learn More, link" repeated without knowing which service or page each link refers to. This fails WCAG 2.4.4 (Link Purpose) at Level A.

**Solution:** Use descriptive link text or `aria-label` so each link's purpose is clear. Prefer visible descriptive text when possible for all users; use `aria-label` when design constraints require keeping "Learn More" as the visible text.

### Code Examples

**Option 1: Descriptive visible text (preferred)**
```html
<a href="/services/ai-automation-agentforce/">Explore AI Automation</a>
<a href="/services/custom-software/">Explore Custom Software</a>
<a href="/services/design/">Explore Design Services</a>
```

**Option 2: aria-label for screen readers**
```html
<a href="/services/ai-automation-agentforce/" aria-label="Learn more about AI Automation">Learn More</a>
<a href="/services/custom-software/" aria-label="Learn more about Custom Software">Learn More</a>
<a href="/services/design/" aria-label="Learn more about Design Services">Learn More</a>
```

**Option 3: Visually hidden context (sr-only)**
```html
<a href="/services/ai-automation-agentforce/">
  Learn More <span class="visually-hidden">about AI Automation</span>
</a>
```

**React component example:**
```jsx
const ServiceCard = ({ title, slug, href }) => (
  <article>
    <h3>{title}</h3>
    <p>Description...</p>
    <a href={href} aria-label={`Learn more about ${title}`}>
      Learn More
    </a>
  </article>
);
```

**CSS for visually hidden text:**
```css
.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
```

### Components to Audit
- Services page cards/grid
- Any reusable card or CTA component that renders "Learn More"
- Case study or blog listing components
- Industry or solution pages with multiple CTAs

## Examples from Other Sites

- **Shopify.com** — Each feature or product card link says "Learn more about [specific feature name]" rather than generic "Learn More."
- **Apple.com** — Product and feature links use descriptive text (e.g., "Learn about iPhone 15," "Explore MacBook Pro") so each link's purpose is clear.
