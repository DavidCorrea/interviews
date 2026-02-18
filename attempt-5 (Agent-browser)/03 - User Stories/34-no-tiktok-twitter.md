# No TikTok or Twitter/X Social Presence

**Priority:** Low
**Location:** Footer — "Let's Get Social" section (all pages)
**Related:** [Issue 33 — Neglected Social Media Presence (Instagram)](./33-neglected-instagram.md)

---

## User Story

> As a **Gen Z founder who discovers companies through TikTok and Twitter/X**,
> I want **to find LaunchPad Lab on the platforms I actually use**
> so that **I can engage with their content in my native environment and build trust before ever visiting the website.**

---

## Problem

The site footer's "Let's Get Social" section links to three platforms:

1. **Facebook** — Irrelevant to Gen Z. Usage among 18–24-year-olds has dropped to under 33% (Pew Research, 2024). The presence of a Facebook link without TikTok or Twitter/X signals "this company markets to my parents' generation."
2. **Instagram** — Present but neglected (see Issue 33).
3. **LinkedIn** — Appropriate for professional context but not a discovery platform for Gen Z founders.

What's missing:

- **TikTok** — The dominant discovery platform for Gen Z. Short-form video is how this demographic finds new brands, products, and service providers. Tech-focused TikTok content (build-in-public, coding tips, startup advice) consistently performs well.
- **Twitter/X** — The primary platform for the tech and startup community. Founders, VCs, and developers live here. Not having a presence means missing the conversation entirely.

The current social link set (Facebook, Instagram, LinkedIn) communicates that LaunchPad Lab's marketing is optimized for a 2015 audience, not a 2026 one. For a Gen Z founder evaluating partners, this is a subtle but real signal that the company may not understand their world.

---

## Acceptance Criteria

- [ ] **TikTok:** A TikTok account is created and linked in the footer. Content is posted at least 1–2 times per week.
- [ ] **Twitter/X:** A Twitter/X account is created (or reactivated) and linked in the footer. Content is posted at least 2–3 times per week.
- [ ] **Facebook:** The Facebook link is deprioritized — moved to the end of the social links list or removed entirely if the account is inactive.
- [ ] Footer social links are ordered by relevance to the target audience: LinkedIn → Twitter/X → TikTok → Instagram → (Facebook, if kept).
- [ ] All new social links have proper `aria-label` attributes, `target="_blank"`, and `rel="noopener noreferrer"`.
- [ ] Social icons meet WCAG minimum touch target size (44×44px) and have sufficient color contrast.
- [ ] New platform accounts include a clear bio, link to the website, and consistent branding.

---

## How to Test

1. **Footer audit:** Inspect the footer social links. Verify TikTok and Twitter/X icons and links are present.
2. **Link validation:** Click each social link. Verify it opens the correct profile in a new tab.
3. **Accessibility test:** Navigate the footer with a screen reader. Verify each social link announces the platform and company name (e.g., "LaunchPad Lab on TikTok").
4. **Touch target test:** On a mobile device, verify each social icon is easily tappable without accidentally hitting an adjacent link. Minimum: 44×44px.
5. **Platform presence check:** Visit each linked social profile. Verify the bio is complete, the profile image matches LPL branding, and recent content exists.
6. **Audience alignment test:** Review the platforms linked. Facebook should not be the first or most prominent link if Gen Z is a target audience.

---

## Developer Notes

### Strategy

Add TikTok and Twitter/X to the social link set. Deprioritize Facebook. Ensure all links are accessible, properly ordered, and connected to active accounts with a content strategy.

### Updated footer markup

```html
<nav class="social-links" aria-label="Social media">
  <h2 class="social-links__heading">Let's Get Social</h2>
  <ul class="social-links__list" role="list">
    <li>
      <a href="https://www.linkedin.com/company/launchpad-lab/"
         target="_blank"
         rel="noopener noreferrer"
         aria-label="LaunchPad Lab on LinkedIn">
        <svg aria-hidden="true" class="social-icon" width="24" height="24">
          <use href="#icon-linkedin" />
        </svg>
      </a>
    </li>
    <li>
      <a href="https://twitter.com/launchpadlab"
         target="_blank"
         rel="noopener noreferrer"
         aria-label="LaunchPad Lab on X (formerly Twitter)">
        <svg aria-hidden="true" class="social-icon" width="24" height="24">
          <use href="#icon-x" />
        </svg>
      </a>
    </li>
    <li>
      <a href="https://www.tiktok.com/@launchpadlab"
         target="_blank"
         rel="noopener noreferrer"
         aria-label="LaunchPad Lab on TikTok">
        <svg aria-hidden="true" class="social-icon" width="24" height="24">
          <use href="#icon-tiktok" />
        </svg>
      </a>
    </li>
    <li>
      <a href="https://www.instagram.com/launchpadlab/"
         target="_blank"
         rel="noopener noreferrer"
         aria-label="LaunchPad Lab on Instagram">
        <svg aria-hidden="true" class="social-icon" width="24" height="24">
          <use href="#icon-instagram" />
        </svg>
      </a>
    </li>
  </ul>
</nav>
```

### SVG icons for new platforms

```html
<svg xmlns="http://www.w3.org/2000/svg" style="display: none;">
  <!-- X (formerly Twitter) -->
  <symbol id="icon-x" viewBox="0 0 24 24">
    <path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/>
  </symbol>

  <!-- TikTok -->
  <symbol id="icon-tiktok" viewBox="0 0 24 24">
    <path d="M19.59 6.69a4.83 4.83 0 0 1-3.77-4.25V2h-3.45v13.67a2.89 2.89 0 0 1-2.88 2.5 2.89 2.89 0 0 1-2.89-2.89 2.89 2.89 0 0 1 2.89-2.89c.28 0 .54.04.79.1V9.01a6.27 6.27 0 0 0-.79-.05 6.34 6.34 0 0 0-6.34 6.34 6.34 6.34 0 0 0 6.34 6.34 6.34 6.34 0 0 0 6.34-6.34V9.48a8.18 8.18 0 0 0 4.76 1.52V7.56a4.84 4.84 0 0 1-1-.87z"/>
  </symbol>
</svg>
```

### CSS for consistent social icons

```css
.social-links__list {
  display: flex;
  gap: 0.75rem;
  list-style: none;
  padding: 0;
  margin: 0;
  flex-wrap: wrap;
}

.social-links__list a {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 44px;
  height: 44px;
  border-radius: 50%;
  color: #fff;
  background: rgba(255, 255, 255, 0.1);
  transition: background 0.2s ease, transform 0.15s ease;
}

.social-links__list a:hover {
  background: rgba(255, 255, 255, 0.2);
  transform: scale(1.1);
}

.social-links__list a:focus-visible {
  outline: 3px solid #fff;
  outline-offset: 2px;
}

.social-icon {
  width: 20px;
  height: 20px;
  fill: currentColor;
}
```

### JSON-LD structured data for social profiles

Add social profile links to the organization's structured data so search engines associate the accounts with LaunchPad Lab.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "LaunchPad Lab",
  "url": "https://launchpadlab.com",
  "sameAs": [
    "https://www.linkedin.com/company/launchpad-lab/",
    "https://twitter.com/launchpadlab",
    "https://www.tiktok.com/@launchpadlab",
    "https://www.instagram.com/launchpadlab/"
  ]
}
</script>
```

### TikTok content strategy

TikTok rewards consistency, authenticity, and niche expertise. For a dev agency targeting founders:

| Content Type | Frequency | Examples |
|---|---|---|
| Build-in-public | 2×/week | "Watch us build a feature in 60 seconds," screen recordings of coding, design reviews |
| Startup tips | 1×/week | "3 things first-time founders waste money on," "MVP vs. full product — when to ship" |
| Team personality | 1×/week | "Day in the life of a dev at LPL," office tours, meeting bloopers, "POV: your client changes the scope" |
| Trend responses | As relevant | Reply to trending startup/tech content with LPL's take |

**Best practices:**
- Keep videos 15–60 seconds.
- Use trending audio when natural (don't force it).
- Show faces — TikTok rewards human presence.
- Add captions to all videos (accessibility + many users watch muted).
- Post at peak times for the target audience (typically 7–9 AM and 7–10 PM EST).

### Twitter/X content strategy

Twitter/X is where the tech and startup community has daily conversations. LPL should participate, not just broadcast.

| Content Type | Frequency | Examples |
|---|---|---|
| Thought leadership | 2–3×/week | Short threads on product development, technical decisions, startup advice |
| Project launches | As they happen | "We just shipped [product] for [client]. Here's what we learned." |
| Community engagement | Daily | Reply to founder questions, retweet team members, engage with startup community |
| Blog distribution | When published | Share Insights posts with a hook or key takeaway |

**Best practices:**
- Lead with value, not promotion. Teach something in every tweet.
- Engage with others' content — don't just broadcast.
- Use threads for longer-form insights (3–5 tweets).
- Pin a tweet that explains who LPL is and links to the Discovery offering.
- Follow and engage with founders, VCs, and tech leaders in the startup ecosystem.

### Components to audit

| Component / Section | Page(s) | What to fix |
|---|---|---|
| Footer social links | All pages | Add TikTok and Twitter/X links, deprioritize Facebook |
| Social icon sprite/set | Global | Add TikTok and X (Twitter) SVG icons |
| Structured data (JSON-LD) | All pages | Add new social URLs to `sameAs` array |
| Footer link order | All pages | Reorder: LinkedIn → X → TikTok → Instagram |
| Social icon touch targets | All pages (mobile) | Ensure all icons meet 44×44px minimum |

---

## Examples from Other Sites

### Vercel (@veraborns / @vercel on TikTok & X)
- Active on both TikTok and Twitter/X with content tailored to each platform.
- TikTok: Short, punchy videos about web development, often trending audio with coding visuals.
- Twitter/X: Daily engagement with the developer community, product updates, and technical threads.
- Demonstrates that a B2B tech company can thrive on Gen Z platforms without losing professionalism.

### Notion (@notionhq on TikTok & X)
- TikTok has 300K+ followers with content about productivity, templates, and "how I use Notion" videos.
- Twitter/X is used for product updates, community engagement, and amplifying user stories.
- Proves that even a productivity tool can create engaging short-form video content.

### Figma (@figma on TikTok & X)
- TikTok features design tips, tool tutorials, and community challenges.
- Twitter/X is one of the most active brand accounts in the design/tech space.
- Strong community engagement — they reply, retweet, and participate in conversations.
- Their presence on these platforms directly drives brand awareness among young designers and founders.

### Linear (@linear on X)
- Primarily active on Twitter/X with a focus on product development philosophy.
- Tweets are opinionated and personality-driven — not generic corporate messaging.
- Engages directly with the developer and startup community.
- Shows that a focused presence on one platform (done well) beats a scattered presence on many.

### Webflow (@webflow on TikTok)
- Uses TikTok to showcase no-code development, design tutorials, and customer success stories.
- Content is educational and accessible — targeted at founders and non-technical builders.
- Demonstrates how a development tool company translates complex services into short-form video.
