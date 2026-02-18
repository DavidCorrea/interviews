# Discovery Space Navigator Is Buried

**Priority:** Medium
**Location:** Services page — mid-page section ("Your 3-Step Blueprint for What to Build")
**WCAG:** [2.4.1 Bypass Blocks (A)](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks), [2.4.5 Multiple Ways (AA)](https://www.w3.org/WAI/WCAG21/Understanding/multiple-ways)

---

## User Story

> As a **Gen Z first-time founder figuring out what to build**,
> I want **to immediately find LaunchPad Lab's early-stage offering (prototype in 4 weeks, launch in 6 weeks)**
> so that **I can see this is the right partner for my stage without digging through pages of enterprise-level content.**

---

## Problem

The "Discovery Space Navigator" offering — branded as "Your 3-Step Blueprint for What to Build" with a concrete promise of prototype in 4 weeks and launch in 6 weeks — is the single most startup-friendly piece of content on the entire LaunchPad Lab site. It directly addresses the core anxiety of early-stage founders: "I have an idea but I don't know where to start."

However, this offering is **buried mid-page on the Services page**. It is:

- **Not mentioned on the homepage.** A first-time founder scanning the homepage sees enterprise-grade messaging and no entry point tailored to their stage.
- **Not referenced on the About page.** Founders evaluating the team never learn that a lightweight, fast-start offering exists.
- **Not linked from the Contact page.** When a founder finally decides to reach out, there's no option to say "I want the Discovery Space Navigator" — just a generic form.
- **Not in the main navigation.** There is no top-level menu item or dropdown entry that signals "Start here if you're early-stage."

The exact audience this offering was designed for — early-stage founders with an idea and a limited budget — never discovers it. They bounce after seeing pricing signals and complexity aimed at established companies.

---

## Acceptance Criteria

- [ ] The Discovery Space Navigator offering is featured prominently on the homepage, above the fold or immediately after the hero section.
- [ ] The homepage feature includes: the offering name, the timeline promise ("prototype in 4 weeks"), and a clear CTA button.
- [ ] A dedicated landing page exists at a memorable URL (e.g., `/discovery/` or `/start/`).
- [ ] The Contact page includes a CTA or option specifically referencing the Discovery offering (e.g., "Not sure what to build yet? Start with our Discovery Space Navigator").
- [ ] The About page includes a mention or link to the offering in context (e.g., near the team section or mission statement).
- [ ] The main navigation includes an entry point — either a direct link or a dropdown item under "Services" — labeled in plain language (e.g., "Start Here" or "For Founders").
- [ ] The offering is discoverable within 2 clicks from any page on the site.
- [ ] The CTA uses action-oriented, low-commitment language (e.g., "See How It Works" rather than "Request a Proposal").

---

## How to Test

1. **First-visit simulation:** Open `launchpadlab.com` in an incognito window. Set a 60-second timer. Attempt to find information about the Discovery Space Navigator. If it takes more than 30 seconds or requires scrolling past enterprise content, the offering is buried.
2. **Homepage audit:** Load the homepage. Scan above the fold and the first two scroll lengths. Verify the Discovery offering or a CTA linking to it is visible.
3. **Navigation audit:** Open the main navigation menu. Look for any entry that signals "early-stage," "start here," or "discovery." Verify it exists.
4. **Contact page check:** Navigate to the Contact page or form. Verify there is a path or mention of the Discovery offering for founders who aren't ready for a full engagement.
5. **Cross-page link audit:** Visit the About page. Search (Ctrl+F) for "Discovery" or "blueprint" or "prototype." Verify at least one reference exists.
6. **Mobile test:** Repeat steps 1–4 on a 375px viewport. The CTA should be just as prominent on mobile.
7. **Analytics validation (post-launch):** Confirm click-through rate on the new homepage CTA. Target: ≥ 3% CTR within the first month.

---

## Developer Notes

### Strategy

Elevate the Discovery Space Navigator from a buried mid-page section into a primary conversion path. Treat it as the **low-barrier entry point** for the site — the thing that makes an early-stage founder think "this is for me."

### Homepage feature section

Add a dedicated section on the homepage, positioned after the hero and before or alongside the main services overview.

```html
<section class="discovery-cta" aria-labelledby="discovery-heading">
  <div class="discovery-cta__content">
    <span class="discovery-cta__badge">For Early-Stage Founders</span>
    <h2 id="discovery-heading">Not sure what to build? Start here.</h2>
    <p class="discovery-cta__subtitle">
      Our Discovery Space Navigator gives you a
      <strong>working prototype in 4 weeks</strong> and a
      <strong>launch plan in 6 weeks</strong> — so you can stop guessing
      and start building.
    </p>
    <div class="discovery-cta__steps">
      <div class="discovery-step">
        <span class="discovery-step__number">1</span>
        <p><strong>Define</strong> — We map your idea to a buildable product</p>
      </div>
      <div class="discovery-step">
        <span class="discovery-step__number">2</span>
        <p><strong>Prototype</strong> — You get a working prototype in 4 weeks</p>
      </div>
      <div class="discovery-step">
        <span class="discovery-step__number">3</span>
        <p><strong>Launch</strong> — We build your MVP and launch in 6 weeks</p>
      </div>
    </div>
    <a href="/discovery/" class="btn btn--primary btn--lg">
      See How It Works
    </a>
  </div>
</section>
```

### CSS for the homepage CTA

```css
.discovery-cta {
  background: linear-gradient(135deg, #f0f4ff 0%, #e8f0fe 100%);
  padding: 4rem 2rem;
  text-align: center;
}

.discovery-cta__badge {
  display: inline-block;
  background: #1a73e8;
  color: #fff;
  font-size: 0.8125rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  padding: 0.375rem 1rem;
  border-radius: 100px;
  margin-bottom: 1.5rem;
}

.discovery-cta__subtitle {
  max-width: 640px;
  margin: 1rem auto 2rem;
  font-size: 1.125rem;
  line-height: 1.7;
  color: #333;
}

.discovery-cta__steps {
  display: flex;
  justify-content: center;
  gap: 2rem;
  margin-bottom: 2.5rem;
  flex-wrap: wrap;
}

.discovery-step {
  display: flex;
  align-items: flex-start;
  gap: 0.75rem;
  max-width: 220px;
  text-align: left;
}

.discovery-step__number {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 2rem;
  height: 2rem;
  min-width: 2rem;
  background: #1a73e8;
  color: #fff;
  font-weight: 700;
  border-radius: 50%;
  font-size: 0.875rem;
}

.btn--lg {
  font-size: 1.125rem;
  padding: 1rem 2.5rem;
}

@media (max-width: 600px) {
  .discovery-cta__steps {
    flex-direction: column;
    align-items: center;
  }

  .discovery-step {
    max-width: 300px;
  }
}
```

### Contact page integration

Add a secondary CTA on the Contact page for founders who aren't ready for a full engagement.

```html
<aside class="contact-discovery" aria-labelledby="contact-discovery-heading">
  <h2 id="contact-discovery-heading">Not sure what you need yet?</h2>
  <p>
    If you have an idea but aren't sure where to start, our
    <strong>Discovery Space Navigator</strong> gives you a prototype
    in 4 weeks and a launch plan in 6. No long contracts, no big commitments.
  </p>
  <a href="/discovery/" class="btn btn--secondary">
    Learn About Discovery →
  </a>
</aside>
```

### Navigation integration

Add a "Start Here" or "For Founders" entry to the main navigation. This can be a top-level item or a highlighted item within a "Services" dropdown.

```html
<nav aria-label="Main navigation">
  <ul class="nav-list">
    <li><a href="/services/">Services</a></li>
    <li><a href="/work/">Work</a></li>
    <li><a href="/about/">About</a></li>
    <li><a href="/insights/">Insights</a></li>
    <li>
      <a href="/discovery/" class="nav-highlight">
        Start Here
      </a>
    </li>
    <li><a href="/contact/" class="nav-cta">Contact</a></li>
  </ul>
</nav>
```

```css
.nav-highlight {
  color: #1a73e8;
  font-weight: 600;
  position: relative;
}

.nav-highlight::after {
  content: "";
  position: absolute;
  bottom: -2px;
  left: 0;
  right: 0;
  height: 2px;
  background: #1a73e8;
  border-radius: 1px;
}
```

### Dedicated landing page route

Create a focused landing page at `/discovery/` that expands on the 3-step process, includes social proof (testimonials from founders who've been through it), timeline details, and a low-friction CTA.

```html
<main id="main-content">
  <section class="discovery-hero" aria-labelledby="discovery-hero-heading">
    <h1 id="discovery-hero-heading">
      Your 3-Step Blueprint for What to Build
    </h1>
    <p class="discovery-hero__subtitle">
      Go from idea to working prototype in 4 weeks.
      Launch-ready in 6.
    </p>
    <a href="#get-started" class="btn btn--primary btn--lg">
      Get Started
    </a>
  </section>

  <section class="discovery-details" aria-labelledby="discovery-details-heading">
    <h2 id="discovery-details-heading">How It Works</h2>
    <ol class="discovery-timeline">
      <li>
        <h3>Week 1–2: Define</h3>
        <p>
          We work with you to turn your idea into a clear product
          definition — who it's for, what it does, and what success looks like.
        </p>
      </li>
      <li>
        <h3>Week 3–4: Prototype</h3>
        <p>
          You get a working, clickable prototype you can show to users,
          investors, and co-founders. Real feedback, not guesswork.
        </p>
      </li>
      <li>
        <h3>Week 5–6: Launch Plan</h3>
        <p>
          We deliver a technical roadmap, architecture plan, and sprint
          schedule to take your prototype to a launched MVP.
        </p>
      </li>
    </ol>
  </section>

  <section class="discovery-cta-bottom" aria-labelledby="get-started">
    <h2 id="get-started">Ready to start?</h2>
    <p>
      Tell us about your idea. No pitch deck required — just a paragraph
      about what you want to build.
    </p>
    <a href="/contact/?ref=discovery" class="btn btn--primary btn--lg">
      Tell Us Your Idea
    </a>
  </section>
</main>
```

### Components to audit

| Component / Section | Page(s) | What to fix |
|---|---|---|
| Hero section | Homepage | Add Discovery CTA or feature section below hero |
| Services dropdown / page | Services, Navigation | Elevate Discovery to top of Services or add nav entry |
| Contact form | Contact page | Add "Not sure what you need?" aside with Discovery link |
| About page | About | Add mention of Discovery offering near mission or team |
| Footer | All pages | Add "Start Here" or "For Founders" link |
| Main navigation | All pages | Add "Start Here" nav item linking to `/discovery/` |

---

## Examples from Other Sites

### Vercel (vercel.com)
- Homepage hero immediately communicates the core value prop: "Develop. Preview. Ship."
- A clear "Start Deploying" CTA is visible within 1 second of landing.
- Their "Getting Started" guide is linked from every page, serving as a low-barrier entry for new users.

### Loom (loom.com)
- Homepage has a prominent "Get Loom for Free" CTA that immediately communicates the lowest-commitment entry point.
- Below the hero, a 3-step visual ("Record → Share → Done") mirrors the Discovery Space Navigator's 3-step structure — simple, scannable, and reassuring for first-timers.

### Pilot (pilot.com)
- A startup-focused bookkeeping service that features "For Startups" as a top-level navigation item.
- The homepage CTA speaks directly to early-stage founders: "Focus on building. We'll handle the books."
- Pricing is transparent and segmented by company stage — early-stage founders immediately see what applies to them.

### Notion (notion.so)
- Features a "For Startups" page accessible from the main navigation.
- Offers a free tier specifically for startups with < 10 members, making the entry point obvious and low-risk.
- The startups page includes testimonials from other founders, reinforcing "this is for people like me."

### Y Combinator Startup School (startupschool.org)
- Entire site is structured as a funnel: "Apply" → "Learn" → "Build."
- No enterprise language. Every page speaks to the first-time founder.
- The CTA is "Start Building" — action-oriented and low-commitment, matching the tone early-stage founders respond to.
