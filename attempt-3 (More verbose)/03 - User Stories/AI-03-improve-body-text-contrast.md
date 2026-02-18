# AI-03: Improve Body Text Contrast

## Metadata
- **ID:** AI-03
- **Priority:** 1 Critical
- **Personas Affected:** 10 of 16 personas
- **WCAG Criteria:** 1.4.3 Contrast (Minimum) (AA), 1.4.6 Contrast (Enhanced) (AAA)
- **Effort:** Small (1–2 hours)

---

## User Story

**As a** visitor with low vision, aging eyes, or who reads in bright sunlight,

**I want** all body text on the LaunchPad Lab site to have sufficient contrast against its background,

**So that** I can read the content comfortably without straining or missing information.

---

## Acceptance Criteria

- [ ] All body text achieves at least 4.5:1 contrast ratio against its background (WCAG AA)
- [ ] Body text achieves 7:1 contrast ratio where possible (WCAG AAA)
- [ ] No body text uses a color lighter than #555 on white (#FFFFFF) background
- [ ] Paragraphs, labels, captions, footer text, and testimonial text meet contrast requirements
- [ ] Large text (≥18px normal or ≥14px bold) may use 3:1 minimum if design requires
- [ ] Placeholder text in form fields meets 3:1 minimum (4.5:1 preferred)
- [ ] Third-party embedded content (forms, widgets) is audited; document any that cannot be changed

---

## Test Plan

### Automated Testing
1. Install axe DevTools browser extension or use Lighthouse
2. Run axe on: Home, About, Services, Contact, and any other key pages
3. **Expected:** No contrast violations for text
4. Use WebAIM Contrast Checker (https://webaim.org/resources/contrastchecker/) on sampled text colors

### Manual Color Verification
1. Identify all text colors used for body copy (inspect with DevTools)
2. For each color, check contrast against its background:
   - #666 on #FFF → ~5.7:1 (passes AA, fails AAA)
   - #777 on #FFF → ~4.5:1 (barely passes AA)
   - #333 on #FFF → ~12.6:1 (passes AAA)
   - #555 on #FFF → ~7.5:1 (passes AAA)
3. **Target:** Use #333 or darker for body text on white

### Page-by-Page Audit
- [ ] Home: hero text, body paragraphs, captions, footer
- [ ] About: team bios, descriptions, quotes
- [ ] Services: service descriptions, feature lists
- [ ] Contact: labels, instructions, testimonials
- [ ] Blog/articles: article body, metadata, comments if present

### Edge Cases
- Text on colored backgrounds (e.g., dark sections) — ensure light text has sufficient contrast
- Hover/focus states — ensure contrast is maintained
- Disabled or placeholder text — document and fix where possible

---

## Developer Notes

### CSS Updates
If using design tokens or CSS variables:

```css
:root {
  --color-body-text: #333;      /* was #666 or #777 */
  --color-body-text-muted: #555; /* for secondary text, was #888 */
}
```

Global body/paragraph styles:

```css
body, p, .body-text, .testimonial-text {
  color: #333; /* or var(--color-body-text) */
}
```

### Audit Checklist
1. Search codebase for hex colors: `#666`, `#777`, `#888`, `#999`, `#aaa`
2. Replace with darker equivalents: `#333`, `#444`, `#555`
3. Check Sass/LESS variables, Tailwind config, or design system tokens
4. Verify `color` inheritance — ensure no child elements override with light gray

### Third-Party Content
- HubSpot forms, Calendly embeds, etc. may use their own styles
- Options: (a) override with CSS if possible, (b) request customization from vendor, (c) document as known limitation
- Use `!important` sparingly; prefer vendor customization if available

### Files to Modify
- Global CSS or design tokens file
- Component-specific styles (cards, testimonials, footer)
- Tailwind/PostCSS config if using utility classes

---

## Examples

| Site | Approach |
|------|----------|
| **Apple.com** | High-contrast body text; dark gray on white throughout |
| **GOV.UK** | #0B0C0C on white ≈ 19.4:1; strict contrast standards |
| **Medium.com** | Dark body text (#292929 or similar); readable in all lighting |
| **Stripe.com** | Dark gray body text; consistent contrast across marketing and docs |
