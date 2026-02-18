# Reframe AI Autonomy Messaging to Emphasize Human Oversight

## Priority: Medium

## User Story
As a risk-averse business executive, I want the AI service descriptions to clearly emphasize human oversight and governance controls so that I feel confident the AI won't make unsupervised decisions that could harm my business.

## Acceptance Criteria
- [ ] AI Automation page content leads with human oversight and governance before describing automation capabilities
- [ ] A "Governance & Control" section or callout box is present and visible on the AI Automation page
- [ ] Copy uses phrases such as "human-in-the-loop," "supervised automation," or "you stay in control"
- [ ] Homepage AI service cards (if present) reflect the same governance-first messaging
- [ ] No language suggests AI acts independently without human approval or escalation paths
- [ ] Messaging reassures risk-averse readers that humans remain in control of critical decisions

## Developer Notes

### General Explanation
The AI Automation page currently describes "autonomous AI agents" that "act independently." For non-technical business executives, this framing raises concerns about AI making decisions without human oversight. While the description mentions "escalating when needed," the emphasis on autonomy over governance may deter risk-averse prospects.

**Approach:**
1. **Rewrite copy** — Lead with human oversight, then describe automation. Open with governance and control, then explain how AI augments (not replaces) human decision-making.
2. **Add a Governance & Control section** — Dedicated section or callout that explicitly addresses: human approval workflows, escalation paths, audit trails, and configurable guardrails.
3. **Use reassuring phrases** — "human-in-the-loop," "supervised automation," "you stay in control," "AI assists—humans decide," "built-in escalation and approval workflows."
4. **Audit all AI-related pages** — Ensure consistency across homepage cards, service pages, and any page describing AI agents.

### Code Examples

**Governance callout component (semantic HTML):**
```html
<aside class="governance-callout" aria-labelledby="governance-heading">
  <h2 id="governance-heading">Governance & Control</h2>
  <p>Our AI solutions are built with human-in-the-loop design. You stay in control—AI assists with execution, but critical decisions require your approval. Built-in escalation workflows ensure nothing moves forward without your oversight.</p>
  <ul>
    <li>Human approval for high-impact actions</li>
    <li>Configurable guardrails and thresholds</li>
    <li>Full audit trails for compliance</li>
  </ul>
</aside>
```

**Before/after copy example:**
```text
BEFORE: "Autonomous AI agents act independently to streamline workflows, escalating when needed."
AFTER:  "AI agents work under your supervision—streamlining workflows while you stay in control. Human approval is required for critical actions, with built-in escalation when AI needs your input."
```

### Components to Audit
- AI Automation page (primary)
- Homepage AI service cards
- Any page describing AI agents or automation capabilities
- Navigation or marketing copy that references "autonomous" or "independent" AI

## Examples From Other Sites
- **Microsoft Copilot** — Frames AI as an assistant that "augments" human work; emphasizes "you're always in control" and "AI suggestions you can review and edit." Marketing focuses on productivity gains with human oversight, not replacement.
- **Google Gemini for Business** — Highlights enterprise controls, admin policies, and data governance. Messaging stresses "built for organizations" with "administrative controls" and "audit logs"—governance before capability.
- **Salesforce Einstein** — Describes AI as "assisted intelligence" that "surfaces insights" and "recommends actions" while humans make final decisions. Uses "human-in-the-loop" and "trusted AI" as core messaging pillars.

## References
- Main Report Item 6 (Medium Priority)
- Website: https://launchpadlab.com/
- AI Automation page and related service descriptions
