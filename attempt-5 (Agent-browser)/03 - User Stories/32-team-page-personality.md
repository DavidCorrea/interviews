# Team Page Lacks Personality and Human Connection

**Priority:** Medium
**Location:** About Us page — "Meet Our Leadership Team" section
**WCAG:** [1.1.1 Non-text Content (A)](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content), [2.4.6 Headings and Labels (AA)](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels)

---

## User Story

> As a **Gen Z first-time founder evaluating potential development partners**,
> I want **to see who I'd actually be working with — their personality, what they care about, and what makes them human**
> so that **I feel like I'm hiring real people I can trust, not a faceless org chart.**

---

## Problem

The "Meet Our Leadership Team" section on the About page displays team members as:

- **Circular headshots** — professional, uniformly styled, and interchangeable.
- **Full names** and **formal titles** — "VP of Engineering," "President," "Principal Software Architect II."
- **LinkedIn links** — the only additional context, which redirects users off-site.

What's missing:

- **No bios.** Not a single sentence about who these people are, what they've built, or why they do this work.
- **No personal details.** No fun facts, hobbies, or human touches that make someone memorable.
- **No approachable role descriptions.** "Principal Software Architect II" tells a Gen Z founder nothing about what this person does day-to-day or how they'd help.
- **No candid photos.** Every headshot follows the same corporate template — polished, distant, and impersonal.

For Gen Z, authenticity is a core value. A team section that reads like a corporate directory signals "this company is old-school" and "I won't be treated as a person here." Research from the Stanford Web Credibility Project shows that team pages are among the most visited pages on a company site, and users specifically look for signs of authenticity and relatability.

---

## Acceptance Criteria

- [ ] Each team member has a 1–2 sentence bio that includes: what they do in plain language, something personal or a fun fact.
- [ ] Formal titles are supplemented with a plain-language role description (e.g., "VP of Engineering" → "VP of Engineering — Keeps the code quality high and the team happy").
- [ ] At least one candid or personality-revealing photo is included per person (alongside or instead of the formal headshot).
- [ ] Bios are written in first person or a warm third person, not corporate boilerplate.
- [ ] LinkedIn links are retained but are not the only point of connection — bios provide context without requiring users to leave the site.
- [ ] All team photos have descriptive `alt` text (e.g., "Headshot of Jane Smith, VP of Engineering, smiling in a blue sweater" — not "team member").
- [ ] The section heading is approachable (e.g., "The People Behind the Code" rather than "Meet Our Leadership Team").
- [ ] Content is responsive and readable on mobile — bios don't overflow or get hidden.

---

## How to Test

1. **First-impression test:** Show the team section to 3 people unfamiliar with LaunchPad Lab. Ask: "Would you want to work with these people?" If the answer is hesitation or "they seem corporate," the section needs more personality.
2. **Content audit:** For each team member, verify a bio exists with at least one personal detail and one plain-language description of their role.
3. **Alt text audit:** Inspect each `<img>` in the team section. Verify `alt` text is descriptive and specific, not generic ("team member" or "headshot").
4. **Screen reader test:** Navigate the team section with VoiceOver or NVDA. Verify each person's name, role, and bio are announced in a logical order.
5. **Mobile test:** View the team section on a 375px viewport. Verify bios are visible (not truncated or hidden behind a "read more" that's hard to tap).
6. **Tone test:** Read all bios aloud. They should sound like something a real person would say, not a press release.

---

## Developer Notes

### Strategy

Transform the team section from a corporate directory into a personality-driven showcase. Add bios, humanize titles, mix in candid photography, and use a warm tone that signals "we're real people who love building things."

### Before (current pattern)

```html
<section class="team">
  <h2>Meet Our Leadership Team</h2>
  <div class="team-grid">
    <div class="team-member">
      <img
        src="/team/jane-smith.jpg"
        alt="Jane Smith"
        class="team-photo"
      />
      <h3>Jane Smith</h3>
      <p class="team-title">VP of Engineering</p>
      <a href="https://linkedin.com/in/janesmith"
         target="_blank" rel="noopener noreferrer">
        LinkedIn
      </a>
    </div>

    <div class="team-member">
      <img
        src="/team/alex-chen.jpg"
        alt="Alex Chen"
        class="team-photo"
      />
      <h3>Alex Chen</h3>
      <p class="team-title">Principal Software Architect II</p>
      <a href="https://linkedin.com/in/alexchen"
         target="_blank" rel="noopener noreferrer">
        LinkedIn
      </a>
    </div>
  </div>
</section>
```

### After (improved markup)

```html
<section class="team" aria-labelledby="team-heading">
  <h2 id="team-heading">The People Behind the Code</h2>
  <p class="team__intro">
    We're engineers, designers, and strategists who love turning ideas into
    real products. Here's who you'll be working with.
  </p>

  <ul class="team-grid" role="list">
    <li class="team-card">
      <div class="team-card__photos">
        <img
          src="/team/jane-smith.jpg"
          alt="Jane Smith smiling in a blue sweater at the LaunchPad Lab office"
          class="team-photo"
          width="280"
          height="280"
          loading="lazy"
        />
      </div>
      <div class="team-card__info">
        <h3>Jane Smith</h3>
        <p class="team-card__title">VP of Engineering</p>
        <p class="team-card__subtitle">
          Keeps the code quality high and the team happy.
        </p>
        <p class="team-card__bio">
          Jane has been building web apps since before responsive design was
          a thing. Outside of work, she's a competitive rock climber and
          hosts a monthly board game night.
        </p>
        <a href="https://linkedin.com/in/janesmith"
           target="_blank"
           rel="noopener noreferrer"
           aria-label="Jane Smith on LinkedIn">
          LinkedIn →
        </a>
      </div>
    </li>

    <li class="team-card">
      <div class="team-card__photos">
        <img
          src="/team/alex-chen.jpg"
          alt="Alex Chen laughing during a team whiteboard session"
          class="team-photo"
          width="280"
          height="280"
          loading="lazy"
        />
      </div>
      <div class="team-card__info">
        <h3>Alex Chen</h3>
        <p class="team-card__title">Principal Software Architect</p>
        <p class="team-card__subtitle">
          Designs the systems that make your product fast and reliable.
        </p>
        <p class="team-card__bio">
          Alex geeks out over system design and has architected platforms
          handling millions of users. He's also an amateur
          photographer who shoots street photography on weekends.
        </p>
        <a href="https://linkedin.com/in/alexchen"
           target="_blank"
           rel="noopener noreferrer"
           aria-label="Alex Chen on LinkedIn">
          LinkedIn →
        </a>
      </div>
    </li>
  </ul>
</section>
```

### CSS for the updated team section

```css
.team {
  padding: 4rem 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.team__intro {
  max-width: 600px;
  margin: 0 auto 3rem;
  text-align: center;
  font-size: 1.125rem;
  line-height: 1.7;
  color: #444;
}

.team-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2.5rem;
  list-style: none;
  padding: 0;
  margin: 0;
}

.team-card {
  background: #fff;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
  transition: box-shadow 0.2s ease;
}

.team-card:hover {
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
}

.team-photo {
  width: 100%;
  height: 280px;
  object-fit: cover;
  display: block;
}

.team-card__info {
  padding: 1.5rem;
}

.team-card__info h3 {
  font-size: 1.25rem;
  margin: 0 0 0.25rem;
  color: #1a1a1a;
}

.team-card__title {
  font-size: 0.875rem;
  font-weight: 600;
  color: #1a73e8;
  margin: 0 0 0.25rem;
  text-transform: uppercase;
  letter-spacing: 0.03em;
}

.team-card__subtitle {
  font-size: 0.9375rem;
  color: #555;
  margin: 0 0 0.75rem;
  font-style: italic;
}

.team-card__bio {
  font-size: 0.9375rem;
  line-height: 1.6;
  color: #333;
  margin: 0 0 1rem;
}

.team-card__info a {
  font-size: 0.875rem;
  font-weight: 600;
  color: #1a73e8;
  text-decoration: none;
}

.team-card__info a:hover {
  text-decoration: underline;
}

.team-card__info a:focus-visible {
  outline: 3px solid #1a73e8;
  outline-offset: 2px;
  border-radius: 2px;
}

@media (max-width: 600px) {
  .team-grid {
    grid-template-columns: 1fr;
  }

  .team-photo {
    height: 240px;
  }
}
```

### Content guidelines for bios

Write bios that answer three questions:

1. **What do you do here?** (in plain language, not a title)
2. **What's your superpower?** (one sentence about what makes them great at their job)
3. **What makes you human?** (a hobby, fun fact, or personal detail)

Template:

```markdown
**[Name]** — [Plain-language role].
[One sentence about their professional superpower].
[One sentence personal detail or fun fact].
```

Examples:

> **Jane Smith** — VP of Engineering.
> She's been building web apps since before responsive design was a thing
> and obsesses over code quality. Outside work, she's a competitive rock
> climber and hosts a monthly board game night.

> **Alex Chen** — Principal Software Architect.
> He designs the systems that make your product fast even when a million
> people show up at once. On weekends, he shoots street photography around
> Chicago.

### Title translation reference

| Formal Title | Approachable Subtitle |
|---|---|
| President | Leads the company and keeps clients happy |
| VP of Engineering | Keeps the code quality high and the team running |
| Principal Software Architect II | Designs the systems that make your product reliable |
| Director of Product | Turns your idea into a plan the team can build |
| Senior UX Designer | Makes sure your product is easy and enjoyable to use |
| Director of Operations | Keeps projects on time and on budget |

### Components to audit

| Component / Section | Page(s) | What to fix |
|---|---|---|
| Team grid | About page | Add bios, approachable subtitles, and candid photos |
| Team member `alt` text | About page | Replace generic alt with descriptive, specific text |
| Section heading | About page | Change "Meet Our Leadership Team" to warmer heading |
| Team photos | About page | Commission or collect candid/personality photos |
| LinkedIn links | About page | Add `aria-label` with person's name |

---

## Examples from Other Sites

### Basecamp (basecamp.com/about)
- Team page includes full bios written in first person with genuine personality.
- Photos are casual — some at desks, some outdoors, some with pets.
- Titles are plain: "Designer," "Programmer," "Support" — no corporate ladder language.

### Notion (notion.so/about)
- Team members have short, punchy bios that mix professional background with personal flair.
- Photos are warm and candid — not studio headshots.
- The tone is conversational and inviting.

### Linear (linear.app/about)
- Small team showcased with names, roles, and brief personal bios.
- Emphasis on what each person brings to the product, not their title hierarchy.
- Clean, modern design that feels personal without being unprofessional.

### Vercel (vercel.com/about)
- Team section includes where each person is based, adding a human-geography element.
- Titles are simple and descriptive.
- The overall tone communicates "we're builders" rather than "we're executives."

### Buffer (buffer.com/about)
- Fully transparent team page with salaries, roles, and personal bios.
- Every team member has a paragraph about their life outside work.
- Photos are casual and authentic — some selfies, some action shots.
- This radical transparency is a trust signal that resonates strongly with Gen Z.
