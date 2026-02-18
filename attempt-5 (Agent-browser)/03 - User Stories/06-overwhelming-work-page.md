# Overwhelming Our Work Page (40+ Items, No Hierarchy)

**Priority:** High
**Location:** `/work/`
**WCAG:** [2.4.1 Bypass Blocks (A)](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks), [2.4.6 Headings and Labels (AA)](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels), [1.3.1 Info and Relationships (A)](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships)

---

## User Story

> As a **prospective client evaluating LaunchPad Lab's experience**,
> I want **the Work page to highlight relevant projects and organize them by category**
> so that **I can quickly find case studies in my industry without scrolling through 40+ undifferentiated cards.**

---

## Problem

The `/work/` page displays 40+ case study cards in a flat, uniform grid. There is:
- **No visual hierarchy** — no featured items, no size differentiation, every card looks the same.
- **No category grouping** — no industry headings, no visual sections.
- **No summary section** — no introductory content explaining what types of work are shown.
- **Only a dropdown filter** — easy to miss and requires prior knowledge of available categories.
- **All items visible at once** — triggers "paralysis of choice," making it harder for users with cognitive disabilities (and everyone) to make a decision.

---

## Acceptance Criteria

- [ ] A "Featured Work" section at the top showcases 2–4 highlighted case studies with larger cards and summary text.
- [ ] Case studies are grouped under industry or category headings (e.g., "Healthcare," "Financial Services," "Education").
- [ ] Each group heading is a proper `<h2>` or `<h3>` element for screen reader navigation.
- [ ] Only 6–9 items are visible per category by default, with a "Show more" button to expand.
- [ ] Visual category buttons/tabs replace or supplement the dropdown filter.
- [ ] Each case study card includes: project name, client industry tag, 1-sentence summary, and a thumbnail.
- [ ] Category tags are keyboard-navigable and screen-reader-accessible.
- [ ] A skip link ("Skip to results") is provided at the top of the page.
- [ ] Total count is displayed (e.g., "Showing 9 of 42 projects").

---

## How to Test

1. **First-impression test:** Open `/work/` and note how long it takes to find a project relevant to your industry. If it takes more than 5 seconds of scrolling, the page needs restructuring.
2. **Screen reader navigation:** Use VoiceOver and press the heading shortcut (VO+Cmd+H on macOS). Verify headings outline the page content logically (page title → Featured → Industry 1 → Industry 2 → etc.).
3. **Keyboard navigation:** Tab through the page. Verify category buttons are focusable, filter updates are announced via `aria-live`, and "Show more" buttons are reachable.
4. **Cognitive load test:** Ask 3 users to find a healthcare-related case study. Track time and number of scrolls. Compare before/after redesign.
5. **Count display:** Verify a "Showing X of Y" indicator is visible and updates when filters change.
6. **Mobile test:** On a narrow viewport, verify the category navigation is usable (horizontal scroll or collapsible).

---

## Developer Notes

### Recommended page structure

```html
<main id="main-content">
  <section class="work-page" aria-labelledby="work-heading">
    <h1 id="work-heading">Our Work</h1>
    <p class="work-page__intro">
      We've helped companies across healthcare, finance, education, and more
      build software their users love. Here are some of our favorite projects.
    </p>

    <!-- Featured Section -->
    <section aria-labelledby="featured-heading">
      <h2 id="featured-heading">Featured Projects</h2>
      <div class="work-grid work-grid--featured">
        <article class="work-card work-card--featured">
          <img src="/img/work/project-a.jpg"
               alt="Dashboard interface for Acme Health patient portal" />
          <div class="work-card__content">
            <span class="work-card__tag">Healthcare</span>
            <h3><a href="/work/acme-health/">Acme Health Patient Portal</a></h3>
            <p>
              A patient-facing portal that reduced appointment no-shows by 35 %.
            </p>
          </div>
        </article>
        <!-- 2-3 more featured cards -->
      </div>
    </section>

    <!-- Category Filter -->
    <nav class="work-filters" aria-label="Filter projects by industry">
      <h2 class="sr-only">Filter by Industry</h2>
      <ul role="tablist">
        <li role="presentation">
          <button role="tab" aria-selected="true"
                  aria-controls="panel-all" id="tab-all">
            All Projects
          </button>
        </li>
        <li role="presentation">
          <button role="tab" aria-selected="false"
                  aria-controls="panel-healthcare" id="tab-healthcare">
            Healthcare
          </button>
        </li>
        <li role="presentation">
          <button role="tab" aria-selected="false"
                  aria-controls="panel-finance" id="tab-finance">
            Financial Services
          </button>
        </li>
        <!-- More categories -->
      </ul>
    </nav>

    <!-- Results Count -->
    <p class="work-results-count" aria-live="polite">
      Showing <strong>9</strong> of <strong>42</strong> projects
    </p>

    <!-- Grouped Results -->
    <div id="panel-all" role="tabpanel" aria-labelledby="tab-all">

      <section aria-labelledby="heading-healthcare">
        <h2 id="heading-healthcare">Healthcare</h2>
        <div class="work-grid">
          <!-- 6-9 cards -->
          <article class="work-card">
            <img src="/img/work/project-b.jpg"
                 alt="Mobile app showing medication reminders" />
            <div class="work-card__content">
              <span class="work-card__tag">Healthcare</span>
              <h3><a href="/work/medtrack/">MedTrack Mobile App</a></h3>
              <p>Medication reminders that improved adherence by 28 %.</p>
            </div>
          </article>
          <!-- more cards -->
        </div>
        <button class="btn btn--secondary work-show-more"
                aria-expanded="false"
                aria-controls="healthcare-extra">
          Show more Healthcare projects (6 more)
        </button>
        <div id="healthcare-extra" class="work-grid" hidden>
          <!-- Additional cards -->
        </div>
      </section>

      <section aria-labelledby="heading-finance">
        <h2 id="heading-finance">Financial Services</h2>
        <!-- Similar structure -->
      </section>

    </div>
  </section>
</main>
```

### CSS for the work page grid

```css
.work-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
  margin-bottom: 2rem;
}

.work-grid--featured {
  grid-template-columns: repeat(auto-fill, minmax(400px, 1fr));
  gap: 2.5rem;
  margin-bottom: 3rem;
}

.work-card {
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  overflow: hidden;
  transition: box-shadow 0.2s ease;
  background: #fff;
}

.work-card:hover,
.work-card:focus-within {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.work-card--featured {
  border: 2px solid var(--color-primary);
}

.work-card img {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.work-card--featured img {
  height: 280px;
}

.work-card__content {
  padding: 1.25rem;
}

.work-card__tag {
  display: inline-block;
  font-size: 0.8125rem;
  font-weight: 600;
  color: var(--color-primary);
  background: var(--color-primary-light);
  padding: 0.125rem 0.5rem;
  border-radius: 4px;
  margin-bottom: 0.5rem;
}

.work-card h3 {
  font-size: 1.25rem;
  margin-bottom: 0.5rem;
}

.work-card h3 a {
  text-decoration: none;
  color: inherit;
}

.work-card h3 a:hover,
.work-card h3 a:focus-visible {
  text-decoration: underline;
  outline: 3px solid var(--color-focus-ring);
  outline-offset: 2px;
}

.work-card p {
  font-size: 1rem;
  color: #555;
  line-height: 1.6;
}
```

### CSS for category filter buttons

```css
.work-filters ul {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  list-style: none;
  padding: 0;
  margin-bottom: 1.5rem;
}

.work-filters button {
  padding: 0.5rem 1.25rem;
  font-size: 1rem;
  font-weight: 500;
  border: 2px solid #ccc;
  border-radius: 999px;
  background: transparent;
  color: var(--color-text);
  cursor: pointer;
  transition: all 0.2s ease;
}

.work-filters button[aria-selected="true"] {
  background: var(--color-primary);
  border-color: var(--color-primary);
  color: #fff;
}

.work-filters button:hover {
  border-color: var(--color-primary);
}

.work-filters button:focus-visible {
  outline: 3px solid var(--color-focus-ring);
  outline-offset: 2px;
}
```

### JavaScript for "Show more" and filter behavior

```javascript
document.querySelectorAll('.work-show-more').forEach(button => {
  button.addEventListener('click', () => {
    const targetId = button.getAttribute('aria-controls');
    const target = document.getElementById(targetId);
    const isExpanded = button.getAttribute('aria-expanded') === 'true';

    target.hidden = isExpanded;
    button.setAttribute('aria-expanded', String(!isExpanded));
    button.textContent = isExpanded
      ? button.textContent.replace('Show fewer', 'Show more')
      : button.textContent.replace('Show more', 'Show fewer');

    if (!isExpanded) {
      target.querySelector('.work-card a')?.focus();
    }
  });
});

// Category filter — update count and announce
const resultsCount = document.querySelector('.work-results-count');

document.querySelectorAll('.work-filters button').forEach(tab => {
  tab.addEventListener('click', () => {
    document.querySelectorAll('.work-filters button')
      .forEach(t => t.setAttribute('aria-selected', 'false'));
    tab.setAttribute('aria-selected', 'true');

    const category = tab.id.replace('tab-', '');
    const visibleCount = filterProjects(category);
    resultsCount.innerHTML =
      `Showing <strong>${visibleCount}</strong> of <strong>42</strong> projects`;
  });
});
```

### Components to audit

| Component | Current State | Recommended Change |
|---|---|---|
| Overall page layout | Flat grid, 40+ cards | Add Featured section, group by industry |
| Filter control | Single dropdown | Replace with visible category buttons/tabs |
| Individual cards | Uniform size, no tags | Add industry tags, differentiate featured cards |
| Pagination / limiting | None — all cards visible | Show 6–9 per category, "Show more" to expand |
| Results count | None | Add "Showing X of Y" with `aria-live` |
| Heading structure | Only `<h1>` | Add `<h2>` for each industry group |

---

## Examples from Other Sites

### Thoughtbot (thoughtbot.com/work)
- Features 3 highlighted case studies at top with large images and summaries.
- Remaining projects are below in a tighter grid.
- Clear industry tags on each card.

### Instrument (instrument.com/work)
- Featured hero project at top, smaller grid below.
- Projects are categorized and filterable.
- Clean visual hierarchy with varying card sizes.

### Huge (hugeinc.com/work)
- Uses a masonry-style grid with featured items taking up more space.
- Industry/capability tags on each card.
- Visible filter buttons (not hidden in a dropdown).

### Dribbble (dribbble.com)
- Shows result count ("10,234 shots").
- Large, visible category buttons above the grid.
- Progressive loading instead of showing all items at once.
