# L-56: Wistia Video Embed Lacks Context

**Issue ID:** L-56
**Priority:** Low
**WCAG Criteria:** 1.1.1 Non-text Content (A)
**Affected Personas:** ADHD

---

## User Story

As a **user with ADHD**, I want embedded videos to have a visible title and brief description before I play them so that I can decide whether the video content is relevant to me without committing my attention to watching it.

---

## Acceptance Criteria

- [ ] The Wistia video embed has a visible heading (`<h2>`, `<h3>`, or `<p>` with strong emphasis) immediately above or adjacent to the video player that describes the video's content.
- [ ] A brief (1–2 sentence) description of the video content is displayed near the player, telling the user what to expect.
- [ ] The `<iframe>` or embed `<div>` has a `title` attribute (e.g., `title="LaunchPad Lab company overview video"`).
- [ ] The video's surrounding context makes it clear what the video is about without requiring the user to press play.
- [ ] Screen readers announce the video region with a meaningful label.

---

## How to Test the Change

### Manual Testing
1. Navigate to the page containing the Wistia video embed.
2. **Before playing the video**, confirm:
   - A visible heading/title appears above or next to the player.
   - A short text description explains what the video covers.
3. Inspect the `<iframe>` or Wistia `<div>` element:
   - Verify a `title` attribute exists with a descriptive value.
4. Test with VoiceOver (macOS):
   - Navigate to the video region.
   - Confirm the screen reader announces the video title/label.
5. Test with keyboard only:
   - Tab to the video player.
   - Confirm the focus context (via title or surrounding text) makes the video's purpose clear.

### Automated Testing
1. Check for `title` attribute on video embeds:
   ```javascript
   const iframes = document.querySelectorAll('iframe[src*="wistia"]');
   const wistiaDivs = document.querySelectorAll('.wistia_embed');
   
   iframes.forEach(iframe => {
     expect(iframe.getAttribute('title')).toBeTruthy();
     expect(iframe.getAttribute('title')).not.toBe('');
   });
   ```
2. Run Lighthouse accessibility audit and check for "Frame elements do not have a title" warnings.

---

## Developer Notes

### General Explanation
The Wistia video embed currently appears on the page with no surrounding text to explain its content. Users encountering the video have no way to know what it contains without pressing play. This is especially problematic for users with ADHD who need to evaluate whether content is worth their attention before engaging.

Adding context is straightforward: place a heading and brief description above the player, and add a `title` attribute to the embed element itself.

### Code Examples

```html
<!-- BEFORE: no context -->
<div class="wistia_embed wistia_async_abc123" style="width:640px;height:360px;"></div>

<!-- AFTER: with context -->
<section aria-label="Company overview video">
  <h2>See How We Build Digital Products</h2>
  <p>A 2-minute overview of our approach to custom software development — from discovery through delivery.</p>
  <div class="wistia_embed wistia_async_abc123"
       style="width:640px;height:360px;"
       title="LaunchPad Lab company overview video">
  </div>
</section>
```

If the embed uses an `<iframe>`:
```html
<!-- BEFORE -->
<iframe src="https://fast.wistia.net/embed/iframe/abc123" allowfullscreen></iframe>

<!-- AFTER -->
<iframe src="https://fast.wistia.net/embed/iframe/abc123"
        title="LaunchPad Lab company overview video"
        allowfullscreen>
</iframe>
```

### Wistia-Specific Notes
- Wistia supports a `popover` and `videoFoam` embed style. Regardless of embed type, the surrounding HTML should include context.
- Wistia's embed API allows setting a `name` parameter which populates the `title`:
  ```javascript
  window._wq = window._wq || [];
  _wq.push({
    id: 'abc123',
    options: { playerColor: '#2949E5' },
    onReady: function(video) {
      video.container.setAttribute('title', 'LaunchPad Lab company overview');
    }
  });
  ```

### Components/Files to Audit
- Page template(s) containing the Wistia embed
- WordPress page content (in the block editor or classic editor)
- Any custom shortcode or Wistia plugin configuration
- Theme template files referencing Wistia scripts

---

## Examples from Other Sites

- **Slack:** Video embeds on marketing pages always include a heading, a 1-sentence description, and a `title` attribute on the iframe. Example: "See how Slack brings your team together" followed by a short blurb.
- **Notion:** Feature demo videos have visible titles like "Getting Started with Notion" and captions explaining the content.
- **WebAIM:** Recommends that all embedded media have a descriptive `title` attribute and surrounding context text so users can make informed decisions about engaging with the content.

---

## Additional Context

This fix requires both a **content addition** (visible title/description) and a **technical fix** (`title` attribute on the embed). The content team should provide the video title and description, while the developer adds the `title` attribute and wraps the embed in a semantic container.
