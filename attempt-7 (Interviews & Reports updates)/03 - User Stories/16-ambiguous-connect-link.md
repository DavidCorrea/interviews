# Provide Descriptive Labels for Ambiguous Links

## Priority: Low

## User Story
As a screen reader user, I want all links to clearly describe their destination so that I know where each link will take me without needing visual context.

## Acceptance Criteria
- [ ] The LinkedIn link on the Contact page has descriptive text or an accessible name that indicates the destination
- [ ] Screen reader users hear "Connect with us on LinkedIn" (or equivalent) when focusing the link
- [ ] All site-wide links with ambiguous names ("Connect", "Read More", "Click Here", "Here", etc.) have been identified and remediated
- [ ] No link is announced only as "Connect, link" or similarly vague text

## Developer Notes

### General Explanation
Links must have descriptive text that conveys their purpose and destination. The LinkedIn link on the Contact page is currently labeled only "Connect," which provides no context to screen reader users. Two approaches fix this: (1) change the visible link text to be descriptive, or (2) keep short visible text and add an `aria-label` for assistive technology.

### Code Examples

**Option 1: Change visible link text**
```html
<!-- Before -->
<a href="https://www.linkedin.com/company/launchpad-lab/">Connect</a>

<!-- After -->
<a href="https://www.linkedin.com/company/launchpad-lab/">Connect with us on LinkedIn</a>
```

**Option 2: Use aria-label (keeps short visible text)**
```html
<a href="https://www.linkedin.com/company/launchpad-lab/" aria-label="Connect with us on LinkedIn">Connect</a>
```

**Note:** When using `aria-label`, it overrides the visible text for screen readers. The visible "Connect" remains for sighted users.

### Components to Audit
- Contact page "Let's Connect" section
- Footer social links (LinkedIn, Twitter, etc.)
- Any page with generic link text ("Read More", "Click Here", "Here", "Learn More" without context)
- Blog post cards and list items
- CTA buttons that are implemented as links

## Examples From Other Sites
- **W3C WAI link purpose guidance:** Links should make sense out of context; avoid "click here" and generic labels
- **Deque University link naming best practices:** Use descriptive link text that states the destination or action; supplement with `aria-label` when design constraints require short visible text

## References
- Main Report Item 16
- WCAG 2.4.4 Link Purpose (In Context)
