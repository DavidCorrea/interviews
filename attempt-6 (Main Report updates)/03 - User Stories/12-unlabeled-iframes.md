# Unlabeled Iframes

## Priority
**Medium**

## User Story
As a screen reader user who encounters iframes on the page, I want each iframe to have a descriptive title, so that I can understand what it contains (e.g., reCAPTCHA, video embeds) and whether I need to interact with it.

## Acceptance Criteria

- [ ] All `<iframe>` elements have a `title` attribute
- [ ] Titles are descriptive and context-specific (e.g., "reCAPTCHA verification," "Video: [video name]")
- [ ] Tracking/analytics iframes are hidden with `aria-hidden="true"` (or excluded from accessibility tree)
- [ ] reCAPTCHA iframe has `title="reCAPTCHA verification"` or similar
- [ ] Video embeds have titles like `title="Video: [video name]"`
- [ ] No iframes have empty or generic titles like "iframe"

## How to Test

1. Open https://launchpadlab.com/ and navigate to pages with forms (contact) and video embeds.
2. Inspect the DOM: search for `<iframe>` elements.
3. Verify each iframe has a `title` attribute with a non-empty, descriptive value.
4. Use a screen reader: navigate to iframes and verify they are announced with meaningful descriptions.
5. Run axe DevTools or WAVE — check for iframe-related accessibility violations.
6. Test on mobile: ensure iframes are not announced as "frame" or "unnamed" with no context.

## Developer Notes

### General Explanation
Multiple `<iframe>` elements exist without `title` attributes. Includes reCAPTCHA, video embeds, and unidentified tracking iframes. Screen readers announce "frame" or "unnamed frame" for untitled iframes, which provides no context for users.

**Solution:** Add `title` attribute to all iframes. Hide tracking/analytics iframes with `aria-hidden="true"` so they are not announced. Use descriptive, context-specific titles for each iframe type.

### Code Examples

**reCAPTCHA iframe:**
```html
<iframe
  title="reCAPTCHA verification"
  src="https://www.google.com/recaptcha/api2/anchor?..."
></iframe>
```

**YouTube embed:**
```html
<iframe
  title="Video: [Video Title from LaunchPad Lab]"
  src="https://www.youtube.com/embed/..."
  allowfullscreen
></iframe>
```

**Vimeo embed:**
```html
<iframe
  title="Video: [Video Title]"
  src="https://player.vimeo.com/video/..."
></iframe>
```

**Tracking/analytics iframe (hide from accessibility tree):**
```html
<iframe
  title="Analytics"
  aria-hidden="true"
  src="..."
></iframe>
```

**React example:**
```jsx
<iframe
  title="reCAPTCHA verification"
  src={recaptchaUrl}
  role="presentation"
/>
```

### Components to Audit
- Contact form sections (reCAPTCHA)
- Video embed sections
- Any third-party widget embeds
- Analytics or tracking iframes
- HubSpot form embeds (if used)

## Examples from Other Sites

- **BBC.com** — All iframes have descriptive titles. Video embeds use titles like "Video: [program name]."
- **YouTube embeds best practice** — Use `title="Video: [video name]"` when embedding. YouTube's iframe embed code supports a `title` attribute.
