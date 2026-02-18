# Issue 11: Add Section Navigation for Long Pages

**Priority:** Medium
**Location:** Homepage, Services page, About page
**Reported by:** Jamie Rivera (ADHD), Sam Chen (Dyslexia)

---

## User Story

**As a** user scrolling through a long page with many content sections,
**I want** persistent navigation aids — like a table of contents, section jump links, and a "back to top" button,
**so that** I can jump to relevant sections, maintain my orientation on the page, and easily return to the top without scrolling endlessly.

---

## Problem

Several key pages contain 10+ distinct content sections, requiring extensive scrolling:

- **Homepage:** Hero → Services → Stats → Process tabs → Case studies → Industries → Testimonials → Contact form (8+ sections)
- **Services page:** Hero → Service list → Process → FAQ → Case studies → Contact form (6+ sections)
- **About page:** Hero → Mission → Team → Awards → Values → Video → Contact form (7+ sections)

Users encounter two problems:

1. **ADHD users** lose context as they scroll. After 3-4 sections, they forget what was at the top and what they were originally looking for. Without a way to jump back or see the page structure, they abandon the page.
2. **Dyslexic users** experience cumulative reading fatigue. After scrolling through several text-heavy sections, they need a way to skip to the specific section they care about (e.g., "How to Contact") without re-reading everything.

There are no "back to top" buttons, no sticky table of contents, and no section jump links anywhere on the site.

---

## Acceptance Criteria

- [ ] A sticky/floating table of contents (TOC) is visible on all pages with 5+ content sections
- [ ] The TOC highlights the currently visible section as the user scrolls (active state)
- [ ] Each section of the page has an `id` attribute and a corresponding anchor link in the TOC
- [ ] A "Back to Top" button appears once the user scrolls past the first viewport height
- [ ] The "Back to Top" button smoothly scrolls to the top of the page when clicked
- [ ] TOC and "Back to Top" button are keyboard-accessible (`Tab`, `Enter`)
- [ ] On mobile, the TOC collapses into a dropdown or bottom sheet to conserve space
- [ ] Smooth scroll behavior respects `prefers-reduced-motion` — users who prefer no animation get instant jumps
- [ ] The TOC does not obstruct main content or interactive elements

---

## How to Test

1. **Scroll test:** Navigate to the Homepage, Services page, and About page. Scroll through the full page. Verify the TOC appears and the active section updates as you scroll
2. **Jump link test:** Click each item in the TOC. Confirm it scrolls to the correct section with the section heading visible at or near the top of the viewport
3. **Back to Top test:** Scroll down at least 2 viewports. Confirm the "Back to Top" button appears. Click it and verify smooth scroll to page top
4. **Keyboard test:** Tab to the TOC and each jump link. Press Enter and confirm navigation works. Tab to the "Back to Top" button and press Enter
5. **Reduced motion test:** In OS accessibility settings, enable "Reduce Motion." Repeat the jump link and back-to-top tests. Confirm scrolling is instant (no animation)
6. **Mobile test (375px):** Verify the TOC collapses to a dropdown or bottom sheet. Verify the "Back to Top" button doesn't obstruct content
7. **Screen reader test:** Using VoiceOver/NVDA, confirm the TOC is announced as a navigation landmark ("Page sections") and each link is descriptive

---

## Developer Notes

### Approach

Implement three features: (1) a sticky table of contents with active section highlighting, (2) section anchor IDs, and (3) a floating "Back to Top" button. Use the Intersection Observer API for scroll-aware highlighting.

### Section Anchor IDs

Every major content section needs an `id`:

```html
<section id="services" aria-labelledby="services-heading">
  <h2 id="services-heading">What We Do</h2>
  <!-- ... -->
</section>

<section id="process" aria-labelledby="process-heading">
  <h2 id="process-heading">Our Process</h2>
  <!-- ... -->
</section>

<section id="case-studies" aria-labelledby="case-studies-heading">
  <h2 id="case-studies-heading">Our Work</h2>
  <!-- ... -->
</section>

<section id="contact" aria-labelledby="contact-heading">
  <h2 id="contact-heading">Get in Touch</h2>
  <!-- ... -->
</section>
```

### Sticky Table of Contents

```html
<nav class="page-toc" aria-label="Page sections">
  <h2 class="page-toc__title">On This Page</h2>
  <ol class="page-toc__list">
    <li><a href="#services" class="page-toc__link" aria-current="false">What We Do</a></li>
    <li><a href="#process" class="page-toc__link" aria-current="false">Our Process</a></li>
    <li><a href="#case-studies" class="page-toc__link" aria-current="false">Our Work</a></li>
    <li><a href="#contact" class="page-toc__link" aria-current="false">Get in Touch</a></li>
  </ol>
</nav>
```

```css
.page-toc {
  position: sticky;
  top: 6rem; /* below the main nav */
  align-self: start;
  max-height: calc(100vh - 8rem);
  overflow-y: auto;
  padding: 1.5rem;
  border-left: 2px solid #e5e7eb;
  font-size: 0.875rem;
}

.page-toc__title {
  font-size: 0.75rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: #6b7280;
  margin-bottom: 1rem;
}

.page-toc__list {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.page-toc__link {
  color: #6b7280;
  text-decoration: none;
  padding-left: 0.75rem;
  border-left: 2px solid transparent;
  transition: color 0.2s ease, border-color 0.2s ease;
  display: block;
  line-height: 1.4;
}

.page-toc__link:hover {
  color: #111827;
}

.page-toc__link[aria-current="true"] {
  color: #2563eb;
  font-weight: 600;
  border-left-color: #2563eb;
}

.page-toc__link:focus-visible {
  outline: 2px solid #2563eb;
  outline-offset: 2px;
  border-radius: 2px;
}

/* Page layout with sidebar TOC */
.page-layout {
  display: grid;
  grid-template-columns: 1fr 220px;
  gap: 3rem;
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

@media (max-width: 768px) {
  .page-layout {
    grid-template-columns: 1fr;
  }

  .page-toc {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    top: auto;
    max-height: none;
    background: #ffffff;
    border-left: none;
    border-top: 1px solid #e5e7eb;
    box-shadow: 0 -4px 12px rgba(0, 0, 0, 0.1);
    padding: 1rem;
    z-index: 50;
    transform: translateY(100%);
    transition: transform 0.3s ease;
  }

  .page-toc.is-open {
    transform: translateY(0);
  }

  .page-toc__toggle {
    position: fixed;
    bottom: 1rem;
    left: 1rem;
    z-index: 51;
    padding: 0.5rem 1rem;
    background: #2563eb;
    color: #ffffff;
    border: none;
    border-radius: 9999px;
    font-size: 0.875rem;
    font-weight: 600;
    cursor: pointer;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
  }
}

/* Smooth scroll with reduced motion respect */
html {
  scroll-behavior: smooth;
}

@media (prefers-reduced-motion: reduce) {
  html {
    scroll-behavior: auto;
  }
}
```

### Intersection Observer for Active Section Highlighting

```javascript
class PageTOC {
  constructor() {
    this.links = document.querySelectorAll('.page-toc__link');
    this.sections = [];

    this.links.forEach(link => {
      const id = link.getAttribute('href').slice(1);
      const section = document.getElementById(id);
      if (section) this.sections.push({ id, element: section, link });
    });

    this.initObserver();
  }

  initObserver() {
    const options = {
      rootMargin: '-80px 0px -60% 0px',
      threshold: 0
    };

    const observer = new IntersectionObserver(entries => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          this.setActive(entry.target.id);
        }
      });
    }, options);

    this.sections.forEach(({ element }) => observer.observe(element));
  }

  setActive(activeId) {
    this.links.forEach(link => {
      const isActive = link.getAttribute('href') === `#${activeId}`;
      link.setAttribute('aria-current', isActive ? 'true' : 'false');
    });
  }
}

document.addEventListener('DOMContentLoaded', () => new PageTOC());
```

### Back to Top Button

```html
<button
  class="back-to-top"
  aria-label="Back to top"
  hidden
>
  <svg aria-hidden="true" width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
    <path fill-rule="evenodd" d="M10 3a1 1 0 01.707.293l6 6a1 1 0 01-1.414 1.414L10 5.414 4.707 10.707a1 1 0 01-1.414-1.414l6-6A1 1 0 0110 3z"/>
  </svg>
</button>
```

```css
.back-to-top {
  position: fixed;
  bottom: 2rem;
  right: 2rem;
  z-index: 40;
  width: 3rem;
  height: 3rem;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #1a1a2e;
  color: #ffffff;
  border: none;
  border-radius: 50%;
  cursor: pointer;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  transition: opacity 0.3s ease, transform 0.3s ease;
  opacity: 0;
  transform: translateY(1rem);
  pointer-events: none;
}

.back-to-top[hidden] {
  display: none;
}

.back-to-top.is-visible {
  opacity: 1;
  transform: translateY(0);
  pointer-events: auto;
}

.back-to-top:hover {
  background-color: #2563eb;
  transform: translateY(-2px);
}

.back-to-top:focus-visible {
  outline: 3px solid #93c5fd;
  outline-offset: 2px;
}

@media (prefers-reduced-motion: reduce) {
  .back-to-top {
    transition: none;
  }
}
```

```javascript
const backToTop = document.querySelector('.back-to-top');

if (backToTop) {
  backToTop.removeAttribute('hidden');

  window.addEventListener('scroll', () => {
    const show = window.scrollY > window.innerHeight;
    backToTop.classList.toggle('is-visible', show);
  }, { passive: true });

  backToTop.addEventListener('click', () => {
    window.scrollTo({ top: 0 });
  });
}
```

### Components to Audit

- **Page templates (Homepage, Services, About)** — Add section `id` attributes to every major content block
- **Layout component** — Add the TOC sidebar and "Back to Top" button to the shared layout
- **Section components** — Ensure each section has `aria-labelledby` pointing to its heading
- **Mobile navigation** — Ensure the TOC toggle doesn't conflict with other fixed elements
- **CSS scroll-behavior** — Add to global stylesheet with `prefers-reduced-motion` override

---

## Examples from Other Sites

### MDN Web Docs (developer.mozilla.org)
Every long article has a sticky sidebar table of contents with active section highlighting. The TOC collapses to a dropdown on mobile. Each section has an anchor link icon visible on hover.

### Stripe Documentation (stripe.com/docs)
Uses a persistent left sidebar with section links that highlight as the user scrolls. Each heading generates an anchor ID automatically.

### W3C WAI (w3.org/WAI)
Long guidance pages include a "On this page" section at the top with jump links to each section, plus a "Back to Top" link at the end of each section. Fully accessible with keyboard and screen readers.

### Medium (medium.com)
Long articles show a progress bar at the top of the viewport, giving users a sense of how far through the content they are — complementing a "Back to Top" button.
