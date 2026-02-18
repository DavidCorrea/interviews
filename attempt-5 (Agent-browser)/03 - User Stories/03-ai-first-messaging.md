# AI-First Messaging Obscures Core Value Proposition

**Priority:** High
**Location:** Homepage Hero section
**WCAG:** [2.4.2 Page Titled (A)](https://www.w3.org/WAI/WCAG21/Understanding/page-titled), [3.1.5 Reading Level (AAA)](https://www.w3.org/WAI/WCAG21/Understanding/reading-level)

---

## User Story

> As a **potential client visiting the site for the first time**,
> I want **to immediately understand what LaunchPad Lab does in plain terms**
> so that **I can decide within seconds whether this company can help me, regardless of whether I need AI specifically.**

---

## Problem

The current homepage hero headline is: **"AI Innovation. Digital Solutions. Results that Matter."**

This creates three issues:

1. **AI-first framing alienates most visitors.** Many clients need custom software, not AI. Leading with AI signals that the company is an AI shop, which may cause non-AI prospects to leave.
2. **"Digital Solutions" is vague.** It could mean anything from a website to an ERP system. It does not tell visitors what the company actually builds.
3. **No plain-language description.** There is no secondary headline or subtext that states in concrete terms what LaunchPad Lab does (e.g., "We build custom software for growing businesses").

---

## Acceptance Criteria

- [ ] The hero section contains a primary headline that describes the company's core offering in plain language (e.g., "Custom Software Development").
- [ ] AI is mentioned as a capability, not as the primary identity — positioned in a secondary headline, subtext, or a separate section.
- [ ] The hero subtext includes at least one concrete deliverable (e.g., "web applications," "mobile apps," "internal tools").
- [ ] A clear call-to-action button is present with specific language (e.g., "Talk to us about your project" rather than "Get Started").
- [ ] A first-time visitor with no tech background can describe what the company does after reading only the hero section.

---

## How to Test

1. **5-second test:** Show the hero section to 5 people unfamiliar with the company for 5 seconds. Ask: "What does this company do?" If answers are vague or AI-focused, the messaging needs adjustment. Tools: [UsabilityHub Five Second Test](https://usabilityhub.com/five-second-test) or [Maze](https://maze.co/).
2. **Content review:** Read the hero headline and subtext aloud. Does it answer: "What do they do? For whom? What do I get?"
3. **Competitor comparison:** Compare the hero with competitors like Thoughtbot, Pivotal Labs, or Headway. Do they state their offering more clearly?
4. **Analytics check:** Review bounce rate on the homepage. A high bounce rate with short session time may indicate visitors are not understanding or connecting with the value proposition.
5. **Screen reader test:** Navigate to the homepage with VoiceOver. The first heading announced should convey what the company does.

---

## Developer Notes

### Current hero structure (approximate)

```html
<section class="hero">
  <h1>AI Innovation. Digital Solutions. Results that Matter.</h1>
  <a href="/contact" class="btn">Get Started</a>
</section>
```

### Recommended hero structure

```html
<section class="hero">
  <h1>We Build Custom Software That Grows Your Business</h1>
  <p class="hero__subtitle">
    Web apps, mobile apps, and internal tools —
    designed around your users, built to last.
  </p>
  <p class="hero__ai-callout">
    Now offering <strong>AI-powered features</strong> to help your
    software work smarter.
  </p>
  <a href="/contact" class="btn btn--primary">
    Talk to us about your project
  </a>
</section>
```

### CSS for hero hierarchy

```css
.hero h1 {
  font-family: 'Inter', system-ui, sans-serif;
  font-size: clamp(2rem, 5vw, 3.5rem);
  font-weight: 700;
  line-height: 1.2;
  max-width: 18ch;           /* Keep headline scannable */
  margin-bottom: 1rem;
}

.hero__subtitle {
  font-size: clamp(1.125rem, 2.5vw, 1.5rem);
  line-height: 1.6;
  max-width: 42ch;
  color: var(--color-text-secondary);
  margin-bottom: 0.75rem;
}

.hero__ai-callout {
  font-size: 1rem;
  line-height: 1.6;
  color: var(--color-text-secondary);
  margin-bottom: 2rem;
}

.btn--primary {
  display: inline-block;
  padding: 0.875rem 2rem;
  font-size: 1.125rem;
  font-weight: 600;
  border-radius: 6px;
  background-color: var(--color-primary);
  color: #fff;
  text-decoration: none;
  transition: background-color 0.2s ease;
}

.btn--primary:hover,
.btn--primary:focus-visible {
  background-color: var(--color-primary-dark);
  outline: 3px solid var(--color-focus-ring);
  outline-offset: 2px;
}
```

### Content hierarchy principle

```
┌──────────────────────────────────────────────┐
│  H1: What you do (plain language)            │
│  "We Build Custom Software That Grows        │
│   Your Business"                             │
│                                              │
│  Subtitle: What you deliver (concrete)       │
│  "Web apps, mobile apps, and internal tools" │
│                                              │
│  AI callout: Secondary capability            │
│  "Now offering AI-powered features..."       │
│                                              │
│  [CTA: Talk to us about your project]        │
└──────────────────────────────────────────────┘
```

### Alternative headline options

| Option | Headline | Why it works |
|---|---|---|
| A | We Build Custom Software That Grows Your Business | Direct, outcome-focused, plain language |
| B | Custom Software. Built Around Your Users. | Short, specific, user-centered |
| C | Software Development for Growing Companies | Clear positioning, audience-specific |
| D | Your Idea. Our Engineering. Real Results. | Parallel structure, concrete |

### Components to audit

| Component | Page | What to change |
|---|---|---|
| Hero headline | Homepage | Replace AI-first headline with plain-language core offering |
| Hero subtext | Homepage | Add concrete deliverables |
| CTA button | Homepage | Replace "Get Started" with specific action |
| Meta title / `<title>` | Homepage | Should reflect core offering, not just "AI Innovation" |
| OG / social meta tags | Homepage | Preview text should state what the company does |

---

## Examples from Other Sites

### Thoughtbot (thoughtbot.com)
- Hero: "We help you design, develop, and grow your product."
- Clear, direct, no jargon. AI is mentioned deeper in the site, not as the headline.

### Pivotal Labs / Tanzu Labs
- Hero: "We help enterprises build better software, faster."
- The offering is software development; methodology details come later.

### Basecamp (basecamp.com)
- Hero: "The project management tool that helps small teams move faster and make fewer mistakes."
- Immediately tells you: what it is (project management tool), who it's for (small teams), and what you get (speed, fewer mistakes).

### Headway (headway.io)
- Hero: "We design and develop custom software."
- Six words. Unmistakable.
