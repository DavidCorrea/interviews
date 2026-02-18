# AI-24: Add Accessibility Statement

## Metadata
- **ID:** AI-24
- **Priority:** 4 Low
- **Personas Affected:** 2+ of 16 personas (screen reader, motor impairment — for reporting issues)
- **WCAG Criteria:** Best practice (transparency, accountability)
- **Effort:** Small (1–2 hours)

---

## User Story

**As a** user who encounters an accessibility barrier on the site,

**I want** a dedicated accessibility statement page that explains the site's commitment, conformance target, known limitations, and how to report issues,

**So that** I can understand the organization's accessibility posture and have a clear path to report problems or request accommodations.

---

## Acceptance Criteria

- [ ] Dedicated accessibility statement page exists (e.g., `/accessibility`)
- [ ] Page is linked from footer on all pages
- [ ] Statement includes: WCAG conformance target (e.g., WCAG 2.1 Level AA)
- [ ] Statement includes: known limitations or issues (if any)
- [ ] Statement includes: date of last accessibility assessment
- [ ] Statement includes: contact method for accessibility feedback (email or form)
- [ ] Page has clear heading structure (h1, h2, h3)
- [ ] Link in footer is labeled "Accessibility" or "Accessibility Statement"
- [ ] Page is reachable via keyboard and screen reader

---

## Test Plan

### Footer Link Presence
1. Visit `https://launchpadlab.com/`
2. Scroll to footer
3. **Expected:** "Accessibility" or "Accessibility Statement" link visible
4. **Expected:** Link is in the footer link group (e.g., with Privacy, Terms)
5. Repeat on About, Services, Contact pages
6. **Expected:** Link appears on all pages

### Page Load
1. Click the Accessibility link in footer
2. **Expected:** Dedicated page loads (e.g., `launchpadlab.com/accessibility`)
3. **Expected:** Page has clear title (e.g., "Accessibility Statement")

### Content Verification
1. Read the accessibility statement page
2. **Expected:** WCAG conformance target stated (e.g., "We aim to conform to WCAG 2.1 Level AA")
3. **Expected:** Known limitations section (or "We are not aware of any" if none)
4. **Expected:** Date of last assessment (e.g., "Last assessed: February 2025")
5. **Expected:** Contact method for feedback (e.g., accessibility@launchpadlab.com or contact form link)

### Structure
1. Inspect page with heading structure (browser extension or screen reader)
2. **Expected:** Single h1 (page title)
3. **Expected:** Logical h2/h3 hierarchy for sections
4. **Expected:** No skipped heading levels (e.g., h1 → h3)

### Screen Reader
1. Navigate to footer with screen reader
2. **Expected:** "Accessibility" link is announced and reachable
3. Activate link
4. **Expected:** Page loads; headings and content are announced in logical order

### Contact Method
1. Locate the feedback contact in the statement
2. **Expected:** Email address or link to contact form is provided
3. **Expected:** Contact method is actionable (clickable email or form link)

---

## Developer Notes

### Page Creation
- Create new page at `/accessibility` (or `/accessibility-statement`)
- Add to site navigation/routing
- Add footer link: `<a href="/accessibility">Accessibility</a>`

### Suggested Content Structure
```markdown
# Accessibility Statement

LaunchPad Lab is committed to ensuring our website is accessible to all users,
including people with disabilities. We continually improve the user experience
for everyone and apply relevant accessibility standards.

## Conformance

We aim to conform to the Web Content Accessibility Guidelines (WCAG) 2.1 at
Level AA. These guidelines explain how to make web content more accessible to
people with a wide range of disabilities.

## Known Limitations

[Describe any known issues, e.g., "Some third-party embedded content may not
fully meet our accessibility standards. We are working with vendors to improve
this." Or: "We are not currently aware of any accessibility barriers."]

## Last Assessment

This statement was last reviewed on [DATE]. We regularly assess our site and
update this statement as we make improvements.

## Feedback

If you encounter an accessibility barrier or have suggestions for improvement,
please contact us:

- Email: accessibility@launchpadlab.com
- Or use our [Contact form](/contact)

We aim to respond within [X] business days.
```

### W3C Generator
Use the W3C accessibility statement generator for a template:
https://www.w3.org/WAI/planning/statements/generator/

### Footer Placement
- Add to footer link list (e.g., with Privacy Policy, Terms of Service)
- Ensure sufficient color contrast for link
- Use descriptive link text: "Accessibility" is sufficient

### CMS
- If using WordPress: create new Page, add to menu or footer widget
- If using headless CMS: add page in content model, link from footer component
- If static: add HTML page and footer link

---

## Examples

| Site | Approach |
|------|----------|
| **BBC.com/accessibility** | Comprehensive statement; conformance; feedback form; multiple contact options |
| **Microsoft.com/accessibility** | Detailed statement; product-specific info; feedback mechanism |
| **GitHub.com** | Accessibility page with commitment, conformance, and contact |
| **GOV.UK** | Accessibility statement on all government sites; standard format |
| **W3C** | Statement generator and examples for organizations |
