# 19. Replace Interactive Tab Section with a Static Layout to Reduce Distraction

**Priority:** Medium
**Location:** Homepage — "Ship Game-Changing Digital Products to Market Fast" section
**Reported by:** Jamie Rivera (ADHD)

---

## User Story

**As a** user with ADHD browsing the homepage,
**I want** all service offerings visible at once in a static layout
**so that** I can scan all options quickly without getting sidetracked by the novelty of clicking through interactive tabs.

---

## Acceptance Criteria

- [ ] The 6 service items currently behind tabs are displayed in a static grid or list layout — all visible simultaneously without interaction
- [ ] If tabs are retained as the chosen pattern, each tab panel contains substantive information (not just a heading and a single sentence)
- [ ] If tabs are retained, no visual imagery competes with the tab content for attention (e.g., large hero photos that change on tab switch)
- [ ] The layout works responsively: grid on desktop (2-3 columns), stacked list on mobile
- [ ] Each service item includes: a clear title, a 1-2 sentence description, and a link to learn more
- [ ] The section heading is updated to plain language (see Issue #2 — replace "Ship Game-Changing Digital Products to Market Fast" with a clearer heading)
- [ ] Content is accessible via keyboard navigation (Tab key moves between items, not trapped in the section)
- [ ] The section does not auto-rotate, auto-advance, or animate without user initiation

---

## How to Test

1. **Navigate** to the Homepage
2. **Scroll** to the service offerings section (currently tabbed)
3. **Verify** all 6 service items are visible without clicking any tabs or interactive elements
4. **Count the items** — confirm all 6 are present and none are hidden behind interaction
5. **Read each item** — confirm each has a title, description, and link
6. **Resize the browser** to mobile width — confirm items stack vertically and remain readable
7. **Keyboard test** — Tab through the section and confirm focus moves linearly through items without getting trapped
8. **Screen reader test** — navigate the section with VoiceOver or NVDA; confirm all 6 items are announced in sequence
9. **ADHD simulation** — ask a tester to scan the section and count items. If using tabs, time how long they spend clicking through vs. reading. A static layout should result in less time clicking and more time reading.
10. **Verify no auto-play** — confirm nothing in this section moves, animates, or changes without user initiation

---

## Developer Notes

### Approach

Replace the tabbed interface with a static CSS Grid layout. This eliminates the "novelty trap" where ADHD users compulsively click through tabs for the small dopamine hit of seeing new content appear, rather than processing the information they need.

### Recommended: Static Grid Layout

```html
<section class="services-overview" aria-labelledby="services-heading">
  <h2 id="services-heading">What We Build</h2>
  <p class="section-intro">
    We design and build custom software across six core areas.
  </p>

  <div class="services-grid">
    <article class="service-card">
      <div class="service-icon" aria-hidden="true">
        <!-- SVG or icon -->
      </div>
      <h3>Web Applications</h3>
      <p>
        Custom web-based software for your business operations —
        dashboards, portals, and internal tools built to your exact needs.
      </p>
      <a href="/services/web-app-development/" class="service-link">
        Learn more<span class="sr-only"> about web application development</span>
      </a>
    </article>

    <article class="service-card">
      <div class="service-icon" aria-hidden="true">
        <!-- SVG or icon -->
      </div>
      <h3>Mobile Applications</h3>
      <p>
        Native and cross-platform mobile apps for iOS and Android
        that connect your customers and team on the go.
      </p>
      <a href="/services/mobile-app-development/" class="service-link">
        Learn more<span class="sr-only"> about mobile application development</span>
      </a>
    </article>

    <article class="service-card">
      <div class="service-icon" aria-hidden="true">
        <!-- SVG or icon -->
      </div>
      <h3>Product Strategy & Design</h3>
      <p>
        Research, prototyping, and UX design to validate your idea
        before committing to development.
      </p>
      <a href="/services/product-strategy-design/" class="service-link">
        Learn more<span class="sr-only"> about product strategy and design</span>
      </a>
    </article>

    <article class="service-card">
      <div class="service-icon" aria-hidden="true">
        <!-- SVG or icon -->
      </div>
      <h3>AI & Machine Learning</h3>
      <p>
        Integrate AI into your products — from intelligent automation
        to data analysis and predictive features.
      </p>
      <a href="/services/ai-machine-learning/" class="service-link">
        Learn more<span class="sr-only"> about AI and machine learning</span>
      </a>
    </article>

    <article class="service-card">
      <div class="service-icon" aria-hidden="true">
        <!-- SVG or icon -->
      </div>
      <h3>System Modernization</h3>
      <p>
        Upgrade legacy systems and outdated software to modern,
        maintainable platforms without disrupting your business.
      </p>
      <a href="/services/system-modernization/" class="service-link">
        Learn more<span class="sr-only"> about system modernization</span>
      </a>
    </article>

    <article class="service-card">
      <div class="service-icon" aria-hidden="true">
        <!-- SVG or icon -->
      </div>
      <h3>Ongoing Support & Growth</h3>
      <p>
        Post-launch maintenance, performance optimization, and new
        feature development to keep your software evolving.
      </p>
      <a href="/services/ongoing-support/" class="service-link">
        Learn more<span class="sr-only"> about ongoing support</span>
      </a>
    </article>
  </div>
</section>
```

### CSS for Static Grid

```css
.services-overview {
  padding: 4rem 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.services-overview h2 {
  font-size: 2rem;
  font-weight: 700;
  text-align: center;
  margin-bottom: 0.5rem;
  color: #1a1a2e;
}

.section-intro {
  text-align: center;
  font-size: 1.125rem;
  color: #555555;
  margin-bottom: 2.5rem;
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
  line-height: 1.7;
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

@media (max-width: 900px) {
  .services-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 600px) {
  .services-grid {
    grid-template-columns: 1fr;
  }
}

.service-card {
  background: #ffffff;
  border: 1px solid #e8e8e8;
  border-radius: 12px;
  padding: 2rem;
  transition: box-shadow 0.2s ease;
}

.service-card:hover {
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
}

.service-icon {
  width: 48px;
  height: 48px;
  margin-bottom: 1rem;
}

.service-card h3 {
  font-size: 1.25rem;
  font-weight: 600;
  color: #1a1a2e;
  margin-bottom: 0.75rem;
}

.service-card p {
  font-size: 1rem;
  line-height: 1.7;
  color: #444444;
  margin-bottom: 1rem;
}

.service-link {
  font-size: 0.95rem;
  font-weight: 600;
  color: #1a73e8;
  text-decoration: none;
  display: inline-flex;
  align-items: center;
  gap: 0.25rem;
}

.service-link:hover {
  text-decoration: underline;
}

.service-link:focus-visible {
  outline: 2px solid #1a73e8;
  outline-offset: 4px;
  border-radius: 2px;
}

.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
```

### If Tabs Must Be Retained: Accessible Tab Pattern

If the business decision is to keep tabs, follow the WAI-ARIA Authoring Practices for tabs and ensure the content is substantive:

```html
<div class="tabs-container">
  <div role="tablist" aria-label="Our services">
    <button role="tab" aria-selected="true" aria-controls="panel-1" id="tab-1">
      Web Applications
    </button>
    <button role="tab" aria-selected="false" aria-controls="panel-2" id="tab-2" tabindex="-1">
      Mobile Applications
    </button>
    <!-- ... more tabs ... -->
  </div>

  <div role="tabpanel" id="panel-1" aria-labelledby="tab-1">
    <!-- SUBSTANTIVE content here — not just a title and image -->
    <h3>Web Applications</h3>
    <p>Full description with examples, outcomes, and a clear CTA...</p>
    <ul>
      <li>Custom dashboards and admin panels</li>
      <li>Customer-facing portals</li>
      <li>Internal workflow tools</li>
    </ul>
    <a href="/services/web-app-development/">Learn more</a>
  </div>

  <div role="tabpanel" id="panel-2" aria-labelledby="tab-2" hidden>
    <!-- ... -->
  </div>
</div>
```

```javascript
const tabs = document.querySelectorAll('[role="tab"]');
const panels = document.querySelectorAll('[role="tabpanel"]');

tabs.forEach(tab => {
  tab.addEventListener('click', () => {
    tabs.forEach(t => {
      t.setAttribute('aria-selected', 'false');
      t.setAttribute('tabindex', '-1');
    });
    panels.forEach(p => p.setAttribute('hidden', ''));

    tab.setAttribute('aria-selected', 'true');
    tab.removeAttribute('tabindex');
    document.getElementById(tab.getAttribute('aria-controls')).removeAttribute('hidden');
  });

  tab.addEventListener('keydown', (e) => {
    const tabArray = Array.from(tabs);
    const index = tabArray.indexOf(tab);
    let newIndex;

    if (e.key === 'ArrowRight') {
      newIndex = (index + 1) % tabArray.length;
    } else if (e.key === 'ArrowLeft') {
      newIndex = (index - 1 + tabArray.length) % tabArray.length;
    } else {
      return;
    }

    e.preventDefault();
    tabArray[newIndex].click();
    tabArray[newIndex].focus();
  });
});
```

### Components to Audit

- **Homepage tab component** — Replace with grid layout or enhance with ARIA + substantive content
- **Associated images** — If large images change per tab, they create additional visual distraction; remove or make static
- **Section heading** — Replace "Ship Game-Changing Digital Products to Market Fast" with plain language (e.g., "What We Build" or "Our Services")
- **Mobile behavior** — Ensure the grid stacks properly; tabs on mobile are especially problematic for touch targets

### WCAG References

- **WCAG 2.1 SC 2.2.2 Pause, Stop, Hide (A):** If any auto-advancing behavior exists in the tabs, users must be able to pause, stop, or hide it
- **WCAG 2.1 SC 1.3.1 Info and Relationships (A):** If using tabs, the tab/panel relationship must be programmatically conveyed via ARIA roles
- **WCAG 2.1 SC 2.1.1 Keyboard (A):** Tab navigation must follow WAI-ARIA tab pattern (Arrow keys between tabs, Tab key into panel content)
- **WCAG 2.1 SC 2.4.3 Focus Order (A):** Focus must move logically through the section without trapping users
- **Cognitive Accessibility Guidance (COGA):** Minimize the number of steps required to access content; avoid interaction patterns that encourage repetitive, non-productive behavior

---

## Examples from Other Sites

### Stripe (stripe.com)
Stripe's homepage presents all product categories in a static grid with cards. Each card has a title, description, and icon. No tabs, no clicks required — everything is visible at once. Despite having more products than most companies, the grid keeps the page scannable.

### Linear (linear.app)
Linear's features page uses a single-column layout with alternating left/right feature blocks. All features are visible as the user scrolls. No tabs, no accordions — just clear, sequential content. This is especially effective for users who need to see "everything" to build a mental model.

### Vercel (vercel.com)
Vercel's homepage uses a card grid for features. Each card is static, contains a brief description and icon, and links to a detail page. The pattern works because there's no hidden content — what you see is what there is.

### Notion (notion.so)
Notion's homepage previously used tabs but switched to a scrollable feature grid after user research showed people weren't clicking past the first tab. The static layout increased engagement with non-first features.

### Key Pattern
Research on tabbed interfaces and attention:
1. **Most users only see the first tab** — studies show 60-80% of users never click past the default tab
2. **Static grids increase discovery** — all items get equal visibility, eliminating the "first tab bias"
3. **For ADHD users, tabs create a loop** — the novelty of clicking and seeing content change is more engaging than the content itself
4. **If tabs must be used** — ensure each panel has enough content to justify the interaction cost; a title + one sentence is not enough
