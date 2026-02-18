# 42. ChatGPT Name-Drop Undermines Expert Positioning

**Priority:** Low
**Location:** About Us page — "On the Cutting Edge" section
**Reported by:** Margaret Sullivan (AI-Curious Business Executive)

---

## User Story

**As a** 57-year-old insurance company president who is skeptical of AI hype and cautious about choosing a technology partner,
**I want** to see evidence of deep, specialized AI expertise — not name-drops of consumer tools I already know about,
**so that** I feel confident this firm has capabilities beyond what my nephew could do with a ChatGPT subscription.

---

## Problem

The About Us page includes the following statement in the "On the Cutting Edge" section:

> "From AI like ChatGPT to Salesforce products like Agentforce, we're on the cutting edge."

This sentence has two problems:

### 1. ChatGPT as a Credibility Marker Is Counterproductive

ChatGPT is a consumer product that Margaret's grandchildren use for homework. Citing it as evidence of AI expertise is like a construction firm saying "We use hammers" or an accounting firm saying "We use Excel." It demonstrates *awareness* of a mainstream tool, not deep capability.

For Margaret's persona specifically:
- She's already heard of ChatGPT — everyone has. Mentioning it tells her nothing new.
- She's looking for a firm that can do things she *can't* do herself. ChatGPT is something she could use herself (and probably has).
- The mention subtly signals that the company's AI capabilities are entry-level: "We know about the tool that literally everyone knows about."

### 2. "Cutting Edge" Claim Without Substantiation

The phrase "we're on the cutting edge" is an unsupported claim. What does "cutting edge" mean in practice? For an executive evaluating AI vendors, this needs specifics:
- What have you *built* with AI?
- What *outcomes* have you delivered?
- What AI capabilities do you have that your competitors don't?

The current sentence answers none of these questions. It's marketing assertion without evidence.

### Combined Effect

An AI-skeptical executive reads this sentence and thinks one of two things:
1. "These people think knowing about ChatGPT makes them AI experts — that's not reassuring."
2. "This is marketing fluff with no substance — what do they actually do?"

Neither reaction builds the confidence needed to proceed to a contact form.

---

## Acceptance Criteria

### A. Content Replacement
- [ ] The ChatGPT name-drop is removed from the About page
- [ ] The replacement copy describes **specific AI capabilities** LaunchPad Lab has built or delivered (not consumer tool names)
- [ ] The replacement copy includes at least one **concrete outcome or metric** (e.g., "reduced processing time by X%," "automated Y documents per month")
- [ ] The copy focuses on what LaunchPad Lab **builds**, not what tools they're aware of
- [ ] The tone conveys expertise through specifics, not through claims like "cutting edge"

### B. Show, Don't Tell
- [ ] The "On the Cutting Edge" section includes or links to at least one AI case study or example
- [ ] If a case study isn't available, the section includes a brief description of a real AI project with anonymized details
- [ ] Salesforce/Agentforce mention is acceptable if paired with a specific capability description (what they *do* with it, not just that they know it exists)

### C. Sitewide Consistency
- [ ] Audit all pages for other instances of consumer tool name-drops used as credibility markers
- [ ] Any remaining tool mentions are paired with descriptions of what the company builds with those tools
- [ ] "Cutting edge" and similar unsupported superlatives are replaced with evidence-based claims across the site

---

## How to Test

### Content Review
1. Navigate to the About Us page (`/about/` or `/about-us/`)
2. Scroll to the "On the Cutting Edge" section
3. Verify the ChatGPT name-drop has been removed
4. Read the replacement copy — verify it describes specific capabilities, not consumer tools
5. Verify the replacement includes at least one concrete metric or outcome
6. Verify the section links to or includes a relevant case study or project example

### Tone Audit
1. Read the replacement copy aloud
2. Ask: "Would this impress a skeptical executive who doesn't understand AI?"
3. Ask: "Does this tell me something I couldn't learn from Googling 'ChatGPT'?"
4. Ask: "Does this differentiate LaunchPad Lab from any other agency that says they do AI?"
5. If any answer is "no," the copy needs revision

### Sitewide Audit
1. Search the site for "ChatGPT" — verify zero results (or only in blog posts where contextually appropriate)
2. Search for "cutting edge," "state of the art," "world-class," "best in class" — verify all are either removed or substantiated with evidence
3. Search for other consumer AI brand names (Gemini, Copilot, Claude, Siri) — verify none are used as standalone credibility markers

### A/B Testing (Post-Launch)
1. If possible, A/B test the old copy vs. new copy on the About page
2. Track time-on-page and scroll depth for each variant
3. Track downstream conversion (About page → Contact form submission)

---

## Developer Notes

### Strategy

Replace the ChatGPT name-drop with outcome-focused copy that demonstrates AI expertise through specifics. The fix is primarily a content change, but the component structure should support richer content (metrics, case study links, capability descriptions).

### Current Copy (Before)

```html
<section class="about-innovation">
  <h2>On the Cutting Edge</h2>
  <p>
    From AI like ChatGPT to Salesforce products like Agentforce,
    we're on the cutting edge.
  </p>
</section>
```

### Recommended Copy (After) — Option A: Capability-Focused

```html
<section class="about-innovation" aria-labelledby="innovation-heading">
  <h2 id="innovation-heading">What We Build with AI</h2>
  <p class="about-innovation__intro">
    We build AI solutions that handle the work your team shouldn't
    have to do manually — from document processing that reads and
    routes thousands of forms per day, to intelligent workflows that
    cut decision turnaround from days to minutes.
  </p>

  <ul class="about-innovation__capabilities">
    <li>
      <strong>Intelligent Document Processing</strong>
      <span>
        AI that reads, extracts, and routes unstructured documents —
        claims forms, invoices, applications — with 95%+ accuracy
      </span>
    </li>
    <li>
      <strong>Workflow Automation</strong>
      <span>
        End-to-end process automation that connects your existing
        systems, eliminating manual handoffs and reducing cycle time
      </span>
    </li>
    <li>
      <strong>Conversational AI</strong>
      <span>
        Custom AI assistants trained on your data and policies — not
        generic chatbots, but tools that understand your business
      </span>
    </li>
    <li>
      <strong>Predictive Analytics</strong>
      <span>
        Models that surface patterns in your data to support faster,
        more informed business decisions
      </span>
    </li>
  </ul>

  <div class="about-innovation__proof">
    <blockquote>
      <p>
        "LaunchPad Lab's AI solution processes 2,000+ documents per day
        that our team used to handle manually. That's 200 hours a month
        back in our people's hands."
      </p>
      <footer>
        <cite>— Director of Operations, Regional Financial Services Firm</cite>
      </footer>
    </blockquote>
    <a href="/work/" class="about-innovation__link">
      See our AI work
      <span aria-hidden="true">→</span>
    </a>
  </div>
</section>
```

### Recommended Copy (After) — Option B: Concise Replacement

If the section needs to stay brief, a minimal fix:

```html
<section class="about-innovation" aria-labelledby="innovation-heading">
  <h2 id="innovation-heading">AI That Delivers Results</h2>
  <p>
    From custom document processing systems that read thousands of
    forms per day, to enterprise automation that eliminates manual
    workflows — we build AI solutions that deliver measurable
    business outcomes. Our clients have seen processing times drop
    by 40% and staff hours freed by the hundreds.
  </p>
  <a href="/work/" class="about-innovation__link">
    See our results →
  </a>
</section>
```

### CSS for Capability List (Option A)

```css
.about-innovation {
  padding: 4rem 2rem;
  max-width: 900px;
  margin: 0 auto;
}

.about-innovation__intro {
  font-size: 1.125rem;
  line-height: 1.8;
  color: #374151;
  margin-bottom: 2.5rem;
  max-width: 720px;
}

.about-innovation__capabilities {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
  list-style: none;
  padding: 0;
  margin: 0 0 3rem;
}

.about-innovation__capabilities li {
  padding: 1.5rem;
  background-color: #f9fafb;
  border-radius: 12px;
  border: 1px solid #e5e7eb;
}

.about-innovation__capabilities strong {
  display: block;
  font-size: 1rem;
  color: #111827;
  margin-bottom: 0.5rem;
}

.about-innovation__capabilities span {
  font-size: 0.9375rem;
  line-height: 1.6;
  color: #4b5563;
}

.about-innovation__proof {
  padding: 2rem 2.5rem;
  background-color: #f0f7ff;
  border-left: 4px solid #2563eb;
  border-radius: 0 12px 12px 0;
  margin-bottom: 1.5rem;
}

.about-innovation__proof blockquote {
  margin: 0 0 1rem;
}

.about-innovation__proof p {
  font-size: 1.0625rem;
  line-height: 1.7;
  color: #1e3a5f;
  font-style: italic;
  margin: 0 0 0.75rem;
}

.about-innovation__proof cite {
  font-size: 0.875rem;
  color: #4b5563;
  font-style: normal;
}

.about-innovation__link {
  display: inline-flex;
  align-items: center;
  gap: 0.375rem;
  font-size: 1rem;
  font-weight: 600;
  color: #2563eb;
  text-decoration: none;
}

.about-innovation__link:hover {
  text-decoration: underline;
}

.about-innovation__link:focus-visible {
  outline: 2px solid #2563eb;
  outline-offset: 2px;
  border-radius: 2px;
}
```

### Content Principles for AI Credibility

When writing about AI capabilities on a consulting site, follow these principles:

| Don't | Do |
|---|---|
| Name-drop consumer tools (ChatGPT, Copilot) | Describe what you build with AI |
| Say "cutting edge" or "state of the art" | Show outcomes: "reduced by 40%," "2,000 docs/day" |
| List tools you know about | List problems you've solved |
| Use AI buzzwords (leverage, harness, unlock) | Use concrete verbs (build, process, automate, reduce) |
| Imply awareness = expertise | Demonstrate expertise through case studies and metrics |

### Salesforce/Agentforce Reference

The Salesforce/Agentforce mention can be retained if reframed from awareness to capability:

**Before (awareness):** "Salesforce products like Agentforce"

**After (capability):**
```
We're certified Salesforce partners who build custom Agentforce
implementations — from lead routing automation to AI-powered
service agents that resolve 60% of customer inquiries without
human intervention.
```

The difference: the "before" says "we know this product exists." The "after" says "here's what we build with it and the results we deliver."

### WCAG References

- **WCAG 2.1 SC 2.4.6 Headings and Labels (AA):** Section headings should accurately describe the content. "On the Cutting Edge" is vague; "What We Build with AI" or "AI That Delivers Results" is descriptive and scannable.
- **WCAG 2.1 SC 1.3.1 Info and Relationships (A):** Capability lists should use semantic `<ul>` / `<li>` structure so screen readers convey the list relationship.
- **WCAG 2.1 SC 2.4.4 Link Purpose (A):** The "See our AI work" link should clearly indicate where it goes. Avoid "Learn more" or "Click here."

### Components to Audit

| Component / Section | Page(s) | What to Fix |
|---|---|---|
| "On the Cutting Edge" section | About page | Replace ChatGPT name-drop with capability-focused copy |
| Section heading | About page | Change from vague "Cutting Edge" to descriptive heading |
| AI service descriptions | AI Automation page, Services page | Audit for consumer tool name-drops; replace with outcomes |
| Blog posts | Blog | ChatGPT mentions in blog context are acceptable — they're educational, not credibility claims |
| Homepage hero copy | Homepage | Audit for unsupported superlatives ("world-class," "best in class") |
| Case study links | About page, Service pages | Add links from capability descriptions to relevant case studies |

---

## Examples from Other Sites

### Thoughtbot (thoughtbot.com/services/ai)
Thoughtbot's AI services page describes what they build, not what tools they use: "We help teams integrate AI into existing products — from recommendation engines to document analysis to conversational interfaces." No ChatGPT mention. No "cutting edge." Just capabilities and outcomes.

### Palantir (palantir.com)
Palantir never name-drops consumer AI tools. Their messaging focuses entirely on what their platform *does*: "Deploy AI on real-world data to make better decisions." Every claim is paired with a case study or demo. The credibility comes from demonstrated capability, not tool awareness.

### McKinsey Digital (mckinsey.com/capabilities/mckinsey-digital)
McKinsey's AI messaging focuses on business outcomes: "Rewiring organizations for AI-powered growth." They reference proprietary tools and frameworks, not consumer brands. When they mention specific technologies, it's in the context of what they built: "We developed a custom NLP pipeline that processes 10,000 legal documents per hour."

### Slalom (slalom.com/capabilities/ai-and-machine-learning)
Slalom describes AI capabilities by industry vertical: "In insurance, we've built AI systems that automate claims triage, reducing processing time by 45%." The specificity builds credibility. They mention technology platforms (Azure AI, AWS SageMaker) but always in the context of what they built, not as standalone credentials.

### IBM Consulting (ibm.com/consulting/artificial-intelligence)
IBM's AI consulting pages never say "We use Watson" as a standalone claim. Instead: "We helped [client] build a custom AI solution using Watson that processes 500,000 customer inquiries per month with 92% accuracy." The tool is mentioned as an ingredient, not the dish.

### Key Patterns
1. **Lead with outcomes, not tools** — "Reduced processing time by 40%" beats "We use ChatGPT"
2. **Describe what you build, not what you know** — Awareness of a tool is not a differentiator
3. **Industry-specific examples** — "In insurance, we built X" is more persuasive to an insurance exec than generic AI claims
4. **Show, don't tell** — Replace "cutting edge" with a case study link or a specific metric
5. **Consumer tools in context only** — It's fine to mention ChatGPT in a blog post explaining AI concepts. It's not fine to cite it as evidence of expertise on your About page.
