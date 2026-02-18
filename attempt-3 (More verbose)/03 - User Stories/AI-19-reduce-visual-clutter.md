# AI-19: Reduce Visual Clutter

## Metadata
- **ID:** AI-19
- **Priority:** 3 Medium
- **Personas Affected:** 3+ of 16 personas (ADHD, cognitive disability, senior)
- **WCAG Criteria:** Best practice (cognitive accessibility)
- **Effort:** Medium (4–8 hours)

---

## User Story

**As a** user with ADHD, cognitive disability, or who is easily overwhelmed by too many choices,

**I want** the page to show fewer logos, badges, and CTAs per viewport, with more whitespace and a clearer focus,

**So that** I can make decisions without feeling paralyzed by too many competing elements.

---

## Acceptance Criteria

- [ ] Maximum 4–6 logos visible per viewport in partner/client sections
- [ ] Maximum 2–3 badges/awards visible per viewport
- [ ] Maximum 1–2 CTAs per viewport (1 primary, 1 secondary optional)
- [ ] Increased whitespace between sections
- [ ] "View all" or "See more" links for overflow content (progressive disclosure)
- [ ] Primary CTA is visually dominant; secondary is subdued (outline/text)
- [ ] Content containers have max-width for readable, comfortable layout
- [ ] ADHD tester feedback: "Does not feel overwhelming"

---

## Test Plan

### Logo Count
1. Open `https://launchpadlab.com/` and scroll through homepage
2. In each viewport, count visible client/partner logos
3. **Expected:** Max 6 logos per viewport
4. If more: add "View all partners" link and show subset

### Badge Count
1. Count visible awards/certifications/badges in each viewport
2. **Expected:** Max 3 badges visible
3. Additional badges: "See all awards" link or dedicated page

### CTA Count
1. In each viewport, count call-to-action buttons/links
2. **Expected:** Max 2 CTAs (1 primary, 1 secondary)
3. **Expected:** Primary is full color; secondary is outline or text style
4. Reduce or consolidate if more than 2

### Whitespace
1. Measure padding between sections (e.g., py-16 vs py-24)
2. **Expected:** Generous spacing; no cramped sections
3. Content max-width: comfortable reading (e.g., 65ch for text, 1200px for layout)

### User Testing
1. Ask ADHD tester (or simulate): "Does this feel overwhelming?"
2. **Expected:** No — clear hierarchy, limited choices, breathing room
3. Ask: "Can you identify the main action you should take?"
4. **Expected:** Yes — primary CTA is obvious

---

## Developer Notes

### Logo Section
- Show 4–6 representative logos
- Add "View all partners" or "See our clients" link
- Use carousel or grid with pagination for overflow
- Avoid "wall of logos" — curate for impact

### Badge Section
- Display top 3 awards/certifications
- Add "See all awards" link or dedicated Awards page
- Consider rotating badges if many exist

### CTA Strategy
- **Primary:** Full color button, one per viewport (e.g., "Get in touch")
- **Secondary:** Outline or text link (e.g., "Learn more")
- Avoid: 3+ buttons competing for attention
- Use visual weight: primary = bold, secondary = lighter

### Section Padding
```css
section {
  padding-top: 6rem;   /* 96px - was py-16 = 4rem */
  padding-bottom: 6rem;
}
/* Or use utility: py-24 */
```

### Content Max-Width
```css
.content-container {
  max-width: 1200px;
  margin: 0 auto;
}
.text-content {
  max-width: 65ch; /* readable line length */
}
```

### Progressive Disclosure
- "View all partners" → expands or navigates to full list
- "See all awards" → dedicated page or expandable section
- Reduces initial cognitive load

### Components to Audit (LaunchPad Lab)
- [ ] Client/partner logo section
- [ ] Awards/badges section
- [ ] Hero CTA area
- [ ] Mid-page CTAs
- [ ] Footer CTA
- [ ] Section spacing (padding/margin)

### Visual Hierarchy
- One primary focus per section
- Use size, color, and position to establish hierarchy
- Whitespace = emphasis — don't fill every pixel

---

## Examples

| Site | Approach |
|------|----------|
| **Linear.app** | Minimal; focused sections; one CTA per area; clean hierarchy |
| **Basecamp.com** | One CTA per section; no logo walls; simple layout |
| **Notion.com** | Clean visual hierarchy; limited elements per viewport; breathing room |
