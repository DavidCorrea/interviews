# Add Descriptive `title` Attributes to All Iframes

## Priority: High

## User Story

As a screen reader user, I want every iframe to have a descriptive title so that I know what content it contains and whether I need to interact with it.

## Acceptance Criteria

- [ ] Every interactive iframe (CAPTCHA, embedded video, embedded forms) has a `title` attribute describing its purpose
- [ ] CAPTCHA iframes use a title such as "Security verification" or "CAPTCHA - prove you are human"
- [ ] Embedded video iframes use a title such as "[Video topic] - embedded video"
- [ ] Decorative or tracking-only iframes use `aria-hidden="true"` and `tabindex="-1"` to remove them from the accessibility tree
- [ ] Screen readers announce the iframe's purpose (e.g., "Security verification, frame") instead of "frame" with no context
- [ ] No iframe on the site lacks either a descriptive `title` or `aria-hidden="true"` (for decorative only)

## Developer Notes

### General Explanation

Multiple iframes across the site (CAPTCHA, embedded widgets, possibly video) have no `title` attribute. Screen readers announce them only as "frame" with no context. Users cannot determine whether an iframe is relevant, interactive, or safe to skip. Violates WCAG 4.1.2 (Name, Role, Value).

**Fix:** Add a `title` attribute to every `<iframe>` that conveys its purpose. For decorative or tracking-only iframes that users should not interact with, use `aria-hidden="true"` and `tabindex="-1"` to hide them from assistive technology.

### Code Examples

**CAPTCHA iframe:**

```html
<!-- Before -->
<iframe src="https://captcha-provider.com/widget" ...></iframe>

<!-- After -->
<iframe
  src="https://captcha-provider.com/widget"
  title="Security verification - prove you are human"
  ...>
</iframe>
```

**Embedded video (e.g., YouTube, Vimeo):**

```html
<!-- Before -->
<iframe src="https://www.youtube.com/embed/VIDEO_ID" ...></iframe>

<!-- After -->
<iframe
  src="https://www.youtube.com/embed/VIDEO_ID"
  title="LaunchPad Lab company overview - embedded video"
  ...>
</iframe>
```

**Embedded form or widget:**

```html
<iframe
  src="/embed/contact-form"
  title="Contact form - request a consultation"
  ...>
</iframe>
```

**Decorative or tracking-only iframe (hide from AT):**

```html
<!-- Analytics, tracking pixels, or purely decorative iframes -->
<iframe
  src="https://analytics.example.com/pixel"
  aria-hidden="true"
  tabindex="-1"
  ...>
</iframe>
```

**React component with dynamic title:**

```jsx
function CaptchaIframe({ src }) {
  return (
    <iframe
      src={src}
      title="Security verification - prove you are human"
      role="application"
      aria-label="Security verification"
    />
  );
}
```

**Note:** The `title` attribute is the primary mechanism for naming iframes. `aria-label` can supplement but is not a replacement for `title` in all screen readers for iframes.

### Components to Audit

- Contact form (CAPTCHA iframe)
- Any embedded widgets (calendars, maps, forms)
- Video embeds (YouTube, Vimeo, etc.)
- Footer iframes (e.g., newsletter signup, social widgets)
- Third-party script injections that add iframes (check for reCAPTCHA, HubSpot, etc.)

## Examples From Other Sites

- **YouTube** embeds include a `title` attribute when you use their standard embed code. The title typically describes the video (e.g., "Video title - YouTube"). This pattern is recommended in their [embed documentation](https://developers.google.com/youtube/player_parameters).
- **gov.uk** follows the [GDS design system](https://design-system.service.gov.uk/) guidance for iframes. Their embedded content (e.g., maps, forms) includes descriptive `title` attributes. CAPTCHA and security widgets are labeled with clear, user-friendly descriptions.
- **W3C WAI** tutorials recommend providing a `title` for every iframe that conveys its purpose, and hiding purely decorative iframes from the accessibility tree.

## References

- [James Okafor Interview — Tasks 1 & 3](../01%20-%20Interviews/james-okafor-interview.md)
- [James Okafor Report — Interactive Widget Issues](../02%20-%20Reports/james-okafor-report.md)
- [Main Report — Item 12: Unlabeled Iframes Throughout the Site](../main-report.md)
