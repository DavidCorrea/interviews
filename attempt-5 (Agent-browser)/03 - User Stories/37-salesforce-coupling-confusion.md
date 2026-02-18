# 37. Salesforce/Agentforce Coupling Creates AI Scope Confusion

**Priority:** Medium
**Location:** AI Automation page (Agentforce Quick Start, related content), Homepage footer
**Reported by:** Margaret Sullivan (57-year-old president of a mid-size insurance brokerage)
**WCAG:** [2.4.6 Headings and Labels (AA)](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels), [3.1.5 Reading Level (AAA)](https://www.w3.org/WAI/WCAG21/Understanding/reading-level)

---

## User Story

**As a** business executive whose company does not use Salesforce,
**I want** to clearly understand that LaunchPad Lab's AI capabilities work with any technology stack,
**so that** I don't dismiss them as a "Salesforce shop" and miss out on AI solutions that could work with my existing systems (Applied Epic, a custom SQL database, and Microsoft 365).

---

## Problem

The AI Automation page gives a strongly Salesforce-centric impression that misrepresents the breadth of LaunchPad Lab's AI capabilities:

1. **Agentforce dominates the page.** The Salesforce "Agentforce Quick Start Program" is featured prominently — often above the fold or as the first callout in the AI section. For Margaret, whose brokerage doesn't use Salesforce, this immediately signals: "This isn't for me."

2. **Related content reinforces the coupling.** Blog posts, webinar links, and downloadable resources in the AI section reference Salesforce-specific topics: "Agentforce best practices," "Salesforce AI implementation," etc. The content feed creates the impression that AI at LaunchPad Lab = Salesforce AI.

3. **Platform-agnostic work is buried or invisible.** LaunchPad Lab has delivered AI projects using OpenAI API, Microsoft Azure AI, custom ML pipelines, and direct database integrations (e.g., the healthcare case study using OpenAI API + MS SQL Server). But none of this technology diversity is visible on the AI page. You have to read individual case studies in detail to discover it.

4. **Homepage footer reinforces the impression.** Salesforce partnership badges or Agentforce mentions in the footer create a site-wide "Salesforce shop" signal that colors the visitor's perception of every page.

5. **The competitive implication is significant.** Margaret's brokerage uses Applied Epic (an insurance-specific platform), Microsoft SQL Server, and various legacy systems. If she believes LaunchPad Lab only does Salesforce AI, she'll move on to a competitor — even though LaunchPad Lab could absolutely build AI solutions for her stack.

### Margaret's Internal Monologue

> "I see Salesforce everywhere on their AI page. We don't use Salesforce — we use Applied Epic and a bunch of Microsoft tools. I don't think they can help us. Let me look at [competitor] instead."

This happens within 15-30 seconds of landing on the AI page. The opportunity is lost before LaunchPad Lab's actual capabilities are even discovered.

---

## Acceptance Criteria

### A. Platform-Agnostic Positioning
- [ ] The AI Automation page includes an explicit statement that AI solutions work with any technology stack — positioned above or alongside the Agentforce content (not below it)
- [ ] The statement is plain language: e.g., "Our AI solutions integrate with your existing systems — Salesforce, Microsoft, custom databases, or legacy platforms"
- [ ] At least one non-Salesforce AI case study or example is featured with equal visual prominence to the Agentforce Quick Start

### B. Clear Delineation of Salesforce vs. General AI
- [ ] Salesforce/Agentforce content is grouped under a clearly labeled section (e.g., "For Salesforce Customers" or "Salesforce Agentforce Quick Start") so visitors can identify it as one offering among many
- [ ] General AI capabilities are presented in their own section (e.g., "AI for Any Platform") that precedes or sits alongside the Salesforce section
- [ ] The page structure makes it clear that Salesforce AI is a subset of capabilities, not the entirety

### C. Technology Diversity Showcase
- [ ] The AI page displays a "Technology Partners" or "We Work With" section showing logos/names of platforms beyond Salesforce: OpenAI, Microsoft Azure AI, AWS AI/ML, Google Cloud AI, custom/open-source frameworks
- [ ] At least 2-3 case study references on the AI page highlight non-Salesforce technology stacks
- [ ] Case study cards or references include a "Technology" tag showing the stack used (e.g., "OpenAI API + MS SQL Server," "Azure Cognitive Services," "Custom ML pipeline")

### D. Related Content Balance
- [ ] The blog posts, webinars, or resources surfaced on the AI page include at least equal representation of non-Salesforce AI topics
- [ ] If a content feed is algorithm-driven, ensure the algorithm doesn't over-index on Salesforce content
- [ ] Resource titles avoid implying Salesforce exclusivity (e.g., "How to Get Started with AI" instead of "How to Get Started with Agentforce")

### E. Footer and Site-Wide Signals
- [ ] Salesforce partnership badges in the footer are balanced with other technology partner logos or a general "Technology Partners" link
- [ ] The footer does not create the impression that the company is exclusively a Salesforce consultancy

---

## How to Test

### First-Impression Test
1. Navigate to the AI Automation page
2. Without scrolling past the first viewport, note the technology brands visible
3. **Pass criteria:** At least one non-Salesforce technology or a "platform-agnostic" statement is visible above the fold
4. **Fail criteria:** Only Salesforce/Agentforce branding is visible above the fold

### Content Ratio Audit
1. On the AI Automation page, count the number of content blocks (sections, callouts, blog links, CTAs) that reference Salesforce or Agentforce
2. Count the number of content blocks that reference non-Salesforce AI capabilities
3. **Pass criteria:** Non-Salesforce AI content represents at least 50% of the page's AI content
4. **Fail criteria:** Salesforce content exceeds 60% of total AI content blocks

### User Perception Test
1. Show the AI Automation page to 3-5 people unfamiliar with LaunchPad Lab
2. After 30 seconds of browsing, ask: "What technology platforms does this company work with for AI?"
3. **Pass criteria:** At least 3 of 5 mention multiple platforms or describe the company as "platform-agnostic"
4. **Fail criteria:** Majority say "Salesforce" or "Agentforce" exclusively

### Case Study Technology Visibility
1. On the AI page, review all case study references or cards
2. Verify at least one non-Salesforce case study is featured
3. Verify case study cards include a visible technology tag

### Keyboard and Screen Reader Test
1. Navigate the AI page using keyboard only
2. Tab through the page — verify Salesforce and non-Salesforce sections are equally reachable
3. Use a screen reader: listen to the page headings (VoiceOver rotor > Headings). Verify both "Salesforce/Agentforce" and "Platform-Agnostic AI" (or equivalent) headings are present
4. Verify heading hierarchy makes the relationship clear: Salesforce AI is a subsection, not the primary topic

### Footer Audit
1. Scroll to the site footer on any page
2. Note the technology/partner logos displayed
3. **Pass criteria:** Multiple technology partners visible, or no single-vendor dominance
4. **Fail criteria:** Only Salesforce badges visible

---

## Developer Notes

### Approach: Restructure the AI Page into Platform Sections

The core fix is restructuring the AI Automation page to lead with platform-agnostic capabilities and then present Salesforce as one of several implementation paths.

### HTML: Page Structure with Clear Delineation

```html
<main>
  <!-- Hero: Platform-agnostic AI messaging -->
  <section class="ai-hero" aria-labelledby="ai-hero-heading">
    <h1 id="ai-hero-heading">AI Solutions That Work With Your Stack</h1>
    <p class="ai-hero__lead">
      We build AI-powered features that integrate with your existing
      systems — whether you're on Salesforce, Microsoft, AWS, or a
      custom platform. No lock-in. No rip-and-replace.
    </p>
    <a href="/contact/" class="btn btn--primary">
      Discuss your AI project
    </a>
  </section>

  <!-- Technology partners bar -->
  <section class="tech-partners" aria-label="Technology platforms we work with">
    <h2 class="tech-partners__heading">We Build AI With</h2>
    <div class="tech-partners__grid">
      <figure class="tech-partner">
        <img src="/images/logos/openai.svg" alt="" width="120" height="40"
             loading="lazy" />
        <figcaption>OpenAI</figcaption>
      </figure>
      <figure class="tech-partner">
        <img src="/images/logos/salesforce.svg" alt="" width="120" height="40"
             loading="lazy" />
        <figcaption>Salesforce</figcaption>
      </figure>
      <figure class="tech-partner">
        <img src="/images/logos/azure-ai.svg" alt="" width="120" height="40"
             loading="lazy" />
        <figcaption>Microsoft Azure AI</figcaption>
      </figure>
      <figure class="tech-partner">
        <img src="/images/logos/aws.svg" alt="" width="120" height="40"
             loading="lazy" />
        <figcaption>AWS AI/ML</figcaption>
      </figure>
      <figure class="tech-partner">
        <img src="/images/logos/google-cloud.svg" alt="" width="120"
             height="40" loading="lazy" />
        <figcaption>Google Cloud AI</figcaption>
      </figure>
      <figure class="tech-partner">
        <img src="/images/logos/huggingface.svg" alt="" width="120"
             height="40" loading="lazy" />
        <figcaption>Hugging Face</figcaption>
      </figure>
    </div>
  </section>

  <!-- General AI capabilities -->
  <section class="ai-capabilities" aria-labelledby="ai-cap-heading">
    <h2 id="ai-cap-heading">What We Build</h2>
    <p>
      Platform-agnostic AI capabilities that plug into your existing
      workflows and data.
    </p>
    <div class="ai-capabilities__grid">
      <article class="ai-cap-card">
        <h3>Intelligent Document Processing</h3>
        <p>
          Extract structured data from PDFs, emails, and forms using
          OCR + LLMs. Integrates with any database or document
          management system.
        </p>
        <span class="tech-tag">OpenAI · Azure AI · Custom</span>
      </article>
      <article class="ai-cap-card">
        <h3>Conversational AI Agents</h3>
        <p>
          AI-powered assistants that answer customer questions, route
          inquiries, and handle routine tasks — deployed on your
          website, in your app, or within tools like Slack and Teams.
        </p>
        <span class="tech-tag">OpenAI · Salesforce · Custom</span>
      </article>
      <article class="ai-cap-card">
        <h3>Predictive Analytics</h3>
        <p>
          Machine learning models that forecast trends, identify risks,
          and inform decisions — built on your data, in your
          environment.
        </p>
        <span class="tech-tag">Python · AWS SageMaker · Azure ML</span>
      </article>
      <article class="ai-cap-card">
        <h3>Workflow Automation</h3>
        <p>
          AI-driven automation for repetitive business processes:
          data entry, report generation, email triage, and more.
        </p>
        <span class="tech-tag">Any platform · API-based</span>
      </article>
    </div>
  </section>

  <!-- Case studies showing technology diversity -->
  <section class="ai-proof" aria-labelledby="ai-proof-heading">
    <h2 id="ai-proof-heading">AI in Action</h2>
    <div class="ai-proof__grid">
      <article class="case-card">
        <span class="case-card__tag case-card__tag--healthcare">
          Healthcare
        </span>
        <h3>Healthcare Insurance Platform</h3>
        <p>
          AI-powered claims intake that reduced manual data entry by
          60% using document parsing and structured extraction.
        </p>
        <div class="case-card__tech">
          <span class="tech-chip">OpenAI API</span>
          <span class="tech-chip">MS SQL Server</span>
          <span class="tech-chip">React</span>
        </div>
        <a href="/work/healthcare-insurance-platform/">
          Read the case study
          <span aria-hidden="true">→</span>
        </a>
      </article>

      <article class="case-card">
        <span class="case-card__tag case-card__tag--finance">
          Financial Services
        </span>
        <h3>Wealth Management AI Assistant</h3>
        <p>
          Conversational AI agent helping advisors research market
          data and generate client reports in seconds.
        </p>
        <div class="case-card__tech">
          <span class="tech-chip">Azure OpenAI</span>
          <span class="tech-chip">Python</span>
          <span class="tech-chip">.NET</span>
        </div>
        <a href="/work/wealth-management-ai/">
          Read the case study
          <span aria-hidden="true">→</span>
        </a>
      </article>

      <article class="case-card">
        <span class="case-card__tag case-card__tag--salesforce">
          Salesforce
        </span>
        <h3>Agentforce Quick Start</h3>
        <p>
          Deploy Salesforce's AI agents in weeks — configured,
          customized, and integrated with your Salesforce org.
        </p>
        <div class="case-card__tech">
          <span class="tech-chip">Salesforce</span>
          <span class="tech-chip">Agentforce</span>
          <span class="tech-chip">Apex</span>
        </div>
        <a href="/services/agentforce-quick-start/">
          Learn about Agentforce Quick Start
          <span aria-hidden="true">→</span>
        </a>
      </article>
    </div>
  </section>

  <!-- Explicit platform-agnostic statement -->
  <section class="ai-commitment" aria-labelledby="ai-commit-heading">
    <h2 id="ai-commit-heading">Your Stack. Our AI Engineering.</h2>
    <p>
      We don't require you to adopt a specific platform. Our AI
      solutions integrate with the tools you already use:
    </p>
    <ul class="platform-list">
      <li><strong>CRM:</strong> Salesforce, HubSpot, Microsoft Dynamics, or custom CRM</li>
      <li><strong>Databases:</strong> SQL Server, PostgreSQL, MongoDB, Snowflake, or legacy systems</li>
      <li><strong>Cloud:</strong> AWS, Azure, Google Cloud, or on-premises</li>
      <li><strong>Industry tools:</strong> Applied Epic, Guidewire, Duck Creek, or other domain-specific platforms</li>
      <li><strong>Communication:</strong> Slack, Microsoft Teams, email, or custom portals</li>
    </ul>
    <p>
      <a href="/contact/">Tell us about your current technology stack</a>
      — we'll show you what's possible.
    </p>
  </section>
</main>
```

### CSS: Technology Tags and Platform Section

```css
/* Technology partner bar */
.tech-partners {
  padding: 3rem 1.5rem;
  background-color: #f9fafb;
  text-align: center;
}

.tech-partners__heading {
  font-size: 0.8125rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: #9ca3af;
  margin-bottom: 2rem;
}

.tech-partners__grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  gap: 2rem 3rem;
  max-width: 960px;
  margin: 0 auto;
}

.tech-partner {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  margin: 0;
}

.tech-partner img {
  height: 2rem;
  width: auto;
  object-fit: contain;
  filter: grayscale(100%);
  opacity: 0.5;
  transition: opacity 0.2s ease, filter 0.2s ease;
}

.tech-partner:hover img {
  filter: grayscale(0%);
  opacity: 1;
}

.tech-partner figcaption {
  font-size: 0.75rem;
  font-weight: 500;
  color: #9ca3af;
}

/* Technology chips on case study cards */
.case-card__tech {
  display: flex;
  flex-wrap: wrap;
  gap: 0.375rem;
  margin: 1rem 0;
}

.tech-chip {
  display: inline-block;
  padding: 0.1875rem 0.625rem;
  font-size: 0.6875rem;
  font-weight: 600;
  color: #4b5563;
  background-color: #f3f4f6;
  border-radius: 999px;
  white-space: nowrap;
}

/* Case card tag colors by category */
.case-card__tag {
  display: inline-block;
  padding: 0.1875rem 0.625rem;
  font-size: 0.6875rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.04em;
  border-radius: 999px;
  margin-bottom: 0.75rem;
}

.case-card__tag--healthcare {
  color: #065f46;
  background-color: #d1fae5;
}

.case-card__tag--finance {
  color: #1e40af;
  background-color: #dbeafe;
}

.case-card__tag--salesforce {
  color: #0c4a6e;
  background-color: #e0f2fe;
}

/* Platform-agnostic commitment section */
.ai-commitment {
  padding: 3rem 1.5rem;
  max-width: 720px;
  margin: 0 auto;
}

.ai-commitment h2 {
  font-size: clamp(1.5rem, 3.5vw, 2rem);
  font-weight: 700;
  margin-bottom: 1rem;
}

.platform-list {
  padding-left: 1.25rem;
  margin: 1.5rem 0;
}

.platform-list li {
  font-size: 1rem;
  line-height: 1.8;
  color: #374151;
  margin-bottom: 0.5rem;
}

.platform-list li strong {
  color: #111827;
}

/* AI capabilities grid */
.ai-capabilities__grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1.5rem;
  margin-top: 2rem;
}

.ai-cap-card {
  padding: 1.5rem;
  background: #ffffff;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
}

.ai-cap-card h3 {
  font-size: 1.0625rem;
  font-weight: 700;
  color: #111827;
  margin-bottom: 0.5rem;
}

.ai-cap-card p {
  font-size: 0.9375rem;
  line-height: 1.6;
  color: #4b5563;
  margin-bottom: 0.75rem;
}

.tech-tag {
  font-size: 0.75rem;
  font-weight: 500;
  color: #9ca3af;
}
```

### Footer Rebalancing

```html
<!-- Current footer (approximate): Salesforce-only badge -->
<!-- Replace with a balanced partner section -->
<footer class="site-footer">
  <div class="footer__partners">
    <h3 class="footer__partners-heading">Technology Partners</h3>
    <div class="footer__partner-logos">
      <img src="/images/logos/salesforce-partner.svg"
           alt="Salesforce Consulting Partner" width="100" height="32" />
      <img src="/images/logos/aws-partner.svg"
           alt="AWS Partner" width="100" height="32" />
      <img src="/images/logos/microsoft-partner.svg"
           alt="Microsoft Partner" width="100" height="32" />
      <img src="/images/logos/clutch-badge.svg"
           alt="Clutch Top Developer 2024" width="100" height="32" />
    </div>
  </div>
</footer>
```

```css
.footer__partners {
  padding: 2rem 0;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
}

.footer__partners-heading {
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: rgba(255, 255, 255, 0.5);
  margin-bottom: 1rem;
}

.footer__partner-logos {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 2rem;
}

.footer__partner-logos img {
  height: 1.5rem;
  width: auto;
  opacity: 0.6;
  filter: brightness(0) invert(1);
  transition: opacity 0.2s ease;
}

.footer__partner-logos img:hover {
  opacity: 1;
}
```

### Content Strategy: Related Content Balance

If the AI page uses a CMS-driven content feed (blog posts, webinars), add content category filtering:

```javascript
// Ensure the related content feed doesn't over-index on Salesforce
function balanceContentFeed(articles) {
  const salesforceArticles = articles.filter(a =>
    a.tags.some(t => ['salesforce', 'agentforce'].includes(t.toLowerCase()))
  );
  const generalArticles = articles.filter(a =>
    !a.tags.some(t => ['salesforce', 'agentforce'].includes(t.toLowerCase()))
  );

  const balanced = [];
  const maxSalesforce = Math.ceil(articles.length * 0.4);

  balanced.push(...generalArticles);
  balanced.push(...salesforceArticles.slice(0, maxSalesforce));

  return balanced
    .sort((a, b) => new Date(b.publishedAt) - new Date(a.publishedAt))
    .slice(0, 6);
}
```

### Components to Audit

| Component | Page | What to Change |
|---|---|---|
| AI hero section | AI Automation page | Add "works with your stack" messaging; reduce Agentforce dominance |
| Agentforce callout | AI Automation page | Move into a labeled subsection ("For Salesforce Customers") |
| Technology partner bar | AI Automation page | Add multi-vendor logo bar: OpenAI, Azure, AWS, Google Cloud, etc. |
| Case study cards on AI page | AI Automation page | Add technology tags showing stack diversity |
| Related content feed | AI Automation page | Balance Salesforce vs. non-Salesforce article ratio |
| Footer partner badges | All pages | Add badges for non-Salesforce partnerships |
| CMS content model | Backend | Add "technology_stack" tags to case studies and blog posts |
| AI capabilities section | AI Automation page | Lead with platform-agnostic capabilities before platform-specific offerings |

---

## Examples from Other Sites

### Thoughtbot (thoughtbot.com)
Thoughtbot works heavily with Rails but doesn't let their site suggest they're a "Rails shop." Their services page leads with "Design, develop, and grow your product" — the technology is mentioned as a capability, not a constraint. They list multiple technology competencies (Rails, React Native, Elixir, etc.) with equal visual weight.

### Slalom (slalom.com)
Slalom is a major Salesforce partner but their AI/technology pages carefully balance Salesforce with other platforms. Their AI services page lists "Salesforce," "AWS," "Microsoft," "Google Cloud," and "custom solutions" as parallel options. Salesforce has its own dedicated section, clearly labeled — it doesn't bleed into the general AI narrative.

### Deloitte Digital
Deloitte is a Salesforce Platinum Partner but their digital services pages present Salesforce as one of many platforms. Their AI pages lead with industry problems, not vendor names. Technology choices are presented as implementation details, not defining characteristics.

### Accenture (accenture.com/ai)
Accenture's AI page leads with capabilities ("Generative AI," "Responsible AI," "AI Strategy") and then mentions technology partners (Google, AWS, Microsoft, Salesforce) as implementation paths. The messaging is: "We solve your problem using the best-fit technology" — not "We sell this vendor's product."

### Key Patterns
1. **Lead with problems, not platforms** — The AI page should first describe what AI can do for the visitor, then mention which platforms enable it
2. **Label vendor-specific content** — Salesforce content is fine, but it should be in a clearly labeled section, not the page default
3. **Show technology breadth** — A logo bar or chip set showing 4-6 technology platforms immediately signals "platform-agnostic"
4. **Case studies carry tech tags** — Every case study reference includes the technology stack used, so visitors can see diversity
5. **Footer balance** — Multiple partner badges, not just one vendor
