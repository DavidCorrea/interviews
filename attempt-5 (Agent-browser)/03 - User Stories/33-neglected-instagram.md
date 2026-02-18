# Neglected Social Media Presence (Instagram)

**Priority:** Medium
**Location:** Instagram (@launchpadlab), linked from footer on all pages
**Related:** [Issue 34 — No TikTok or Twitter/X Social Presence](./34-no-tiktok-twitter.md)

---

## User Story

> As a **Gen Z founder checking out a potential development partner**,
> I want **to see an active, authentic Instagram presence when I click through from the website**
> so that **I feel confident this company is alive, current, and run by real people — not a ghost ship.**

---

## Problem

LaunchPad Lab's Instagram account (@launchpadlab) is linked in the footer of every page on the site under "Let's Get Social." When a Gen Z user clicks through, they find:

- **463 posts** but only **~250 followers** — a stark ratio that signals low engagement and low relevance.
- **Last post: December 2025** — nearly two months of inactivity at the time of this audit (February 2026).
- **Content is corporate:** Award announcements, holiday graphics, and promotional material. Minimal comments, minimal likes, minimal engagement.
- **No behind-the-scenes content.** No team moments, no project showcases, no office culture, no process insights.
- **No personality.** The feed reads like a press release archive, not a living company.

For Gen Z, social media is a primary trust signal. An inactive or low-engagement social presence communicates:

- "This company might be struggling or winding down."
- "They don't care about staying current."
- "They're not authentic — they only post when they want something."

Linking to a neglected account is **worse than not linking at all**. It actively undermines the trust the website is trying to build.

---

## Acceptance Criteria

- [ ] **Option A (Invest):** Instagram is updated with fresh content at least 2–3 times per week, following a content strategy that includes behind-the-scenes, project showcases, team personality, and tech insights.
- [ ] **Option B (Remove):** If the team cannot commit to regular content, the Instagram link is removed from the footer and all pages until the account is active.
- [ ] If Option A: Posts include a mix of content types — Reels, Stories, carousel posts, and static images.
- [ ] If Option A: Engagement metrics are tracked monthly with targets (e.g., > 2% engagement rate per post).
- [ ] If Option A: The account bio is updated with a clear value prop and link to the website (using a link-in-bio tool).
- [ ] If Option A: The feed reflects the company's current work, team, and culture — not just awards.
- [ ] Social links in the footer open in a new tab with `target="_blank"` and `rel="noopener noreferrer"`.
- [ ] Social links have accessible `aria-label` attributes (e.g., `aria-label="LaunchPad Lab on Instagram"`).

---

## How to Test

1. **Freshness check:** Open Instagram and search for @launchpadlab. Check the date of the most recent post. If it's older than 2 weeks, the account is neglected.
2. **Engagement audit:** Review the last 10 posts. Calculate the average engagement rate: (likes + comments) ÷ followers × 100. Target: > 2%. Anything below 1% indicates the content isn't resonating.
3. **Content mix audit:** Categorize the last 20 posts. Count how many are: awards/announcements, team/culture, project showcases, educational/tech content. If > 60% are awards/announcements, the mix is off.
4. **Follower-to-post ratio:** Compare followers (~250) to posts (463). A healthy account should have more followers than posts. This ratio suggests the account is broadcasting without building an audience.
5. **Footer link test:** Click the Instagram icon in the footer. Verify it opens in a new tab, goes to the correct account, and has proper `aria-label`.
6. **Screen reader test:** Navigate to the footer social links with VoiceOver or NVDA. Verify the Instagram link announces "LaunchPad Lab on Instagram" or equivalent — not just "Instagram" or a bare URL.

---

## Developer Notes

### Strategy

Either invest in Instagram as a real channel or remove the link. A neglected social link is a negative trust signal. If investing, follow a content strategy that prioritizes authenticity and consistency over polish.

### Fix the footer link markup

Regardless of whether the account stays or goes, the current social links should be accessible.

```html
<nav class="social-links" aria-label="Social media">
  <h2 class="social-links__heading">Let's Get Social</h2>
  <ul class="social-links__list" role="list">
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
  </ul>
</nav>
```

### CSS for social links

```css
.social-links__list {
  display: flex;
  gap: 1rem;
  list-style: none;
  padding: 0;
  margin: 0;
}

.social-links__list a {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 44px;
  height: 44px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.1);
  transition: background 0.2s ease, transform 0.2s ease;
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

### If removing Instagram: conditional rendering

If the team decides to remove the Instagram link until the account is active, use a feature flag or CMS toggle rather than deleting the markup.

```javascript
const SOCIAL_LINKS = [
  {
    platform: 'linkedin',
    url: 'https://www.linkedin.com/company/launchpad-lab/',
    label: 'LaunchPad Lab on LinkedIn',
    active: true,
  },
  {
    platform: 'instagram',
    url: 'https://www.instagram.com/launchpadlab/',
    label: 'LaunchPad Lab on Instagram',
    active: false, // Disabled until content strategy is in place
  },
  {
    platform: 'facebook',
    url: 'https://www.facebook.com/LaunchPadLab/',
    label: 'LaunchPad Lab on Facebook',
    active: false, // Deprioritized — see Issue 34
  },
];

function renderSocialLinks(links) {
  return links
    .filter(link => link.active)
    .map(link => `
      <li>
        <a href="${link.url}"
           target="_blank"
           rel="noopener noreferrer"
           aria-label="${link.label}">
          <svg aria-hidden="true" class="social-icon" width="24" height="24">
            <use href="#icon-${link.platform}" />
          </svg>
        </a>
      </li>
    `)
    .join('');
}
```

### Instagram content strategy recommendations

If the team chooses to invest, here's a sustainable content calendar:

| Day | Content Type | Example |
|---|---|---|
| Monday | Project spotlight | "We just shipped [feature] for [client]. Here's why it matters." |
| Wednesday | Team / culture | "Our designer [Name] shares their workspace setup" or "Friday team lunch" |
| Friday | Tech insight / tip | "3 things we learned building [feature]" or "Why we chose [technology]" |

**Content pillars:**

1. **Behind the scenes** (40%) — Team activities, office culture, brainstorming sessions, whiteboard photos, standups, celebrations.
2. **Project showcases** (30%) — Screenshots, short videos of shipped products, before/after comparisons, client testimonials.
3. **Tech insights** (20%) — Short tips, "things we learned," architecture diagrams, code snippets as carousel posts.
4. **Awards / milestones** (10%) — Keep these, but as a small share, not the dominant content.

**Format recommendations:**

- **Reels (15–30 seconds):** Quick project walkthroughs, "a day in the life," coding timelapses.
- **Carousels (5–7 slides):** "How we built X," team introductions, process breakdowns.
- **Stories:** Daily low-effort content — team lunches, desk setups, polls ("React or Vue?"), Q&A stickers.

### Embedding Instagram feed on the website (optional)

If the account becomes active, consider embedding a live feed widget on the About or homepage.

```html
<section class="instagram-feed" aria-labelledby="instagram-heading">
  <h2 id="instagram-heading">What We're Up To</h2>
  <div class="instagram-grid" id="instagram-widget">
    <!-- Populated via Instagram Basic Display API or a service like Elfsight -->
  </div>
  <a href="https://instagram.com/launchpadlab"
     target="_blank"
     rel="noopener noreferrer"
     class="btn btn--secondary">
    Follow Us on Instagram →
  </a>
</section>
```

### Components to audit

| Component / Section | Page(s) | What to fix |
|---|---|---|
| Footer social links | All pages | Add `aria-label`, ensure proper `target`/`rel` attributes |
| Instagram link specifically | All pages (footer) | Either invest in content or remove the link |
| Social icons | All pages (footer) | Ensure minimum 44×44px touch target, `aria-hidden` on SVGs |
| "Let's Get Social" heading | All pages (footer) | Keep or rephrase based on which platforms remain active |

---

## Examples from Other Sites

### Metalab (metalab.com)
- Instagram feed is curated with a mix of project showcases, team culture, and design inspiration.
- Posts are visually consistent with a recognizable aesthetic.
- The account feels alive — posts go out 2–3 times per week.
- Team personality shines through without sacrificing professionalism.

### Thoughtbot (thoughtbot.com)
- Thoughtbot made the deliberate choice to link only to platforms they actively maintain (Twitter/X, GitHub, LinkedIn).
- No dead links to neglected accounts.
- Their blog serves as the primary content channel, with social used for distribution.

### Stripe
- Stripe's Instagram focuses on product design, team culture, and events.
- High production value but still feels authentic — not overly polished.
- Consistent posting schedule builds trust.

### Figma (@figma on Instagram)
- Gold standard for a tech company Instagram: mix of user-generated content, product tips, design inspiration, and team highlights.
- Active community engagement — they reply to comments and reshare user content.
- Demonstrates that a tech company can have a vibrant, authentic Instagram presence.
- Over 600K followers built through genuine, useful content — not paid promotion.
