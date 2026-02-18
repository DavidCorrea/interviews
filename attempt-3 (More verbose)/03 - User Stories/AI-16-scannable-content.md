# AI-16: Break Up Dense Text into Scannable Content

## Metadata
- **ID:** AI-16
- **Priority:** 2 High
- **Personas Affected:** 5+ of 16 personas
- **WCAG Criteria:** 1.4.8 Visual Presentation (AAA), 2.4.10 Section Headings (AAA)
- **Effort:** Medium (4–8 hours)

---

## User Story

**As a** user with ADHD, cognitive disability, or limited time,

**I want** content broken into short paragraphs, bullet points, subheadings, and summaries,

**So that** I can quickly scan the page and find the key information I need without feeling overwhelmed by dense blocks of text.

---

## Acceptance Criteria

- [ ] No paragraph exceeds 3 sentences (ideally 2–3)
- [ ] Every long section (4+ paragraphs) has subheadings (H3/H4) every 2–3 paragraphs
- [ ] Features, benefits, and process steps are presented as bullet lists (`<ul>` or `<ol>`)
- [ ] Long sections have a TL;DR or summary callout at the top
- [ ] Visual hierarchy is clear: headings, lists, and whitespace create breathing room
- [ ] Key info can be found in ~10 seconds when scanning (per ADHD persona guidelines)
- [ ] Lists use semantic `<ul>` and `<ol>` — not styled paragraphs that look like lists

---

## Test Plan

### Visual Scan
1. Open each page on `https://launchpadlab.com/`
2. **Expected:** No paragraph exceeds 3 sentences
3. **Expected:** Every long section has subheadings
4. **Expected:** Features/benefits/steps use bullet or numbered lists
5. Count paragraphs with 5+ lines — **Expected:** Zero

### Subheading Audit
1. Use HeadingsMap or similar to view outline
2. **Expected:** H2s followed by H3s/H4s at logical intervals
3. **Expected:** No long stretches of text without a subheading

### List Usage
1. Identify sections describing: features, benefits, process steps, options
2. **Expected:** These use `<ul>` or `<ol>` — inspect element to verify
3. **Expected:** No "fake lists" (paragraphs with • or - that aren't semantic lists)

### ADHD Persona Test
1. Set a 10-second timer
2. Ask: "Can I find what this company does and who they help in 10 seconds?"
3. **Expected:** Yes — key info is in hero, subheadings, or first bullets
4. Ask: "Does this feel overwhelming?"
5. **Expected:** No — whitespace, short blocks, and structure reduce cognitive load

### TL;DR Check
1. For any section over 200 words
2. **Expected:** TL;DR or summary callout at top, or clear first sentence that summarizes

---

## Developer Notes

### Content Restructuring Pass
- **Service descriptions:** Convert prose to bullet lists
  - Before: "We offer custom development, design, and strategy..."
  - After: "We offer: • Custom development • Design • Strategy"
- **About page:** Add H3 subheadings every 2–3 paragraphs
- **Testimonials:** Use shorter excerpts; link to full quote if needed

### TL;DR Callout Boxes
```html
<div class="tldr" role="note">
  <strong>TL;DR:</strong> We build websites, apps, and AI tools for businesses. 
  Our process: research, design, build, launch.
</div>
```

### Semantic Lists
```html
<!-- Good -->
<ul>
  <li>Custom development</li>
  <li>Design</li>
  <li>Strategy</li>
</ul>

<!-- Bad - styled to look like list but not semantic -->
<p>• Custom development • Design • Strategy</p>
```

### Subheading Structure
- Add `<h3>` and `<h4>` at logical break points
- One subheading per 2–3 paragraphs
- Subheadings should be descriptive, not generic ("Our Process" not "Section 2")

### Paragraph Length
- Target: 2–3 sentences per paragraph
- Max: 3 sentences
- Break long paragraphs at natural thought boundaries

### Section Padding
- Increase whitespace between sections: `py-16` → `py-24` or equivalent
- Use `max-width` on content containers (e.g., 65ch) for readable line length

### Files to Modify
- Homepage (all sections)
- Services page
- About page
- Case studies
- Blog posts (if applicable)

---

## Examples

| Site | Approach |
|------|----------|
| **Stripe.com/docs** | Scannable; bullet-heavy; short paragraphs; clear hierarchy |
| **Notion.com/product** | Short paragraphs; visual breaks; lots of whitespace |
| **Apple.com** | Minimal text; strong visual hierarchy; one idea per section |
