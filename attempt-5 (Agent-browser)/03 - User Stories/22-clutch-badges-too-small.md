# Clutch Award Badges Too Small to Read

**Priority:** Low
**Location:** About page — below "We Help Unleash Your Digital Potential" section
**WCAG:** [1.1.1 Non-text Content (A)](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content), [1.4.4 Resize Text (AA)](https://www.w3.org/WAI/WCAG21/Understanding/resize-text), [1.4.5 Images of Text (AA)](https://www.w3.org/WAI/WCAG21/Understanding/images-of-text)

---

## User Story

> As a **user with low vision or a cognitive disability**,
> I want **award badges to be large enough to read and accompanied by text labels**
> so that **I can understand LaunchPad Lab's credentials without straining to decipher tiny badge images.**

---

## Problem

The About page displays 7–8 Clutch award badges at approximately 80–100px wide. At this size:

- The text within the badges is nearly **illegible** — typically 6–8px rendered font size.
- Users with low vision cannot read the award names, categories, or years even at 200% zoom.
- The badges are images of text, violating WCAG 1.4.5 which discourages images of text when the same visual presentation can be achieved with real text.
- Crowding 7–8 small badges together creates **visual clutter** rather than inspiring trust.
- Screen readers likely receive only generic `alt` text (e.g., "Clutch badge") or none at all, losing the specific award information.

What should be a compelling trust signal instead becomes noise.

---

## Acceptance Criteria

- [ ] Each badge is displayed at a minimum width of 150px (or equivalent responsive size).
- [ ] No more than 3–4 of the most impressive/relevant awards are shown.
- [ ] Each badge has a descriptive text label below or beside it (e.g., "Top Web Developer 2024 — Clutch").
- [ ] Each badge `<img>` has descriptive `alt` text that includes the award name, category, and year.
- [ ] Badge text remains readable at 200% browser zoom.
- [ ] On mobile viewports, badges stack or scroll horizontally with adequate size.
- [ ] An optional "View all awards" link leads to a full list in accessible text format.

---

## How to Test

1. **Visual legibility test:** Open the About page at 100% zoom. Without leaning forward or squinting, try to read each badge. If you cannot identify the award name and year, the badge is too small.
2. **200% zoom test:** Zoom the browser to 200%. Badges and their labels should remain readable without horizontal scrolling.
3. **Screen reader test:** Navigate to the badge section with VoiceOver or NVDA. Confirm each badge announces its full award name (e.g., "Top App Development Company, Clutch 2024"), not just "badge" or "image".
4. **Mobile test:** View the About page on a 375px-wide viewport. Badges should not be squished below readable size.
5. **Contrast check:** If text labels are added, verify they meet 4.5:1 contrast ratio against the background using a tool like [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/).
6. **Count audit:** Confirm no more than 3–4 badges are displayed in the primary section.

---

## Developer Notes

### Strategy

Replace the current row of tiny badge images with a curated selection of 3–4 key awards, displayed at a larger size with real-text labels beneath them. This turns illegible visual clutter into a clear, accessible trust signal.

### Before (current pattern)

```html
<div class="clutch-badges">
  <img src="/badges/clutch-1.png" alt="Clutch badge" width="80" />
  <img src="/badges/clutch-2.png" alt="Clutch badge" width="80" />
  <img src="/badges/clutch-3.png" alt="Clutch badge" width="80" />
  <img src="/badges/clutch-4.png" alt="Clutch badge" width="80" />
  <img src="/badges/clutch-5.png" alt="Clutch badge" width="80" />
  <img src="/badges/clutch-6.png" alt="Clutch badge" width="80" />
  <img src="/badges/clutch-7.png" alt="Clutch badge" width="80" />
</div>
```

### After (improved markup)

```html
<section class="awards" aria-labelledby="awards-heading">
  <h2 id="awards-heading">Awards & Recognition</h2>

  <ul class="awards-grid" role="list">
    <li class="award-card">
      <img
        src="/badges/clutch-top-developer-2024.svg"
        alt=""
        aria-hidden="true"
        class="award-badge"
        width="150"
        height="160"
      />
      <p class="award-label">
        <strong>Top Web Developer</strong>
        <span>Clutch · 2024</span>
      </p>
    </li>

    <li class="award-card">
      <img
        src="/badges/clutch-top-app-company-2024.svg"
        alt=""
        aria-hidden="true"
        class="award-badge"
        width="150"
        height="160"
      />
      <p class="award-label">
        <strong>Top App Development Company</strong>
        <span>Clutch · 2024</span>
      </p>
    </li>

    <li class="award-card">
      <img
        src="/badges/clutch-top-ux-agency-2023.svg"
        alt=""
        aria-hidden="true"
        class="award-badge"
        width="150"
        height="160"
      />
      <p class="award-label">
        <strong>Top UX Agency</strong>
        <span>Clutch · 2023</span>
      </p>
    </li>
  </ul>

  <p>
    <a href="/awards">View all awards →</a>
  </p>
</section>
```

Note: Because the real-text labels carry the information, the badge images are marked `aria-hidden="true"` with empty `alt` to avoid redundant screen reader announcements. The decorative badge image complements the text label.

### Alternative approach — text-only list

```html
<section class="awards" aria-labelledby="awards-heading">
  <h2 id="awards-heading">Awards & Recognition</h2>
  <ul>
    <li>🏆 <strong>Top Web Developer</strong> — Clutch, 2024</li>
    <li>🏆 <strong>Top App Development Company</strong> — Clutch, 2024</li>
    <li>🏆 <strong>Top UX Agency</strong> — Clutch, 2023</li>
  </ul>
</section>
```

### CSS

```css
.awards-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  justify-content: center;
  list-style: none;
  padding: 0;
  margin: 2rem 0;
}

.award-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  max-width: 180px;
}

.award-badge {
  width: 150px;
  height: auto;
  margin-bottom: 0.75rem;
}

.award-label strong {
  display: block;
  font-size: 1rem;
  font-weight: 600;
  color: #1a1a1a;
  line-height: 1.3;
}

.award-label span {
  display: block;
  font-size: 0.875rem;
  color: #555;
  margin-top: 0.25rem;
}

/* Responsive: stack on small screens */
@media (max-width: 600px) {
  .awards-grid {
    flex-direction: column;
    align-items: center;
  }

  .award-card {
    max-width: 250px;
  }

  .award-badge {
    width: 120px;
  }
}
```

### Components to audit

| Component / Section | Page(s) | What to fix |
|---|---|---|
| Clutch badge row | About page | Reduce to 3–4 badges, increase size, add text labels |
| Badge `alt` attributes | About page | Add descriptive alt text for each badge |
| Trust signal section | Homepage (if badges appear) | Apply same pattern |
| Footer badges (if any) | All pages | Ensure same accessible treatment |

---

## Examples from Other Sites

### Thoughtbot (thoughtbot.com)
- Displays 3 key awards with large, readable badge images.
- Each badge is accompanied by a text description of the award.
- Clean layout avoids visual clutter.

### Toptal (toptal.com)
- Shows a curated selection of trust badges at generous sizes (~200px).
- Awards are listed with company name, award title, and year in text.
- Badges link to the verification page on the awarding site.

### 18F (18f.gsa.gov)
- Lists certifications and recognitions as styled text with icons, not as image-of-text badges.
- Fully accessible and readable at any zoom level.
