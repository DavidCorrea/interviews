# H-12: Identical "Learn More" Links

**Issue ID:** H-12
**Priority:** High
**WCAG Criteria:** 2.4.4 Link Purpose (In Context) (A), 2.4.9 Link Purpose (Link Only) (AAA), 2.5.3 Label in Name (A)
**Affected Personas:** Screen Reader, Voice Control, ADHD, Cognitive Disability

---

## User Story

**As a** screen reader user browsing the services section,
**I want** each "Learn More" link to have a unique, descriptive accessible name,
**so that** when I list all page links I can distinguish which service each one refers to without guessing.

---

## Acceptance Criteria

- [ ] No two links on the same page share identical accessible names while pointing to different destinations.
- [ ] Each "Learn More" link within a service card includes a unique `aria-label` or `aria-labelledby` that incorporates the service name (e.g., `aria-label="Learn more about AI Development"`).
- [ ] The visible text "Learn More" is still present (do not remove it) so that `aria-label` starts with the visible text to satisfy 2.5.3 Label in Name.
- [ ] When a screen reader lists all links (`Insert+F7` in NVDA, `VO+U` in VoiceOver), each "Learn More" entry is uniquely identifiable.
- [ ] Voice control users saying "click Learn More about AI Development" can target the correct link without a disambiguation dialog.
- [ ] The link purpose is clear from the link text and its programmatic context (heading, `aria-label`, or surrounding content).

---

## How to Test the Change

### Manual Testing

1. **Screen reader link list:** Using NVDA (`Insert+F7`) or VoiceOver (`VO+U`), open the links list on the services page. Confirm each "Learn More" link has a unique description (e.g., "Learn more about AI Development," "Learn more about Web Applications").
2. **Voice control test:** Using macOS Voice Control or Dragon, say "click Learn More." If multiple matches exist, the system should show numbered overlays — but ideally, saying "click Learn More about [Service Name]" should target exactly one link.
3. **Visual inspection:** Right-click each "Learn More" link → Inspect → verify the `aria-label` or `aria-labelledby` attribute includes the service name.
4. **Tab navigation:** Tab through service cards. Confirm the screen reader announces the full accessible name, not just "Learn More."

### Automated Testing

- Run `axe-core` or Lighthouse: check for "Links must have discernible text" and "Identical links have different purposes."

```javascript
// Check for duplicate link accessible names
const links = document.querySelectorAll('a');
const nameMap = {};
links.forEach(link => {
  const name = (link.getAttribute('aria-label') || link.textContent).trim();
  const href = link.href;
  if (nameMap[name] && nameMap[name] !== href) {
    console.warn(`Duplicate link name "${name}" with different destinations:`, nameMap[name], href);
  }
  nameMap[name] = href;
});
```

---

## Developer Notes

### General Approach

Add `aria-label` attributes to each "Learn More" link that include the service name. Ensure the `aria-label` begins with "Learn More" to satisfy WCAG 2.5.3 Label in Name (the accessible name must contain the visible text).

### Current State (Problem)

```html
<!-- All 6-7 service cards have identical link text -->
<div class="service-card">
  <h3>AI Development</h3>
  <a href="/services/ai-development/">Learn More</a>
</div>

<div class="service-card">
  <h3>Web Applications</h3>
  <a href="/services/web-applications/">Learn More</a>
</div>

<div class="service-card">
  <h3>Mobile Development</h3>
  <a href="/services/mobile-development/">Learn More</a>
</div>
<!-- Screen reader link list shows: "Learn More", "Learn More", "Learn More"... -->
```

### Recommended Fix — Option A: `aria-label`

```html
<div class="service-card">
  <h3>AI Development</h3>
  <a href="/services/ai-development/"
     aria-label="Learn more about AI Development">
    Learn More
  </a>
</div>

<div class="service-card">
  <h3>Web Applications</h3>
  <a href="/services/web-applications/"
     aria-label="Learn more about Web Applications">
    Learn More
  </a>
</div>
```

### Recommended Fix — Option B: `aria-labelledby`

```html
<div class="service-card">
  <h3 id="service-ai">AI Development</h3>
  <a href="/services/ai-development/"
     aria-labelledby="service-ai learn-more-ai">
    <span id="learn-more-ai">Learn More</span>
  </a>
</div>
```

### Recommended Fix — Option C: Visually Hidden Text

```html
<a href="/services/ai-development/">
  Learn More<span class="sr-only"> about AI Development</span>
</a>
```

```css
.sr-only {
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

### Components / Files to Audit

- Service card component template (e.g., `partials/service-card.php`, `components/ServiceCard`)
- Any loop that renders service cards and generates the "Learn More" links
- CMS/ACF field group for service cards (if the link text is editor-configurable)
- Case study cards and any other repeated "Learn More" patterns across the site

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **IBM** | Card links read "Learn more about IBM Cloud Pak for Data" | Full context in the accessible name; no ambiguity in link lists. |
| **Salesforce** | "Learn More" links use `aria-label="Learn more about Sales Cloud"` | Accessible name starts with visible text, includes product name. |
| **Microsoft** | Product cards use `aria-label` on the card link with the product name | Screen reader users get the full context on each link. |
| **GOV.UK Design System** | Recommends against "Learn More" entirely; prefers descriptive link text like "Read about universal credit" | Eliminates the problem by making visible text unique. |
