# Clarify the "Technologies" Navigation Label for Non-Technical Users

## Priority: Low

## User Story

As a non-technical website visitor, I want the navigation labels to clearly indicate what I'll find on each page so that I can confidently navigate without worrying I'll land on content I don't understand.

## Acceptance Criteria

- [ ] The "Technologies" navigation label is replaced with a more descriptive, non-intimidating label (e.g., "How We Build," "Tools & Platforms," or "Technologies We Use")
- [ ] If the original label is kept, descriptive subtext is added in the dropdown (e.g., "The tools and platforms we use to build your products")
- [ ] The Technologies page itself leads with a business-friendly introduction, not a raw list of logos or technical names
- [ ] Navigation labels pass a clarity test with non-technical users (no ambiguity about what they'll find)
- [ ] The label change is reflected across all screen sizes (desktop, tablet, mobile)
- [ ] ARIA attributes are correctly applied if subtext is used (`aria-describedby` linking label to description)

## Developer Notes

### General Explanation

The "Technologies" navigation item creates hesitation for non-technical visitors who are unsure whether the page will contain content relevant to them. The fix involves either renaming the nav item or adding contextual subtext that sets expectations.

**Renaming options (in order of recommendation):**
1. "How We Build" — frames technology from the user's perspective
2. "Tools & Platforms" — concrete and non-intimidating
3. "Technologies We Use" — keeps the original word but adds context
4. "Our Tech Stack" — shorter but "stack" is itself jargon (not recommended)

### Code Examples

**Adding descriptive subtext to a nav item (HTML):**

```html
<nav aria-label="Main navigation">
  <ul>
    <li>
      <a href="/technologies" aria-describedby="tech-desc">
        How We Build
      </a>
      <span id="tech-desc" class="nav-description">
        The tools and platforms we use to deliver your projects
      </span>
    </li>
  </ul>
</nav>
```

```css
.nav-description {
  display: block;
  font-size: 0.8rem;
  color: #666;
  font-weight: normal;
  margin-top: 2px;
}
```

**React component with description:**

```jsx
function NavItem({ href, label, description }) {
  const descId = `nav-desc-${label.replace(/\s+/g, '-').toLowerCase()}`;

  return (
    <li className="nav-item">
      <a href={href} aria-describedby={description ? descId : undefined}>
        {label}
      </a>
      {description && (
        <span id={descId} className="nav-description">
          {description}
        </span>
      )}
    </li>
  );
}
```

**Mega-menu dropdown with section descriptions:**

```html
<div class="mega-menu" role="menu" aria-label="How We Build">
  <div class="mega-menu-header">
    <h3>How We Build</h3>
    <p>We use proven, modern technologies to deliver reliable, scalable products. Here's what powers our work.</p>
  </div>
  <div class="mega-menu-grid">
    <!-- Technology category cards -->
  </div>
</div>
```

### Components to Audit

- Main navigation component (desktop and mobile variants)
- Navigation dropdown/mega-menu for the "Technologies" item
- Technologies page header and introductory content
- Any internal links that reference "Technologies" (e.g., footer links, service page cross-links)
- Mobile hamburger menu layout

## Examples From Other Sites

- **Thoughtbot** uses "Services" as their primary nav label and nests technology specifics beneath, so non-technical visitors always see the service/outcome framing first. Technology details are secondary.
- **Pivotal Labs (now part of VMware Tanzu)** uses "What We Do" as the umbrella term, with technology specifics nested in sub-pages. The top-level navigation never assumes the visitor knows or cares about specific technologies.
- **IDEO** labels their equivalent section "Our Work" and organizes by outcome/industry rather than technology. This ensures all visitors — regardless of technical sophistication — can find relevant content.
- **Accenture** uses "Insights & Innovation" rather than "Technologies," framing their tech capabilities as forward-looking business value rather than a list of tools.

## References

- [Margaret Chen Interview — Task 1: First Impressions](../01%20-%20Interviews/margaret-chen-interview.md)
- [Margaret Chen Report — Navigation & Information Architecture Issues](../02%20-%20Reports/margaret-chen-report.md)
- [Main Report — Item 9: "Technologies" Navigation Label Is Unclear](../main-report.md)
