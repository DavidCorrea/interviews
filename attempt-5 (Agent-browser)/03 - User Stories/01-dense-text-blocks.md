# Dense Text Blocks & Complex Sentence Structures

**Priority:** High
**Location:** All pages — hero sections, service descriptions, about copy, process sections
**WCAG:** [1.3.1 Info and Relationships (A)](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships), [3.1.5 Reading Level (AAA)](https://www.w3.org/WAI/WCAG21/Understanding/reading-level)

---

## User Story

> As a **user with a cognitive disability, ADHD, or low literacy**,
> I want **body text to be broken into short paragraphs with visual anchors like bold keywords and bullet points**
> so that **I can scan the page quickly, find what I need, and understand the content without re-reading.**

---

## Problem

The LaunchPad Lab site relies on multi-sentence paragraphs (3–5 lines) with complex sentence structures throughout its pages. There are no bold keywords, no bullet points, and no visual anchors to break up the text. This creates a "wall of text" that is difficult to scan and cognitively taxing to read for users with ADHD, dyslexia, cognitive disabilities, or anyone in a hurry.

**Current pattern (example):**

```html
<p>
  We partner with forward-thinking organizations to design, build, and scale
  custom digital products that drive measurable business outcomes. Our
  cross-functional teams bring together product strategy, user experience
  design, and modern engineering practices to deliver solutions that are
  both innovative and sustainable. From initial discovery through ongoing
  optimization, we embed with your team to ensure lasting impact.
</p>
```

---

## Acceptance Criteria

- [ ] No paragraph exceeds 3 sentences or roughly 60 words.
- [ ] At least one visual anchor (bold keyword, subheading, or bullet list) appears within every 150 words of body copy.
- [ ] Sentences average 15–20 words; no sentence exceeds 25 words.
- [ ] Active voice is used in at least 90 % of sentences.
- [ ] Process or list-like content is converted from prose to bullet/numbered lists.
- [ ] Each content section has a descriptive subheading (`<h2>` or `<h3>`) above its text.
- [ ] Content passes a Flesch-Kincaid readability test at grade 8 or below.

---

## How to Test

1. **Visual scan test:** Open each page and attempt to find a specific piece of information (e.g., "What services do they offer?") in under 5 seconds. If the answer is buried in a paragraph, the content needs restructuring.
2. **Paragraph length audit:** Inspect body text blocks. Count sentences per paragraph — flag any with more than 3 sentences.
3. **Readability score:** Paste page copy into [Hemingway Editor](https://hemingwayapp.com/) or [Readable](https://readable.com/). Verify the grade level is ≤ 8.
4. **Screen reader test:** Use VoiceOver (macOS) or NVDA (Windows) to listen to a full section. Long, unbroken paragraphs are read as a single block with no pause points — note where natural breaks are needed.
5. **Keyboard navigation:** Tab through heading landmarks (`h2`, `h3`). Verify the heading hierarchy gives a meaningful content outline.

---

## Developer Notes

### Strategy

Break every long paragraph into shorter chunks, add semantic structure, and introduce visual markers so users can scan rather than read linearly.

### Before (current markup)

```html
<section class="services">
  <h2>Our Services</h2>
  <p>
    We partner with forward-thinking organizations to design, build, and scale
    custom digital products that drive measurable business outcomes. Our
    cross-functional teams bring together product strategy, user experience
    design, and modern engineering practices to deliver solutions that are
    both innovative and sustainable. From initial discovery through ongoing
    optimization, we embed with your team to ensure lasting impact.
  </p>
</section>
```

### After (improved markup)

```html
<section class="services">
  <h2>Our Services</h2>
  <p>
    We help organizations <strong>design, build, and grow</strong> custom
    software that delivers real results.
  </p>

  <h3>What we bring to every project</h3>
  <ul>
    <li><strong>Product strategy</strong> — aligning your goals with a clear plan</li>
    <li><strong>User experience design</strong> — making software easy to use</li>
    <li><strong>Modern engineering</strong> — building with reliable, up-to-date technology</li>
  </ul>

  <p>
    We work alongside your team from <strong>first idea through launch and
    beyond</strong>, so improvements keep coming.
  </p>
</section>
```

### CSS for readable text blocks

```css
.services p,
.services li {
  max-width: 70ch;           /* Limit line length for readability */
  line-height: 1.8;          /* Generous spacing between lines   */
  margin-bottom: 1rem;       /* Breathing room between paragraphs */
}

.services ul {
  padding-left: 1.25rem;
  list-style-type: disc;
  margin-bottom: 1.5rem;
}

.services strong {
  font-weight: 600;          /* Visual anchor without full bold   */
}
```

### Components to audit

| Component / Section | Page(s) | What to fix |
|---|---|---|
| Hero description text | Homepage, Services, About | Break into ≤ 2 sentences, bold the value prop |
| Service description blocks | Services, Homepage | Convert to heading + bullet list |
| About / mission copy | About | Shorten sentences, add subheadings |
| Process / methodology section | Services, About | Convert numbered prose to `<ol>` steps |
| Case study intro paragraphs | /work/ detail pages | Split into short paragraphs, bold key outcomes |
| Footer "about" blurb | All pages | Limit to 1–2 sentences |

---

## Examples from Other Sites

### Basecamp (basecamp.com)
- Body copy rarely exceeds 2 sentences per block.
- Bullet lists with bold lead-ins summarize features.
- Every section has a clear subheading.

### GOV.UK (gov.uk)
- The gold standard for plain-language web content.
- Paragraphs are 1–2 sentences, bulleted lists are the default for any list-like information.
- Average sentence length: 12–15 words.
- Content style guide: <https://www.gov.uk/guidance/content-design/writing-for-gov-uk>

### Mailchimp Content Style Guide
- Recommends: "Use short sentences. Use short paragraphs. Use bullet points."
- Publicly available at <https://styleguide.mailchimp.com/writing-principles/>
