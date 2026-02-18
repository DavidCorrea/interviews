# Salesforce Dependency Unclear

## Priority
**High**

## User Story
As a potential client evaluating AI services, I want to understand whether LaunchPad Lab's AI capabilities work with my technology stack (Salesforce or otherwise), so that I can assess fit before engaging.

## Acceptance Criteria

- [ ] AI Automation page clearly distinguishes Salesforce-specific services from platform-agnostic AI capabilities
- [ ] Users can determine if AI services require Salesforce or work with other stacks
- [ ] A clear statement exists (e.g., "Our AI services work with any technology stack, including Salesforce Agentforce")
- [ ] URL structure or page organization reflects the distinction (e.g., separate pages or clearly labeled sections)
- [ ] No user confusion about whether AI services are Salesforce-only
- [ ] Content is accurate and not misleading about partnerships vs. general capabilities

## How to Test

1. Navigate to the AI Automation page (e.g., `/services/ai-automation-agentforce/`).
2. Read the page content and note references to Salesforce, Agentforce, and generic AI.
3. Determine: Is it clear that AI services can work outside Salesforce?
4. Search the page for phrases like "platform-agnostic," "any stack," "Salesforce and other platforms."
5. Check if there are separate sections or pages for Salesforce vs. general AI.
6. Ask a colleague unfamiliar with the site: "Can I use LaunchPad Lab's AI services if I don't use Salesforce?" — Note their answer.
7. Verify the statement about technology stack compatibility is prominent and accurate.

## Developer Notes

### General Explanation
The AI Automation page heavily features Salesforce Agentforce branding and the URL includes "agentforce." This creates ambiguity: Are AI services only for Salesforce customers? Do they work with other platforms? Unclear positioning can lose non-Salesforce prospects and frustrate those seeking clarity.

**Solution:** Clearly separate Salesforce-specific AI services from platform-agnostic AI capabilities. Options: (1) Add a prominent statement that AI services work with any stack, including Salesforce; (2) Create separate sections or pages for "Salesforce AI" vs. "General AI"; (3) Reorganize content so the relationship is explicit.

### Code Examples

**Content structure — Add clarifying statement:**
```html
<section aria-labelledby="ai-capabilities-heading">
  <h2 id="ai-capabilities-heading">AI Capabilities</h2>
  <p>
    Our AI services work with any technology stack. We have deep expertise in
    Salesforce Agentforce and other enterprise platforms, but we're not limited
    to them.
  </p>
  <h3>Salesforce Agentforce</h3>
  <p>For Salesforce customers, we offer...</p>
  <h3>Platform-Agnostic AI</h3>
  <p>We also build custom AI solutions for...</p>
</section>
```

**Page structure — Separate sections:**
```html
<main>
  <h1>AI Automation</h1>
  <p class="lead">
    We help organizations automate with AI — whether you use Salesforce,
    custom systems, or other platforms.
  </p>
  <section>
    <h2>Salesforce Agentforce</h2>
    <p>Specialized AI solutions for the Salesforce ecosystem...</p>
  </section>
  <section>
    <h2>Custom AI Solutions</h2>
    <p>Platform-agnostic AI development for any stack...</p>
  </section>
</main>
```

**Consider separate routes:**
- `/services/ai-automation/` — General AI capabilities
- `/services/ai-automation-agentforce/` — Salesforce-specific (or `/services/salesforce-ai/`)

### Components to Audit
- AI Automation page template
- Services navigation and routing
- Any shared "AI" or "Automation" content blocks
- Partner/technology logos section (ensure messaging aligns)

## Examples from Other Sites

- **Accenture.com** — Separates platform-specific services (e.g., Salesforce, SAP) from general consulting and technology capabilities. Clear labeling of partnerships vs. broad offerings.
- **Deloitte.com** — Clear labeling of technology partnerships (e.g., "Salesforce practice") alongside general AI and digital transformation services. Users can distinguish between partnership-specific and general capabilities.
