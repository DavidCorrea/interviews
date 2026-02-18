# AI-12: Make "Learn More" Links Unique and Descriptive

## Metadata
- **ID:** AI-12
- **Priority:** 2 High
- **Personas Affected:** 3+ of 16 personas
- **WCAG Criteria:** 2.4.4 Link Purpose (A), 2.5.3 Label in Name (A)
- **Effort:** Small (1–2 hours)

---

## User Story

**As a** screen reader user or someone using voice control,

**I want** each "Learn More" link to have unique, descriptive text that indicates its destination,

**So that** I can distinguish between links in a list, choose the correct one, and use voice commands like "Click Learn more about AI Automation" to activate the right link.

---

## Acceptance Criteria

- [ ] No two links on the same page share identical link text when they point to different destinations
- [ ] Each "Learn More" link has unique text: e.g., "Learn more about AI Automation," "Learn more about Web Development"
- [ ] If using `aria-label`, the visible text ("Learn More") must be contained within the aria-label per WCAG 2.5.3
- [ ] Case study "View project" links are similarly unique (e.g., "View [Project Name] project")
- [ ] Screen reader links list shows each link with distinct, meaningful text
- [ ] Voice control can target each link by its unique text

---

## Test Plan

### Screen Reader Links List
1. **NVDA (Windows):** Insert+F7 to open Elements List → Links
2. **VoiceOver (macOS):** VO+U for Rotor → Links
3. **JAWS:** Insert+F7 → Links
4. Navigate to `https://launchpadlab.com/` and open links list
5. **Expected:** Each "Learn More" appears as "Learn more about [Service Name]" — no duplicate "Learn More" entries
6. Same for "View project" — each should include project name

### Voice Control
1. Enable voice control (e.g., Windows Speech Recognition, macOS Voice Control)
2. Say "Click Learn more about AI Automation"
3. **Expected:** Correct link activates (AI Automation service)
4. Say "Click Learn more about Web Development"
5. **Expected:** Different link activates
6. If all links say "Learn More," voice control cannot distinguish — test fails

### Visual Verification
- Links should display descriptive text visibly where possible
- If design requires "Learn More" visible, ensure `aria-label` contains it: `aria-label="Learn more about AI Automation"` (not just "AI Automation")

### Automated Testing
- Run axe DevTools: **Expected:** No "Link purpose" or "Link name" violations
- Check for "Links with the same text go to different destinations" — resolve all

---

## Developer Notes

### Option A (Preferred): Change Visible Link Text
Replace generic "Learn More" with descriptive text:
```html
<!-- Before -->
<a href="/services/ai-automation">Learn More</a>

<!-- After -->
<a href="/services/ai-automation">Learn more about AI Automation</a>
```

### Option B: aria-label (If Design Requires "Learn More" Visible)
Per WCAG 2.5.3 Label in Name: the visible text must be a substring of the accessible name.
```html
<!-- Correct: "Learn More" is contained in "Learn more about AI Automation" -->
<a href="/services/ai-automation" aria-label="Learn more about AI Automation">Learn More</a>

<!-- Incorrect: "Learn More" not in "AI Automation" -->
<a href="/services/ai-automation" aria-label="AI Automation">Learn More</a>
```

### Service Links to Update (LaunchPad Lab)
- Learn more about AI Automation
- Learn more about Web Development
- Learn more about [each of 6 services — audit page for exact names]

### Case Study Links
```html
<!-- Before -->
<a href="/work/project-x">View project</a>

<!-- After -->
<a href="/work/project-x">View [Project Name] project</a>
```

### Files to Modify
- Services section template/component
- Case study cards
- Any reusable "Learn More" or "View project" link component

---

## Examples

| Site | Approach |
|------|----------|
| **Deloitte.com/services** | Unique link text per service; "Explore [Service Name]" |
| **IBM.com** | Descriptive links; no generic "Learn more" without context |
| **Microsoft.com/accessibility** | Each link describes destination; screen reader friendly |
