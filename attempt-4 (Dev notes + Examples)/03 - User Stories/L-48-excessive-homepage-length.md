# L-48: Excessive Homepage Length (11+ Sections)

**Issue ID:** L-48
**Priority:** Low
**WCAG Criteria:** 2.4.1 Bypass Blocks (A)
**Affected Personas:** ADHD, Big Company Owner, Senior Person

---

## User Story

As a **user with ADHD, a busy executive, or an older person**, I want **the homepage to be concise and scannable** so that **I can quickly understand what the company offers and find what I need without scrolling through 11+ full-width sections that create information overload.**

---

## Acceptance Criteria

- [ ] The homepage is reduced to a maximum of **6–7 focused sections** (e.g., Hero, Services overview, Social proof, Case study highlight, CTA, Footer).
- [ ] Secondary content (additional testimonials, extra stat sections, multiple carousels) is moved to dedicated subpages or removed.
- [ ] A "sticky" or in-page table of contents / anchor navigation is provided if the page retains more than 5 sections, allowing users to jump directly to a section of interest.
- [ ] Each remaining section has a clear purpose and distinct heading that aids scanning.
- [ ] The homepage loads completely (including lazy-loaded content) within 3 seconds on a standard connection.
- [ ] Users can reach the primary CTA (Contact) within 2 scrolls (roughly 2 viewport heights) from the top.

---

## How to Test the Change

### Manual Testing

1. Open the redesigned homepage and count the number of full-width sections.
2. Confirm the count is 7 or fewer.
3. Scroll through the page and time how long it takes to reach the bottom — compare to the original.
4. Verify each section has a clear heading visible in the HeadingsMap extension.
5. If anchor navigation is provided, click each anchor link and verify it jumps to the correct section.
6. Ask 2–3 non-technical users to find "how to contact the company" starting from the homepage. Measure time and number of scrolls.

### Automated Testing

1. Count sections programmatically:
   ```javascript
   const sections = document.querySelectorAll('main > section, main > div[class*="section"]');
   console.log(`Homepage sections: ${sections.length}`);
   // Target: <= 7
   ```
2. Run Lighthouse performance audit — verify load time improvement from reduced content.
3. Run axe DevTools — check for bypass block (2.4.1) compliance if anchor navigation is added.

---

## Developer Notes

### General Explanation

The current homepage has 11+ full-width sections, creating a "wall of content" that overwhelms users — especially those with attention differences, time-constrained executives, and older users unfamiliar with lengthy scrolling pages. The fix involves content strategy (consolidation and prioritization) combined with technical implementation (section reduction, optional anchor navigation). This is a content architecture change more than a code-only fix.

### Recommended Section Structure

```
1. Hero — Clear value proposition + primary CTA
2. Services Overview — 3-4 cards (not 6-7)
3. Social Proof — Client logos + 1 highlighted testimonial
4. Case Study Spotlight — 1-2 featured case studies with results
5. Differentiators/Why Us — Brief, scannable
6. Contact CTA — Final conversion section
7. Footer
```

### Code Examples

**Add anchor navigation for remaining sections:**
```html
<nav class="page-sections" aria-label="Page sections">
  <ul>
    <li><a href="#services">Services</a></li>
    <li><a href="#case-studies">Case Studies</a></li>
    <li><a href="#about">About Us</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>
```

**Consolidate multiple testimonial sections into one:**
```html
<!-- Before: 3 separate testimonial sections scattered across the page -->
<!-- After: 1 consolidated section with 2-3 highlighted quotes -->
<section id="testimonials" aria-label="Client testimonials">
  <h2>What Our Clients Say</h2>
  <blockquote>
    <p>"LaunchPad Lab transformed our digital strategy..."</p>
    <cite>— Jane Doe, CTO at Acme Corp</cite>
  </blockquote>
  <!-- 1-2 more quotes max -->
</section>
```

**Lazy-load below-the-fold sections (performance benefit):**
```html
<section id="case-studies" loading="lazy">
  <!-- Case study content -->
</section>
```

### Components / Files to Audit

- Homepage template (e.g., `front-page.php`, Elementor/Gutenberg homepage layout)
- Section order and content priority (work with content/marketing team)
- Identify which sections can be consolidated, moved to subpages, or removed
- Hero section CTA placement
- Any Elementor/Gutenberg page builder section blocks

---

## Examples from Other Sites

- **Stripe.com:** Homepage has approximately 5 clear sections: Hero, Products grid, Customer stories, Developer experience, CTA. Clean, focused, and scannable.
- **Linear.app:** Homepage uses 4-5 sections with generous whitespace, making each section feel intentional rather than overwhelming.
- **Basecamp.com:** Famously simple homepage — Hero + brief pitch + testimonials + pricing + CTA. Under 4 scrolls total.
- **Notion.com:** Homepage has a clear hero, 3-4 use case sections, and a CTA — all navigable within ~5 viewport heights.
