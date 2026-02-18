# L-49: No Pricing or Engagement Model Info

**Issue ID:** L-49
**Priority:** Low
**WCAG Criteria:** N/A (UX / trust concern)
**Affected Personas:** Skeptical User, Big Company Owner

---

## User Story

As a **potential client evaluating development agencies**, I want **to find basic information about pricing ranges, engagement models, and the process of working with this company** so that **I can determine if LaunchPad Lab is within my budget and understand what to expect before committing to a sales conversation.**

---

## Acceptance Criteria

- [ ] The site includes a dedicated "How We Work" or "Engagement Models" page or section that describes the company's engagement process.
- [ ] At minimum, the content covers: engagement types (fixed-price, time & materials, dedicated team), typical project timeline, and a general pricing range or "starting at" figure.
- [ ] If exact pricing cannot be shared, a clear process overview is provided (e.g., "Step 1: Discovery call → Step 2: Proposal → Step 3: Kickoff").
- [ ] The pricing/process page is accessible from the primary navigation or the Services section.
- [ ] The content is written in plain language without unexplained jargon.
- [ ] A CTA to request a detailed quote is included on the page.

---

## How to Test the Change

### Manual Testing

1. Navigate to the site and look for a "Pricing," "How We Work," or "Engagement Models" link in the navigation.
2. Click through and verify the page/section exists and contains engagement model information.
3. Confirm at least one of: pricing range, engagement types, or process timeline is described.
4. Verify the content is understandable to a non-technical reader.
5. Check that a CTA (e.g., "Request a Quote" or "Schedule a Call") is present on the page.
6. Ask a non-technical person to review the page and report whether they understand how to engage the company.

### Automated Testing

1. Verify the page exists and is linked in navigation:
   ```javascript
   const nav = document.querySelector('nav.primary-nav');
   const processLink = nav?.querySelector('a[href*="how-we-work"], a[href*="pricing"], a[href*="engagement"], a[href*="process"]');
   console.log('Process page link:', processLink ? processLink.href : 'MISSING');
   ```
2. Run Lighthouse accessibility audit on the new page.
3. Run a readability analysis tool (e.g., Hemingway Editor) on the page content — target Grade 8 reading level or below.

---

## Developer Notes

### General Explanation

The site provides zero information about pricing, engagement models, or the working process. Decision-makers — especially enterprise buyers and skeptical evaluators — expect transparency before investing time in a sales conversation. The absence of this information creates a "black box" perception that reduces trust and increases bounce rates. The fix involves creating a new page (or adding a section to the Services page) that outlines how the company engages with clients.

### Content Structure Recommendation

```markdown
# How We Work

## Our Process
1. **Discovery** — We learn about your business, goals, and technical needs (1-2 weeks)
2. **Proposal** — We deliver a detailed scope, timeline, and cost estimate
3. **Design & Build** — Iterative development with regular check-ins
4. **Launch & Support** — Deployment plus ongoing maintenance options

## Engagement Models
- **Project-Based** — Fixed scope and timeline for well-defined projects
- **Team Augmentation** — Dedicated developers embedded in your team
- **Ongoing Partnership** — Retainer-based long-term collaboration

## Investment
Our projects typically range from $50K–$500K+ depending on scope and complexity.
[Request a Custom Quote →]
```

### Code Examples

**New page template (WordPress):**
```php
<?php
/* Template Name: How We Work */
get_header();
?>

<main id="primary">
  <section class="process-hero">
    <h1>How We Work</h1>
    <p>From discovery to delivery, here's what to expect when you partner with us.</p>
  </section>

  <section class="process-steps" aria-label="Our process">
    <h2>Our Process</h2>
    <ol class="steps-list">
      <li>
        <h3>Discovery</h3>
        <p>We learn about your business, goals, and technical landscape.</p>
      </li>
      <!-- Additional steps -->
    </ol>
  </section>

  <section class="engagement-models" aria-label="Engagement models">
    <h2>Engagement Models</h2>
    <!-- Engagement model cards -->
  </section>

  <section class="cta-section">
    <h2>Ready to Get Started?</h2>
    <a href="/contact/" class="btn-primary">Request a Quote</a>
  </section>
</main>

<?php get_footer(); ?>
```

**Add to navigation:**
```html
<nav class="primary-nav" aria-label="Main navigation">
  <ul>
    <li><a href="/services/">Services</a></li>
    <li><a href="/how-we-work/">How We Work</a></li>
    <li><a href="/case-studies/">Case Studies</a></li>
    <li><a href="/about/">About</a></li>
    <li><a href="/contact/">Contact</a></li>
  </ul>
</nav>
```

### Components / Files to Audit

- Primary navigation menu (WordPress Menus admin)
- Services page — add cross-link to "How We Work"
- Contact page — reference the engagement process
- Create new page template or use Gutenberg/Elementor page builder
- Coordinate with sales/marketing team for accurate pricing and process content

---

## Examples from Other Sites

- **Thoughtbot.com/playbook:** Publishes their entire engagement process as a public playbook, including how they estimate, how they collaborate, and what tools they use.
- **Pivotal Labs (VMware Tanzu Labs):** Describes their engagement model with phases (Discovery & Framing, Inception, Delivery) and typical timelines.
- **Toptal.com:** Clear pricing page with engagement models (hourly, part-time, full-time) and a transparent process flow.
- **Deloitte Digital:** Describes engagement types (strategy, implementation, managed services) with enough detail for enterprise buyers to self-qualify.
