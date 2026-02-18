# 20. Address Similar-Looking Words in Close Proximity for Dyslexic Readers

**Priority:** Medium
**Location:** Homepage tabs, process section, About page
**Reported by:** Sam Chen (Dyslexic)

---

## User Story

**As a** dyslexic user reading the website,
**I want** visually similar words to be differentiated or not placed near each other
**so that** I don't confuse words like "modernize" and "monetize" or "develop" and "deploy," which causes me to misread content and lose confidence in my understanding.

---

## Acceptance Criteria

- [ ] Identified confusing word pairs are addressed throughout the site:
  - "modernize" / "monetize" — separated or differentiated
  - "Expansive" / "Expensive" — separated or replaced with a less confusable alternative
  - "develop" / "deliver" / "deploy" — differentiated when appearing in proximity
  - "AI-Centered" / "AI-Censored" — "AI-Centered" is replaced or styled to prevent misreading
- [ ] Where similar words must appear near each other, at least one differentiation technique is applied:
  - Increased `letter-spacing` (minimum `0.05em`)
  - Bold or color emphasis on the differentiating syllable/letters
  - Alternative word choice
- [ ] Body text uses a minimum `letter-spacing` of `0.05em` sitewide (benefits all users, not just dyslexic)
- [ ] No new instances of confusable word pairs are introduced in close proximity
- [ ] Content changes maintain the same meaning and professional tone

---

## How to Test

1. **Navigate** to the Homepage, scroll to the tabbed section and process section
2. **Search** for the identified confusing word pairs:
   - "modernize" near "monetize"
   - "Expansive" near or resembling "Expensive"
   - "develop," "deliver," "deploy" in close proximity
   - "AI-Centered"
3. **Verify differentiation** — for each pair, confirm at least one technique is applied (alternative word, bold on differentiating letters, increased spacing, or physical separation)
4. **Dyslexia simulation test** — use a dyslexia simulation tool (e.g., [Dyslexia Simulator Chrome extension](https://chrome.google.com/webstore/detail/dyslexia-simulator)) and verify the words are still distinguishable
5. **Quick-scan test** — ask a tester to skim the page quickly and then recall key terms. If they confuse similar-looking words, the differentiation is insufficient.
6. **Check letter-spacing** — inspect body text in browser DevTools and confirm `letter-spacing` is at least `0.05em`
7. **Navigate** to the About page and repeat the checks for any identified confusable words
8. **Content review** — read the replacement text and confirm it conveys the same meaning as the original

---

## Developer Notes

### Understanding the Problem

Dyslexic readers process words primarily by their overall visual shape (word envelope) rather than individual letter sequences. Words with similar shapes — same length, similar ascenders/descenders, shared letter sequences — are easily confused, especially when they appear on the same page or in close proximity.

The confusable pairs on the LaunchPad Lab site:

| Word A | Word B | Why They Confuse |
|--------|--------|------------------|
| modernize | monetize | Same length (9 letters), share "m-o-...-ize" pattern |
| Expansive | Expensive | Share "Exp-...-ive" pattern, differ by only 2 internal letters |
| develop | deliver | Share "de-...-ve-" pattern, same start and similar shape |
| develop | deploy | Share "de-...-lo-" pattern, nearly identical start |
| deliver | deploy | Share "de-...-l-" pattern, start identically |
| AI-Centered | AI-Censored | Share "AI-Cen-...-ed" pattern, nearly identical shape |

### Strategy 1: Replace with Alternative Words (Preferred)

The most effective fix is to choose words that look visually distinct.

| Original | Replacement | Rationale |
|----------|-------------|-----------|
| modernize | **upgrade** or **rebuild** | Visually distinct from "monetize"; shorter, simpler word |
| monetize | **earn revenue from** or **generate income with** | Phrase instead of single word avoids confusion entirely |
| Expansive | **broad** or **wide-ranging** or **comprehensive** | Visually distinct from "Expensive"; also simpler to read |
| deploy | **launch** or **release** | Visually distinct from "develop" and "deliver" |
| AI-Centered | **AI-focused** or **AI-first** | Visually distinct from "AI-Censored"; shorter and clearer |

#### Before

```html
<div class="process-steps">
  <div class="step">
    <h3>Develop</h3>
    <p>We develop your application using agile sprints.</p>
  </div>
  <div class="step">
    <h3>Deliver</h3>
    <p>We deliver incremental releases for your review.</p>
  </div>
  <div class="step">
    <h3>Deploy</h3>
    <p>We deploy your finished product to production.</p>
  </div>
</div>
```

#### After

```html
<div class="process-steps">
  <div class="step">
    <h3>Build</h3>
    <p>We build your application in short, focused cycles.</p>
  </div>
  <div class="step">
    <h3>Review</h3>
    <p>We share progress regularly so you can give feedback.</p>
  </div>
  <div class="step">
    <h3>Launch</h3>
    <p>We release your finished product to your users.</p>
  </div>
</div>
```

### Strategy 2: Typographic Differentiation (When Words Can't Be Changed)

When the exact words must remain (e.g., they're part of a quoted case study, client testimonial, or technical section), apply CSS differentiation:

#### Increased Letter-Spacing Sitewide

```css
body {
  letter-spacing: 0.05em;
}

h1, h2, h3, h4, h5, h6 {
  letter-spacing: 0.03em;
}
```

#### Bold the Differentiating Letters

```html
<p>
  We help companies <strong>modern</strong>ize their systems
  and <strong>monet</strong>ize their data.
</p>
```

```css
/* Alternatively, use a highlight class */
.word-diff {
  font-weight: 700;
  color: #1a1a2e;
}

/* Or use a subtle background highlight */
.word-highlight {
  background-color: rgba(26, 115, 232, 0.08);
  padding: 0.05em 0.15em;
  border-radius: 2px;
}
```

#### Increase Spacing Around Confusable Words

```css
.confusable-word {
  letter-spacing: 0.08em;
  font-weight: 500;
}
```

### Strategy 3: Physical Separation

Don't place confusable words in the same section, list item, or visible viewport. If "modernize" and "monetize" are both key messages, put them in different sections with a clear visual break between them.

```html
<!-- BEFORE: confusable words in same section -->
<section>
  <h2>We help you modernize your systems and monetize your data.</h2>
</section>

<!-- AFTER: separated into distinct sections -->
<section class="capability">
  <h2>Upgrade Your Systems</h2>
  <p>Replace outdated technology with modern, reliable software.</p>
</section>

<section class="capability">
  <h2>Earn Revenue from Your Data</h2>
  <p>Turn your data into actionable insights and new income streams.</p>
</section>
```

### Global Typography Improvements (Benefits Everyone)

These CSS changes improve readability sitewide for dyslexic users and create a baseline that prevents future confusable-word issues:

```css
:root {
  --letter-spacing-body: 0.05em;
  --letter-spacing-heading: 0.03em;
  --word-spacing-body: 0.05em;
  --line-height-body: 1.8;
  --font-family-body: 'Inter', 'Atkinson Hyperlegible', -apple-system, sans-serif;
}

body {
  font-family: var(--font-family-body);
  letter-spacing: var(--letter-spacing-body);
  word-spacing: var(--word-spacing-body);
  line-height: var(--line-height-body);
}

h1, h2, h3, h4, h5, h6 {
  letter-spacing: var(--letter-spacing-heading);
  font-style: normal; /* Avoid italic headings — harder for dyslexic readers */
}
```

### Font Recommendation

Consider using [Atkinson Hyperlegible](https://brailleinstitute.org/freefont) — a free font designed by the Braille Institute specifically to maximize character distinction. It differentiates similar-looking characters (e.g., I/l/1, O/0, p/q/b/d) far better than most sans-serif fonts.

```css
@font-face {
  font-family: 'Atkinson Hyperlegible';
  src: url('/fonts/atkinson-hyperlegible-regular.woff2') format('woff2');
  font-weight: 400;
  font-display: swap;
}

@font-face {
  font-family: 'Atkinson Hyperlegible';
  src: url('/fonts/atkinson-hyperlegible-bold.woff2') format('woff2');
  font-weight: 700;
  font-display: swap;
}
```

### Components to Audit

- **Homepage — tabbed section** — Check for "modernize" / "monetize" proximity
- **Homepage — process section** — Check for "develop" / "deliver" / "deploy" proximity
- **About page** — Check for "Expansive" and any "AI-Centered" references
- **Services page** — Check all service descriptions for confusable word pairs
- **Sitewide body text** — Apply `letter-spacing: 0.05em` globally
- **CMS content** — Create a style guide note for content authors: "Avoid placing visually similar words in the same section"

### WCAG References

- **WCAG 2.1 SC 1.4.12 Text Spacing (AA):** Content must not lose information when letter-spacing is set to at least 0.12em — ensuring the site supports increased spacing helps dyslexic users who use custom stylesheets
- **WCAG 2.1 SC 3.1.5 Reading Level (AAA):** Supplementary content or simpler word choices should be available when text requires more than a lower secondary reading level
- **WCAG 2.1 SC 1.4.8 Visual Presentation (AAA):** Users should be able to adjust text spacing and font — implementing CSS custom properties enables this
- **Cognitive Accessibility (COGA) Guidance:** Avoid text that is likely to be confusing due to unusual word choices, visual similarity, or ambiguity

---

## Examples from Other Sites

### BBC (bbc.com)
The BBC's editorial style guide explicitly warns writers against placing visually similar words near each other. Their accessibility team reviews content for confusable word proximity as part of their publishing workflow.

### GOV.UK (gov.uk)
The UK government's content design principles mandate "one idea per sentence" and recommend choosing the simplest synonym available. Their writing guide includes a section on avoiding words that look or sound alike, with specific alternatives listed.

### Dyslexie Font / Atkinson Hyperlegible
These typefaces were specifically designed to maximize visual distinction between similar-looking characters. Dyslexie (paid) tilts and weights letter shapes to make each unique. Atkinson Hyperlegible (free, from the Braille Institute) exaggerates distinctive features of letters. Both demonstrate that the typography layer is the strongest defense against confusion.

### Medium (medium.com)
Medium uses generous letter-spacing (0.05em on body, 0.1em on headings) and word-spacing that creates visual breathing room between words. While not specifically designed for dyslexia, the result is that confusable words are easier to distinguish because each letter has more space around it.

### Key Principles
1. **Prevention over mitigation** — the best fix is to choose words that don't look alike
2. **Letter-spacing is the strongest CSS lever** — even 0.05em makes a measurable difference in word-shape distinction
3. **Separation reduces confusion** — if two words look similar, putting them in different sections eliminates the comparison trap
4. **Content style guides prevent recurrence** — a writing guideline for content authors is as important as the CSS fix
