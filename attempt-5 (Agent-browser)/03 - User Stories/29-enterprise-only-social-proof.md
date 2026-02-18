# 29. Enterprise-Only Social Proof (Case Studies & Client Logos)

**Priority:** High
**Location:** Homepage carousel, Our Work page, client logo bar
**Reported by:** Zara Mitchell (Gen Z First-Time Founder)

---

## User Story

**As a** first-time startup founder evaluating development agencies,
**I want** to see evidence that LaunchPad Lab has worked with startups and early-stage companies,
**so that** I feel confident they understand my constraints, budget, and pace — not just those of Fortune 500 companies.

---

## Problem

LaunchPad Lab's social proof across the site is heavily skewed toward enterprise clients:

1. **Homepage carousel** features only large corporations: Millennium Trust, Prosci, CDK Global. A 22-year-old founder with a pre-revenue idea sees these names and thinks, "These guys work with massive companies — they're out of my league."

2. **Client logo bar** displays Kawasaki, Harvard, Whirlpool, and other household-name brands. There are no startup logos visible. The visual message is unambiguous: "We serve enterprises."

3. **Startup case studies exist but are buried.** Tiny House Listings, Breadcrumb, and AlgoFast are on the Our Work page, but they're mixed in among enterprise projects with no way to filter or find them. A founder scrolling through case studies sees enterprise work first and may leave before discovering relevant examples.

4. **No startup-specific trust signals.** There are no testimonials from startup founders, no "we've helped X startups launch" messaging, no early-stage project highlights.

The cumulative effect: the site's social proof acts as a filter that selects for enterprise buyers and repels startup founders. Even though LaunchPad Lab has done startup work, the site hides it.

---

## Acceptance Criteria

### A. Homepage Carousel
- [ ] At least one startup or early-stage company case study is featured in the homepage carousel (among the first 3-4 slides)
- [ ] The startup case study card includes context that resonates with founders (e.g., "Helped launch from idea to MVP in 12 weeks")
- [ ] Carousel slides include a mix of enterprise and startup clients — not all one or the other
- [ ] If startup work is under NDA, a generic "Startup MVP" case study with anonymized details is included

### B. Client Logo Bar
- [ ] The logo bar includes at least 2-3 startup or emerging company logos alongside enterprise logos
- [ ] If startup logos are unavailable (NDA), add a text element: "...and 50+ startups and emerging companies"
- [ ] The logo bar has a tooltip or alt text for each logo identifying the company name (accessibility)
- [ ] All logos have consistent sizing and visual weight — startup logos are not smaller or less prominent than enterprise logos

### C. Our Work Page — Startup Filter
- [ ] A filter or tab system exists on the Our Work page allowing users to filter by audience type (e.g., "Startups," "Enterprise," "All")
- [ ] When "Startups" is selected, only startup-relevant case studies appear (Tiny House Listings, Breadcrumb, AlgoFast, etc.)
- [ ] The filter state is reflected in the URL (e.g., `/work/?filter=startups`) for shareability and back-button support
- [ ] The filter controls are keyboard accessible (Tab + Enter/Space to toggle)
- [ ] The filter announces changes to assistive technology (e.g., via `aria-live` region)

### D. Startup Testimonials
- [ ] At least one testimonial from a startup founder or early-stage company is visible on the homepage or Contact page
- [ ] The testimonial includes the person's name, role, and company (with their permission)
- [ ] If no testimonials are available, a pull quote from a blog post or case study is used as interim content

---

## How to Test

### Homepage Carousel
1. Navigate to the homepage (`/`)
2. Observe the case study carousel
3. Verify at least one slide features a startup or early-stage company
4. Read the slide copy — confirm it includes startup-relevant language (MVP, launch, early stage, etc.)
5. Navigate through all carousel slides — confirm a mix of enterprise and startup clients is represented

### Client Logo Bar
1. On the homepage (or wherever the logo bar appears), inspect the logos
2. Verify at least 2-3 startup/emerging company logos are present, **or** verify a "...and 50+ startups" text element exists
3. Hover over each logo — verify a tooltip or visual label identifies the company name
4. Inspect HTML: confirm each `<img>` has a descriptive `alt` attribute (e.g., `alt="Tiny House Listings logo"`)
5. Verify logos are visually consistent in size — no startup logo is noticeably smaller

### Our Work Page Filters
1. Navigate to `/work/` (or equivalent)
2. Locate filter controls — verify a "Startups" option exists
3. Click "Startups" — verify the page updates to show only startup case studies
4. Check the URL — verify it reflects the filter state (e.g., `/work/?filter=startups`)
5. Click browser back button — verify you return to the unfiltered state
6. Test keyboard navigation: Tab to the filter, press Enter/Space to select "Startups"
7. Use a screen reader: confirm filter changes are announced (e.g., "Showing 5 startup projects")

### Testimonials
1. On the homepage, scroll to find testimonials
2. Verify at least one testimonial is from a startup founder or non-enterprise client
3. Confirm the testimonial includes attribution (name, role, company)

---

## Developer Notes

### A. Homepage Carousel — Adding Startup Slide

Add a startup case study slide to the existing carousel component. The key is placing it among the first 3 slides (not buried at the end):

```html
<!-- New carousel slide for a startup case study -->
<div class="carousel-slide" role="group" aria-roledescription="slide" aria-label="3 of 5">
  <div class="carousel-slide__content">
    <span class="carousel-slide__tag">Startup MVP</span>
    <h3 class="carousel-slide__title">Tiny House Listings</h3>
    <p class="carousel-slide__description">
      Helped a first-time founder go from idea to launched marketplace
      in 14 weeks — now serving thousands of users nationwide.
    </p>
    <a href="/work/tiny-house-listings/" class="carousel-slide__link">
      Read the case study
      <span aria-hidden="true">→</span>
    </a>
  </div>
  <div class="carousel-slide__image">
    <img
      src="/images/work/tiny-house-listings-hero.jpg"
      alt="Tiny House Listings marketplace showing property cards on desktop and mobile"
      loading="lazy"
      width="640"
      height="400"
    />
  </div>
</div>
```

```css
.carousel-slide__tag {
  display: inline-block;
  padding: 0.25rem 0.75rem;
  font-size: 0.75rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: #7c3aed;
  background-color: #ede9fe;
  border-radius: 999px;
  margin-bottom: 1rem;
}
```

### B. Logo Bar — Adding Startup Logos and Fallback Text

```html
<section class="logo-bar" aria-label="Trusted by leading companies and startups">
  <h2 class="logo-bar__heading">Trusted by</h2>
  <div class="logo-bar__grid">
    <!-- Enterprise logos -->
    <img src="/images/logos/kawasaki.svg" alt="Kawasaki logo" class="logo-bar__logo" width="120" height="40" loading="lazy" />
    <img src="/images/logos/harvard.svg" alt="Harvard University logo" class="logo-bar__logo" width="120" height="40" loading="lazy" />
    <img src="/images/logos/whirlpool.svg" alt="Whirlpool logo" class="logo-bar__logo" width="120" height="40" loading="lazy" />

    <!-- Startup logos -->
    <img src="/images/logos/tiny-house-listings.svg" alt="Tiny House Listings logo" class="logo-bar__logo" width="120" height="40" loading="lazy" />
    <img src="/images/logos/breadcrumb.svg" alt="Breadcrumb logo" class="logo-bar__logo" width="120" height="40" loading="lazy" />
    <img src="/images/logos/algofast.svg" alt="AlgoFast logo" class="logo-bar__logo" width="120" height="40" loading="lazy" />

    <!-- NDA fallback -->
    <span class="logo-bar__more">...and 50+ startups</span>
  </div>
</section>
```

```css
.logo-bar {
  padding: 3rem 1.5rem;
  text-align: center;
  background-color: #f9fafb;
}

.logo-bar__heading {
  font-size: 0.875rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: #9ca3af;
  margin-bottom: 2rem;
}

.logo-bar__grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  gap: 2.5rem 3rem;
  max-width: 960px;
  margin: 0 auto;
}

.logo-bar__logo {
  height: 2rem;
  width: auto;
  object-fit: contain;
  filter: grayscale(100%);
  opacity: 0.6;
  transition: opacity 0.2s ease, filter 0.2s ease;
}

.logo-bar__logo:hover {
  filter: grayscale(0%);
  opacity: 1;
}

.logo-bar__more {
  font-size: 0.9375rem;
  font-weight: 600;
  color: #6b7280;
  font-style: italic;
  white-space: nowrap;
}
```

### C. Our Work Page — Filter System

#### HTML Structure

```html
<section class="work-filters" aria-label="Filter projects by audience">
  <div class="work-filters__controls" role="tablist" aria-label="Project filters">
    <button role="tab" aria-selected="true" aria-controls="work-grid"
            class="work-filter work-filter--active" data-filter="all">
      All Projects
    </button>
    <button role="tab" aria-selected="false" aria-controls="work-grid"
            class="work-filter" data-filter="startups">
      Startups
    </button>
    <button role="tab" aria-selected="false" aria-controls="work-grid"
            class="work-filter" data-filter="enterprise">
      Enterprise
    </button>
    <button role="tab" aria-selected="false" aria-controls="work-grid"
            class="work-filter" data-filter="healthcare">
      Healthcare
    </button>
    <button role="tab" aria-selected="false" aria-controls="work-grid"
            class="work-filter" data-filter="fintech">
      Fintech
    </button>
  </div>

  <div id="work-grid" role="tabpanel" class="work-grid" aria-live="polite">
    <!-- Case study cards rendered here -->
  </div>

  <div class="sr-only" aria-live="polite" id="filter-announcement"></div>
</section>
```

#### CSS for Filters

```css
.work-filters__controls {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 2rem;
  padding-bottom: 1rem;
  border-bottom: 1px solid #e5e7eb;
}

.work-filter {
  padding: 0.5rem 1.25rem;
  font-size: 0.9375rem;
  font-weight: 500;
  color: #6b7280;
  background: none;
  border: 1px solid transparent;
  border-radius: 999px;
  cursor: pointer;
  transition: all 0.2s ease;
}

.work-filter:hover {
  color: #111827;
  background-color: #f3f4f6;
}

.work-filter--active,
.work-filter[aria-selected="true"] {
  color: #ffffff;
  background-color: #111827;
  border-color: #111827;
}

.work-filter:focus-visible {
  outline: 2px solid #2563eb;
  outline-offset: 2px;
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

#### JavaScript for Filtering

```javascript
class WorkFilter {
  constructor() {
    this.filters = document.querySelectorAll('.work-filter');
    this.grid = document.getElementById('work-grid');
    this.announcement = document.getElementById('filter-announcement');
    this.cards = this.grid.querySelectorAll('.work-card');

    this.init();
  }

  init() {
    this.filters.forEach(filter => {
      filter.addEventListener('click', () => this.handleFilter(filter));
      filter.addEventListener('keydown', (e) => this.handleKeyboard(e));
    });

    const params = new URLSearchParams(window.location.search);
    const initialFilter = params.get('filter') || 'all';
    const initialButton = document.querySelector(`[data-filter="${initialFilter}"]`);
    if (initialButton) {
      this.handleFilter(initialButton, false);
    }
  }

  handleFilter(activeFilter, updateURL = true) {
    const filterValue = activeFilter.dataset.filter;

    this.filters.forEach(f => {
      f.classList.remove('work-filter--active');
      f.setAttribute('aria-selected', 'false');
    });
    activeFilter.classList.add('work-filter--active');
    activeFilter.setAttribute('aria-selected', 'true');

    let visibleCount = 0;
    this.cards.forEach(card => {
      const categories = card.dataset.categories?.split(',') || [];
      const isVisible = filterValue === 'all' || categories.includes(filterValue);

      card.style.display = isVisible ? '' : 'none';
      if (isVisible) visibleCount++;
    });

    const label = activeFilter.textContent.trim();
    this.announcement.textContent = `Showing ${visibleCount} ${label} project${visibleCount !== 1 ? 's' : ''}`;

    if (updateURL) {
      const url = new URL(window.location);
      if (filterValue === 'all') {
        url.searchParams.delete('filter');
      } else {
        url.searchParams.set('filter', filterValue);
      }
      history.pushState({}, '', url);
    }
  }

  handleKeyboard(e) {
    const filterArray = Array.from(this.filters);
    const currentIndex = filterArray.indexOf(e.target);

    if (e.key === 'ArrowRight' || e.key === 'ArrowDown') {
      e.preventDefault();
      const next = filterArray[(currentIndex + 1) % filterArray.length];
      next.focus();
    } else if (e.key === 'ArrowLeft' || e.key === 'ArrowUp') {
      e.preventDefault();
      const prev = filterArray[(currentIndex - 1 + filterArray.length) % filterArray.length];
      prev.focus();
    }
  }
}

document.addEventListener('DOMContentLoaded', () => new WorkFilter());
```

#### Case Study Card with Category Data

```html
<!-- Startup case study card -->
<article class="work-card" data-categories="startups,marketplace">
  <a href="/work/tiny-house-listings/" class="work-card__link">
    <img
      src="/images/work/tiny-house-listings-thumb.jpg"
      alt="Tiny House Listings marketplace showing property search results"
      class="work-card__image"
      loading="lazy"
      width="400"
      height="300"
    />
    <div class="work-card__content">
      <span class="work-card__category">Startup MVP</span>
      <h3 class="work-card__title">Tiny House Listings</h3>
      <p class="work-card__excerpt">
        From concept to launched marketplace in 14 weeks
      </p>
    </div>
  </a>
</article>

<!-- Enterprise case study card -->
<article class="work-card" data-categories="enterprise,fintech">
  <a href="/work/millennium-trust/" class="work-card__link">
    <img
      src="/images/work/millennium-trust-thumb.jpg"
      alt="Millennium Trust digital banking dashboard"
      class="work-card__image"
      loading="lazy"
      width="400"
      height="300"
    />
    <div class="work-card__content">
      <span class="work-card__category">Enterprise</span>
      <h3 class="work-card__title">Millennium Trust</h3>
      <p class="work-card__excerpt">
        Modernizing retirement account management
      </p>
    </div>
  </a>
</article>
```

### D. Startup Testimonial Block

```html
<blockquote class="testimonial testimonial--startup">
  <p class="testimonial__text">
    "I came to LaunchPad Lab with just a napkin sketch and a lot of enthusiasm.
    They didn't make me feel like my project was too small — they helped me
    think through the product, prioritize features, and launch an MVP that
    actually got users."
  </p>
  <footer class="testimonial__attribution">
    <img
      src="/images/testimonials/founder-avatar.jpg"
      alt=""
      class="testimonial__avatar"
      width="48"
      height="48"
      loading="lazy"
    />
    <div>
      <cite class="testimonial__name">Alex Chen</cite>
      <span class="testimonial__role">Founder, Tiny House Listings</span>
    </div>
  </footer>
</blockquote>
```

```css
.testimonial {
  max-width: 640px;
  margin: 3rem auto;
  padding: 2rem;
  background-color: #fafafa;
  border-left: 4px solid #2563eb;
  border-radius: 0 12px 12px 0;
}

.testimonial__text {
  font-size: 1.125rem;
  line-height: 1.8;
  color: #1f2937;
  font-style: italic;
  margin-bottom: 1.5rem;
}

.testimonial__attribution {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.testimonial__avatar {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  object-fit: cover;
}

.testimonial__name {
  display: block;
  font-weight: 700;
  font-size: 0.9375rem;
  color: #111827;
  font-style: normal;
}

.testimonial__role {
  display: block;
  font-size: 0.8125rem;
  color: #6b7280;
}
```

### WCAG References

- **WCAG 2.1 SC 1.1.1 Non-text Content (A):** All logo images must have descriptive `alt` text (e.g., "Tiny House Listings logo")
- **WCAG 2.1 SC 1.3.1 Info and Relationships (A):** Filter controls must communicate state (selected/unselected) programmatically via `aria-selected`
- **WCAG 2.1 SC 4.1.3 Status Messages (AA):** Filter result counts must be announced to screen readers via `aria-live="polite"`
- **WCAG 2.1 SC 2.4.6 Headings and Labels (AA):** Filter labels must clearly describe what they filter
- **WCAG 2.1 SC 2.1.1 Keyboard (A):** All filter controls and carousel navigation must be keyboard operable

### Components to Audit

- **Homepage carousel component** — Add startup case study slide(s) among the first 3 positions
- **Logo bar / trust bar component** — Add startup logos or "...and 50+ startups" fallback text
- **Our Work page template** — Add filter controls and category data attributes to case study cards
- **Case study card component** — Add `data-categories` attribute for filtering
- **Testimonial component** — Create or update to support startup founder testimonials
- **CMS/content management** — Tag existing case studies with audience categories (startup, enterprise, etc.)
- **Image assets** — Obtain or create startup client logos in SVG format for the logo bar

---

## Examples from Other Sites

### Thoughtbot (thoughtbot.com/work)
Their case studies page shows a mix of startup and enterprise work. They explicitly tag projects as "Startup" or "Enterprise" and include filtering. Their startup case studies emphasize speed: "Launched in 8 weeks," "From idea to App Store."

### Pivotal Labs / VMware Tanzu Labs
Their portfolio prominently features startup work alongside enterprise clients. Startup case studies are framed around outcomes: "Achieved product-market fit," "Raised Series A after launch." The messaging speaks to founders, not just CTOs.

### Toptal (toptal.com)
Their client logo bar includes both Fortune 500 logos and startup logos side by side. Below the logos, text reads "Trusted by leading brands and the world's top startups." This dual framing makes both audiences feel welcome.

### Lemon Squeezy
Uses a "Wall of Love" section — a grid of tweets and testimonials from indie makers and startup founders. No corporate testimonials. This resonates strongly with solo founders and small teams.

### Webflow (webflow.com/customers)
Their customer stories page has clear filter tabs: "Agency," "Startup," "Enterprise," "Education." Clicking "Startup" immediately shows relevant stories. Each card includes the company stage and a pull quote from the founder.

### Key Patterns
1. **Mix, don't segregate** — Show startup and enterprise work together on the homepage to signal breadth
2. **Tag and filter on portfolio pages** — Let users self-select their audience type to find relevant examples
3. **Frame startup work around outcomes** — "Launched in X weeks," "Y users in first month," "Raised $Z after launch"
4. **Include startup logos** — Even small logos alongside big ones signal inclusivity; add "...and X startups" if logos aren't available
5. **Startup testimonials on the homepage** — One founder quote can shift the entire site's perceived audience
