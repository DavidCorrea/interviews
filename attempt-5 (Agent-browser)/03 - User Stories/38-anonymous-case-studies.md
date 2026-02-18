# 38. Anonymous Case Study Company Names Reduce Trust

**Priority:** Medium
**Location:** Our Work page, Insurance page (case study references)
**Reported by:** Margaret Sullivan (57-year-old president of a mid-size insurance brokerage)
**WCAG:** [1.3.1 Info and Relationships (A)](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships), [2.4.6 Headings and Labels (AA)](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels), [3.1.5 Reading Level (AAA)](https://www.w3.org/WAI/WCAG21/Understanding/reading-level)

---

## User Story

**As a** business executive comparing development agencies for a major project,
**I want** case studies to include enough identifying detail that I can assess whether the company served businesses comparable to mine,
**so that** I can trust the claimed results and confidently recommend this agency to my board — even when the client name is confidential.

---

## Problem

Several case studies across the LaunchPad Lab site use generic, anonymized titles that strip away the context executives need to evaluate relevance and credibility:

1. **"Healthcare Insurance Platform"** — What kind of healthcare insurance? A 50-person benefits administrator or a 10,000-employee carrier? A Medicare supplement provider or a commercial group health insurer? The anonymized name reveals nothing that helps Margaret assess comparability to her own brokerage.

2. **"Financial Services Firm"** — This could mean anything from a two-person RIA to Goldman Sachs. Without any detail about the firm's size, sub-segment, or geography, Margaret can't determine whether the challenges described are relevant to a mid-size insurance brokerage.

3. **"Actuarial Firm"** — Slightly more specific, but still opaque. Was this a consulting actuarial firm or an in-house actuarial department? How large? What lines of business?

4. **"Wealth Management Firm"** — Again, the range is enormous. A solo financial advisor and a $50B AUM wealth management firm face completely different technology challenges.

### Why This Matters for Margaret

Margaret's decision-making process for a $200K+ software engagement involves:

- **Board presentation:** She must justify the vendor choice to skeptical board members. "They built a platform for an anonymous healthcare company" carries zero persuasive weight. "They built a claims automation platform for a 300-employee P&C brokerage serving the Midwest" is something the board can evaluate.

- **Peer validation:** Insurance executives talk to each other. Margaret wants to ask: "Has anyone worked with LaunchPad Lab?" Named clients enable this. Anonymous ones don't.

- **Comparability assessment:** The single most important question Margaret asks when reading a case study is: "Is this company like mine?" Anonymized titles make this assessment impossible.

- **Trust calibration:** In a skeptical executive's mind, anonymization raises the question: "Are they hiding something? Did this project actually go well?" Even though NDA-driven anonymization is standard practice, the default assumption for a skeptical buyer is suspicion, not understanding.

### The Trust Spectrum

| Level | Example | Trust Impact |
|---|---|---|
| **Named client + testimonial** | "Prosci — a 500-employee change management firm" | Highest trust: verifiable, peer-referenceable |
| **Named client, no testimonial** | "CDK Global" | High trust: verifiable, no social proof |
| **Anonymous + rich context** | "A 300-employee P&C brokerage in the Midwest" | Moderate trust: comparable, not verifiable |
| **Anonymous + minimal context** | "Healthcare Insurance Platform" | Low trust: neither comparable nor verifiable |
| **Completely generic** | "A company in the insurance space" | Lowest trust: provides no useful information |

Most of LaunchPad Lab's anonymous case studies fall at "Low trust" — the second-worst level. Moving them to "Moderate trust" with added context would significantly improve their persuasive value.

---

## Acceptance Criteria

### A. Enriched Anonymous Case Studies
- [ ] Every anonymized case study includes at minimum: industry sub-segment, approximate company size (employees or revenue range), geography (region, not city), and project scope (duration, team size)
- [ ] Each case study title is descriptive enough that a reader can assess comparability: e.g., "Claims Automation for a Mid-Size P&C Brokerage" instead of "Healthcare Insurance Platform"
- [ ] A brief "About the Client" section appears at the top of each case study with the contextual details, even when the client name is withheld
- [ ] The reason for anonymization is acknowledged naturally (e.g., "Client name withheld per NDA")

### B. Named Client Acquisition
- [ ] A process exists for requesting client permission to use their name in case studies (even if retroactive)
- [ ] At least 50% of featured case studies on the Our Work page use named clients (aspirational target, measured over 6 months)
- [ ] For any new project, client permission for a named case study is requested during the project close-out process (a checkbox in the project wrap-up checklist)

### C. Video Testimonials
- [ ] At least 2-3 video testimonials from named clients are available on the site (homepage, Our Work page, or a dedicated Testimonials page)
- [ ] Video testimonials include the speaker's name, title, and company
- [ ] Videos are captioned for accessibility (WCAG 1.2.2 Captions — Prerecorded, Level A)
- [ ] Videos have a text transcript available (WCAG 1.2.1 Audio-only and Video-only — Prerecorded, Level A)

### D. Case Study Card Improvements
- [ ] Case study cards on the Our Work page display contextual metadata: industry sub-segment, company size category (startup / mid-market / enterprise), and key technologies
- [ ] Anonymous case studies are not visually indistinguishable from named ones — they include the enriched context directly on the card
- [ ] Card titles avoid generic labels; they describe the project outcome or challenge (e.g., "Automating Claims Intake for a Regional Brokerage" not "Insurance Platform")

---

## How to Test

### Context Audit
1. Navigate to the Our Work page (`/work/` or equivalent)
2. Identify all case studies with anonymized company names
3. For each, check whether the following details are present:
   - Industry sub-segment (e.g., "P&C brokerage" vs. just "insurance")
   - Company size (employees, revenue range, or descriptive category)
   - Geography (region or market)
   - Project type and scope
4. **Pass criteria:** All four details are present for every anonymous case study
5. **Fail criteria:** Any anonymous case study has fewer than 3 of these details

### Comparability Test
1. Show 3 anonymous case study cards to someone in Margaret's position (an insurance executive or business owner)
2. Ask: "Which of these companies is most similar to yours?"
3. **Pass criteria:** The person can make a meaningful comparison based on the information shown
4. **Fail criteria:** The person says "I can't tell — there's not enough information"

### Title Specificity Test
1. Read each case study title aloud, without opening the page
2. For each title, ask: "Can I identify what industry, what size company, and what was built?"
3. **Pass criteria:** At least 2 of 3 are identifiable from the title alone
4. **Fail criteria:** The title is generic (e.g., "Financial Services Firm") with no outcome or scope

### Video Testimonial Test
1. If video testimonials exist, play each one
2. Verify captions are available and accurate (WCAG 1.2.2)
3. Verify a transcript link is available below the video (WCAG 1.2.1)
4. Verify the speaker's name, title, and company are displayed

### Screen Reader Test
1. Navigate to the Our Work page with a screen reader
2. Browse the case study cards
3. Verify the card content (including contextual metadata) is announced in a logical order: title → client context → project summary → technology tags → link
4. Verify the "About the Client" section within individual case studies is marked up with appropriate headings

---

## Developer Notes

### Approach: Enrich Anonymous Case Study Cards and Detail Pages

This requires both content and structural changes. The HTML templates need new fields; the content team needs to provide the contextual details.

### HTML: Enriched Case Study Card

```html
<!-- Before: Generic anonymous card -->
<!--
<article class="case-card">
  <h3>Healthcare Insurance Platform</h3>
  <p>Built a modern claims management platform.</p>
  <a href="/work/healthcare-insurance-platform/">View case study</a>
</article>
-->

<!-- After: Context-rich anonymous card -->
<article class="case-card" data-industry="insurance" data-size="mid-market">
  <div class="case-card__header">
    <span class="case-card__industry">Property & Casualty Insurance</span>
    <span class="case-card__nda" aria-label="Client name confidential">
      NDA
    </span>
  </div>

  <h3 class="case-card__title">
    Automating Claims Intake for a Regional Brokerage
  </h3>

  <div class="case-card__context">
    <dl class="case-card__meta">
      <div class="case-card__meta-item">
        <dt class="sr-only">Company size</dt>
        <dd>~300 employees</dd>
      </div>
      <div class="case-card__meta-item">
        <dt class="sr-only">Region</dt>
        <dd>Midwest U.S.</dd>
      </div>
      <div class="case-card__meta-item">
        <dt class="sr-only">Project duration</dt>
        <dd>6-month engagement</dd>
      </div>
    </dl>
  </div>

  <p class="case-card__summary">
    Replaced a manual, email-based claims intake process with an
    AI-powered system that extracts data from loss notices and
    populates the client's Applied Epic instance — reducing processing
    time by 60%.
  </p>

  <div class="case-card__tech">
    <span class="tech-chip">OpenAI API</span>
    <span class="tech-chip">Applied Epic</span>
    <span class="tech-chip">React</span>
  </div>

  <a href="/work/healthcare-insurance-platform/" class="case-card__link">
    Read the full case study
    <span aria-hidden="true">→</span>
  </a>
</article>
```

### CSS: Enhanced Case Study Cards

```css
.case-card {
  display: flex;
  flex-direction: column;
  padding: 1.75rem;
  background: #ffffff;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  transition: box-shadow 0.2s ease, border-color 0.2s ease;
}

.case-card:hover {
  border-color: #c7d2fe;
  box-shadow: 0 4px 12px rgba(99, 102, 241, 0.08);
}

.case-card__header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.75rem;
}

.case-card__industry {
  font-size: 0.75rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.04em;
  color: #6366f1;
}

.case-card__nda {
  display: inline-flex;
  align-items: center;
  padding: 0.125rem 0.5rem;
  font-size: 0.625rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.06em;
  color: #92400e;
  background-color: #fef3c7;
  border-radius: 999px;
}

.case-card__title {
  font-size: 1.1875rem;
  font-weight: 700;
  color: #111827;
  line-height: 1.3;
  margin-bottom: 0.75rem;
}

.case-card__context {
  margin-bottom: 1rem;
}

.case-card__meta {
  display: flex;
  flex-wrap: wrap;
  gap: 0.375rem;
  margin: 0;
}

.case-card__meta-item {
  display: inline-flex;
}

.case-card__meta-item dd {
  display: inline-block;
  padding: 0.1875rem 0.625rem;
  font-size: 0.75rem;
  font-weight: 500;
  color: #4b5563;
  background-color: #f3f4f6;
  border-radius: 999px;
  margin: 0;
}

.case-card__summary {
  font-size: 0.9375rem;
  line-height: 1.6;
  color: #4b5563;
  margin-bottom: 1rem;
  flex-grow: 1;
}

.case-card__tech {
  display: flex;
  flex-wrap: wrap;
  gap: 0.375rem;
  margin-bottom: 1.25rem;
}

.tech-chip {
  display: inline-block;
  padding: 0.1875rem 0.5rem;
  font-size: 0.6875rem;
  font-weight: 600;
  color: #6b7280;
  background-color: #f9fafb;
  border: 1px solid #e5e7eb;
  border-radius: 999px;
}

.case-card__link {
  font-size: 0.9375rem;
  font-weight: 600;
  color: #4f46e5;
  text-decoration: none;
  margin-top: auto;
}

.case-card__link:hover {
  text-decoration: underline;
  text-underline-offset: 2px;
}

.case-card__link:focus-visible {
  outline: 2px solid #4f46e5;
  outline-offset: 2px;
  border-radius: 4px;
}
```

### HTML: "About the Client" Section Within Case Study Pages

```html
<!-- At the top of each anonymous case study detail page -->
<article class="case-study">
  <header class="case-study__header">
    <h1>Automating Claims Intake for a Regional Brokerage</h1>
    <p class="case-study__subtitle">
      AI-powered document processing replacing a manual,
      email-based intake workflow.
    </p>
  </header>

  <aside class="case-study__client-context"
         aria-labelledby="client-context-heading">
    <h2 id="client-context-heading" class="sr-only">About the Client</h2>
    <dl class="client-context__grid">
      <div class="client-context__item">
        <dt>Industry</dt>
        <dd>Property & casualty insurance brokerage</dd>
      </div>
      <div class="client-context__item">
        <dt>Company Size</dt>
        <dd>~300 employees across 12 offices</dd>
      </div>
      <div class="client-context__item">
        <dt>Region</dt>
        <dd>Midwest United States</dd>
      </div>
      <div class="client-context__item">
        <dt>Project Duration</dt>
        <dd>6 months (discovery through launch)</dd>
      </div>
      <div class="client-context__item">
        <dt>Team</dt>
        <dd>2 engineers, 1 designer, 1 product strategist</dd>
      </div>
      <div class="client-context__item">
        <dt>Technology</dt>
        <dd>OpenAI API, Applied Epic integration, React, Node.js</dd>
      </div>
    </dl>
    <p class="client-context__nda-note">
      <em>Client name withheld per mutual non-disclosure agreement.</em>
    </p>
  </aside>

  <!-- Rest of case study content -->
</article>
```

### CSS: Client Context Section

```css
.case-study__client-context {
  padding: 1.5rem;
  background-color: #f9fafb;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  margin: 2rem 0;
}

.client-context__grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem 2rem;
  margin: 0;
}

.client-context__item {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}

.client-context__item dt {
  font-size: 0.6875rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.06em;
  color: #9ca3af;
}

.client-context__item dd {
  font-size: 0.9375rem;
  font-weight: 500;
  color: #111827;
  margin: 0;
}

.client-context__nda-note {
  margin-top: 1rem;
  padding-top: 1rem;
  border-top: 1px solid #e5e7eb;
  font-size: 0.8125rem;
  color: #9ca3af;
}
```

### HTML: Video Testimonial Component

```html
<section class="testimonials-video" aria-labelledby="video-test-heading">
  <h2 id="video-test-heading">What Our Clients Say</h2>

  <div class="video-testimonial">
    <div class="video-testimonial__player">
      <video controls preload="metadata" width="640" height="360"
             poster="/images/testimonials/client-a-poster.jpg">
        <source src="/videos/testimonials/client-a.mp4" type="video/mp4" />
        <track kind="captions" src="/videos/testimonials/client-a.vtt"
               srclang="en" label="English captions" default />
        Your browser does not support the video element.
      </video>
    </div>
    <div class="video-testimonial__details">
      <blockquote class="video-testimonial__quote">
        "LaunchPad Lab didn't just build us software — they helped us
        rethink how our entire claims team operates. The AI intake
        system paid for itself in four months."
      </blockquote>
      <div class="video-testimonial__attribution">
        <img src="/images/testimonials/client-a-avatar.jpg" alt=""
             class="video-testimonial__avatar"
             width="48" height="48" loading="lazy" />
        <div>
          <cite class="video-testimonial__name">Sarah Kowalski</cite>
          <span class="video-testimonial__role">
            COO, Regional Insurance Brokerage (300 employees)
          </span>
        </div>
      </div>
      <details class="video-testimonial__transcript">
        <summary>Read transcript</summary>
        <div class="transcript-content">
          <p>
            [Sarah Kowalski, COO of a regional insurance brokerage,
            speaking from her office]
          </p>
          <p>
            "When we first talked to LaunchPad Lab, I was skeptical.
            We'd been burned before by vendors who promised the moon.
            But they took the time to understand our claims workflow —
            they sat with our adjusters, watched how they processed
            loss notices, and mapped out every bottleneck..."
          </p>
          <!-- Full transcript continues -->
        </div>
      </details>
    </div>
  </div>
</section>
```

### CSS: Video Testimonial

```css
.video-testimonial {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
  align-items: start;
  max-width: 1100px;
  margin: 2rem auto;
}

@media (max-width: 768px) {
  .video-testimonial {
    grid-template-columns: 1fr;
  }
}

.video-testimonial__player video {
  width: 100%;
  height: auto;
  border-radius: 8px;
  background-color: #000;
}

.video-testimonial__quote {
  font-size: 1.125rem;
  line-height: 1.7;
  color: #1f2937;
  font-style: italic;
  margin: 0 0 1.5rem;
  padding: 0;
  border: none;
}

.video-testimonial__attribution {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  margin-bottom: 1.5rem;
}

.video-testimonial__avatar {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  object-fit: cover;
}

.video-testimonial__name {
  display: block;
  font-weight: 700;
  font-size: 0.9375rem;
  color: #111827;
  font-style: normal;
}

.video-testimonial__role {
  display: block;
  font-size: 0.8125rem;
  color: #6b7280;
}

.video-testimonial__transcript summary {
  font-size: 0.875rem;
  font-weight: 600;
  color: #4f46e5;
  cursor: pointer;
  padding: 0.5rem 0;
}

.video-testimonial__transcript summary:hover {
  text-decoration: underline;
}

.video-testimonial__transcript summary:focus-visible {
  outline: 2px solid #4f46e5;
  outline-offset: 2px;
  border-radius: 4px;
}

.transcript-content {
  padding: 1rem;
  background-color: #f9fafb;
  border-radius: 8px;
  margin-top: 0.5rem;
  font-size: 0.875rem;
  line-height: 1.8;
  color: #4b5563;
}
```

### CMS Content Model Changes

For a CMS-driven site, add these fields to the case study content type:

```javascript
// Example schema for a headless CMS (Contentful, Sanity, etc.)
const caseStudySchema = {
  name: 'caseStudy',
  fields: [
    // Existing fields
    { name: 'title', type: 'string', required: true },
    { name: 'slug', type: 'slug', required: true },
    { name: 'body', type: 'richText', required: true },

    // New fields for anonymous case study context
    {
      name: 'clientName',
      type: 'string',
      description: 'Client company name (leave blank if NDA)',
    },
    {
      name: 'isAnonymous',
      type: 'boolean',
      description: 'Is the client name withheld?',
      default: false,
    },
    {
      name: 'industrySubSegment',
      type: 'string',
      description: 'Specific industry niche (e.g., "P&C brokerage", not just "insurance")',
      required: true,
    },
    {
      name: 'companySize',
      type: 'string',
      description: 'Approximate size: employees, revenue range, or category',
      required: true,
    },
    {
      name: 'geography',
      type: 'string',
      description: 'Region or market served (e.g., "Midwest U.S.")',
      required: true,
    },
    {
      name: 'projectDuration',
      type: 'string',
      description: 'Engagement length (e.g., "6 months")',
    },
    {
      name: 'teamComposition',
      type: 'string',
      description: 'Team size and roles (e.g., "2 engineers, 1 designer")',
    },
    {
      name: 'technologyStack',
      type: 'array',
      of: [{ type: 'string' }],
      description: 'Technologies used in the project',
      required: true,
    },
    {
      name: 'executiveSponsorTitle',
      type: 'string',
      description: 'Title of the client-side executive sponsor (e.g., "COO")',
    },
  ],

  // Validation: anonymous case studies must have enriched context
  validation: (doc) => {
    if (doc.isAnonymous) {
      const required = ['industrySubSegment', 'companySize', 'geography'];
      const missing = required.filter(f => !doc[f]);
      if (missing.length > 0) {
        return `Anonymous case studies require: ${missing.join(', ')}`;
      }
    }
    return true;
  },
};
```

### Title Improvement Matrix

| Current Title | Improved Title | Context Added |
|---|---|---|
| Healthcare Insurance Platform | Automating Claims Intake for a Regional P&C Brokerage | Sub-segment, project outcome, company type |
| Financial Services Firm | Modernizing Client Onboarding for a Mid-Market Wealth Advisor | Sub-segment, company size, project scope |
| Actuarial Firm | Predictive Analytics Dashboard for a 50-Person Actuarial Consultancy | Company size, deliverable, sub-segment |
| Wealth Management Firm | AI-Powered Portfolio Reporting for a $2B AUM Advisory Firm | Asset scale, deliverable, technology angle |

### Components to Audit

| Component | Page | What to Change |
|---|---|---|
| Case study card component | Our Work page | Add metadata fields: industry sub-segment, company size, geography, NDA badge |
| Case study detail template | Individual case study pages | Add "About the Client" context section at top |
| Case study CMS model | Backend | Add required fields for anonymous context (industry, size, geography, tech) |
| Case study titles | All pages with case study references | Replace generic titles with outcome-focused, context-rich titles |
| Video testimonial component | Homepage, Our Work page, Contact page | Create component with captions, transcripts, and attribution |
| Homepage carousel | Homepage | Update case study slide titles to use enriched versions |
| Insurance page references | Insurance page | Update any inline case study mentions with enriched context |

---

## Examples from Other Sites

### Bain & Company (bain.com/results)
Bain's case study pages are exemplary for anonymous work. Each case study includes: industry, company size ("a $5B specialty insurer"), geography ("North America"), the client executive's title ("the Chief Claims Officer"), and detailed methodology. The anonymization is handled so gracefully that readers forget the company name is missing — the context tells the whole story.

### McKinsey (mckinsey.com/client-stories)
McKinsey's client stories follow a strict template: "A [size] [industry] company in [region] facing [challenge]." Even when the client name is withheld, the opening sentence provides enough context for a reader to assess relevance. Named clients appear alongside anonymous ones without visual distinction — the focus is on the work, not the brand.

### Deloitte (deloitte.com/case-studies)
Deloitte mixes named and anonymous case studies on the same page. Anonymous ones use descriptive titles ("Transforming Claims Operations for a Top-10 P&C Insurer") and include a structured "Client Profile" sidebar with industry, size, geography, and challenge summary. The sidebar ensures context is always visible, not buried in the narrative.

### IDEO (ideo.com/work)
IDEO's portfolio uses named clients where possible but enriches every case study — named or not — with project context: the challenge, the team composition, the timeline, and the outcome. Their approach shows that even named case studies benefit from explicit context. The metadata isn't just for anonymous work.

### Thoughtbot (thoughtbot.com/work)
Thoughtbot names most of their clients and includes a project summary card at the top of each case study: client name, industry, engagement type, team size, duration, and technologies. This structured metadata appears consistently across all case studies, creating a scannable pattern that helps visitors quickly assess relevance.

### Key Patterns
1. **Structured context block** — Every case study (named or anonymous) gets a consistent metadata card: industry, size, geography, duration, team, technology
2. **Descriptive titles over generic labels** — "Automating Claims for a Regional Brokerage" vs. "Insurance Platform"
3. **Acknowledge the NDA naturally** — A brief "Client name withheld per NDA" is more trustworthy than silently omitting the name
4. **Executive sponsor title** — Mentioning "the COO" or "the VP of Claims" signals executive-level engagement without revealing the person's identity
5. **Video testimonials as trust accelerators** — Even one or two video testimonials dramatically increase perceived credibility; pair them with written case studies for maximum impact
6. **Consistent template** — Apply the same enriched structure to all case studies so visitors develop a reading pattern and know where to look for context
