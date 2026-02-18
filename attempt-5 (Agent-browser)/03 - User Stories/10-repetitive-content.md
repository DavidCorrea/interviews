# Issue 10: Reduce Repetitive Content Across Pages

**Priority:** Medium
**Location:** All pages
**Reported by:** Jamie Rivera (ADHD), Yuki Tanaka (Non-Native English Speaker)

---

## User Story

**As a** user navigating between pages on the LaunchPad Lab website,
**I want** each page to have distinct, unique content that clearly differentiates it from other pages,
**so that** I can tell where I am, avoid re-reading the same information, and trust that navigation is actually working.

---

## Problem

The same content blocks are repeated on nearly every page:

- **Identical contact forms** appear on the Homepage, Services page, About page, Industries page, and the Contact page itself
- **Identical stats** ("12+ years," "730+ projects," "240+ clients") appear on multiple pages in the same format
- **Similar case study carousels** appear on the Homepage, About page, and Contact page
- **The Contact page** displays content that is nearly identical to the Homepage, making users question whether clicking "Contact" actually navigated them to a different page

This creates three distinct problems:

1. **ADHD users** lose context — when the same content appears repeatedly, they can't tell if the page changed or if navigation failed
2. **Non-native speakers** waste cognitive effort re-reading content they've already processed, unsure if subtle differences exist
3. **All users** experience diminished trust — if every page looks the same, the site feels shallow and the navigation feels broken

---

## Acceptance Criteria

- [ ] Full contact forms appear on a maximum of 2 pages: the Contact page and the Homepage
- [ ] All other pages use a simplified CTA section (headline + button linking to Contact page) instead of an embedded form
- [ ] The Contact page has distinct visual styling and content that clearly differentiates it from the Homepage
- [ ] Stats ("12+ years," "730+ projects," "240+ clients") appear on no more than 2 pages, with the primary instance on the About or Homepage
- [ ] Case study carousels on different pages show different selections or are replaced with contextually relevant content
- [ ] Breadcrumbs or a page title indicator is visible on every interior page
- [ ] Each page passes a "distinctiveness test" — a user should be able to identify which page they're on within 3 seconds without looking at the URL

---

## How to Test

1. **Content duplication audit:** Open the Homepage, Services, About, Industries, and Contact pages in separate tabs. Screenshot the bottom half of each page and compare side-by-side. Identify all identical or near-identical sections
2. **Navigation confidence test:** Have a user click "Contact" from the Homepage. Ask them: "Did the page change?" If they hesitate, the differentiation is insufficient
3. **CTA audit:** Verify that only the Homepage and Contact page contain a full form. All other pages should have a simplified CTA
4. **Breadcrumb verification:** Navigate to every interior page and confirm breadcrumbs (or a page title indicator) are visible
5. **Stats audit:** Search the rendered HTML for "730+" and "12+ years" — confirm each appears on no more than 2 pages
6. **Screen reader navigation:** Using VoiceOver/NVDA, navigate from the Homepage to the Contact page. Confirm the screen reader announces a distinct page title and landmark structure

---

## Developer Notes

### Approach

The fix involves: (1) replacing repeated full forms with simplified CTAs, (2) adding breadcrumbs for wayfinding, (3) ensuring each page has unique above-the-fold content, and (4) varying the contextual content per page.

### Simplified CTA Component (replaces full form)

Use this lightweight CTA section on interior pages instead of the full contact form:

```html
<section class="cta-banner" aria-label="Get in touch">
  <div class="cta-banner__inner">
    <h2>Ready to start your project?</h2>
    <p>Tell us about your goals and we'll get back to you within one business day.</p>
    <a href="/contact/" class="btn btn--primary">Contact Us</a>
  </div>
</section>
```

```css
.cta-banner {
  padding: 3rem 2rem;
  background-color: #1a1a2e;
  color: #ffffff;
  text-align: center;
}

.cta-banner h2 {
  font-size: 1.75rem;
  font-weight: 700;
  margin-bottom: 0.75rem;
}

.cta-banner p {
  font-size: 1.125rem;
  line-height: 1.6;
  max-width: 500px;
  margin: 0 auto 1.5rem;
  opacity: 0.9;
}

.cta-banner .btn--primary {
  display: inline-block;
  padding: 0.875rem 2rem;
  background-color: #ffffff;
  color: #1a1a2e;
  font-weight: 600;
  border-radius: 8px;
  text-decoration: none;
  transition: background-color 0.2s ease, transform 0.1s ease;
}

.cta-banner .btn--primary:hover {
  background-color: #e2e8f0;
  transform: translateY(-1px);
}

.cta-banner .btn--primary:focus-visible {
  outline: 3px solid #93c5fd;
  outline-offset: 2px;
}
```

### Adding Breadcrumbs

Add breadcrumbs to every interior page (not the Homepage):

```html
<nav aria-label="Breadcrumb" class="breadcrumbs">
  <ol class="breadcrumbs__list">
    <li class="breadcrumbs__item">
      <a href="/">Home</a>
    </li>
    <li class="breadcrumbs__item" aria-current="page">
      Services
    </li>
  </ol>
</nav>
```

```css
.breadcrumbs {
  padding: 1rem 2rem;
  font-size: 0.875rem;
  color: #6b7280;
}

.breadcrumbs__list {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  list-style: none;
  margin: 0;
  padding: 0;
}

.breadcrumbs__item + .breadcrumbs__item::before {
  content: "/";
  margin-right: 0.5rem;
  color: #d1d5db;
}

.breadcrumbs__item a {
  color: #2563eb;
  text-decoration: none;
}

.breadcrumbs__item a:hover {
  text-decoration: underline;
}

.breadcrumbs__item[aria-current="page"] {
  color: #111827;
  font-weight: 600;
}
```

Use structured data for SEO:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    { "@type": "ListItem", "position": 1, "name": "Home", "item": "https://launchpadlab.com/" },
    { "@type": "ListItem", "position": 2, "name": "Services", "item": "https://launchpadlab.com/services/" }
  ]
}
</script>
```

### Differentiating the Contact Page

The Contact page should look and feel distinct from the Homepage:

```html
<main class="contact-page">
  <nav aria-label="Breadcrumb" class="breadcrumbs"><!-- ... --></nav>

  <section class="contact-hero">
    <h1>Let's Talk About Your Project</h1>
    <p>Fill out the form below and we'll respond within one business day.</p>
  </section>

  <div class="contact-layout">
    <div class="contact-layout__form">
      <!-- THE form — the only one on this page -->
      <form><!-- ... --></form>
    </div>
    <aside class="contact-layout__info">
      <h2>Other Ways to Reach Us</h2>
      <ul>
        <li><strong>Email:</strong> hello@launchpadlab.com</li>
        <li><strong>Phone:</strong> (312) 555-0100</li>
        <li><strong>Office:</strong> Chicago, IL</li>
      </ul>
      <h2>What Happens Next?</h2>
      <ol>
        <li>We review your message (within 4 business hours)</li>
        <li>A team member reaches out to schedule a call</li>
        <li>Free 30-minute discovery conversation</li>
      </ol>
    </aside>
  </div>
</main>
```

### Contextually Varying Content

Instead of identical stats blocks on every page, tailor the content:

| Page | Stats/Social Proof to Show |
|------|---------------------------|
| Homepage | Full stats block (12+ years, 730+ projects, 240+ clients) |
| Services | Relevant service-specific metric ("200+ web applications built") |
| About | Full stats block + team info |
| Industries | Industry-specific case study count ("40+ healthcare projects") |
| Contact | No stats — focus on the form and next steps |

### Components to Audit

- **Contact form component** — Make it conditionally rendered (full form vs. simplified CTA) based on page context
- **Stats block component** — Add a prop or CMS field to control which stats are shown, or remove it from pages where it's redundant
- **Case study carousel component** — Accept a `category` or `featured` prop to show different content per page
- **Page templates** — Audit each template to ensure unique above-the-fold content
- **Layout component** — Add breadcrumbs to the shared layout, conditionally hidden on Homepage
- **`<title>` and `<h1>` tags** — Ensure every page has a unique, descriptive `<title>` and `<h1>`

---

## Examples from Other Sites

### Apple (apple.com)
Each product page has entirely distinct content. The contact/support page is visually and structurally different from product pages. No content is repeated verbatim across pages.

### Mailchimp (mailchimp.com)
Interior pages use a simplified "Get Started" CTA banner instead of embedding the full signup form on every page. The full form lives only on the dedicated signup page.

### Stripe (stripe.com)
Every page has distinct visual treatment. The "Contact Sales" page is clearly different from the homepage — different layout, different color scheme, different content focus. Breadcrumbs appear on documentation and interior pages.

### GOV.UK
Each page has breadcrumb navigation and a unique `<h1>`. Repeated elements (like the search bar) are visually consistent but the page content is always distinct. Users always know where they are.
