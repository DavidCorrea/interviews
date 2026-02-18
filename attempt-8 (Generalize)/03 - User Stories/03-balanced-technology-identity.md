# User Story: Balanced Technology Identity Beyond Salesforce

**Priority:** Medium  
**Related Finding:** [Finding 3](../main-report.md#3-salesforce-branding-overrepresentation)

## Story
As a potential client who doesn't need Salesforce, I want the agency's brand to represent its full range of technology capabilities, so that I don't incorrectly assume this is primarily a Salesforce consultancy.

## Context
Salesforce branding permeates the entire site — footer badge, dedicated service pages, Agentforce mentions on the AI page, Clutch badges highlighting Salesforce, and the Technologies page leading with Salesforce products. For users who don't need Salesforce (most startup founders, consumer product builders), this creates the impression that the agency is primarily a Salesforce shop — even though they offer much broader services.

## Acceptance Criteria
- Non-Salesforce technologies and capabilities receive equal visual weight on the Technologies page
- The footer Salesforce badge is balanced with other technology/partnership badges (if available)
- The AI Automation page presents agentic AI as a broader capability, not exclusively via Salesforce Agentforce
- Homepage service cards don't disproportionately emphasize Salesforce

## How to Test
1. Navigate to the Technologies page — confirm Salesforce does not occupy more than 30% of the visual space
2. Check the AI Automation page — confirm agentic AI is framed as a general capability, not just Agentforce
3. Review the footer — confirm Salesforce badge is not the only technology badge displayed
4. Ask a non-technical person to skim the homepage and identify what the company does — "Salesforce" should not be their first answer

## Developer Notes

### General Approach
Restructure the Technologies page to lead with broader capability categories (AI, Web, Mobile) before platform-specific sections. Reduce the visual weight of Salesforce-specific content relative to other technologies.

### Components to Audit
- Technologies page layout and section ordering
- Footer partner badges section
- AI Automation page — Agentforce vs. general agentic AI sections
- Homepage service cards ordering

### Code Examples
```jsx
// Technologies page: lead with capability categories, not vendor products
<section className="tech-categories">
  <h2>Our Technology Expertise</h2>
  <div className="category-grid">
    <TechCategory title="Artificial Intelligence" items={["OpenAI", "LangChain", "Custom ML", "Agentforce"]} />
    <TechCategory title="Web Development" items={["React", "Next.js", "Ruby on Rails", "Node.js"]} />
    <TechCategory title="Mobile" items={["React Native", "Ionic", "Flutter"]} />
    <TechCategory title="Cloud & Infrastructure" items={["Heroku", "AWS", "Vercel"]} />
    <TechCategory title="CRM & Business Systems" items={["Salesforce", "HubSpot"]} />
  </div>
</section>
```

## How Other Sites Achieve This
- **Slalom** (slalom.com) — Salesforce partner but presents services by capability (AI, Cloud, Design) first, with Salesforce as one of many platforms under each
- **Accenture** — partners with Salesforce, AWS, Google, etc., and gives equal visual treatment to all partnerships
- **Pivotal Labs** (now VMware Tanzu) — tech-agnostic framing with capability-first messaging
