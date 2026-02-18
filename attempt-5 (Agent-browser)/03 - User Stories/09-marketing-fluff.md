# Issue 9: Replace Marketing Fluff with Concrete Service Descriptions

**Priority:** Medium
**Location:** Homepage services cards, Services page, hero sections
**Reported by:** Yuki Tanaka (Non-Native English Speaker), Richard Okonkwo (Non-Technical Business Executive)

---

## User Story

**As a** prospective client evaluating LaunchPad Lab's services,
**I want** service descriptions that clearly explain what the company does and what outcomes I can expect,
**so that** I can quickly determine whether their offerings match my business needs without decoding marketing language.

---

## Problem

Service taglines across the site use aspirational marketing language that provides no concrete information:

| Service | Current Tagline | Problem |
|---------|----------------|---------|
| Web App Development | "Bespoke, redefining experiences" | "Bespoke" is jargon; "redefining experiences" says nothing about the actual service |
| Mobile App Development | "Meeting users where they are" | Cliché idiom; doesn't explain the service at all |
| Product Strategy & Design | "Agile, cross-functional expertise" | Two jargon words; meaningless to non-technical audiences |

Additionally, superlatives like "high-impact," "world-class," "award-winning," "mission-critical," and "cutting-edge" appear throughout without supporting evidence. These words are:

- **Empty for non-native speakers** — "cutting-edge" is an idiom with no literal meaning; "world-class" is unmeasurable
- **Frustrating for business executives** — vague claims without metrics, case studies, or testimonials to back them up
- **Inaccessible for users with cognitive disabilities** — jargon and fluff increase cognitive load without adding information

---

## Acceptance Criteria

- [ ] Each service card on the homepage has a tagline that describes the service in plain language (no idioms, no jargon)
- [ ] Each tagline communicates a concrete benefit or outcome, not an aspiration
- [ ] All superlatives ("world-class," "cutting-edge," "high-impact," etc.) are either removed or replaced with specific, verifiable claims
- [ ] Where a superlative is retained, it is immediately supported by evidence (e.g., "Award-winning — rated #1 on Clutch for Chicago app development, 2025")
- [ ] Service descriptions on the Services page use plain language understandable by a non-native English speaker at B1-B2 level
- [ ] Readability of service descriptions tests at or below 8th-grade reading level (Flesch-Kincaid)

---

## How to Test

1. **Content audit:** Review every service card on the homepage and Services page. For each tagline, ask: "Does this tell a first-time visitor what the service actually is?"
2. **Plain language check:** Run all service descriptions through the [Hemingway Editor](https://hemingwayapp.com/) and verify they score at Grade 8 or below
3. **Superlative scan:** Search the codebase for the following terms and verify each instance is either removed or supported by evidence:
   - `world-class`, `cutting-edge`, `high-impact`, `best-in-class`, `mission-critical`, `award-winning`, `game-changing`, `revolutionary`
4. **Non-native speaker test:** Have a non-native English speaker (or use a B1-level English comprehension rubric) read each service description and confirm they can explain what the service is
5. **A/B comparison:** Compare old vs. new taglines side-by-side and verify the new versions communicate concrete information
6. **Screen reader:** Verify service card descriptions are announced correctly and make sense when read aloud sequentially

---

## Developer Notes

### Approach

This is primarily a content change, but it may require template modifications if taglines are hardcoded or if new elements (evidence badges, metric callouts) are added.

### Replacing Taglines

Replace vague taglines with concrete benefit statements:

```html
<!-- BEFORE -->
<div class="service-card">
  <h3>Web App Development</h3>
  <p class="service-card__tagline">Bespoke, redefining experiences</p>
</div>

<!-- AFTER -->
<div class="service-card">
  <h3>Web App Development</h3>
  <p class="service-card__tagline">
    Custom web-based software for your business —
    portals, dashboards, internal tools, and customer-facing platforms.
  </p>
</div>
```

Recommended replacement taglines:

| Service | Before | After |
|---------|--------|-------|
| Web App Development | "Bespoke, redefining experiences" | "Custom web applications — portals, dashboards, and internal tools built for your business" |
| Mobile App Development | "Meeting users where they are" | "iOS and Android apps that give your customers and team mobile access to your systems" |
| Product Strategy & Design | "Agile, cross-functional expertise" | "We help you define what to build, design how it works, and plan the fastest path to launch" |
| AI Solutions | "Harness the power of AI" | "Integrate AI features — like document processing, predictions, and chatbots — into your software" |

### Replacing Superlatives with Evidence

```html
<!-- BEFORE -->
<p>We deliver world-class, cutting-edge digital solutions.</p>

<!-- AFTER -->
<p>
  We've delivered <strong>730+ projects</strong> across 12 years for clients
  including Kawasaki, TransUnion, and the American Medical Association.
</p>
```

If awards are cited, make them specific:

```html
<!-- BEFORE -->
<span class="badge">Award-Winning</span>

<!-- AFTER -->
<span class="badge" aria-label="Clutch Top App Developer 2025">
  Clutch Top App Developer — 2025
</span>
```

### Writing Guidelines for Content Authors

Create a content style guide that enforces:

```markdown
## Service Description Rules

1. **Lead with what, not how it feels.**
   Bad:  "Redefining the digital experience"
   Good: "Custom web applications for business operations"

2. **Name the deliverable.**
   Bad:  "Meeting users where they are"
   Good: "iOS and Android apps"

3. **Use numbers when possible.**
   Bad:  "Extensive experience across industries"
   Good: "730+ projects across 50+ industries since 2012"

4. **No idioms.**
   Bad:  "Move the needle," "Hit the ground running"
   Good: "Improve your metrics," "Start building in week one"

5. **Max 20 words per sentence. Active voice. Grade 8 reading level.**
```

### CSS for Evidence Callouts

If adding inline evidence or metrics alongside claims:

```css
.evidence-callout {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.25rem 0.75rem;
  background-color: #ecfdf5;
  border: 1px solid #a7f3d0;
  border-radius: 6px;
  font-size: 0.875rem;
  font-weight: 600;
  color: #065f46;
}

.evidence-callout__icon {
  width: 1rem;
  height: 1rem;
}
```

```html
<span class="evidence-callout">
  <svg class="evidence-callout__icon" aria-hidden="true"><!-- checkmark icon --></svg>
  730+ projects delivered
</span>
```

### Components to Audit

- **Homepage service cards** — Replace all taglines
- **Services page** — Replace hero text, section descriptions, and any marketing copy
- **Hero sections across all pages** — Scan for superlatives and replace
- **CMS content fields** — If taglines are CMS-managed, update them there
- **Meta descriptions / SEO** — Update page meta descriptions if they contain the old fluff language
- **Component library** — If service cards are a shared component, ensure the tagline field supports longer text (may need to adjust `max-width` or truncation logic)

---

## Examples from Other Sites

### Basecamp (basecamp.com)
Uses concrete, plain-language descriptions: "Basecamp is a project management tool that helps teams track work, communicate, and meet deadlines." No fluff, no superlatives.

### Stripe (stripe.com)
"Financial infrastructure for the internet. Millions of businesses use Stripe to accept payments, send payouts, and manage their businesses online." Specific, evidence-backed, plain language.

### Gov.uk Design System
The UK Government Digital Service mandates plain language at a reading age of 9. Every service description explains what it does in one sentence: "Check if you need a tax return" — not "Unleash your financial potential."

### Thoughtbot
Service descriptions read: "We help you validate your product idea, design the user experience, and build the first version." Concrete steps, no idioms.
