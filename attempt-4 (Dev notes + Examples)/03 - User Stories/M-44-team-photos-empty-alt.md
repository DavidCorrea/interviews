# M-44: About Page Team Photos Have Empty Alt Text

**Issue ID:** M-44
**Priority:** Medium
**WCAG Criteria:** 1.1.1 Non-text Content (A)
**Affected Personas:** Skeptical User

---

## User Story

As a **potential client evaluating this company**, I want **team member photos to include the person's name and role in the alt text** so that **I can learn about the leadership team even when images don't load, and so screen reader users receive the same trust-building information as sighted users.**

---

## Acceptance Criteria

- [ ] All team member `<img>` elements on the About page have descriptive `alt` text that includes at minimum the person's **name** and **role/title**.
- [ ] Alt text follows a consistent format, e.g., `alt="Jane Smith, VP of Engineering"`.
- [ ] No team member photos have `alt=""` (empty alt).
- [ ] If team members also appear on other pages (e.g., case study author bios), those images also have proper alt text.
- [ ] Alt text is concise (under 125 characters) and does not include redundant phrasing like "Photo of" or "Image of" (since screen readers already announce `<img>`).

---

## How to Test the Change

### Manual Testing

1. Navigate to the About page.
2. Open DevTools and inspect each team member `<img>` element.
3. Verify each has an `alt` attribute containing the person's name and title.
4. Disable images (Chrome DevTools > Settings > Show images unchecked, or use the Web Developer extension) and confirm the alt text displays meaningfully in place of images.
5. Use VoiceOver or NVDA to navigate through the team section — confirm each person is announced with name and role.

### Automated Testing

1. Run axe DevTools on the About page — check for "Images must have alternate text" violations.
2. Script to audit alt text:
   ```javascript
   document.querySelectorAll('.team-section img, .leadership img').forEach(img => {
     const alt = img.getAttribute('alt');
     console.log(`${img.src}: alt="${alt}"`);
     if (!alt || alt.trim() === '') {
       console.warn('MISSING ALT:', img.src);
     }
   });
   ```
3. Run `pa11y` or `html-validate` on the About page URL.

---

## Developer Notes

### General Explanation

Fifteen leadership team photos on the About page have `alt=""`, which tells screen readers to skip them entirely (treating them as decorative). However, team photos are **not decorative** — they convey meaningful content about who leads the company, which is critical for trust-building. Each photo should have alt text that includes the person's name and role. If the name and role are also present as visible text adjacent to the photo, the alt can be simpler (just the name) since the role is already programmatically associated.

### Code Examples

**Before (current):**
```html
<div class="team-member">
  <img src="/images/jane-smith.jpg" alt="">
  <h3>Jane Smith</h3>
  <p>VP of Engineering</p>
</div>
```

**After — Option A (name + role in alt):**
```html
<div class="team-member">
  <img src="/images/jane-smith.jpg" alt="Jane Smith, VP of Engineering">
  <h3>Jane Smith</h3>
  <p>VP of Engineering</p>
</div>
```

**After — Option B (name only, since role is adjacent):**
```html
<div class="team-member">
  <img src="/images/jane-smith.jpg" alt="Jane Smith">
  <h3>Jane Smith</h3>
  <p>VP of Engineering</p>
</div>
```

**After — Option C (use `figure` for better grouping):**
```html
<figure class="team-member">
  <img src="/images/jane-smith.jpg" alt="Jane Smith">
  <figcaption>
    <strong>Jane Smith</strong>
    <span>VP of Engineering</span>
  </figcaption>
</figure>
```

**WordPress — if using ACF or custom fields, ensure alt is populated:**
```php
<?php
$team_members = get_field('team_members');
foreach ($team_members as $member) :
  $name = $member['name'];
  $role = $member['role'];
  $photo = $member['photo']; // ACF image array
?>
  <div class="team-member">
    <img src="<?= esc_url($photo['url']) ?>"
         alt="<?= esc_attr($name . ', ' . $role) ?>">
    <h3><?= esc_html($name) ?></h3>
    <p><?= esc_html($role) ?></p>
  </div>
<?php endforeach; ?>
```

### Components / Files to Audit

- About page template (e.g., `page-about.php` or Elementor/Gutenberg block)
- Team member component or widget
- WordPress Media Library — check if alt text is set on the uploaded images themselves
- Any other page featuring team member photos (e.g., individual service pages, case study author bios)

---

## Examples from Other Sites

- **Thoughtbot.com:** Team page photos use `alt="Person Name, Job Title"` consistently for every team member.
- **Basecamp.com:** About page team photos include name and role: `alt="Jason Fried, Co-founder & CEO"`.
- **Automattic.com:** Team member photos use just the name (`alt="Matt Mullenweg"`) with the role provided in adjacent text.
- **18F (government digital agency):** Team photos follow the pattern `alt="First Last — Role"` per their accessibility guidelines.
