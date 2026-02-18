# H-18: Hero Headline Fails to Communicate Core Offering

**Issue ID:** H-18
**Priority:** High
**WCAG Criteria:** 3.1.5 Reading Level (AAA)
**Affected Personas:** Big Company Owner, Senior Person, Cognitive Disability, Non-Native Speaker, Skeptical User

---

## User Story

**As a** prospective client visiting the homepage for the first time,
**I want** the hero headline to clearly describe what the company does,
**so that** I can immediately understand the service offering without having to scroll or read multiple paragraphs.

---

## Acceptance Criteria

- [ ] The homepage hero `<h1>` communicates the company's core offering in plain, concrete language (e.g., what they build, for whom, and the outcome).
- [ ] A user unfamiliar with the company can read the headline and supporting text and correctly identify the service category (e.g., "custom software development") within 5 seconds.
- [ ] The headline avoids vague buzzwords like "Innovation," "Solutions," and "Results that Matter" unless they are accompanied by specific, concrete descriptors.
- [ ] The supporting `<p>` text beneath the headline expands on the `<h1>` with a one-sentence value proposition that names the audience and benefit.
- [ ] Readability of the hero section scores at or below a Grade 8 reading level (Flesch-Kincaid or Hemingway).
- [ ] The headline remains meaningful when read out of context (e.g., by a screen reader listing headings).

---

## How to Test the Change

### Manual Testing

1. **Five-second test:** Show the hero section to 3–5 people unfamiliar with the company. Ask them to write down what the company does after 5 seconds. At least 4 of 5 should correctly identify the core service.
2. **Screen reader heading navigation:** Using NVDA or VoiceOver, press `H` to navigate headings. Confirm the `<h1>` alone conveys the service offering without needing surrounding content.
3. **Readability check:** Paste the headline + supporting text into [Hemingway Editor](https://hemingwayapp.com/) and confirm the reading level is Grade 8 or below.
4. **Non-native speaker review:** Ask a non-native English speaker to paraphrase the headline. They should be able to do so accurately.

### Automated Testing

- Run a Flesch-Kincaid readability analysis on the hero text content using a CI tool like `textstat` (Python) or `readable` (npm).
- Lint heading hierarchy: confirm the page has exactly one `<h1>` and it is inside the hero section.

---

## Developer Notes

### General Approach

Replace the current vague headline with a clear, specific value proposition. The pattern is: **[What you do] + [for whom] + [outcome/differentiator]**.

### Current State (Problem)

```html
<h1>AI Innovation. Digital Solutions. Results that Matter.</h1>
<p>We harness the power of technology to ship game-changing products.</p>
```

### Recommended Fix

```html
<h1>Custom Software & AI Development for Growing Businesses</h1>
<p>
  LaunchPad Lab designs, builds, and scales web and mobile applications
  that help companies modernize operations and reach customers faster.
</p>
```

### Guidelines

- Lead with the concrete service (e.g., "Custom Software Development").
- Name the audience (e.g., "for Growing Businesses," "for Enterprise Teams").
- End with a tangible outcome (e.g., "modernize operations," "increase revenue").
- Avoid jargon: replace "bespoke," "agentic AI," and "cross-functional" with plain equivalents.
- Keep the `<h1>` under 10 words if possible.

### Components / Files to Audit

- Homepage hero template (e.g., `front-page.php`, `hero.php`, or equivalent theme partial)
- Any ACF / custom field group populating the hero headline
- CMS entry for the homepage hero section

---

## Examples from Other Sites

| Site | Hero Headline | Why It Works |
|---|---|---|
| **Thoughtbot** | "We help you design, build, and grow your product." | Names the service (design, build, grow) and the object (your product). |
| **Pivotal Labs (VMware Tanzu)** | "Build software that transforms your business." | Action-oriented, names the outcome. |
| **Basecamp** | "The project management tool that helps small teams move faster." | Names the tool type, the audience, and the benefit in one line. |
| **Stripe** | "Financial infrastructure for the internet." | Extremely concise; names the category and scope. |
