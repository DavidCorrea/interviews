# AI-25: Publish Detailed Case Studies with Measurable Outcomes

## Metadata
- **ID:** AI-25
- **Priority:** 4 Low
- **Personas Affected:** 1 of 16 personas (Skeptical User)
- **WCAG Criteria:** Usability/trust (not WCAG-specific)
- **Effort:** Large (16–40 hours)

---

## User Story

**As a** skeptical evaluator researching agencies before making contact,

**I want** detailed case studies that include client names, problem statements, approaches, solutions, and measurable results (percentages, dollars, time saved),

**So that** I can assess LaunchPad Lab's capabilities and credibility without having to schedule a call or rely on generic testimonials.

---

## Acceptance Criteria

- [ ] At least 3 in-depth case studies published
- [ ] Each case study includes: client name (or approved attribution)
- [ ] Each case study includes: industry/sector
- [ ] Each case study includes: problem/challenge statement (2–3 sentences)
- [ ] Each case study includes: approach taken (3–5 bullet points)
- [ ] Each case study includes: solution delivered (what was built, technologies, timeline)
- [ ] Each case study includes: measurable results (2–3 quantified metrics)
- [ ] Metrics are specific (e.g., "40% increase in conversion," "3x faster page loads," "$2M revenue impact")
- [ ] Client logos on homepage/Work page link to corresponding case studies
- [ ] Case studies are discoverable from Work/Case Studies section
- [ ] Skeptical user can evaluate capabilities without contacting sales

---

## Test Plan

### Case Study Count
1. Visit `https://launchpadlab.com/work` or Case Studies section
2. **Expected:** At least 3 detailed case studies listed
3. **Fail:** Only client logos with no project context

### Content Completeness (Per Case Study)
For each of the 3+ case studies, verify:
1. **Client name & logo:** Present (or "Confidential" with industry if NDA)
2. **Industry:** Stated (e.g., Healthcare, FinTech, E-commerce)
3. **Challenge:** 2–3 sentences describing the problem
4. **Approach:** 3–5 bullet points or paragraphs on methodology
5. **Solution:** Description of what was built, tech stack, timeline
6. **Results:** At least 2 quantified metrics (%, $, time, etc.)

### Metric Specificity
1. Read the Results section of each case study
2. **Expected:** Specific numbers (e.g., "40% increase," "3x faster," "$500K saved")
3. **Fail:** Vague claims ("significant improvement," "better performance")

### Discoverability
1. From homepage, locate client logos or "Our Work" section
2. **Expected:** Logos or items link to case studies (or Work page with case study links)
3. From Work page, **Expected:** Clear path to individual case studies
4. **Expected:** Case studies are not buried or require contact to access

### Skeptical User Journey
1. Simulate: User lands on site, wants to evaluate before contacting
2. Navigate: Home → Work → Case Studies
3. **Expected:** Can read 3+ full case studies with metrics
4. **Expected:** Can form an opinion on capabilities without filling out a form or calling

### Structured Data (Optional)
1. View page source of a case study
2. **Expected:** JSON-LD Case Study or Article schema if implemented
3. Test with Google Rich Results Test

---

## Developer Notes

### Case Study Template
```markdown
# [Client Name] — [Project Title]

**Industry:** [Sector]
**Timeline:** [Duration]

## The Challenge

[2-3 sentences: What problem did the client face? What were the stakes?]

## Our Approach

- [Bullet 1: Discovery/research]
- [Bullet 2: Strategy/architecture]
- [Bullet 3: Development process]
- [Bullet 4: Testing/launch]
- [Bullet 5: Ongoing support if applicable]

## The Solution

[What was built: product, platform, integration. Technologies used. Key features.]

## Results

- [Metric 1: e.g., "40% increase in conversion rate"]
- [Metric 2: e.g., "$2M additional revenue in first year"]
- [Metric 3: e.g., "3x faster page load times"]
```

### Client Approval
- Obtain written approval from clients before publishing metrics
- Some clients prefer anonymized ("Fortune 500 retailer") — still include metrics
- Include "Results shared with client permission" if appropriate

### Linking from Homepage
- Client logo grid: each logo links to `/work/[client-slug]` or case study
- "View Case Study" or "Read more" on each card
- Ensure link purpose is clear (2.4.4)

### Structured Data (JSON-LD)
```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "[Client] Case Study",
  "author": { "@type": "Organization", "name": "LaunchPad Lab" },
  "datePublished": "2025-02-01",
  "mainEntityOfPage": { "@type": "WebPage", "@id": "https://launchpadlab.com/work/client-slug" }
}
```

### Content Creation Effort
- This is primarily a content/writing task, not a development task
- Coordinate with: account leads, clients, marketing
- Estimate: 4–8 hours per case study (interviews, writing, approval, design)
- Development: 2–4 hours for template, CMS setup, linking

### Metrics to Pursue
- Conversion rate changes
- Revenue impact
- Time/cost savings
- Performance improvements (load time, uptime)
- User satisfaction (NPS, surveys)
- Operational efficiency (e.g., "50% fewer support tickets")

---

## Examples

| Site | Approach |
|------|----------|
| **Thoughtbot.com/case-studies** | Detailed case studies with metrics; problem/solution/results format |
| **Pivotal Labs** | Case studies with client attribution; quantified outcomes |
| **McKinsey.com/our-insights** | In-depth client work; problem, approach, results |
| **IDEO** | Case studies with measurable impact; human-centered design outcomes |
| **Frog Design** | Case studies with client names; specific deliverables and results |

Professional services firms that publish detailed, metric-driven case studies build trust with skeptical buyers and reduce friction in the sales process.
