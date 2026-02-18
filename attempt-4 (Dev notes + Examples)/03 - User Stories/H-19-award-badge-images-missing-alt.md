# H-19: Award/Badge Images Missing Alt Text

**Issue ID:** H-19
**Priority:** High
**WCAG Criteria:** 1.1.1 Non-text Content (A)
**Affected Personas:** Screen Reader, Blue-Yellow Color Blind, Red-Green Color Blind, Low Vision Screen Magnifier, Low Vision, Skeptical User, Situational Contrast

---

## User Story

**As a** screen reader user evaluating the company's credibility,
**I want** award and certification badge images to have descriptive alt text,
**so that** I can understand the company's accolades and ratings without relying on visual information.

---

## Acceptance Criteria

- [ ] Every Clutch award/badge `<img>` has a meaningful `alt` attribute that describes the award, rating, ranking, and year (e.g., `alt="Clutch Top B2B Company 2024 — 4.9 star rating"`).
- [ ] No award badge image uses `alt=""` (empty alt) since these convey meaningful credibility information.
- [ ] Alt text is concise (under 125 characters) but includes the key data: source (Clutch), award type, rating/ranking, and year.
- [ ] When images fail to load, the alt text serves as a meaningful fallback.
- [ ] If badges are wrapped in links, the link's accessible name includes the badge context (e.g., `aria-label="View Clutch profile — Top B2B Company 2024"`).

---

## How to Test the Change

### Manual Testing

1. **Screen reader audit:** Navigate to the badges section using VoiceOver (macOS) or NVDA (Windows). Tab or use the image navigation shortcut (`G` in NVDA) to land on each badge image. Confirm the screen reader announces the award name, rating, and year.
2. **Images-off test:** Disable images in browser DevTools (or use a text-only browser). Confirm meaningful fallback text appears where each badge was.
3. **Visual inspection:** Right-click each badge image → Inspect → verify the `alt` attribute is populated with a descriptive string, not empty.

### Automated Testing

- Run `axe-core` or Lighthouse accessibility audit. Confirm no "Images must have alternate text" violations on badge images.
- Use a custom script to query `document.querySelectorAll('img[alt=""]')` and verify none of the results are award/badge images.

```javascript
// Quick console check
document.querySelectorAll('img[alt=""]').forEach(img => {
  if (img.src.includes('clutch') || img.closest('.awards, .badges')) {
    console.warn('Badge image missing alt:', img.src);
  }
});
```

---

## Developer Notes

### General Approach

Add descriptive `alt` text to all seven Clutch badge images. The alt text should communicate the same credibility information that a sighted user gets from viewing the badge.

### Current State (Problem)

```html
<img src="/wp-content/uploads/clutch-badge-2024.png" alt="">
<img src="/wp-content/uploads/clutch-top-company.png" alt="">
<!-- ... 5 more badges with alt="" -->
```

### Recommended Fix

```html
<img
  src="/wp-content/uploads/clutch-badge-2024.png"
  alt="Clutch Top B2B Company 2024 — 4.9 out of 5 stars"
>
<img
  src="/wp-content/uploads/clutch-top-company.png"
  alt="Clutch Top 1000 Global Company 2024"
>
<img
  src="/wp-content/uploads/clutch-top-developer-chicago.png"
  alt="Clutch Top Software Developer in Chicago 2024"
>
```

### If Badges Link to External Profiles

```html
<a href="https://clutch.co/profile/launchpad-lab"
   aria-label="View LaunchPad Lab's Clutch profile — Top B2B Company 2024, 4.9 stars">
  <img
    src="/wp-content/uploads/clutch-badge-2024.png"
    alt="Clutch Top B2B Company 2024 — 4.9 out of 5 stars"
  >
</a>
```

### Components / Files to Audit

- Awards/badges section template (e.g., `partials/badges.php`, `components/awards-section`)
- Any ACF or custom field group for badge images
- Media Library entries for each badge image (alt text may be stored in WordPress media metadata)
- Homepage and About page templates where badges appear

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **Accenture** | Badge images have alt text like "Fortune World's Most Admired Companies 2024" | Conveys the award name and year without visual dependency. |
| **Deloitte** | Uses text + image badges with `alt` matching the visible badge text | Ensures screen reader and visual experiences align. |
| **HubSpot** | Partner badges include `alt="HubSpot Certified Partner — Gold Tier"` | Describes certification level, not just "badge." |
