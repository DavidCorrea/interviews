# Leadership Contact Info

## Priority
**Low**

## User Story
As a potential client interested in sales or business development, I want direct contact information (email or scheduling links) for customer-facing leadership team members, so that I can reach the right person without relying solely on a general contact form.

## Acceptance Criteria

- [ ] Customer-facing roles (Head of Sales, Business Development, etc.) have email addresses or "Schedule a Call" links
- [ ] Email links use `mailto:` and are keyboard accessible
- [ ] "Schedule a Call" links point to Calendly or similar scheduling tool
- [ ] Contact info is visible and not hidden behind multiple clicks
- [ ] Links have descriptive `aria-label` or visible text (e.g., "Email [Name]" or "Schedule a call with [Name]")
- [ ] At least 2–3 customer-facing team members have direct contact options

## How to Test

1. Navigate to the About page on https://launchpadlab.com/.
2. Locate the leadership team section (15 members).
3. Identify customer-facing roles: Head of Sales, Business Development, Partners, etc.
4. Verify these roles have email or "Schedule a Call" links in addition to LinkedIn.
5. Click email links — confirm `mailto:` opens correctly.
6. Click "Schedule a Call" links — confirm they open scheduling tool.
7. Use keyboard navigation — verify all contact links are focusable and activatable.
8. Use a screen reader — confirm link purpose is clear.

## Developer Notes

### General Explanation
The About page lists 15 leadership team members with LinkedIn links only. No email or direct contact for customer-facing roles. Potential clients who want to speak with sales or business development may not know how to reach the right person. Adding email or scheduling links reduces friction and aligns with consulting firm best practices.

**Solution:** Add email addresses for customer-facing team members (Head of Sales, Business Development). Consider "Schedule a Call" links for sales contacts. Use `mailto:` links or integrate Calendly/Cal.com. Ensure links are accessible and clearly labeled.

### Code Examples

**Team member card with email and schedule link:**
```html
<div class="team-member">
  <img src="photo.jpg" alt="Jane Smith" />
  <h3>Jane Smith</h3>
  <p class="role">Head of Sales</p>
  <div class="contact-links">
    <a href="https://linkedin.com/in/janesmith" aria-label="Jane Smith on LinkedIn">
      LinkedIn
    </a>
    <a href="mailto:jane@launchpadlab.com" aria-label="Email Jane Smith">
      Email
    </a>
    <a href="https://calendly.com/launchpadlab/jane" aria-label="Schedule a call with Jane Smith">
      Schedule a Call
    </a>
  </div>
</div>
```

**React team member component:**
```jsx
const TeamMember = ({ name, role, photo, linkedIn, email, calendly }) => (
  <div className="team-member">
    <img src={photo} alt={name} />
    <h3>{name}</h3>
    <p className="role">{role}</p>
    <div className="contact-links">
      {linkedIn && (
        <a href={linkedIn} aria-label={`${name} on LinkedIn`}>
          LinkedIn
        </a>
      )}
      {email && (
        <a href={`mailto:${email}`} aria-label={`Email ${name}`}>
          Email
        </a>
      )}
      {calendly && (
        <a href={calendly} aria-label={`Schedule a call with ${name}`}>
          Schedule a Call
        </a>
      )}
    </div>
  </div>
);
```

**Data structure for customer-facing roles:**
```javascript
const teamMembers = [
  {
    name: 'Jane Smith',
    role: 'Head of Sales',
    email: 'jane@launchpadlab.com',
    calendly: 'https://calendly.com/launchpadlab/jane',
    linkedIn: 'https://linkedin.com/in/janesmith',
  },
  // ...
];
```

### Components to Audit
- About page leadership section
- Team member card component
- CMS or data source for team member info
- Any conditional rendering of contact links

## Examples from Other Sites

- **Thoughtbot.com** — Team page includes email links for team leads and partners. Direct contact for key roles.
- **Consulting firm websites** — Typically show direct contact (email or scheduling) for partners and directors.
- **Basecamp (basecamp.com)** — Team page with clear contact options for different roles.
