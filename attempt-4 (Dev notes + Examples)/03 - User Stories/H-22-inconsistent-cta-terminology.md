# H-22: Inconsistent CTA Terminology

**Issue ID:** H-22
**Priority:** High
**WCAG Criteria:** 3.2.4 Consistent Identification (AA)
**Affected Personas:** Cognitive Disability, Non-Native Speaker, Senior Person

---

## User Story

**As a** user with a cognitive disability,
**I want** call-to-action buttons that perform the same function to use the same wording across the site,
**so that** I can predict what each button does and navigate confidently without confusion.

---

## Acceptance Criteria

- [ ] All CTAs that lead to the contact page or contact form use a single, consistent label (e.g., "Contact Us" or "Get in Touch").
- [ ] All CTAs that link to a service detail page use a single, consistent label (e.g., "Learn More About [Service]").
- [ ] The chosen CTA labels are plain language and clearly communicate the action (avoid idioms like "Let's Build Something Great").
- [ ] No more than 2–3 distinct CTA label patterns are used site-wide, each for a clearly different action.
- [ ] The CTA terminology is documented in a content style guide or component library for future consistency.
- [ ] Non-native English speakers can understand the CTA labels without idiomatic knowledge.

---

## How to Test the Change

### Manual Testing

1. **Content audit:** Open every page in the site. List all CTA button/link text. Confirm that CTAs leading to the same destination use the same label.
2. **Screen reader link list:** Using NVDA or VoiceOver, open the links list (`Insert+F7` in NVDA or `VO+U` in VoiceOver). Verify that identically-purposed CTAs have identical text.
3. **Cognitive walkthrough:** Ask a user with limited English or cognitive differences to complete the task "contact the company." Measure hesitation or confusion when encountering CTAs.
4. **Cross-page comparison:** Open the homepage, services page, about page, and contact page side by side. Confirm the primary CTA text is identical across all.

### Automated Testing

```javascript
// Gather all CTA button/link text
const ctas = document.querySelectorAll('a.btn, a.cta, button.cta, .wp-block-button a');
const ctaTexts = [...ctas].map(el => el.textContent.trim());
const uniqueTexts = [...new Set(ctaTexts)];
console.log('Unique CTA labels:', uniqueTexts);
console.assert(uniqueTexts.length <= 4, `Too many CTA variations: ${uniqueTexts.length}`);
```

- Create a site-wide scrape that collects all CTA labels and flags any page where a "contact" CTA does not match the agreed standard label.

---

## Developer Notes

### General Approach

Audit all CTA buttons/links across the site and consolidate to a small, consistent set of labels. Map each action to a single phrase.

### Current State (Problem)

The site uses 5+ different labels for what is essentially the same action (contact/connect):

| Current CTA Text | Destination |
|---|---|
| "Connect with an Expert" | Contact page |
| "Let's Build Something Great" | Contact page |
| "Reach Out" | Contact page |
| "Let's Connect" | Contact page |
| "Let's Get Social" | Social links / Contact page |

### Recommended CTA Mapping

| Action | Standard Label | Notes |
|---|---|---|
| Navigate to contact form | **"Contact Us"** | Clear, universally understood, translatable |
| Learn more about a service | **"Learn More"** with `aria-label="Learn more about [Service]"` | Specific context via ARIA |
| View a case study | **"View Case Study: [Client Name]"** | Includes context |
| Follow on social | **"Follow Us on [Platform]"** | Names the action and destination |

### Implementation

```html
<!-- Primary CTA: always the same text for contact -->
<a href="/contact/" class="btn btn-primary">Contact Us</a>

<!-- Service CTA: consistent label + ARIA context -->
<a href="/services/ai-development/"
   class="btn btn-secondary"
   aria-label="Learn more about AI Development">
  Learn More
</a>

<!-- Case study CTA: includes client name -->
<a href="/case-studies/cameo/"
   class="btn btn-outline"
   aria-label="View case study: Cameo">
  View Case Study
</a>
```

### Components / Files to Audit

- All page templates and partials that render CTA buttons
- Hero sections across all pages
- Service card components
- Footer CTA sections
- Case study card components
- CMS/ACF fields that allow editors to customize CTA text (consider restricting to a dropdown)

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **Mailchimp** | Uses "Get Started" consistently for sign-up CTAs across every page | One phrase, one action — zero ambiguity. |
| **Slack** | "Try for Free" is the primary CTA everywhere; "Contact Sales" is the secondary | Two CTAs, clearly differentiated, always the same. |
| **Basecamp** | "Try Basecamp" on every page for the primary action | Repetition builds recognition and confidence. |
| **GOV.UK** | Design system mandates specific button labels for each action type | Governance ensures long-term consistency. |
