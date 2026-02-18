# 17. Clarify Creative Product Names with Plain-Language Subtitles

**Priority:** Medium
**Location:** Services page, Industries page
**Reported by:** Yuki Tanaka (Non-Native English Speaker), Richard Okonkwo (Non-Technical Business Executive)

---

## User Story

**As a** non-native English speaker or non-technical business executive visiting the site,
**I want** product and service names that clearly describe what they do
**so that** I can immediately understand the offering without needing to decode creative metaphors or culturally specific references.

---

## Acceptance Criteria

- [ ] Every creative/metaphorical product name is accompanied by a plain-language subtitle or descriptor that explains its actual function
- [ ] "Discovery Space Navigator" is either renamed to a descriptive term or includes a subtitle like "Our process for identifying your best product opportunities"
- [ ] "Mission Control" is either renamed to a descriptive term (e.g., "AI Analysis Platform" or "Project Analyzer") or includes a subtitle explaining its function
- [ ] Subtitles are visually distinct from the product name (smaller font, different weight, or muted color) but still clearly readable
- [ ] Subtitles are part of the DOM (not CSS pseudo-elements) so screen readers announce them
- [ ] The plain-language descriptor appears anywhere the product name is used (navigation, cards, headings, etc.)
- [ ] Product names and subtitles are readable at an 8th-grade level or below

---

## How to Test

1. **Navigate** to the Services page and Industries page
2. **Locate** any branded/creative product names (e.g., "Discovery Space Navigator," "Mission Control")
3. **Verify** each has a visible subtitle or descriptor that explains its function in plain language
4. **Read the subtitle in isolation** — confirm a user with no prior context can understand what the product does from the subtitle alone
5. **Screen reader test** — use VoiceOver (macOS) or NVDA (Windows) to navigate to each product name; confirm the subtitle is announced in sequence with the product name
6. **Non-native speaker test** — run the subtitle text through a tool like [Hemingway Editor](https://hemingwayapp.com/) or [Readable.com](https://readable.com/) to verify it is at or below an 8th-grade reading level
7. **Mobile test** — verify subtitles are visible and not truncated on small screens
8. **Consistency check** — search the entire site for any instance of the product name and confirm the subtitle appears alongside it everywhere

---

## Developer Notes

### Approach

There are two strategies, from least to most disruptive:

1. **Add subtitles** — Keep the creative names but add a plain-language descriptor below each one
2. **Rename entirely** — Replace creative names with descriptive ones (most accessible, but may conflict with brand identity)

The recommended approach is **Option 1** (add subtitles) as it preserves brand identity while solving the accessibility problem.

### Implementation: Subtitle Pattern

#### Card/Section Layout

```html
<div class="product-card">
  <h3 class="product-name">
    Discovery Space Navigator
    <span class="product-subtitle">
      Our step-by-step process for finding your best product opportunity
    </span>
  </h3>
  <p class="product-description">
    We analyze your business, market, and users to identify the highest-impact
    software solution for your needs.
  </p>
  <a href="/services/discovery/" class="product-link">Learn more</a>
</div>

<div class="product-card">
  <h3 class="product-name">
    Mission Control
    <span class="product-subtitle">
      AI-powered project analysis and tracking platform
    </span>
  </h3>
  <p class="product-description">
    A centralized dashboard that uses AI to monitor project health, flag risks,
    and recommend next steps.
  </p>
  <a href="/services/mission-control/" class="product-link">Learn more</a>
</div>
```

#### CSS for Subtitles

```css
.product-name {
  font-size: 1.5rem;
  font-weight: 700;
  color: #1a1a2e;
  line-height: 1.3;
  margin-bottom: 0.75rem;
}

.product-subtitle {
  display: block;
  font-size: 0.95rem;
  font-weight: 400;
  color: #555555;
  margin-top: 0.25rem;
  letter-spacing: 0.01em;
  line-height: 1.5;
}

/* Ensure sufficient contrast — 4.5:1 minimum */
/* #555555 on #ffffff = 7.46:1 ✓ */
```

### Alternative: Rename Entirely

If the team decides to drop the space-themed naming:

| Current Name | Descriptive Alternative |
|---|---|
| Discovery Space Navigator | Product Discovery Process |
| Mission Control | AI Project Analyzer |
| (any future space-themed name) | (plain-language equivalent) |

```html
<!-- Renamed approach — no subtitle needed -->
<h3 class="product-name">Product Discovery Process</h3>
<p class="product-description">
  We analyze your business, market, and users to identify the highest-impact
  software solution for your needs.
</p>
```

### Hybrid Approach: Name with Inline Clarifier

For contexts where a full subtitle doesn't fit (navigation, breadcrumbs, tags):

```html
<!-- In navigation or breadcrumbs -->
<a href="/services/discovery/">
  Discovery Space Navigator
  <span class="sr-only">(Product Discovery Process)</span>
</a>

<!-- In tag/badge contexts -->
<span class="service-tag">
  Discovery Space Navigator
  <abbr title="Product Discovery Process" class="name-clarifier">— Discovery Process</abbr>
</span>
```

```css
.name-clarifier {
  font-weight: 400;
  font-size: 0.85em;
  color: #777777;
  text-decoration: none;
  border-bottom: none;
}

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

### Components to Audit

- **Services page** — All product/service cards with creative names; headers and section titles
- **Industries page** — Any references to branded tools or processes
- **Homepage** — Any mentions of "Discovery Space Navigator" or "Mission Control" in service overview sections
- **Navigation / mega-menu** — If product names appear in dropdowns, add descriptors there too
- **Footer links** — Any branded product name links
- **Case study pages** — References to the tools in project write-ups
- **Meta tags / page titles** — If product names are in `<title>` or `<meta description>`, add the descriptor there for SEO clarity

### WCAG References

- **WCAG 2.1 SC 3.1.3 Unusual Words (AAA):** A mechanism is available for identifying specific definitions of words used in an unusual or restricted way — metaphorical product names qualify as "unusual" usage
- **WCAG 2.1 SC 3.1.4 Abbreviations (AAA):** A mechanism for identifying the expanded form or meaning of abbreviations is available — while not abbreviations, the same principle applies to obscured names
- **WCAG 2.1 SC 3.1.5 Reading Level (AAA):** When text requires more than a lower secondary education reading level, supplementary content is available — subtitles serve as the supplementary content
- **WCAG 2.1 SC 2.4.6 Headings and Labels (AA):** Headings and labels describe topic or purpose — a metaphorical name alone fails this when the purpose is unclear

---

## Examples from Other Sites

### Slack
Slack uses creative feature names like "Huddles" and "Canvas" but always pairs them with a one-line descriptor: "Huddles — lightweight audio calls for quick conversations." The creative name builds brand identity while the descriptor ensures clarity.

### Atlassian (Jira, Confluence)
Products have branded names, but every reference includes a functional subtitle: "Jira — Project and issue tracking" and "Confluence — Team knowledge base." This pattern appears consistently in navigation, marketing pages, and product descriptions.

### Notion
Uses terms like "Databases" and "Blocks" that could be ambiguous, but their onboarding and documentation always contextualize: "Databases — structured views for any type of content (tables, boards, timelines)."

### Salesforce
Has many branded product names (Einstein, Lightning, Trailhead), but each is always accompanied by a category descriptor: "Einstein — AI for CRM," "Lightning — App development platform," "Trailhead — Free online learning."

### Key Pattern
Successful creative naming + accessibility follows this formula:
1. **Creative name** for brand recognition and memorability
2. **Plain descriptor** for immediate comprehension
3. **Consistent pairing** — the descriptor appears everywhere the name appears
4. **Descriptor can stand alone** — if you removed the creative name, the descriptor would still make sense
