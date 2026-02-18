# L-63: Case Study Button Text Is Ambiguous

**Issue ID:** L-63
**Priority:** Low
**WCAG Criteria:** 2.4.4 Link Purpose (In Context) (A)
**Affected Personas:** Screen Reader, Voice Control

---

## User Story

As a **screen reader user** navigating the case study section, I want case study CTA buttons to include a clear action verb so that I can understand what will happen when I activate the link, rather than hearing only a company name with no indication of the action.

---

## Acceptance Criteria

- [ ] Every case study CTA button/link includes an action verb that describes what will happen (e.g., "Read Cameo Case Study," "View GoHealth Results," or "See the Cameo story").
- [ ] The visible button text alone makes the action clear — a user should not need surrounding context to understand the link purpose.
- [ ] If the visible button text must remain short (e.g., for design reasons), an `aria-label` provides the full descriptive text (e.g., `aria-label="Read the Cameo case study"`).
- [ ] Voice control users can activate the button by saying a phrase that matches the visible text (the `aria-label` must start with or include the visible text per WCAG 2.5.3).
- [ ] Screen readers announce the full link purpose, not just a company name.
- [ ] The pattern is consistent across all case study cards/carousel items site-wide.

---

## How to Test the Change

### Manual Testing
1. Navigate to the homepage or any page with case study cards/carousel.
2. Read the CTA button text on each case study card:
   - Confirm each includes an action verb (e.g., "Read," "View," "Explore") plus the company name.
3. Test with VoiceOver (macOS):
   - Press `VO + U` to open the **Links** rotor.
   - Find the case study links — confirm each has a descriptive label (not just a company name).
   - Activate one and confirm it navigates to the expected case study page.
4. Test with voice control (macOS Voice Control or Dragon):
   - Say "Click Read Cameo Case Study" (or the visible button text).
   - Confirm the correct button activates without a disambiguation dialog.
5. Tab through the case study section with keyboard only:
   - Confirm each button's accessible name (shown in DevTools > Accessibility tab) is descriptive.

### Automated Testing
1. Check all case study links for descriptive text:
   ```javascript
   const caseStudyLinks = await page.$$('.case-study a, .case-study-card a');
   for (const link of caseStudyLinks) {
     const text = await link.textContent();
     const ariaLabel = await link.getAttribute('aria-label');
     const label = ariaLabel || text;
     // Should contain an action verb
     expect(label).toMatch(/read|view|see|explore|learn|discover/i);
     // Should contain more than just a company name
     expect(label.split(' ').length).toBeGreaterThan(1);
   }
   ```
2. Run `axe-core` with the `link-name` rule to flag ambiguous link text.

---

## Developer Notes

### General Explanation
Case study CTA buttons currently display only the client company name (e.g., "Cameo," "GoHealth") with no action verb. When a screen reader user lists all links on the page, they hear a list of company names with no indication that these are case study links or what clicking them will do. Voice control users also struggle because saying "click Cameo" may match multiple elements.

### Code Examples

**Before (ambiguous):**
```html
<a href="/case-studies/cameo/" class="case-study-cta">Cameo</a>
<a href="/case-studies/gohealth/" class="case-study-cta">GoHealth</a>
```

**After (Option A — descriptive visible text):**
```html
<a href="/case-studies/cameo/" class="case-study-cta">Read Cameo Case Study</a>
<a href="/case-studies/gohealth/" class="case-study-cta">Read GoHealth Case Study</a>
```

**After (Option B — short visible text + aria-label):**
```html
<a href="/case-studies/cameo/" class="case-study-cta"
   aria-label="Read the Cameo case study">
  Cameo <span aria-hidden="true">→</span>
</a>
```

> **Important:** When using `aria-label`, the visible text ("Cameo") must appear within the `aria-label` value to satisfy WCAG 2.5.3 Label in Name. This ensures voice control users can say "click Cameo" and still match.

**After (Option C — visually hidden supplemental text):**
```html
<a href="/case-studies/cameo/" class="case-study-cta">
  <span class="sr-only">Read case study: </span>Cameo
</a>
```

### Components/Files to Audit
- Case study carousel/slider template
- Case study card component template
- WordPress loop rendering case study entries
- Any ACF fields or custom post type templates for case studies
- Homepage template where case studies are displayed

---

## Examples from Other Sites

- **IBM:** Case study cards use "Read the case study" as the CTA text, with the client name in the card heading above. Each link is unambiguous.
- **Salesforce:** Case study CTAs read "Read [Company Name]'s story" — combining the action and the subject in a single descriptive phrase.
- **Deloitte:** Uses "Explore the [Company] case study" as link text, making the action and destination explicit.
- **HubSpot:** Case study carousel cards use "Read the full story" with the company name provided by the surrounding card context and an `aria-label` combining both.

---

## Additional Context

This fix intersects with issue H-12 (Identical "Learn More" links). Both issues stem from the same root problem: generic or insufficient link text that fails to convey purpose. Fixing L-63 alongside H-12 in a single pass would create consistent, descriptive link patterns across all card-based content on the site.
