# No Search Functionality

**Priority:** Low
**Location:** Sitewide — navigation / header
**WCAG:** [2.4.5 Multiple Ways (AA)](https://www.w3.org/WAI/WCAG21/Understanding/multiple-ways), [3.2.3 Consistent Navigation (AA)](https://www.w3.org/WAI/WCAG21/Understanding/consistent-navigation)

---

## User Story

> As a **user with a motor disability, cognitive disability, or limited time**,
> I want **a search bar in the site header that lets me find content by keyword**
> so that **I don't have to navigate through multiple pages and menus to locate the information I need.**

---

## Problem

The LaunchPad Lab website has no search functionality anywhere on the site. Users must manually browse through navigation menus, service pages, case studies, blog posts, and the about page to find specific information. This is especially burdensome for:

- **Motor-impaired users** who minimize clicks and page loads.
- **Cognitively impaired users** who struggle with complex navigation hierarchies.
- **Screen reader users** who benefit from jumping directly to relevant content rather than traversing every page.
- **Any user in a hurry** looking for a specific service, case study, or contact detail.

WCAG 2.4.5 (Multiple Ways) requires that more than one way is available to locate a web page within a set of pages. Currently the site offers only sequential navigation — no search, no sitemap, and no A–Z index.

---

## Acceptance Criteria

- [ ] A search input is present in the site header on every page.
- [ ] The search input is keyboard-accessible (`Tab` to focus, `Enter` to submit).
- [ ] The search input has a visible label or accessible `aria-label`.
- [ ] Search results are ranked by relevance (not just alphabetical or chronological).
- [ ] Each result displays a title, a short excerpt with the search term highlighted, and a link to the page.
- [ ] A "No results found" message appears with helpful suggestions when there are no matches.
- [ ] The search can be triggered via a keyboard shortcut (e.g., `/` or `Ctrl+K`).
- [ ] Search works without JavaScript where possible (progressive enhancement).
- [ ] Focus moves to the results region after submission for screen reader users.
- [ ] The search component is responsive and usable on mobile viewports.

---

## How to Test

1. **Presence check:** Load every major page (Home, About, Services, Work, Blog, Contact). Confirm the search input is visible in the header.
2. **Keyboard test:** Press `Tab` until focus reaches the search field. Type a query and press `Enter`. Verify results appear without using a mouse.
3. **Screen reader test:** Use VoiceOver (macOS) or NVDA (Windows). Navigate to the search field — confirm it announces its role ("search", "combobox", or "textbox") and label. Submit a search and confirm the results region is announced.
4. **Relevance test:** Search for "rails" or "mobile app". Verify results are ordered by relevance (title matches first, then body-text matches).
5. **Empty-state test:** Search for a nonsense string (e.g., "xyzzy123"). Verify a friendly "no results" message appears.
6. **Mobile test:** On a 375px viewport, confirm the search is accessible (icon toggle or visible input) and results are readable.
7. **Keyboard shortcut test:** Press `/` or `Ctrl+K` from any page. Verify the search input receives focus.

---

## Developer Notes

### Strategy

Add a site-wide search component in the header. For a static/Jamstack site, a client-side search index (e.g., Lunr.js, Fuse.js, or Pagefind) works well without a backend. For a CMS-backed site, use the CMS search API or Algolia.

### Recommended markup

```html
<header class="site-header">
  <nav aria-label="Main navigation">
    <!-- existing nav links -->
  </nav>

  <search>
    <form role="search" action="/search" method="get">
      <label for="site-search" class="sr-only">Search the site</label>
      <input
        type="search"
        id="site-search"
        name="q"
        placeholder="Search…"
        autocomplete="off"
        aria-describedby="search-hint"
      />
      <span id="search-hint" class="sr-only">
        Press Enter to search or Escape to close
      </span>
      <button type="submit" aria-label="Submit search">
        <svg aria-hidden="true" width="20" height="20" viewBox="0 0 24 24">
          <path d="M15.5 14h-.79l-.28-.27A6.47 6.47 0 0 0 16 9.5
                   A6.5 6.5 0 1 0 9.5 16c1.61 0 3.09-.59
                   4.23-1.57l.27.28v.79l5 4.99L20.49
                   19l-4.99-5zm-6 0C7.01 14 5 11.99 5
                   9.5S7.01 5 9.5 5 14 7.01 14 9.5
                   11.99 14 9.5 14z" />
        </svg>
      </button>
    </form>
  </search>
</header>
```

### Results region markup

```html
<section aria-label="Search results" aria-live="polite" id="search-results">
  <h2>Results for "<mark>mobile app</mark>"</h2>
  <p>3 results found</p>

  <ol class="search-results-list">
    <li>
      <a href="/work/mobile-app-case-study">
        <h3>Mobile App Case Study</h3>
        <p>We built a cross-platform <mark>mobile app</mark> for…</p>
      </a>
    </li>
    <!-- more results -->
  </ol>
</section>
```

### CSS

```css
/* Search input */
[role="search"] input[type="search"] {
  min-width: 200px;
  padding: 0.5rem 1rem;
  border: 2px solid #767676;
  border-radius: 6px;
  font-size: 1rem;
  transition: border-color 0.2s ease, box-shadow 0.2s ease;
}

[role="search"] input[type="search"]:focus {
  outline: none;
  border-color: #1a73e8;
  box-shadow: 0 0 0 3px rgba(26, 115, 232, 0.3);
}

/* Screen-reader-only label */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}

/* Results */
.search-results-list li {
  padding: 1rem 0;
  border-bottom: 1px solid #e0e0e0;
}

.search-results-list mark {
  background-color: #fff3cd;
  padding: 0.1em 0.2em;
  border-radius: 2px;
}
```

### JavaScript — keyboard shortcut & client-side search

```js
document.addEventListener('keydown', (e) => {
  const searchInput = document.getElementById('site-search');
  const activeTag = document.activeElement.tagName;

  if ((e.key === '/' || (e.ctrlKey && e.key === 'k')) &&
      activeTag !== 'INPUT' && activeTag !== 'TEXTAREA') {
    e.preventDefault();
    searchInput.focus();
  }
});

// Client-side search with Fuse.js (example)
import Fuse from 'fuse.js';

const fuse = new Fuse(pageIndex, {
  keys: [
    { name: 'title', weight: 2 },
    { name: 'body', weight: 1 },
    { name: 'tags', weight: 1.5 }
  ],
  threshold: 0.3,
  includeMatches: true,
});

function handleSearch(query) {
  const results = fuse.search(query);
  const container = document.getElementById('search-results');

  if (results.length === 0) {
    container.innerHTML = `
      <h2>No results for "${query}"</h2>
      <p>Try different keywords or <a href="/contact">contact us</a> directly.</p>
    `;
  } else {
    // render results list
  }

  container.focus();
}
```

### Components to audit

| Component / Section | Page(s) | What to fix |
|---|---|---|
| Site header | All pages | Add search input with accessible label |
| Mobile nav drawer | All pages (mobile) | Include search field at top of drawer |
| 404 page | /404 | Add search input as recovery path |
| Blog listing | /blog | Add search/filter for posts |

---

## Examples from Other Sites

### Stripe (stripe.com)
- Prominent search accessible via `Ctrl+K` / `⌘K` shortcut.
- Results grouped by category (Docs, API, Support).
- Keyboard-navigable result list with highlighted matches.

### MDN Web Docs (developer.mozilla.org)
- Search in header on every page with `aria-label="Search MDN"`.
- Auto-suggest dropdown with categorized results.
- Search results page shows highlighted excerpts and breadcrumb context.

### GOV.UK (gov.uk)
- Persistent search box in the header — visible on every page.
- Results sorted by relevance with clear titles and excerpts.
- Meets WCAG 2.4.5 by providing search alongside navigation and sitemap.
