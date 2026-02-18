# Video Embed Without Preview Information

**Priority:** Low
**Location:** About page — "Solve complex problems" section
**WCAG:** [1.1.1 Non-text Content (A)](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content), [1.2.1 Audio-only and Video-only (A)](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded), [2.4.6 Headings and Labels (AA)](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels)

---

## User Story

> As a **user on a slow connection, with a cognitive disability, or using a screen reader**,
> I want **embedded videos to display a title, duration, and brief description before I play them**
> so that **I can decide whether to invest my time watching the video without having to start it first.**

---

## Problem

The About page features an embedded video in the "Solve complex problems" section, but the embed provides no contextual information:

- **No visible title** — Users cannot tell what the video is about before clicking play.
- **No duration** — Users don't know if it's a 30-second clip or a 15-minute presentation.
- **No description** — There is no text summary of the video's content.
- **No accessible name** — Screen reader users encounter an `<iframe>` with a generic or missing `title` attribute.
- **No engaging thumbnail** — The default embed frame may show a random frame rather than an intentional, informative preview image.

This forces users to commit to watching before understanding what the video contains. Users with cognitive disabilities, attention limitations, or slow connections are disproportionately affected — they need to make informed decisions about time and bandwidth.

---

## Acceptance Criteria

- [ ] The video has a visible heading (e.g., `<h3>`) immediately above or overlaid on the embed.
- [ ] The video duration is displayed near the title (e.g., "2:30").
- [ ] A 1–2 sentence description appears below the title or below the embed.
- [ ] The `<iframe>` has a descriptive `title` attribute (e.g., `title="LaunchPad Lab team overview — 2 minutes 30 seconds"`).
- [ ] A custom thumbnail image with a centered play button overlay is shown before the video loads.
- [ ] The video does not autoplay.
- [ ] A text transcript or link to transcript is provided below the embed (WCAG 1.2.1).
- [ ] The play button is keyboard accessible and has an accessible label.

---

## How to Test

1. **Visual inspection:** Load the About page. Before playing the video, confirm you can see a title, duration, and short description.
2. **Screen reader test:** Navigate to the video area with VoiceOver/NVDA. Confirm the iframe announces a descriptive title (not "YouTube video player" or blank).
3. **Keyboard test:** Tab to the video. Confirm you can activate the play button with `Enter` or `Space`. If using a facade/placeholder, confirm the facade button is focusable.
4. **No-autoplay test:** Load the page and confirm the video does not begin playing automatically.
5. **Slow connection test:** Throttle the network to "Slow 3G" in DevTools. Confirm the lightweight thumbnail and text information are visible before the iframe loads.
6. **Transcript test:** Check that a text transcript or a link to one is available near the video.

---

## Developer Notes

### Strategy

Wrap the video embed in a semantic container with a heading, duration badge, description, and an optional "facade" pattern that loads the heavy iframe only when the user clicks play. This improves both accessibility and performance.

### Before (current pattern)

```html
<div class="video-section">
  <iframe
    src="https://www.youtube.com/embed/VIDEO_ID"
    frameborder="0"
    allowfullscreen
  ></iframe>
</div>
```

### After (improved markup)

```html
<section class="video-section" aria-labelledby="video-title">
  <h3 id="video-title">How We Solve Complex Problems</h3>

  <div class="video-container">
    <div class="video-facade" id="video-facade">
      <img
        src="/images/video-thumbnail.jpg"
        alt="LaunchPad Lab team collaborating at a whiteboard"
        class="video-thumbnail"
        width="800"
        height="450"
        loading="lazy"
      />
      <button
        type="button"
        class="video-play-btn"
        aria-label="Play video: How We Solve Complex Problems (2 minutes 30 seconds)"
        data-video-id="VIDEO_ID"
      >
        <svg aria-hidden="true" width="68" height="48" viewBox="0 0 68 48">
          <path d="M66.52 7.74c-.78-2.93-2.49-5.41-5.42-6.19
                   C55.79.13 34 0 34 0S12.21.13 6.9 1.55
                   C3.97 2.33 2.27 4.81 1.48 7.74
                   .06 13.05 0 24 0 24s.06 10.95 1.48
                   16.26c.78 2.93 2.49 5.41 5.42 6.19
                   C12.21 47.87 34 48 34 48s21.79-.13
                   27.1-1.55c2.93-.78 4.64-3.26 5.42-6.19
                   C67.94 34.95 68 24 68 24s-.06-10.95-1.48-16.26z"
                fill="#212121" fill-opacity="0.8" />
          <path d="M45 24 27 14v20" fill="#fff" />
        </svg>
      </button>
      <span class="video-duration" aria-hidden="true">2:30</span>
    </div>
  </div>

  <p class="video-description">
    Watch how our cross-functional team approaches product challenges —
    from discovery workshops to iterative delivery.
    <span class="video-duration-text">(2 minutes, 30 seconds)</span>
  </p>

  <details class="video-transcript">
    <summary>Read transcript</summary>
    <div class="transcript-content">
      <p>In this video, the LaunchPad Lab team walks through our approach to
      solving complex product challenges…</p>
      <!-- full transcript text -->
    </div>
  </details>
</section>
```

### CSS

```css
.video-container {
  position: relative;
  max-width: 800px;
  margin: 1rem 0;
}

.video-facade {
  position: relative;
  aspect-ratio: 16 / 9;
  cursor: pointer;
  border-radius: 8px;
  overflow: hidden;
  background: #000;
}

.video-thumbnail {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.video-play-btn {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: none;
  border: none;
  cursor: pointer;
  padding: 0;
  transition: transform 0.2s ease;
}

.video-play-btn:hover,
.video-play-btn:focus-visible {
  transform: translate(-50%, -50%) scale(1.1);
}

.video-play-btn:focus-visible {
  outline: 3px solid #fff;
  outline-offset: 4px;
  border-radius: 4px;
}

.video-duration {
  position: absolute;
  bottom: 12px;
  right: 12px;
  background: rgba(0, 0, 0, 0.8);
  color: #fff;
  font-size: 0.875rem;
  font-weight: 500;
  padding: 0.2em 0.5em;
  border-radius: 4px;
}

.video-description {
  font-size: 0.95rem;
  color: #444;
  max-width: 800px;
  margin-top: 0.75rem;
  line-height: 1.6;
}

.video-duration-text {
  color: #666;
  font-size: 0.85rem;
}

.video-transcript {
  max-width: 800px;
  margin-top: 1rem;
}

.video-transcript summary {
  cursor: pointer;
  color: #1a73e8;
  font-weight: 500;
}

.transcript-content {
  padding: 1rem;
  background: #f8f9fa;
  border-radius: 4px;
  margin-top: 0.5rem;
  line-height: 1.7;
}
```

### JavaScript — facade pattern (lazy-load iframe on click)

```js
document.querySelectorAll('.video-play-btn').forEach((btn) => {
  btn.addEventListener('click', () => {
    const videoId = btn.dataset.videoId;
    const facade = btn.closest('.video-facade');

    const iframe = document.createElement('iframe');
    iframe.src = `https://www.youtube.com/embed/${videoId}?autoplay=1&rel=0`;
    iframe.title = 'How We Solve Complex Problems — 2 minutes 30 seconds';
    iframe.allow = 'accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture';
    iframe.allowFullscreen = true;
    iframe.style.cssText = 'position:absolute;top:0;left:0;width:100%;height:100%;border:0;';

    facade.style.position = 'relative';
    facade.innerHTML = '';
    facade.appendChild(iframe);
  });
});
```

### Components to audit

| Component / Section | Page(s) | What to fix |
|---|---|---|
| Video embed in "Solve complex problems" | About page | Add title, duration, description, facade thumbnail |
| `<iframe>` element | About page | Add descriptive `title` attribute |
| Any other embedded videos | Blog, case studies | Apply same facade pattern with metadata |
| Video transcripts | All video pages | Provide transcript via `<details>` or linked document |

---

## Examples from Other Sites

### Wistia (wistia.com)
- Every embedded video displays a custom thumbnail, visible title, and duration overlay.
- Facade pattern loads the player only on click, improving page load performance.
- Transcripts are available in a tab below the video.

### A List Apart (alistapart.com)
- Video embeds are preceded by a heading and a short paragraph describing the content.
- Duration is noted in the intro text.
- Transcript is provided as expandable content below the video.

### TED (ted.com)
- Talks display title, speaker, duration, and a 1-sentence synopsis before the player.
- Full interactive transcript syncs with playback.
- Custom, high-quality thumbnails with a prominent play button.
