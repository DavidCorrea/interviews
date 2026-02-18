# AI-18: Fix Heading Hierarchy

## Metadata
- **ID:** AI-18
- **Priority:** 2 High
- **Personas Affected:** Screen reader users primarily; benefits all
- **WCAG Criteria:** 2.4.6 Headings and Labels (AA), 1.3.1 Info and Relationships (A)
- **Effort:** Small–Medium (2–4 hours)

---

## User Story

**As a** screen reader user who navigates by headings,

**I want** a logical heading hierarchy (H1 → H2 → H3) with one H2 per section, no skips, and no duplicate headings,

**So that** I can quickly understand the page structure and jump to the sections I care about using heading navigation.

---

## Acceptance Criteria

- [ ] Single H1 per page (page title)
- [ ] One H2 per major section — no duplicate H2s within a section
- [ ] Statistics (e.g., "12+ Years") are not marked as H2 — use `<p>` or `<dl>` instead
- [ ] No heading level skips (e.g., H2 → H4 without H3)
- [ ] Logical nesting: H1 → H2 → H3 → H4
- [ ] Heading outline makes sense when read in order (HeadingsMap, screen reader heading list)
- [ ] No decorative or stylistic use of heading tags for non-heading content

---

## Test Plan

### HeadingsMap Extension
1. Install HeadingsMap browser extension
2. Open each page on `https://launchpadlab.com/`
3. **Expected:** Single H1
4. **Expected:** No duplicate H2s within the same section
5. **Expected:** No heading level skips (H2 → H3 → H4, not H2 → H4)
6. **Expected:** Statistics (numbers, years) not marked as headings

### Screen Reader Heading Navigation
1. Use NVDA, VoiceOver, or JAWS
2. Use heading navigation (H key in NVDA, Rotor in VoiceOver)
3. **Expected:** Outline tells a coherent story of the page
4. **Expected:** Can jump to each section and understand context
5. **Expected:** No confusing entries like "12+ Years" as a section heading

### axe DevTools
1. Run axe DevTools on each page
2. **Expected:** No "Heading order" or "Heading levels should only increase by one" violations
3. **Expected:** No "Page must have a level-one heading" (if H1 is present)
4. Fix any heading-related violations

### Manual Audit
1. List all headings on each page
2. Check: Is "12+ Years" or similar a heading? → Should be `<p class="stat">` or `<dd>` in `<dl>`
3. Check: Are there two H2s in one section? → Keep one, demote the other to H3 or remove

---

## Developer Notes

### Statistics: Wrong vs. Right
**Wrong:**
```html
<h2>12+ Years</h2>
<p>In business</p>
```

**Right:**
```html
<h2>Our Track Record</h2>
<dl>
  <dt>Experience</dt>
  <dd>12+ Years</dd>
</dl>
<!-- Or -->
<p class="stat-number">12+ Years</p>
<p class="stat-label">In business</p>
```

### One H2 Per Section
**Wrong:** Multiple H2s in one section
```html
<section>
  <h2>Services</h2>
  <h2>What We Offer</h2>  <!-- Duplicate concept -->
</section>
```

**Right:**
```html
<section>
  <h2>Services</h2>
  <h3>What We Offer</h3>
  ...
</section>
```

### No Level Skips
**Wrong:** H2 → H4
```html
<h2>About</h2>
<h4>Our Team</h4>
```

**Right:** H2 → H3
```html
<h2>About</h2>
<h3>Our Team</h3>
```

### Audit Process
1. Run HeadingsMap on each page
2. Export or screenshot the outline
3. For each violation:
   - Duplicate H2 → choose one, demote or remove
   - Stat as H2 → change to `<p>` or `<dl>`
   - Skip → insert missing level or adjust
4. Test with NVDA heading list (Insert+F6) to verify

### Definition List for Stats
```html
<dl class="stats">
  <dt>Years in business</dt>
  <dd>12+</dd>
  <dt>Projects delivered</dt>
  <dd>200+</dd>
</dl>
```

### Files to Modify
- All page templates
- Homepage sections
- Services, About, Contact pages
- Case study pages
- Component partials (header, footer, cards)

---

## Examples

| Site | Approach |
|------|----------|
| **GOV.UK** | Perfect heading hierarchy; one H1; logical H2/H3 structure |
| **W3C.org** | Clean heading structure; no skips; semantic use |
| **MDN Web Docs** | Logical heading nesting; scannable outline |
