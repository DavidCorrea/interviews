# AI-21: Use "Contact" as Primary Navigation Label

## Metadata
- **ID:** AI-21
- **Priority:** 3 Medium
- **Personas Affected:** 3+ of 16 personas (senior, non-native speaker, cognitive disability)
- **WCAG Criteria:** 2.4.4 Link Purpose (A), 3.2.4 Consistent Identification (AA)
- **Effort:** Small (30 minutes)

---

## User Story

**As a** senior user, non-native English speaker, or someone who expects conventional website patterns,

**I want** the main navigation to say "Contact" or "Contact Us" instead of "Connect with an Expert",

**So that** I can immediately identify how to reach the company without guessing or translating unconventional phrasing.

---

## Acceptance Criteria

- [ ] Primary navigation link text is "Contact" or "Contact Us"
- [ ] Clicking the link navigates to the contact page
- [ ] Footer includes a "Contact" link with consistent labeling
- [ ] Screen reader announces "Contact" (or "Contact Us") as the link purpose
- [ ] "Connect with an Expert" may remain as CTA text on the Contact page or as a button within page content
- [ ] Label is consistent across all pages (3.2.4 Consistent Identification)
- [ ] No other page uses "Connect with an Expert" as the primary nav label

---

## Test Plan

### Visual Inspection
1. Visit `https://launchpadlab.com/`
2. Locate the main navigation (typically top-right or in hamburger menu)
3. **Expected:** Link reads "Contact" or "Contact Us"
4. **Fail:** Link reads "Connect with an Expert" or similar unconventional label

### Navigation Flow
1. Click the Contact link in the main nav
2. **Expected:** Browser navigates to contact page (e.g., `/contact` or `/connect`)
3. **Expected:** Page loads with contact form or contact information

### Footer Consistency
1. Scroll to footer on any page
2. **Expected:** Footer contains "Contact" or "Contact Us" link
3. **Expected:** Footer label matches main nav label (or is clearly "Contact")
4. Click footer Contact link — navigates to same contact destination

### Screen Reader Test
1. Enable VoiceOver (Mac) or NVDA (Windows)
2. Navigate to the site and tab to the Contact link
3. **Expected:** Screen reader announces "Contact" or "Contact Us" (not "Connect with an Expert")
4. Link purpose must be determinable from link text alone (2.4.4)

### Cross-Page Consistency
1. Visit Home, About, Services, Work, and Contact pages
2. On each page, check main nav and footer
3. **Expected:** "Contact" label appears consistently (3.2.4)
4. **Expected:** Same link destination across all pages

### Secondary CTA Preservation
1. Visit the Contact page
2. **Expected:** "Connect with an Expert" may appear as CTA button text, heading, or subheading
3. **Expected:** This is acceptable — the fix applies to nav/footer, not page content

---

## Developer Notes

### HTML Changes
```html
<!-- Before -->
<nav>
  <a href="/contact">Connect with an Expert</a>
</nav>

<!-- After -->
<nav>
  <a href="/contact">Contact</a>
</nav>
```

### Footer Update
```html
<footer>
  <a href="/contact">Contact</a>
  <!-- Other footer links -->
</footer>
```

### CMS / Framework Considerations
- If using WordPress: Appearance → Menus → Edit nav item label to "Contact"
- If using a headless CMS: Update the menu item `label` or `title` field in the CMS
- If hardcoded: Global find/replace for nav and footer instances

### Preserving "Connect with an Expert"
- Keep as hero CTA on Contact page: "Connect with an Expert" button
- Keep as form submit button: "Connect with an Expert"
- Keep as page heading or subheading on Contact page
- Do NOT use as primary nav or footer link label

### Accessibility
- Link text must describe destination (2.4.4)
- "Contact" is universally understood; "Connect with an Expert" requires interpretation
- Avoid redundant "Contact - Connect with an Expert" — pick one for nav

---

## Examples

| Site | Approach |
|------|----------|
| **Accenture.com** | Main nav: "Contact Us" |
| **Deloitte.com** | Footer and nav: "Contact" |
| **McKinsey.com** | "Contact" in main navigation |
| **IBM.com** | "Contact IBM" in nav |
| **Salesforce.com** | "Contact" or "Contact Us" in nav and footer |
| **Microsoft.com** | "Contact" in footer |

Nearly every professional B2B site uses "Contact" or "Contact Us" as the primary label. This is an established convention that reduces cognitive load and supports international users.
