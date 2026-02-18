# 36. Unattributed Statistics Undermine Credibility

**Priority:** High
**Location:** AI Automation page (stats section), Insurance page (stats section), Services page
**Reported by:** Margaret Sullivan (57-year-old president of a mid-size insurance brokerage)
**WCAG:** [1.1.1 Non-text Content (A)](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content), [2.4.4 Link Purpose (A)](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context), [3.1.5 Reading Level (AAA)](https://www.w3.org/WAI/WCAG21/Understanding/reading-level)

---

## User Story

**As a** skeptical executive evaluating whether to invest six figures in a development partner,
**I want** every statistic on the site to be traceable to a specific client, case study, or methodology,
**so that** I can distinguish evidence-backed claims from marketing fluff and build confidence that these results are real and repeatable for a company like mine.

---

## Problem

Prominent statistics appear across multiple LaunchPad Lab pages without attribution, sources, or links to supporting evidence:

1. **"60%+ reduction in repetitive manual work"** — appears on the AI Automation page. Whose manual work? Which processes? Over what time period? Was this measured by the client or by LaunchPad Lab? There is no footnote, no case study link, and no methodology explanation.

2. **"3x faster response"** — appears without context. Faster than what baseline? Response to what (customer inquiries, system processing, deployment cycles)? Measured how?

3. **"140% increase in online conversions"** — a bold claim with no client attribution. Which client? What kind of conversions (sign-ups, purchases, form completions)? What was the baseline conversion rate? Over what period?

4. **"$2M in projected profit"** — "projected" is a red flag for an executive like Margaret. Projected by whom? Based on what model? Has it been validated? This reads as a forecast, not a result.

5. **Pattern across the site:** Stats are presented as large, visually prominent hero numbers — big font, accent colors, positioned to draw the eye — yet they carry zero evidentiary weight because none link to anything verifiable.

### Why This Matters for Margaret

Margaret is the president of a mid-size insurance brokerage. She reports to a board. If she recommends LaunchPad Lab as a vendor, she needs to present evidence to skeptical board members. Unattributed stats are not evidence — they're marketing assertions. Board members will ask: "Where did this number come from?" If Margaret can't answer, her credibility suffers alongside LaunchPad Lab's.

Insurance executives are trained to scrutinize numbers. Actuaries, underwriters, and risk managers deal in verifiable data every day. Presenting statistics without sources is the digital equivalent of an unsubstantiated insurance claim — it triggers distrust, not confidence.

---

## Acceptance Criteria

### A. Attribution Requirements
- [ ] Every statistic displayed on the site links to or cites a specific source: a named case study, a published report, a client testimonial, or an internal methodology description
- [ ] Attribution is visible immediately adjacent to the statistic (not hidden in a footer or separate page)
- [ ] Attribution includes at minimum: the client or project name (or anonymized descriptor), the metric being measured, and the time period
- [ ] For averaged or aggregated statistics (e.g., "clients typically see 60%+ reduction"), the methodology is explained: "Based on measurements across N client projects between [date range]"

### B. Link to Case Studies
- [ ] Each attributed statistic includes a hyperlink to the full case study or project description
- [ ] The link text is descriptive (e.g., "Read the full Healthcare Insurance Platform case study" — not "Learn more")
- [ ] Clicking the link takes the user directly to the relevant section of the case study where the metric is discussed
- [ ] Links are keyboard accessible and have visible focus indicators

### C. Handling Projections and Estimates
- [ ] Statistics labeled as "projected" or "estimated" are clearly marked with qualifying language (e.g., "Projected by [methodology] based on [data]")
- [ ] Projected stats are visually differentiated from measured results (e.g., italicized, with a "projected" badge, or in a distinct color)
- [ ] Projected stats do not appear as hero metrics or primary proof points — measured results take precedence

### D. Visual Design
- [ ] Stats remain visually prominent (large numbers, accent styling) but now include visible attribution below each number
- [ ] Attribution text is legible: minimum 14px font size, sufficient contrast (4.5:1 minimum per WCAG AA)
- [ ] The stats section does not feel cluttered despite added attribution — use progressive disclosure (tooltip or expandable detail) if space is constrained

---

## How to Test

### Attribution Audit
1. Navigate to the AI Automation page (`/services/ai-automation/` or equivalent)
2. Identify all statistics displayed as prominent numbers (large font, accent styling)
3. For each statistic, verify:
   - A source or client name is visible adjacent to the number
   - A link to a case study or methodology explanation exists
   - Clicking the link arrives at relevant supporting content
4. Repeat for the Insurance page and Services page

### Link Verification
1. For each stat with a case study link, click the link
2. Verify the destination page contains the specific metric cited
3. Verify the metric on the destination page matches (same number, same context)
4. If the link uses an anchor (`#section`), verify it scrolls to the correct section

### Keyboard and Accessibility Test
1. Tab through the stats section using keyboard only
2. Verify each stat's case study link is reachable via Tab
3. Verify focus indicators are visible on each link
4. Use a screen reader (VoiceOver/NVDA): verify the stat, its attribution, and its link are read as a coherent group
5. Verify link text is descriptive when read out of context (screen reader link lists)

### Contrast Check
1. Use a contrast checker (e.g., axe DevTools, WebAIM Contrast Checker) on the attribution text
2. Verify attribution text meets WCAG AA contrast ratio (4.5:1 for text below 18px, 3:1 for 18px+ bold)
3. Verify stat numbers themselves also meet contrast requirements

### Credibility Test
1. Show the stats section to a colleague unfamiliar with the company
2. Ask: "Do you believe these numbers? Why or why not?"
3. If the answer is "no" or "I'd need to see the source," the attribution is insufficient
4. After adding attribution, repeat the test — the answer should shift to "I'd want to read the case study" (engagement, not skepticism)

---

## Developer Notes

### Current State (Approximate)

```html
<!-- Current: unattributed stats displayed as hero numbers -->
<section class="stats-bar">
  <div class="stat">
    <span class="stat__number">60%+</span>
    <span class="stat__label">reduction in repetitive manual work</span>
  </div>
  <div class="stat">
    <span class="stat__number">3×</span>
    <span class="stat__label">faster response</span>
  </div>
  <div class="stat">
    <span class="stat__number">140%</span>
    <span class="stat__label">increase in online conversions</span>
  </div>
  <div class="stat">
    <span class="stat__number">$2M</span>
    <span class="stat__label">in projected profit</span>
  </div>
</section>
```

### Recommended: Attributed Stats with Case Study Links

```html
<section class="stats-bar" aria-label="Results from client projects">
  <h2 class="stats-bar__heading">Measurable Results</h2>

  <div class="stats-bar__grid">
    <figure class="stat" role="group" aria-label="60%+ reduction statistic">
      <div class="stat__metric">
        <span class="stat__number">60%+</span>
        <span class="stat__label">reduction in repetitive manual work</span>
      </div>
      <figcaption class="stat__attribution">
        Measured across the
        <a href="/work/healthcare-insurance-platform/#results"
           class="stat__source-link">
          Healthcare Insurance Platform
        </a>
        claims intake modernization (2024).
      </figcaption>
    </figure>

    <figure class="stat" role="group" aria-label="3x faster response statistic">
      <div class="stat__metric">
        <span class="stat__number">3×</span>
        <span class="stat__label">faster customer response time</span>
      </div>
      <figcaption class="stat__attribution">
        Achieved by
        <a href="/work/financial-services-portal/#results"
           class="stat__source-link">
          a financial services client
        </a>
        after deploying an AI-powered support agent (2024).
      </figcaption>
    </figure>

    <figure class="stat" role="group"
            aria-label="140% conversion increase statistic">
      <div class="stat__metric">
        <span class="stat__number">140%</span>
        <span class="stat__label">increase in online conversions</span>
      </div>
      <figcaption class="stat__attribution">
        E-commerce conversion lift for
        <a href="/work/tiny-house-listings/#results"
           class="stat__source-link">
          Tiny House Listings
        </a>
        after UX redesign (Q2–Q4 2023).
      </figcaption>
    </figure>

    <figure class="stat stat--projected" role="group"
            aria-label="$2M projected profit statistic">
      <div class="stat__metric">
        <span class="stat__number">$2M</span>
        <span class="stat__label">in projected annual profit impact</span>
        <span class="stat__badge" aria-label="This is a projected estimate">
          Projected
        </span>
      </div>
      <figcaption class="stat__attribution">
        Based on a
        <a href="/work/actuarial-platform/#roi-model"
           class="stat__source-link">
          validated ROI model
        </a>
        for an actuarial analytics platform, using client-provided
        baseline data and 12-month post-launch projections.
      </figcaption>
    </figure>
  </div>
</section>
```

### CSS: Attributed Stats

```css
.stats-bar {
  padding: 4rem 1.5rem;
  background-color: #f9fafb;
}

.stats-bar__heading {
  font-size: 0.875rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: #6b7280;
  text-align: center;
  margin-bottom: 2.5rem;
}

.stats-bar__grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 2rem;
  max-width: 1100px;
  margin: 0 auto;
}

.stat {
  text-align: center;
  padding: 1.5rem;
}

.stat__number {
  display: block;
  font-size: clamp(2.5rem, 5vw, 3.5rem);
  font-weight: 800;
  color: #111827;
  line-height: 1.1;
}

.stat__label {
  display: block;
  font-size: 1rem;
  font-weight: 500;
  color: #374151;
  margin-top: 0.5rem;
  line-height: 1.4;
}

.stat__attribution {
  font-size: 0.875rem;
  line-height: 1.6;
  color: #6b7280;
  margin-top: 0.75rem;
  padding-top: 0.75rem;
  border-top: 1px solid #e5e7eb;
}

.stat__source-link {
  color: #4f46e5;
  text-decoration: underline;
  text-underline-offset: 2px;
  font-weight: 500;
}

.stat__source-link:hover {
  color: #4338ca;
}

.stat__source-link:focus-visible {
  outline: 2px solid #4f46e5;
  outline-offset: 2px;
  border-radius: 2px;
}

/* Projected stats: visually differentiated */
.stat--projected .stat__number {
  color: #6b7280;
}

.stat__badge {
  display: inline-block;
  margin-top: 0.5rem;
  padding: 0.125rem 0.5rem;
  font-size: 0.6875rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: #92400e;
  background-color: #fef3c7;
  border-radius: 999px;
}
```

### Alternative: Tooltip-Based Attribution (Space-Constrained Layouts)

If the design cannot accommodate visible attribution text below every stat, use a tooltip pattern:

```html
<div class="stat">
  <span class="stat__number">60%+</span>
  <span class="stat__label">reduction in repetitive manual work</span>
  <button class="stat__info-trigger"
          aria-expanded="false"
          aria-controls="stat-60-detail"
          aria-label="View source for 60% reduction statistic">
    <svg aria-hidden="true" width="16" height="16" viewBox="0 0 16 16">
      <circle cx="8" cy="8" r="7" fill="none" stroke="currentColor"
              stroke-width="1.5"/>
      <text x="8" y="11.5" text-anchor="middle" font-size="10"
            fill="currentColor" font-weight="bold">i</text>
    </svg>
  </button>
  <div class="stat__tooltip" id="stat-60-detail" role="tooltip" hidden>
    <p>
      Measured across the
      <a href="/work/healthcare-insurance-platform/#results">
        Healthcare Insurance Platform
      </a>
      claims intake modernization (2024). Manual data entry tasks
      were reduced from ~40 hours/week to ~15 hours/week.
    </p>
  </div>
</div>
```

```javascript
class StatTooltip {
  constructor() {
    document.querySelectorAll('.stat__info-trigger').forEach(trigger => {
      const tooltipId = trigger.getAttribute('aria-controls');
      const tooltip = document.getElementById(tooltipId);

      trigger.addEventListener('click', () => {
        const isExpanded = trigger.getAttribute('aria-expanded') === 'true';
        trigger.setAttribute('aria-expanded', String(!isExpanded));
        tooltip.hidden = isExpanded;
      });

      // Close on Escape
      tooltip.addEventListener('keydown', (e) => {
        if (e.key === 'Escape') {
          trigger.setAttribute('aria-expanded', 'false');
          tooltip.hidden = true;
          trigger.focus();
        }
      });

      // Close when clicking outside
      document.addEventListener('click', (e) => {
        if (!trigger.contains(e.target) && !tooltip.contains(e.target)) {
          trigger.setAttribute('aria-expanded', 'false');
          tooltip.hidden = true;
        }
      });
    });
  }
}

document.addEventListener('DOMContentLoaded', () => new StatTooltip());
```

```css
.stat__info-trigger {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 20px;
  height: 20px;
  padding: 0;
  margin-left: 0.25rem;
  background: none;
  border: none;
  color: #9ca3af;
  cursor: pointer;
  vertical-align: middle;
  transition: color 0.15s ease;
}

.stat__info-trigger:hover,
.stat__info-trigger:focus-visible {
  color: #4f46e5;
}

.stat__info-trigger:focus-visible {
  outline: 2px solid #4f46e5;
  outline-offset: 2px;
  border-radius: 50%;
}

.stat__tooltip {
  position: absolute;
  top: calc(100% + 8px);
  left: 50%;
  transform: translateX(-50%);
  width: 280px;
  padding: 1rem;
  background: #ffffff;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  font-size: 0.8125rem;
  line-height: 1.6;
  color: #374151;
  z-index: 10;
}

.stat {
  position: relative;
}
```

### Methodology Page (For Aggregated Stats)

If statistics represent averages across multiple clients, create a methodology section:

```html
<!-- Linked from stats that cite aggregated data -->
<section id="methodology" aria-labelledby="methodology-heading">
  <h2 id="methodology-heading">How We Measure Results</h2>

  <dl class="methodology-list">
    <div class="methodology-item">
      <dt>What we measure</dt>
      <dd>
        Time savings, conversion rates, cost reductions, and user
        satisfaction scores — comparing pre-engagement baselines to
        post-launch metrics.
      </dd>
    </div>
    <div class="methodology-item">
      <dt>When we measure</dt>
      <dd>
        Baseline metrics are captured during discovery. Post-launch
        metrics are measured at 30, 90, and 180 days after deployment.
      </dd>
    </div>
    <div class="methodology-item">
      <dt>How we calculate averages</dt>
      <dd>
        Aggregated statistics (e.g., "clients typically see 60%+
        reduction") represent the median result across all measured
        projects in that category, not cherry-picked best cases.
      </dd>
    </div>
    <div class="methodology-item">
      <dt>Client verification</dt>
      <dd>
        All published metrics are reviewed and approved by the client
        before publication. Where clients prefer anonymity, we describe
        the project type and industry without naming the company.
      </dd>
    </div>
  </dl>
</section>
```

### Components to Audit

| Component | Page | What to Change |
|---|---|---|
| Stats bar / metrics section | AI Automation page | Add `<figcaption>` attribution with case study links to each stat |
| Stats section | Insurance page | Add attribution or remove unsubstantiated numbers |
| Stats section | Services page | Add attribution to any prominent metrics |
| Case study pages | Our Work | Ensure each case study page includes a `#results` section with the specific metrics cited elsewhere |
| Hero / banner stats | Any page with hero-level stats | Add visible attribution — these are the highest-visibility, highest-skepticism stats |
| CMS / content model | All pages | Add "source" and "case study link" fields to the stat content type so editors must provide attribution |

---

## Examples from Other Sites

### Salesforce (salesforce.com)
Salesforce displays stats like "25% increase in revenue" with immediate attribution: "See the Spotify customer story." Each stat links to a named customer case study with detailed metrics, methodology, and a video testimonial. The attribution is part of the stat's visual design, not an afterthought.

### HubSpot (hubspot.com/roi)
HubSpot has a dedicated ROI page where every metric links to a specific customer story. Stats are presented with context: "HubSpot customers see a 129% increase in leads within 12 months (based on 100,000+ customers)." The sample size and time frame are always stated.

### McKinsey (mckinsey.com)
McKinsey cites stats with footnotes linking to published research: "AI could deliver $1.2 trillion in value to the insurance industry (McKinsey Global Institute, 2023)." Even internal projections include methodology: "Based on analysis of 400+ insurance companies across 15 markets."

### Accenture (accenture.com)
Every stat on Accenture's site includes a source. Their typical pattern: big number → descriptive label → source citation → "Read the study" link. Projected numbers are explicitly labeled "projected" or "estimated" and include the research methodology in a linked report.

### Basecamp (basecamp.com)
Basecamp shows customer counts ("millions of users") with a link to a public customer directory. Specific outcome claims link to customer testimonials. Their approach is transparent: "Don't take our word for it — here are the people saying it."

### Key Patterns
1. **Every stat needs a source** — Named client, case study, research report, or methodology explanation
2. **Attribution is adjacent** — Visible directly below or beside the number, not on a separate page
3. **Hyperlink to proof** — One click from the stat to the full supporting evidence
4. **Projections are labeled** — "Projected" or "estimated" stats get different visual treatment and include methodology
5. **Sample sizes and time frames** — "Based on N clients" and "measured over X months" add credibility even when clients are anonymous
