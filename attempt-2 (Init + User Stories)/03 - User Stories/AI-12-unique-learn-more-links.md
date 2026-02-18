# AI-12: Unique Learn More Links

## User Story

As a **screen reader or voice control user**, I want **all "Learn More" links to have unique, descriptive visible text**, so that **I can distinguish between links and navigate to the correct destination without confusion**.

## Acceptance Criteria

- [ ] Each "Learn More" link has unique text (e.g., "Learn more about AI Automation")
- [ ] Screen reader links list shows distinct text for each link
- [ ] Voice control user can say "click Learn more about [Service Name]" and the correct link activates
- [ ] Visible text is descriptive and indicates the destination or purpose
- [ ] No two links share identical visible text when they point to different destinations

## How to Test

1. **Screen reader test:** Use NVDA, JAWS, or VoiceOver
   - Navigate to the links list (e.g., NVDA: Insert+F7)
   - Verify each link has unique, descriptive text
   - No duplicate "Learn more" entries without context

2. **Voice control test:** Use Voice Control (macOS) or Voice Access (Windows)
   - Say "click Learn more about AI Automation" → correct service link activates
   - Say "click Learn more about [other service]" → correct link activates
   - Each service card link should be uniquely identifiable by voice

3. **Visual test:** Each link should display unique visible text (not just "Learn more")

## Developer Notes

- Change visible link text to **"Learn more about [Service Name]"** for each service card
- Example: "Learn more about AI Automation", "Learn more about Custom Software", etc.
- Ensure visible text matches or is contained in `aria-label` if used
- **Do NOT rely on `aria-label` alone** — visible text must be unique for voice control users
- Voice control activates links by their visible text; `aria-label` is not always used

## WCAG References

- **2.4.4 Link Purpose (In Context) (Level A):** The purpose of each link can be determined from the link text alone or from the link text together with its programmatically determined link context.
- **2.5.3 Label in Name (Level A):** For user interface components with labels that include text or images of text, the name contains the text that is presented visually.

## Priority & Effort

| Priority | Effort Estimate |
|----------|-----------------|
| P2 High | Small (1–2h) |
