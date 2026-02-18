# M-33: Dense Paragraph Text Without Chunking

**Issue ID:** M-33
**Priority:** Medium
**WCAG Criteria:** 3.1.5 Reading Level (AAA), 1.4.8 Visual Presentation (AAA)
**Affected Personas:** ADHD, Dyslexic, Non-Native Speaker

---

## User Story

**As a** user with ADHD reading about LaunchPad Lab's services,
**I want** long text blocks to be broken into shorter paragraphs with sub-headings, bullet points, and visual separators,
**so that** I can scan the content quickly, maintain focus, and find the information I need without losing my place in a wall of text.

---

## Acceptance Criteria

- [ ] No body text paragraph exceeds 40 words (approximately 2–3 sentences) without a visual break (sub-heading, bullet list, separator, or new paragraph).
- [ ] Sections with 3+ related points use bullet or numbered lists instead of inline comma-separated or semicolon-separated enumerations.
- [ ] Each major content section has a descriptive sub-heading (`<h3>` or `<h4>`) that allows users to scan and skip to relevant information.
- [ ] Content editors have clear guidelines (in the CMS or style guide) specifying maximum paragraph length and when to use lists vs. prose.
- [ ] The visual rhythm of the page alternates between paragraphs, lists, and headings — no more than two consecutive paragraphs appear without a visual break.
- [ ] The changes do not alter the meaning or reduce the information conveyed — only the presentation is restructured.

---

## How to Test the Change

### Manual Testing

1. **Word count check:** Select any paragraph on the Services, About, or homepage. Count the words. Confirm no paragraph exceeds ~40 words.
2. **Scan test:** Ask a colleague unfamiliar with the site to spend 15 seconds scanning a page. Ask them to identify the 3 main points. If they can't, the chunking needs improvement.
3. **Screen reader navigation:** Using NVDA or VoiceOver, navigate by headings (`H` key). Confirm sub-headings exist within content sections that allow jumping past long text blocks.
4. **Mobile readability:** View the Services and About pages on a mobile device. Confirm text blocks feel manageable and don't require excessive scrolling through unbroken prose.

### Automated Testing

```javascript
// Check for overly long paragraphs
const paragraphs = document.querySelectorAll('main p, .page-content p, .entry-content p');
const longParagraphs = [];
paragraphs.forEach(p => {
  const wordCount = p.textContent.trim().split(/\s+/).length;
  if (wordCount > 50) {
    longParagraphs.push({ text: p.textContent.substring(0, 80) + '...', wordCount });
  }
});
if (longParagraphs.length > 0) {
  console.warn('Paragraphs exceeding 50 words:', longParagraphs);
}
```

```javascript
// Check for sections without sub-headings
const sections = document.querySelectorAll('section, .content-block');
sections.forEach(section => {
  const paragraphs = section.querySelectorAll('p');
  const subHeadings = section.querySelectorAll('h3, h4, h5');
  if (paragraphs.length > 3 && subHeadings.length === 0) {
    console.warn('Section has 3+ paragraphs but no sub-headings:', section);
  }
});
```

---

## Developer Notes

### General Explanation

Body copy across the site — particularly on the Services, About, and case study pages — consists of dense 40–80+ word paragraphs with no visual chunking. Long unbroken text blocks are a significant barrier for users with ADHD (difficulty maintaining focus), dyslexia (losing one's place in dense text), and non-native speakers (struggling to parse complex sentence structures in long paragraphs).

The fix is a content restructuring effort: breaking long paragraphs into shorter ones, adding sub-headings for scannability, and converting inline lists into bullet points. This is primarily a content/copywriting task rather than a code change, but the theme's CSS should also support good content structure with appropriate spacing.

### Current State (Problem)

```html
<!-- Dense, unbroken paragraph (72 words) -->
<p>
  LaunchPad Lab brings together cross-functional teams of designers,
  developers, and strategists who work collaboratively with your
  organization to identify opportunities for digital transformation,
  build bespoke software solutions tailored to your unique business
  challenges, and deliver measurable results that drive growth and
  competitive advantage in today's rapidly evolving technology
  landscape where AI and automation are reshaping every industry
  and customer expectation.
</p>
```

### Recommended Fix — Restructured Content

```html
<h3>How We Work</h3>
<p>
  We bring together cross-functional teams of designers, developers,
  and strategists who collaborate directly with your organization.
</p>

<p>Together, we focus on three areas:</p>
<ul>
  <li><strong>Identify opportunities</strong> for digital transformation</li>
  <li><strong>Build tailored solutions</strong> for your unique business challenges</li>
  <li><strong>Deliver measurable results</strong> that drive growth and competitive advantage</li>
</ul>
```

### CSS Support for Chunked Content

Ensure the theme CSS provides comfortable spacing for chunked content:

```css
/* Generous paragraph spacing for readability */
.entry-content p,
.page-content p {
  margin-bottom: 1.25em;
  max-width: 70ch; /* Limit line length for readability */
}

/* List styling with clear visual hierarchy */
.entry-content ul,
.entry-content ol {
  margin-bottom: 1.25em;
  padding-left: 1.5em;
}

.entry-content li {
  margin-bottom: 0.5em;
  line-height: 1.6;
}

/* Sub-heading spacing */
.entry-content h3,
.entry-content h4 {
  margin-top: 2em;
  margin-bottom: 0.75em;
}
```

### Content Restructuring Guidelines

| Pattern | Before | After |
|---|---|---|
| **Inline list** | "We offer design, development, strategy, and support services." | Bullet list with one item per service |
| **Long paragraph** | 60+ word paragraph covering multiple ideas | 2–3 shorter paragraphs, each focused on one idea |
| **Missing structure** | 4 paragraphs under a single `<h2>` | Add `<h3>` sub-headings to group related paragraphs |
| **Dense stats** | "We have 12 years of experience, 300 completed projects, and a team of 50 experts serving clients across healthcare, fintech, and education." | Break into a visual stat block or structured list |

### Pages / Content to Audit

The following pages have the most significant dense text blocks:

1. **Services page** — Service descriptions are 60–80 word paragraphs
2. **About page** — Company story and team description sections
3. **Homepage** — "Why Choose Us" and services overview sections
4. **Individual service pages** — Process descriptions and feature lists written as prose
5. **Case study pages** — Challenge/solution/results sections

### Components / Files to Audit

- WordPress page templates for Services, About, and Homepage
- Content editor fields in the CMS (add max-length guidance)
- Theme CSS for paragraph, list, and heading spacing
- Any Gutenberg or Elementor content blocks
- Editorial style guide (create or update with chunking guidelines)

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **Stripe** | Service descriptions use short 1–2 sentence paragraphs interspersed with bullet lists, code samples, and visual diagrams | Content is scannable; users find what they need in seconds. |
| **Basecamp** | Marketing pages use extremely short paragraphs (1–2 sentences max), bold lead sentences, and generous whitespace | ADHD-friendly — no wall of text, every paragraph is a "bite." |
| **GOV.UK** | Content design guidelines mandate paragraphs of no more than 5 lines, with bullet lists for 3+ items, and sub-headings every 3–4 paragraphs | Government standard based on extensive readability research. |
| **Mailchimp Content Style Guide** | Recommends short paragraphs, scannable headings, and bulleted lists for features/benefits | Widely referenced style guide with specific chunking rules. |
| **Nielsen Norman Group** | Research shows users scan (not read) web content; recommends chunking, sub-headings, and bullet lists as core web writing practices | Evidence-based UX writing recommendations from decades of research. |
