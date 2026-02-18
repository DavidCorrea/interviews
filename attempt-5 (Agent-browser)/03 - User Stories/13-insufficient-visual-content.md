# Issue 13: Add Visual Content to Supplement Text-Heavy Pages

**Priority:** Medium
**Location:** Homepage, Services page, Industries page
**Reported by:** Sam Chen (Dyslexia), Yuki Tanaka (Non-Native English Speaker)

---

## User Story

**As a** user who processes information more effectively through visuals than through dense text,
**I want** illustrations, icons, diagrams, and other visual content alongside service descriptions and process explanations,
**so that** I can understand what LaunchPad Lab does without relying entirely on reading complex text.

---

## Problem

Core informational content across the site is almost entirely text-based:

- **Service descriptions** — Text-only cards with no icons or illustrations to visually represent each service
- **Process section** — The "Discover → Deliver → Release" process is described in text only. There is no visual flow diagram, timeline, or step illustration to help users understand the sequence
- **Industry pages** — Text descriptions of industries served with no iconography, imagery, or case study screenshots
- **About page** — Mission, values, and capabilities conveyed entirely through paragraphs

This disproportionately impacts:

- **Dyslexic users** who experience reading fatigue quickly and rely on visual cues to extract meaning. A page that is "all text" is exhausting and may cause them to leave before understanding the content.
- **Non-native English speakers** who can often understand a concept through a diagram or icon much faster than by reading and mentally translating a paragraph of complex English.

The site's visual design uses photography and gradients for aesthetic effect but not for information delivery. Decorative images don't help users understand what the company does.

---

## Acceptance Criteria

- [ ] Each service card on the Homepage and Services page includes a meaningful icon or illustration that visually represents the service
- [ ] Icons are not purely decorative — they communicate the concept of the service (e.g., a mobile phone for Mobile App Development, a paintbrush/wireframe for Product Strategy & Design)
- [ ] The "Discover → Deliver → Release" process has a visual diagram — either a flowchart, timeline, or step-by-step illustration with icons
- [ ] The process diagram is accessible: it includes `alt` text (if an image) or uses semantic HTML with ARIA labels (if SVG/HTML)
- [ ] At least one explanatory video or animated explainer is available for a key service area (e.g., "How We Work")
- [ ] Industry cards include representative icons or imagery for each industry
- [ ] All visual content has appropriate alternative text for screen readers
- [ ] Visual content renders correctly on mobile viewports without breaking layout

---

## How to Test

1. **Visual audit:** Navigate to the Homepage, Services page, and Industries page. For each major content section, verify there is at least one visual element (icon, illustration, diagram, or video) that communicates information — not just decoration
2. **Remove-the-text test:** Cover (or mentally ignore) all text on the service cards. Can you still get a rough idea of what each service is from the icon/illustration alone? If not, the visuals aren't informative enough
3. **Process diagram test:** Find the Discover → Deliver → Release section. Verify a visual diagram exists. Confirm it communicates the sequential nature of the process visually (arrows, numbered steps, timeline layout)
4. **Alt text audit:** Inspect each icon, illustration, and diagram. Verify `alt` attributes (for `<img>`) or `aria-label` (for `<svg>`) are present and descriptive. Decorative elements should have `alt=""` or `aria-hidden="true"`
5. **Screen reader test:** Navigate the Services page with VoiceOver or NVDA. Confirm icons are either properly described or hidden from the accessibility tree (if the adjacent text already describes the service)
6. **Video accessibility test:** If a video is present, verify it has captions and a transcript available
7. **Mobile test (375px):** Confirm icons and diagrams resize properly and don't overflow or overlap text

---

## Developer Notes

### Approach

The fix involves: (1) adding informative icons to service and industry cards, (2) creating a visual process diagram for the Discover → Deliver → Release workflow, (3) optionally adding an explainer video, and (4) providing text-to-speech or read-aloud functionality.

### Service Card Icons

Add SVG icons to each service card. Use inline SVGs for styling flexibility or an icon sprite:

```html
<div class="service-card">
  <div class="service-card__icon" aria-hidden="true">
    <svg width="48" height="48" viewBox="0 0 48 48" fill="none">
      <!-- Web app icon: browser window with code brackets -->
      <rect x="4" y="8" width="40" height="32" rx="4" stroke="currentColor" stroke-width="2"/>
      <line x1="4" y1="16" x2="44" y2="16" stroke="currentColor" stroke-width="2"/>
      <circle cx="10" cy="12" r="1.5" fill="currentColor"/>
      <circle cx="15" cy="12" r="1.5" fill="currentColor"/>
      <circle cx="20" cy="12" r="1.5" fill="currentColor"/>
      <path d="M18 28L14 32L18 36" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
      <path d="M30 28L34 32L30 36" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
    </svg>
  </div>
  <h3>Web App Development</h3>
  <p>Custom web applications — portals, dashboards, and internal tools built for your business.</p>
</div>
```

```css
.service-card {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  padding: 2rem;
  background: #ffffff;
  border-radius: 12px;
  border: 1px solid #e5e7eb;
  transition: box-shadow 0.2s ease;
}

.service-card:hover {
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08);
}

.service-card__icon {
  width: 3.5rem;
  height: 3.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #eff6ff;
  border-radius: 12px;
  color: #2563eb;
  margin-bottom: 1.25rem;
  padding: 0.5rem;
}

.service-card__icon svg {
  width: 2rem;
  height: 2rem;
}
```

Since the icons are accompanied by text labels and descriptions, mark them as `aria-hidden="true"` to avoid redundant announcements for screen reader users.

### Visual Process Diagram

Build the Discover → Deliver → Release process as an accessible HTML diagram rather than a flat image:

```html
<section class="process-diagram" aria-label="Our development process">
  <h2>How We Work</h2>
  <div class="process-diagram__steps">

    <div class="process-step">
      <div class="process-step__number" aria-hidden="true">1</div>
      <div class="process-step__icon" aria-hidden="true">
        <svg width="40" height="40" viewBox="0 0 40 40">
          <!-- Magnifying glass / compass icon -->
          <circle cx="18" cy="18" r="10" stroke="currentColor" stroke-width="2" fill="none"/>
          <line x1="25" y1="25" x2="34" y2="34" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
        </svg>
      </div>
      <h3 class="process-step__title">Discover</h3>
      <p class="process-step__desc">
        We learn about your business, users, and goals.
        Then we define the right product to build.
      </p>
    </div>

    <div class="process-step__connector" aria-hidden="true">
      <svg width="48" height="24" viewBox="0 0 48 24">
        <path d="M0 12 H40 L36 6 M40 12 L36 18" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round"/>
      </svg>
    </div>

    <div class="process-step">
      <div class="process-step__number" aria-hidden="true">2</div>
      <div class="process-step__icon" aria-hidden="true">
        <svg width="40" height="40" viewBox="0 0 40 40">
          <!-- Code/build icon -->
          <rect x="6" y="6" width="28" height="28" rx="4" stroke="currentColor" stroke-width="2" fill="none"/>
          <path d="M14 16L10 20L14 24" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
          <path d="M26 16L30 20L26 24" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
          <line x1="22" y1="14" x2="18" y2="26" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
        </svg>
      </div>
      <h3 class="process-step__title">Deliver</h3>
      <p class="process-step__desc">
        We design, build, and test your software in short cycles.
        You see progress every two weeks.
      </p>
    </div>

    <div class="process-step__connector" aria-hidden="true">
      <svg width="48" height="24" viewBox="0 0 48 24">
        <path d="M0 12 H40 L36 6 M40 12 L36 18" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round"/>
      </svg>
    </div>

    <div class="process-step">
      <div class="process-step__number" aria-hidden="true">3</div>
      <div class="process-step__icon" aria-hidden="true">
        <svg width="40" height="40" viewBox="0 0 40 40">
          <!-- Rocket / launch icon -->
          <path d="M20 6C20 6 32 12 32 24L28 28L20 24L12 28L8 24C8 12 20 6 20 6Z" stroke="currentColor" stroke-width="2" fill="none"/>
          <circle cx="20" cy="18" r="3" stroke="currentColor" stroke-width="2" fill="none"/>
        </svg>
      </div>
      <h3 class="process-step__title">Release</h3>
      <p class="process-step__desc">
        We launch your product, monitor performance,
        and provide ongoing support and updates.
      </p>
    </div>

  </div>
</section>
```

```css
.process-diagram {
  padding: 4rem 2rem;
  text-align: center;
}

.process-diagram h2 {
  font-size: 2rem;
  font-weight: 700;
  margin-bottom: 3rem;
}

.process-diagram__steps {
  display: flex;
  align-items: flex-start;
  justify-content: center;
  gap: 0;
  max-width: 900px;
  margin: 0 auto;
}

.process-step {
  flex: 1;
  max-width: 260px;
  text-align: center;
  padding: 0 1rem;
}

.process-step__number {
  width: 2rem;
  height: 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #2563eb;
  color: #ffffff;
  font-size: 0.875rem;
  font-weight: 700;
  border-radius: 50%;
  margin: 0 auto 1rem;
}

.process-step__icon {
  width: 4rem;
  height: 4rem;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #eff6ff;
  border-radius: 50%;
  color: #2563eb;
  margin: 0 auto 1rem;
}

.process-step__title {
  font-size: 1.25rem;
  font-weight: 700;
  margin-bottom: 0.75rem;
}

.process-step__desc {
  font-size: 1rem;
  line-height: 1.7;
  color: #4b5563;
}

.process-step__connector {
  display: flex;
  align-items: center;
  padding-top: 3.5rem;
  color: #d1d5db;
  flex-shrink: 0;
}

@media (max-width: 768px) {
  .process-diagram__steps {
    flex-direction: column;
    align-items: center;
    gap: 1rem;
  }

  .process-step__connector {
    transform: rotate(90deg);
    padding-top: 0;
  }
}
```

### Explainer Video Embed

If adding a video, use an accessible embed with captions:

```html
<section class="explainer-video" aria-label="How we work video">
  <h2>See How We Work</h2>
  <p>A 2-minute overview of our process, from discovery to launch.</p>
  <div class="explainer-video__wrapper">
    <iframe
      src="https://www.youtube.com/embed/VIDEO_ID?cc_load_policy=1"
      title="LaunchPad Lab: How We Build Custom Software — 2-minute overview"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen
      loading="lazy"
    ></iframe>
  </div>
  <details class="explainer-video__transcript">
    <summary>Read transcript</summary>
    <div class="explainer-video__transcript-content">
      <p>At LaunchPad Lab, we build custom software for businesses...</p>
    </div>
  </details>
</section>
```

```css
.explainer-video__wrapper {
  position: relative;
  padding-bottom: 56.25%; /* 16:9 aspect ratio */
  height: 0;
  overflow: hidden;
  max-width: 800px;
  margin: 1.5rem auto;
  border-radius: 12px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.1);
}

.explainer-video__wrapper iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border: 0;
}

.explainer-video__transcript {
  max-width: 800px;
  margin: 1.5rem auto 0;
  text-align: left;
}

.explainer-video__transcript summary {
  cursor: pointer;
  font-weight: 600;
  color: #2563eb;
  padding: 0.5rem 0;
}

.explainer-video__transcript-content {
  padding: 1rem;
  background-color: #f9fafb;
  border-radius: 8px;
  line-height: 1.8;
}
```

### Text-to-Speech Option

Consider adding a browser-native read-aloud button for key sections:

```javascript
class ReadAloud {
  constructor(selector) {
    this.sections = document.querySelectorAll(selector);
    this.synth = window.speechSynthesis;
    this.sections.forEach(section => this.addButton(section));
  }

  addButton(section) {
    const btn = document.createElement('button');
    btn.className = 'read-aloud-btn';
    btn.setAttribute('aria-label', 'Read this section aloud');
    btn.innerHTML = `
      <svg aria-hidden="true" width="16" height="16" viewBox="0 0 16 16" fill="currentColor">
        <path d="M8 1a.5.5 0 01.5.5v13a.5.5 0 01-.82.384L3.332 11H1.5A.5.5 0 011 10.5v-5a.5.5 0 01.5-.5h1.832L7.68 1.116A.5.5 0 018 1z"/>
        <path d="M11.536 3.464a.5.5 0 010 .707 4.975 4.975 0 000 7.072.5.5 0 11-.707.707 5.975 5.975 0 010-8.486.5.5 0 01.707 0z"/>
      </svg>
      Listen
    `;
    btn.addEventListener('click', () => this.speak(section));
    section.querySelector('h2, h3')?.after(btn);
  }

  speak(section) {
    this.synth.cancel();
    const text = section.innerText;
    const utterance = new SpeechSynthesisUtterance(text);
    utterance.rate = 0.9;
    utterance.lang = 'en-US';
    this.synth.speak(utterance);
  }
}

document.addEventListener('DOMContentLoaded', () => {
  if ('speechSynthesis' in window) {
    new ReadAloud('.service-card, .process-step');
  }
});
```

### Components to Audit

- **Service card component** — Add icon slot/prop
- **Process section component** — Replace text-only layout with visual diagram
- **Industry card component** — Add industry-specific icons
- **Video embed component** — Create or update to include title, duration, and transcript toggle
- **Icon system** — Establish a consistent icon library (e.g., Phosphor Icons, Heroicons, or custom SVGs)
- **Image alt text** — Audit all existing images for appropriate `alt` attributes

---

## Examples from Other Sites

### Asana (asana.com)
Every feature section pairs a concise text description on one side with an animated illustration or product screenshot on the other. The visual tells the same story as the text, benefiting users who process images faster.

### Notion (notion.so)
The "How It Works" section uses a three-step visual flow with icons, numbered steps, and short descriptions. The visual layout itself communicates the sequential process.

### Atlassian (atlassian.com)
Product pages use large, informative illustrations alongside text. The illustrations aren't decorative — they show the product interface and how users interact with it.

### Mailchimp (mailchimp.com)
Service descriptions use colorful, branded illustrations that visually represent abstract concepts (like "audience management" or "automations"). Even without reading the text, users get a sense of what each service does.

### GOV.UK
While minimal in design, GOV.UK uses clear icons alongside service categories (e.g., a passport icon for "Passports, travel, and living abroad"). This helps non-native speakers quickly identify relevant sections.
