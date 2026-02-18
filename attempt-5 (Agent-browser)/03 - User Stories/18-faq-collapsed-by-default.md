# 18. Expand Key FAQ Items by Default for Immediate Visibility

**Priority:** Medium
**Location:** Services page, Industries page — bottom sections
**Reported by:** Richard Okonkwo (Non-Technical Business Executive)

---

## User Story

**As a** time-pressed business executive scanning the site for answers,
**I want** the most important FAQ answers (cost, timeline, process) to be visible without clicking
**so that** I can immediately find the information I need to make a decision, rather than guessing which collapsed items might be relevant.

---

## Acceptance Criteria

- [ ] The first 2-3 FAQ items on each page are expanded (open) by default when the page loads
- [ ] The expanded-by-default items are the most commonly asked: cost/pricing, timeline/duration, and process/how-it-works
- [ ] Expanded items can still be collapsed by clicking their header (standard accordion behavior)
- [ ] Collapsed items can be expanded by clicking their header
- [ ] The visual state (expanded vs. collapsed) is clearly indicated with a chevron, plus/minus icon, or equivalent
- [ ] Accordion behavior works correctly with keyboard navigation (Enter and Space to toggle)
- [ ] Screen readers announce the expanded/collapsed state of each FAQ item
- [ ] The FAQ section is visible on the page without requiring excessive scrolling (consider surfacing it higher on the page or adding a jump link)

---

## How to Test

1. **Navigate** to the Services page and scroll to the FAQ section
2. **Verify** the first 2-3 items are visually expanded (answer text is visible) on page load without any user interaction
3. **Click** an expanded item's header — confirm it collapses and the answer hides
4. **Click** a collapsed item's header — confirm it expands and the answer shows
5. **Keyboard test** — Tab to each FAQ header and press Enter or Space; confirm the item toggles between expanded and collapsed
6. **Screen reader test** — navigate to the FAQ section with VoiceOver or NVDA:
   - Confirm each item's header has `role="button"` or is a `<button>` / `<summary>` element
   - Confirm expanded items announce as "expanded" and collapsed items announce as "collapsed"
   - Confirm pressing Enter toggles the state and the new state is announced
7. **Repeat** for the Industries page
8. **Visual indicator test** — confirm the chevron/icon rotates or changes between expanded and collapsed states
9. **Mobile test** — verify the same behavior on small screens; confirm touch targets for FAQ headers are at least 44x44px

---

## Developer Notes

### Approach

Use the native HTML `<details>`/`<summary>` elements with the `open` attribute for the items that should be expanded by default. This provides built-in accessibility without JavaScript for the basic toggle behavior.

### Option A: Native `<details>` / `<summary>` (Recommended)

```html
<section class="faq-section" aria-labelledby="faq-heading">
  <h2 id="faq-heading">Frequently Asked Questions</h2>

  <!-- Expanded by default: open attribute -->
  <details class="faq-item" open>
    <summary class="faq-question">
      How much does a custom software project cost?
    </summary>
    <div class="faq-answer">
      <p>
        Project costs depend on scope, complexity, and timeline. Most projects
        range from $50K for an MVP to $500K+ for enterprise platforms.
        <a href="/contact/">Contact us</a> for a free estimate tailored to your needs.
      </p>
    </div>
  </details>

  <details class="faq-item" open>
    <summary class="faq-question">
      How long does a typical project take?
    </summary>
    <div class="faq-answer">
      <p>
        Timelines vary by project size. A focused MVP can launch in 8-12 weeks.
        Full applications typically take 3-6 months. We'll provide a detailed
        timeline after our initial discovery session.
      </p>
    </div>
  </details>

  <details class="faq-item" open>
    <summary class="faq-question">
      What does the process look like?
    </summary>
    <div class="faq-answer">
      <p>
        We follow a three-phase approach: <strong>Discover</strong> (understand your
        needs), <strong>Deliver</strong> (build and test in short cycles), and
        <strong>Release</strong> (launch and support). You're involved at every step.
      </p>
    </div>
  </details>

  <!-- Collapsed by default: no open attribute -->
  <details class="faq-item">
    <summary class="faq-question">
      What technologies do you use?
    </summary>
    <div class="faq-answer">
      <p>
        We specialize in React, React Native, Ruby on Rails, and Python,
        among others. We choose the best technology for your specific project needs.
      </p>
    </div>
  </details>

  <details class="faq-item">
    <summary class="faq-question">
      Do you offer ongoing support after launch?
    </summary>
    <div class="faq-answer">
      <p>
        Yes. We offer maintenance and support packages to keep your application
        running smoothly, fix issues, and add new features as your business grows.
      </p>
    </div>
  </details>
</section>
```

### CSS for FAQ Accordion

```css
.faq-section {
  max-width: 800px;
  margin: 3rem auto;
  padding: 0 1.5rem;
}

.faq-item {
  border-bottom: 1px solid #e0e0e0;
  padding: 0;
}

.faq-item:first-of-type {
  border-top: 1px solid #e0e0e0;
}

.faq-question {
  font-size: 1.125rem;
  font-weight: 600;
  color: #1a1a2e;
  padding: 1.25rem 2.5rem 1.25rem 0;
  cursor: pointer;
  list-style: none; /* Remove default marker */
  position: relative;
  line-height: 1.5;
}

/* Remove default disclosure triangle */
.faq-question::-webkit-details-marker {
  display: none;
}

/* Custom chevron indicator */
.faq-question::after {
  content: '';
  position: absolute;
  right: 0.5rem;
  top: 50%;
  transform: translateY(-50%) rotate(0deg);
  width: 0.75rem;
  height: 0.75rem;
  border-right: 2px solid #333333;
  border-bottom: 2px solid #333333;
  transform-origin: center;
  transition: transform 0.2s ease;
}

/* Collapsed state: chevron points down */
.faq-item:not([open]) .faq-question::after {
  transform: translateY(-50%) rotate(45deg);
}

/* Expanded state: chevron points up */
.faq-item[open] .faq-question::after {
  transform: translateY(-25%) rotate(-135deg);
}

.faq-question:hover {
  color: #1a73e8;
}

.faq-question:focus-visible {
  outline: 2px solid #1a73e8;
  outline-offset: 4px;
  border-radius: 2px;
}

.faq-answer {
  padding: 0 0 1.25rem 0;
  font-size: 1rem;
  line-height: 1.8;
  color: #444444;
}

.faq-answer p {
  margin-bottom: 0.75rem;
}

.faq-answer p:last-child {
  margin-bottom: 0;
}
```

### Option B: JavaScript Accordion (For Custom Component Libraries)

If the site uses a custom accordion component instead of native `<details>`:

```html
<div class="accordion" role="region" aria-labelledby="faq-heading">
  <h2 id="faq-heading">Frequently Asked Questions</h2>

  <div class="accordion-item">
    <h3>
      <button
        class="accordion-trigger"
        aria-expanded="true"
        aria-controls="faq-1-content"
        id="faq-1-trigger"
      >
        How much does a custom software project cost?
        <span class="accordion-icon" aria-hidden="true"></span>
      </button>
    </h3>
    <div
      class="accordion-panel"
      id="faq-1-content"
      role="region"
      aria-labelledby="faq-1-trigger"
    >
      <p>Project costs depend on scope, complexity, and timeline...</p>
    </div>
  </div>

  <!-- Collapsed item: aria-expanded="false", panel hidden -->
  <div class="accordion-item">
    <h3>
      <button
        class="accordion-trigger"
        aria-expanded="false"
        aria-controls="faq-4-content"
        id="faq-4-trigger"
      >
        What technologies do you use?
        <span class="accordion-icon" aria-hidden="true"></span>
      </button>
    </h3>
    <div
      class="accordion-panel"
      id="faq-4-content"
      role="region"
      aria-labelledby="faq-4-trigger"
      hidden
    >
      <p>We specialize in React, React Native, Ruby on Rails...</p>
    </div>
  </div>
</div>
```

```javascript
document.querySelectorAll('.accordion-trigger').forEach(button => {
  button.addEventListener('click', () => {
    const expanded = button.getAttribute('aria-expanded') === 'true';
    const panel = document.getElementById(button.getAttribute('aria-controls'));

    button.setAttribute('aria-expanded', String(!expanded));

    if (expanded) {
      panel.setAttribute('hidden', '');
    } else {
      panel.removeAttribute('hidden');
    }
  });
});
```

### Surfacing Key Answers Higher on the Page

In addition to expanding FAQ items, consider extracting the most critical answers into a dedicated "What to Expect" section higher up on the page:

```html
<section class="what-to-expect" aria-labelledby="expect-heading">
  <h2 id="expect-heading">What to Expect</h2>
  <div class="expect-grid">
    <div class="expect-item">
      <h3>Timeline</h3>
      <p>8-12 weeks for an MVP. 3-6 months for a full application.</p>
    </div>
    <div class="expect-item">
      <h3>Investment</h3>
      <p>Projects typically range from $50K to $500K+ depending on scope.</p>
    </div>
    <div class="expect-item">
      <h3>Process</h3>
      <p>Discover → Deliver → Release. You're involved at every step.</p>
    </div>
  </div>
</section>
```

### Components to Audit

- **Services page FAQ accordion** — Set the `open` attribute (or `aria-expanded="true"`) on the first 2-3 items
- **Industries page FAQ accordion** — Same treatment
- **Any other page with FAQ sections** — Apply the same pattern
- **CMS / content management** — If FAQ items are managed via a CMS, add a "expanded by default" boolean field to the FAQ content type

### WCAG References

- **WCAG 2.1 SC 4.1.2 Name, Role, Value (A):** Interactive components must expose their state (expanded/collapsed) to assistive technologies
- **WCAG 2.1 SC 2.4.6 Headings and Labels (AA):** FAQ question text must clearly describe the answer content
- **WCAG 2.1 SC 1.3.1 Info and Relationships (A):** The relationship between the question and its answer must be programmatically determinable
- **WCAG 2.1 SC 2.1.1 Keyboard (A):** All accordion functionality must be operable via keyboard

---

## Examples from Other Sites

### Apple (apple.com)
Apple's product pages (e.g., iPhone comparison) use a FAQ accordion at the bottom, but they keep the first few most-asked items expanded by default. This "progressive disclosure with sensible defaults" means most visitors get their answer without a click.

### Gov.uk (gov.uk)
The UK government's design system recommends expanding the first item of any accordion by default. Their research showed that many users didn't realize collapsed items were interactive, and expanding the first one served as a visual cue that the others were expandable too.

### Stripe (stripe.com/pricing)
Stripe's pricing FAQ section shows the top 3 questions expanded by default and collapses the rest. The expanded items directly address the highest-intent questions (pricing, limits, switching plans).

### Mailchimp (mailchimp.com/pricing)
Their FAQ section uses a "see answer" pattern where the top 3 answers are visible and the remaining items have a "See more FAQs" button. This focuses attention on the most critical information.

### Key Pattern
Research consistently shows:
1. **Many users don't click accordions** — they assume collapsed content is less important or don't notice it's interactive
2. **Expanding 2-3 items by default** doubles the chance that users see the answer they need
3. **The first expanded item teaches the interaction model** — it shows that items can be toggled, making users more likely to explore other items
4. **FAQ order matters** — put the highest-intent questions first (cost, timeline, process), not the easiest to answer
