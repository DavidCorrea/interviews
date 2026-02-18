# M-31: Tab Panel Images Have Empty Alt Text

**Issue ID:** M-31
**Priority:** Medium
**WCAG Criteria:** 1.1.1 Non-text Content (A)
**Affected Personas:** Screen Reader, Low Vision Screen Magnifier, Skeptical User

---

## User Story

**As a** screen reader user exploring the "Problems We Solve" section,
**I want** each tab panel image to have descriptive alt text that conveys what the image illustrates,
**so that** I receive the same contextual information as sighted users and can fully understand each solution being presented.

---

## Acceptance Criteria

- [ ] All six images within the "Problems We Solve" tab panels have descriptive, non-empty `alt` attributes.
- [ ] Each `alt` value meaningfully describes the image content and its relevance to the tab panel topic (not generic text like "image" or "photo").
- [ ] Alt text is concise — ideally under 125 characters — while conveying the key information.
- [ ] If any tab panel image is truly decorative and adds no information beyond the surrounding text, it uses `alt=""` **and** `role="presentation"` with a comment in the code explaining why.
- [ ] Screen readers (NVDA, VoiceOver, JAWS) announce the alt text when navigating through tab panel content.
- [ ] When images fail to load, the alt text is displayed as a visible fallback by the browser.

---

## How to Test the Change

### Manual Testing

1. **Screen reader test:** Open the homepage in Chrome with NVDA (or Safari with VoiceOver). Navigate to the "Problems We Solve" section. Tab through each panel. Confirm every image is announced with a meaningful description.
2. **DOM inspection:** Open DevTools → Elements panel. Search for `<img` within the tab panel containers. Verify each `alt` attribute is non-empty and descriptive.
3. **Disable images test:** In Chrome DevTools, block image loading (Network conditions → Block images). Browse each tab panel. Confirm the alt text appears in place of each image and communicates meaningful context.
4. **Magnifier test:** Using macOS Zoom or Windows Magnifier at 300%+, navigate through tab panels. Confirm images (and their alt text as tooltip on hover in some browsers) are contextually relevant.

### Automated Testing

```bash
# Using axe-core CLI
npx @axe-core/cli https://launchpadlab.com --rules image-alt

# Using pa11y
npx pa11y https://launchpadlab.com --standard WCAG2AA
```

```javascript
// Check all tab panel images have non-empty alt text
const tabPanelImages = document.querySelectorAll('.tab-panel img, [role="tabpanel"] img');
tabPanelImages.forEach(img => {
  const alt = img.getAttribute('alt');
  console.assert(
    alt && alt.trim().length > 0,
    `Image missing alt text: ${img.src}`
  );
  console.assert(
    alt !== 'image' && alt !== 'photo' && alt !== 'picture',
    `Image has generic alt text "${alt}": ${img.src}`
  );
});
```

---

## Developer Notes

### General Explanation

The "Problems We Solve" tabbed interface includes six images — one per tab panel — that visually illustrate each solution category (e.g., a team collaborating, a dashboard interface, a data visualization). These images currently have `alt=""`, which tells assistive technology to skip them as decorative. However, the images carry meaningful context that reinforces the tab's message, making them informational rather than decorative. Each image needs a descriptive `alt` value that conveys what it shows and why it matters in the context of the tab panel.

### Current State (Problem)

```html
<!-- All six tab panel images treated as decorative -->
<div class="tab-panel" role="tabpanel">
  <img src="/images/solutions-digital-transformation.jpg" alt="">
  <h3>Digital Transformation</h3>
  <p>We help companies modernize their technology...</p>
</div>

<div class="tab-panel" role="tabpanel">
  <img src="/images/solutions-ai-integration.jpg" alt="">
  <h3>AI Integration</h3>
  <p>Leverage artificial intelligence to...</p>
</div>
```

### Recommended Fix

```html
<div class="tab-panel" role="tabpanel">
  <img
    src="/images/solutions-digital-transformation.jpg"
    alt="Team of developers reviewing a modernized application interface on a large monitor"
  >
  <h3>Digital Transformation</h3>
  <p>We help companies modernize their technology...</p>
</div>

<div class="tab-panel" role="tabpanel">
  <img
    src="/images/solutions-ai-integration.jpg"
    alt="Interactive dashboard displaying real-time AI-driven analytics and predictions"
  >
  <h3>AI Integration</h3>
  <p>Leverage artificial intelligence to...</p>
</div>
```

### Writing Good Alt Text for These Images

Follow this template for each tab panel image:

| Image Subject | Recommended Alt Text Pattern |
|---|---|
| People collaborating | "[Who] [doing what] [with what context]" — e.g., "Cross-functional team collaborating on a product roadmap in a workshop" |
| Software interface | "[What the interface shows] [key detail]" — e.g., "Analytics dashboard displaying user engagement metrics and growth trends" |
| Abstract/conceptual | "[What concept it represents]" — e.g., "Interconnected nodes representing a scalable cloud architecture" |

**Tips:**
- Describe what the image *shows*, not what it *is* ("team reviewing code on a screen" not "stock photo of people")
- Include context relevant to the tab panel topic
- Avoid starting with "Image of..." or "Picture of..." — screen readers already announce it as an image

### Components / Files to Audit

- Homepage template (section containing the "Problems We Solve" tabs)
- Tab panel partial/component template
- WordPress media library (check if alt text can be set per image in the CMS)
- Any other tabbed interfaces or panels with images elsewhere on the site
- CMS editor instructions (add guidance for content editors on writing alt text)

---

## Examples from Other Sites

| Site | Approach | Why It Works |
|---|---|---|
| **Salesforce** | Tabbed product feature panels include images with descriptive alt text like "Einstein AI analyzing sales pipeline data" | Alt text is specific to the feature being demonstrated, not generic. |
| **IBM** | Solution pages use alt text that describes the illustration's meaning in context: "Hybrid cloud architecture connecting on-premise and cloud services" | Contextual description matches the surrounding copy's message. |
| **GOV.UK** | All informational images require alt text reviewed by content designers; their style guide mandates describing the image's purpose, not just its appearance | Systematic content governance ensures consistently useful alt text. |
| **W3C WAI Images Tutorial** | Canonical guide for deciding whether an image is decorative vs. informational and writing appropriate alt text | The definitive reference — recommends informational images always have descriptive alt. |
