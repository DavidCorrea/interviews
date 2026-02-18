# Informal Tone / Cultural Mismatch

**Priority:** Low
**Location:** CTAs, footer, various headings sitewide
**WCAG:** [3.1.5 Reading Level (AAA)](https://www.w3.org/WAI/WCAG21/Understanding/reading-level), [3.1.3 Unusual Words (AAA)](https://www.w3.org/WAI/WCAG21/Understanding/unusual-words)

---

## User Story

> As a **prospective client from a formal business culture (e.g., Japan, Germany, South Korea)**,
> I want **call-to-action text and headings to offer a professional, culturally neutral option**
> so that **I feel respected and confident that this company understands international business norms.**

---

## Problem

The LaunchPad Lab website uses casual, colloquial phrasing in key conversion points:

- **"Let's Build Something Great"** — informal and presumptuous for a first-time visitor from a formal business culture.
- **"Let's Get Social"** — social media CTAs framed as a personal invitation may feel unprofessional.
- Other headings and CTAs use contractions, slang, or overly familiar phrasing.

While this tone works well for a North American tech audience, it can create friction for:

- **International clients** from cultures where business communication is more formal (Japan, Germany, South Korea, Middle East).
- **Enterprise decision-makers** evaluating multiple vendors — formal tone signals maturity and reliability.
- **Users with cognitive disabilities or low English proficiency** — idiomatic phrases like "Build Something Great" are abstract and harder to parse than concrete language like "Start Your Project."

This isn't about removing personality — it's about ensuring that the **most critical conversion touchpoints** don't alienate segments of the audience.

---

## Acceptance Criteria

- [ ] Primary CTAs (contact forms, "get started" buttons) use clear, professional language.
- [ ] At least one version of each key CTA avoids contractions, slang, or colloquialisms.
- [ ] Headings communicate concrete value rather than abstract enthusiasm.
- [ ] Footer social media links use standard labels ("Follow us on LinkedIn") rather than colloquial phrasing.
- [ ] CTA text passes a plain-language review — understandable by a non-native English speaker at B1 proficiency.
- [ ] Tone is consistent: avoid mixing ultra-casual CTAs with formal body copy.
- [ ] If A/B testing is available, formal and casual CTA variants are tested for conversion.

---

## How to Test

1. **CTA audit:** List every CTA on the site. Flag any that use contractions, slang, idioms, or culturally specific humor.
2. **Non-native speaker review:** Ask a non-native English speaker (or use [Hemingway Editor](https://hemingwayapp.com/)) to evaluate CTA clarity. If the meaning isn't instantly clear, the text needs revision.
3. **Cultural review:** Share key CTAs with colleagues or contacts from formal business cultures. Ask: "Would this feel appropriate on a professional services website in your culture?"
4. **Back-translation test:** Translate key CTAs to Japanese, German, or Korean using Google Translate, then translate back to English. If the meaning shifts significantly, the original text is too idiomatic.
5. **Consistency check:** Read through the site and note where tone shifts abruptly between casual and formal. These transitions can feel disjointed.

---

## Developer Notes

### Strategy

Revise the most critical CTAs to be clear, concrete, and culturally neutral. Keep brand personality in secondary copy (blog posts, team bios, social content) where a casual tone is expected and appropriate.

### Recommended CTA revisions

| Current (Casual) | Suggested (Professional) | Why |
|---|---|---|
| "Let's Build Something Great" | "Start Your Project" or "Discuss Your Project" | Concrete action, no presumed familiarity |
| "Let's Get Social" | "Connect With Us" or "Follow Us" | Standard, internationally understood |
| "Let's Chat" | "Contact Us" or "Schedule a Consultation" | Professional, clear expectation |
| "We'd love to hear from you" | "Get in Touch" or "Send Us a Message" | Direct, less emotionally presumptive |
| "Check out our work" | "View Our Work" or "See Our Case Studies" | Formal, clear |
| "Grab a coffee with us" | "Schedule a Meeting" | Professional, culturally neutral |

### Before (current markup example)

```html
<section class="cta-section">
  <h2>Let's Build Something Great</h2>
  <p>We'd love to hear about your next project.</p>
  <a href="/contact" class="btn btn-primary">Let's Chat</a>
</section>

<footer>
  <div class="social-links">
    <h3>Let's Get Social</h3>
    <a href="https://linkedin.com/company/launchpadlab">LinkedIn</a>
    <a href="https://twitter.com/launchpadlab">Twitter</a>
  </div>
</footer>
```

### After (improved markup)

```html
<section class="cta-section">
  <h2>Start Your Next Project</h2>
  <p>Tell us about your goals — we'll outline how we can help.</p>
  <a href="/contact" class="btn btn-primary">Schedule a Consultation</a>
</section>

<footer>
  <div class="social-links">
    <h3>Connect With Us</h3>
    <a href="https://linkedin.com/company/launchpadlab" aria-label="Follow LaunchPad Lab on LinkedIn">
      LinkedIn
    </a>
    <a href="https://twitter.com/launchpadlab" aria-label="Follow LaunchPad Lab on Twitter">
      Twitter
    </a>
  </div>
</footer>
```

### CSS — CTA button styling (same visual impact, professional text)

```css
.btn-primary {
  display: inline-block;
  padding: 0.875rem 2rem;
  font-size: 1rem;
  font-weight: 600;
  color: #ffffff;
  background-color: #1a73e8;
  border: none;
  border-radius: 6px;
  text-decoration: none;
  text-align: center;
  cursor: pointer;
  transition: background-color 0.2s ease, box-shadow 0.2s ease;
  letter-spacing: 0.01em;
}

.btn-primary:hover {
  background-color: #1558b0;
}

.btn-primary:focus-visible {
  outline: 3px solid #ffdd57;
  outline-offset: 3px;
}
```

### Tone guidelines for content writers

```markdown
## CTA Writing Guidelines

### Do:
- Use concrete verbs: "Start", "View", "Schedule", "Contact", "Explore"
- State what happens next: "Schedule a Consultation" tells users exactly
  what to expect
- Keep CTAs to 2–4 words when possible
- Test with non-native speakers

### Don't:
- Use "Let's" — it presumes a relationship that doesn't exist yet
- Use idioms: "Grab a coffee", "Hit us up", "Drop us a line"
- Use abstract superlatives: "Something Great", "Amazing Things"
- Mix ultra-casual CTAs with formal body copy
```

### Components to audit

| Component / Section | Page(s) | What to fix |
|---|---|---|
| Hero CTA | Homepage | Change "Let's Build Something Great" → "Start Your Project" |
| Contact CTA | Homepage, About, Services | Change "Let's Chat" → "Schedule a Consultation" |
| Footer social heading | All pages | Change "Let's Get Social" → "Connect With Us" |
| Service page CTAs | Services | Review for idiomatic language |
| Blog post CTAs | Blog | "Check out" → "Read" or "View" |
| Contact page heading | Contact | Review for presumptive language |

---

## Examples from Other Sites

### McKinsey (mckinsey.com)
- CTAs are formal and concrete: "Contact us", "Read the article", "Subscribe to our insights".
- No contractions or colloquialisms in conversion-focused elements.
- Tone signals expertise and global professionalism.

### Accenture (accenture.com)
- CTAs: "Get in touch", "Read more", "Explore our services".
- Balanced tone — approachable but professional.
- Explicitly targets global audiences with region-specific content.

### Deloitte (deloitte.com)
- Formal, culturally neutral CTAs: "Contact us", "Learn more", "Read the report".
- Region selector prominently displayed, signaling international awareness.
- Demonstrates that professional tone and strong brand personality are not mutually exclusive.

### Pivotal Labs (now VMware Tanzu)
- Used "Talk to us" instead of "Let's chat" — slightly more formal, still approachable.
- Service descriptions used plain, concrete language rather than abstract enthusiasm.
- Showed that a tech consultancy can be warm without being colloquial.
