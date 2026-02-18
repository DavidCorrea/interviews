# 40. No AI Readiness Assessment or Self-Service Educational Path

**Priority:** Medium
**Location:** Sitewide (absent — no such feature exists)
**Reported by:** Margaret Sullivan (AI-Curious Business Executive)

---

## User Story

**As a** 57-year-old insurance brokerage president who is curious about AI but doesn't understand it,
**I want** a self-guided way to assess whether my business is ready for AI and learn the basics on my own terms,
**so that** I can build enough confidence and vocabulary to have an informed conversation with LaunchPad Lab — without feeling embarrassed about what I don't know.

---

## Problem

LaunchPad Lab's website assumes visitors already understand AI well enough to evaluate service offerings. For Margaret — an executive who is interested in AI but doesn't know where to start — the site offers no self-service educational path:

1. **No "AI Readiness Assessment."** There's no quiz, checklist, or diagnostic tool that helps a visitor understand whether their business is a good fit for AI, what kind of AI would help, or where to begin. Margaret can't answer the question "Is AI right for my business?" from anything on this site.

2. **No downloadable guide.** There's no "AI for Business Leaders" PDF, no "Getting Started with AI" email series, no educational resource that lets Margaret learn at her own pace. She has to piece together understanding from marketing copy on service pages — copy that assumes more knowledge than she has.

3. **No progressive learning path.** The site goes from "here's what we do" (service pages) straight to "contact us" (form). There's no intermediate step for someone who isn't ready to talk to sales but wants to learn more. The educational gap between "I'm curious" and "I'm ready to buy" is completely unserved.

4. **The Discovery Space Navigator is positioned as paid.** This service partially fills the educational role, but it's presented as a consulting engagement ("a six-week engagement") rather than a free self-service tool. Margaret sees it as a commitment, not a starting point.

### Why This Matters

Research from Gartner and McKinsey consistently shows that **executive AI adoption is blocked more by knowledge gaps than by budget constraints.** Executives who don't understand AI can't champion it internally, can't evaluate vendors, and can't approve budgets. The site's lack of educational tools means:

- Margaret leaves without converting because she still doesn't know enough to commit
- LaunchPad Lab misses a lead generation opportunity (gated content captures email addresses)
- Competitors who offer free assessments and guides capture Margaret's attention first

---

## Acceptance Criteria

### A. AI Readiness Assessment (Interactive Quiz)
- [ ] An interactive quiz titled "AI Readiness Assessment" (or similar) exists on the site
- [ ] The quiz contains 5–7 questions covering: current technology stack, data practices, business processes ripe for automation, team readiness, and budget expectations
- [ ] Questions use plain, non-technical language (no jargon, no acronyms without explanation)
- [ ] Each question has 3–4 answer options with clear, descriptive labels
- [ ] Upon completion, the user sees a personalized results page with:
  - A readiness score or tier (e.g., "Exploring," "Ready to Pilot," "Ready to Scale")
  - 2–3 specific recommendations based on their answers
  - A suggested next step (e.g., "Download our guide" or "Schedule a free consultation")
- [ ] The quiz can be completed without creating an account or providing an email (email is optional for receiving results via email)
- [ ] The quiz works on mobile and desktop
- [ ] The quiz is keyboard-navigable and screen reader accessible

### B. Downloadable Guide
- [ ] A downloadable "AI for Business Leaders" guide (PDF or web page) exists
- [ ] The guide covers: what AI is (in plain language), common business applications, how to evaluate if AI is right for your company, questions to ask vendors, and a glossary of key terms
- [ ] The guide is gated (email required) to serve as lead generation, with a clear privacy statement
- [ ] The download link appears on the quiz results page, homepage, and AI-related service pages
- [ ] The PDF is accessible (tagged PDF with reading order, alt text on images, bookmarks)

### C. Site Integration
- [ ] The AI Readiness Assessment is linked from the homepage (above the fold or in a prominent banner)
- [ ] The assessment is linked from the AI Automation service page
- [ ] The assessment is linked from the main navigation or a persistent CTA
- [ ] The assessment URL is shareable and bookmarkable (e.g., `/ai-readiness/`)
- [ ] Results are shareable (unique URL or "share your results" feature)

### D. Accessibility
- [ ] The quiz meets WCAG 2.1 AA standards
- [ ] All form controls have visible labels and are programmatically associated (`<label>` with `for`)
- [ ] Progress through the quiz is announced to screen readers
- [ ] Error states are communicated visually and programmatically
- [ ] Focus management moves logically between questions

---

## How to Test

### Quiz Functionality
1. Navigate to `/ai-readiness/` (or wherever the assessment lives)
2. Verify the page loads with a clear title, brief intro, and a visible "Start Assessment" button
3. Click "Start Assessment" — verify the first question loads with answer options
4. Select an answer — verify the quiz advances to the next question (or a "Next" button becomes active)
5. Complete all 5–7 questions
6. Verify a results page appears with: a readiness tier/score, personalized recommendations, and a CTA
7. Verify the results page includes a link to download the guide and/or schedule a consultation
8. Verify the quiz can be completed without entering an email address

### Keyboard & Screen Reader
1. Start the quiz using keyboard only (Tab to "Start," Enter to begin)
2. Navigate between answer options using Tab or Arrow keys
3. Select an answer using Enter or Space
4. Verify focus moves to the next question after selection
5. Use VoiceOver or NVDA: confirm each question is announced, answer options are described, and the progress indicator is communicated (e.g., "Question 2 of 5")
6. On the results page, confirm the readiness tier and recommendations are read in logical order

### Mobile
1. Open the quiz on a 375px viewport (iPhone SE size)
2. Verify all questions and answer options are fully visible without horizontal scrolling
3. Verify tap targets for answer options are at least 44×44px
4. Verify the results page is readable and the CTA buttons are tappable

### Lead Generation
1. On the results page, verify an email capture field is present but optional
2. Enter an email address — verify a confirmation message appears
3. Verify the submitted email appears in the CRM / email marketing tool (Mailchimp, HubSpot, etc.)
4. Verify a follow-up email is sent with the guide attached or linked

---

## Developer Notes

### Strategy

Build a lightweight, client-side interactive quiz that maps answers to one of three readiness tiers. The quiz serves dual purposes: (1) educational tool for AI-curious visitors and (2) lead generation for the sales team. Pair it with a downloadable PDF guide for visitors who want to learn offline.

### Quiz HTML Structure

```html
<main class="ai-assessment" aria-labelledby="assessment-heading">
  <header class="ai-assessment__header">
    <h1 id="assessment-heading">AI Readiness Assessment</h1>
    <p class="ai-assessment__intro">
      Not sure if AI is right for your business? Answer 5 quick questions
      to get a personalized recommendation — no technical knowledge required.
    </p>
    <p class="ai-assessment__time">
      <svg aria-hidden="true" width="16" height="16" viewBox="0 0 16 16">
        <circle cx="8" cy="8" r="7" stroke="currentColor" stroke-width="1.5" fill="none"/>
        <path d="M8 4v4l3 2" stroke="currentColor" stroke-width="1.5" fill="none" stroke-linecap="round"/>
      </svg>
      Takes about 2 minutes
    </p>
  </header>

  <!-- Progress bar -->
  <div class="ai-assessment__progress" role="progressbar"
       aria-valuenow="0" aria-valuemin="0" aria-valuemax="5"
       aria-label="Assessment progress">
    <div class="ai-assessment__progress-bar" style="width: 0%"></div>
    <span class="ai-assessment__progress-text sr-only">Question 0 of 5</span>
  </div>

  <!-- Quiz form -->
  <form id="ai-quiz" class="ai-quiz" novalidate>

    <!-- Question 1 -->
    <fieldset class="ai-quiz__question ai-quiz__question--active" data-question="1">
      <legend class="ai-quiz__legend">
        <span class="ai-quiz__step">Question 1 of 5</span>
        How would you describe your company's current use of technology?
      </legend>

      <div class="ai-quiz__options">
        <label class="ai-quiz__option">
          <input type="radio" name="q1" value="basic" required />
          <span class="ai-quiz__option-card">
            <strong>Mostly manual</strong>
            <span>We rely on spreadsheets, email, and paper-based processes</span>
          </span>
        </label>

        <label class="ai-quiz__option">
          <input type="radio" name="q1" value="moderate" />
          <span class="ai-quiz__option-card">
            <strong>Some software tools</strong>
            <span>We use industry-specific software but many processes are still manual</span>
          </span>
        </label>

        <label class="ai-quiz__option">
          <input type="radio" name="q1" value="advanced" />
          <span class="ai-quiz__option-card">
            <strong>Well-digitized</strong>
            <span>Most of our operations use modern software and we have good data practices</span>
          </span>
        </label>

        <label class="ai-quiz__option">
          <input type="radio" name="q1" value="cutting-edge" />
          <span class="ai-quiz__option-card">
            <strong>Already using some AI</strong>
            <span>We've experimented with or deployed AI tools in at least one area</span>
          </span>
        </label>
      </div>
    </fieldset>

    <!-- Question 2 -->
    <fieldset class="ai-quiz__question" data-question="2" hidden>
      <legend class="ai-quiz__legend">
        <span class="ai-quiz__step">Question 2 of 5</span>
        What's the biggest bottleneck in your business right now?
      </legend>

      <div class="ai-quiz__options">
        <label class="ai-quiz__option">
          <input type="radio" name="q2" value="data-entry" required />
          <span class="ai-quiz__option-card">
            <strong>Manual data entry and paperwork</strong>
            <span>Staff spend hours re-typing information between systems</span>
          </span>
        </label>

        <label class="ai-quiz__option">
          <input type="radio" name="q2" value="decisions" />
          <span class="ai-quiz__option-card">
            <strong>Slow decision-making</strong>
            <span>We have data but struggle to turn it into timely insights</span>
          </span>
        </label>

        <label class="ai-quiz__option">
          <input type="radio" name="q2" value="customer-service" />
          <span class="ai-quiz__option-card">
            <strong>Customer response time</strong>
            <span>Clients wait too long for answers, quotes, or resolutions</span>
          </span>
        </label>

        <label class="ai-quiz__option">
          <input type="radio" name="q2" value="scaling" />
          <span class="ai-quiz__option-card">
            <strong>Scaling without hiring</strong>
            <span>We need to handle more volume but can't keep adding headcount</span>
          </span>
        </label>
      </div>
    </fieldset>

    <!-- Question 3 -->
    <fieldset class="ai-quiz__question" data-question="3" hidden>
      <legend class="ai-quiz__legend">
        <span class="ai-quiz__step">Question 3 of 5</span>
        How does your team feel about adopting new technology?
      </legend>

      <div class="ai-quiz__options">
        <label class="ai-quiz__option">
          <input type="radio" name="q3" value="resistant" required />
          <span class="ai-quiz__option-card">
            <strong>Cautious</strong>
            <span>Most people prefer the tools they know — change is a hard sell</span>
          </span>
        </label>

        <label class="ai-quiz__option">
          <input type="radio" name="q3" value="mixed" />
          <span class="ai-quiz__option-card">
            <strong>Mixed</strong>
            <span>Some team members are eager, others are skeptical</span>
          </span>
        </label>

        <label class="ai-quiz__option">
          <input type="radio" name="q3" value="open" />
          <span class="ai-quiz__option-card">
            <strong>Generally open</strong>
            <span>The team adapts well when new tools are introduced thoughtfully</span>
          </span>
        </label>

        <label class="ai-quiz__option">
          <input type="radio" name="q3" value="eager" />
          <span class="ai-quiz__option-card">
            <strong>Eager</strong>
            <span>People actively ask for better tools and bring ideas to leadership</span>
          </span>
        </label>
      </div>
    </fieldset>

    <!-- Question 4 -->
    <fieldset class="ai-quiz__question" data-question="4" hidden>
      <legend class="ai-quiz__legend">
        <span class="ai-quiz__step">Question 4 of 5</span>
        How would you describe your company's data situation?
      </legend>

      <div class="ai-quiz__options">
        <label class="ai-quiz__option">
          <input type="radio" name="q4" value="scattered" required />
          <span class="ai-quiz__option-card">
            <strong>Scattered</strong>
            <span>Data lives in many places — some digital, some paper, some in people's heads</span>
          </span>
        </label>

        <label class="ai-quiz__option">
          <input type="radio" name="q4" value="partial" />
          <span class="ai-quiz__option-card">
            <strong>Partially organized</strong>
            <span>Key data is in digital systems but not always connected or clean</span>
          </span>
        </label>

        <label class="ai-quiz__option">
          <input type="radio" name="q4" value="organized" />
          <span class="ai-quiz__option-card">
            <strong>Well organized</strong>
            <span>We have centralized systems and most of our data is structured and accessible</span>
          </span>
        </label>

        <label class="ai-quiz__option">
          <input type="radio" name="q4" value="excellent" />
          <span class="ai-quiz__option-card">
            <strong>Excellent</strong>
            <span>We have a data strategy, clean pipelines, and analytics in place</span>
          </span>
        </label>
      </div>
    </fieldset>

    <!-- Question 5 -->
    <fieldset class="ai-quiz__question" data-question="5" hidden>
      <legend class="ai-quiz__legend">
        <span class="ai-quiz__step">Question 5 of 5</span>
        What best describes your AI budget expectations?
      </legend>

      <div class="ai-quiz__options">
        <label class="ai-quiz__option">
          <input type="radio" name="q5" value="exploring" required />
          <span class="ai-quiz__option-card">
            <strong>Just exploring</strong>
            <span>No budget allocated yet — I need to understand the opportunity first</span>
          </span>
        </label>

        <label class="ai-quiz__option">
          <input type="radio" name="q5" value="pilot" />
          <span class="ai-quiz__option-card">
            <strong>Ready for a small pilot</strong>
            <span>I could allocate budget for a focused proof-of-concept project</span>
          </span>
        </label>

        <label class="ai-quiz__option">
          <input type="radio" name="q5" value="committed" />
          <span class="ai-quiz__option-card">
            <strong>Budget approved</strong>
            <span>We have budget set aside for AI/automation initiatives this year</span>
          </span>
        </label>

        <label class="ai-quiz__option">
          <input type="radio" name="q5" value="scaling" />
          <span class="ai-quiz__option-card">
            <strong>Scaling existing investment</strong>
            <span>We've already invested in AI and want to expand to more areas</span>
          </span>
        </label>
      </div>
    </fieldset>

    <div class="ai-quiz__nav">
      <button type="button" class="ai-quiz__btn ai-quiz__btn--prev" hidden>
        ← Previous
      </button>
      <button type="button" class="ai-quiz__btn ai-quiz__btn--next">
        Next →
      </button>
      <button type="submit" class="ai-quiz__btn ai-quiz__btn--submit" hidden>
        See My Results
      </button>
    </div>
  </form>

  <!-- Results (hidden until quiz completion) -->
  <section id="ai-results" class="ai-results" hidden aria-labelledby="results-heading">
    <h2 id="results-heading">Your AI Readiness Results</h2>

    <div class="ai-results__score">
      <div class="ai-results__tier" data-tier="">
        <!-- Tier name injected by JS -->
      </div>
      <p class="ai-results__summary">
        <!-- Summary text injected by JS -->
      </p>
    </div>

    <div class="ai-results__recommendations">
      <h3>Our Recommendations</h3>
      <ul id="recommendations-list">
        <!-- Recommendations injected by JS -->
      </ul>
    </div>

    <div class="ai-results__cta">
      <a href="/contact/" class="ai-results__btn ai-results__btn--primary">
        Schedule a Free Consultation
      </a>
      <button type="button" class="ai-results__btn ai-results__btn--secondary"
              data-action="download-guide">
        Download "AI for Business Leaders" Guide
      </button>
    </div>

    <!-- Optional email capture -->
    <div class="ai-results__email">
      <p>Want your results emailed to you?</p>
      <form class="ai-results__email-form" id="results-email-form">
        <label for="results-email" class="sr-only">Email address</label>
        <input
          type="email"
          id="results-email"
          name="email"
          placeholder="your@email.com"
          autocomplete="email"
        />
        <button type="submit">Send Results</button>
      </form>
      <p class="ai-results__privacy">
        We'll send your results and guide — nothing else.
        <a href="/privacy/">Privacy policy</a>
      </p>
    </div>
  </section>
</main>
```

### Quiz CSS

```css
.ai-assessment {
  max-width: 720px;
  margin: 0 auto;
  padding: 3rem 2rem 4rem;
}

.ai-assessment__header {
  text-align: center;
  margin-bottom: 2.5rem;
}

.ai-assessment__header h1 {
  font-size: 2rem;
  font-weight: 800;
  color: #111827;
  margin: 0 0 0.75rem;
}

.ai-assessment__intro {
  font-size: 1.125rem;
  line-height: 1.7;
  color: #4b5563;
  max-width: 540px;
  margin: 0 auto 1rem;
}

.ai-assessment__time {
  display: inline-flex;
  align-items: center;
  gap: 0.375rem;
  font-size: 0.875rem;
  color: #6b7280;
}

/* Progress bar */
.ai-assessment__progress {
  height: 6px;
  background-color: #e5e7eb;
  border-radius: 999px;
  overflow: hidden;
  margin-bottom: 2.5rem;
}

.ai-assessment__progress-bar {
  height: 100%;
  background-color: #2563eb;
  border-radius: 999px;
  transition: width 0.3s ease;
}

/* Quiz questions */
.ai-quiz__question {
  border: none;
  padding: 0;
  margin: 0;
}

.ai-quiz__question[hidden] {
  display: none;
}

.ai-quiz__legend {
  font-size: 1.25rem;
  font-weight: 700;
  color: #111827;
  line-height: 1.5;
  margin-bottom: 1.5rem;
  display: block;
}

.ai-quiz__step {
  display: block;
  font-size: 0.8125rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: #2563eb;
  margin-bottom: 0.5rem;
}

/* Answer option cards */
.ai-quiz__options {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.ai-quiz__option {
  cursor: pointer;
}

.ai-quiz__option input[type="radio"] {
  position: absolute;
  opacity: 0;
  width: 0;
  height: 0;
}

.ai-quiz__option-card {
  display: block;
  padding: 1.25rem 1.5rem;
  border: 2px solid #e5e7eb;
  border-radius: 12px;
  background: #fff;
  transition: border-color 0.15s, background-color 0.15s, box-shadow 0.15s;
}

.ai-quiz__option-card strong {
  display: block;
  font-size: 1rem;
  color: #111827;
  margin-bottom: 0.25rem;
}

.ai-quiz__option-card span {
  font-size: 0.9375rem;
  color: #6b7280;
  line-height: 1.5;
}

.ai-quiz__option input:checked + .ai-quiz__option-card {
  border-color: #2563eb;
  background-color: #eff6ff;
  box-shadow: 0 0 0 1px #2563eb;
}

.ai-quiz__option input:focus-visible + .ai-quiz__option-card {
  outline: 2px solid #2563eb;
  outline-offset: 2px;
}

.ai-quiz__option:hover .ai-quiz__option-card {
  border-color: #93c5fd;
  background-color: #f8faff;
}

/* Navigation buttons */
.ai-quiz__nav {
  display: flex;
  justify-content: space-between;
  margin-top: 2rem;
  gap: 1rem;
}

.ai-quiz__btn {
  padding: 0.875rem 2rem;
  font-size: 1rem;
  font-weight: 600;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.15s, color 0.15s;
}

.ai-quiz__btn--prev {
  background: none;
  border: 1px solid #d1d5db;
  color: #374151;
}

.ai-quiz__btn--prev:hover {
  background-color: #f3f4f6;
}

.ai-quiz__btn--next,
.ai-quiz__btn--submit {
  background-color: #2563eb;
  color: #fff;
  border: none;
  margin-left: auto;
}

.ai-quiz__btn--next:hover,
.ai-quiz__btn--submit:hover {
  background-color: #1d4ed8;
}

.ai-quiz__btn:focus-visible {
  outline: 2px solid #2563eb;
  outline-offset: 2px;
}

.ai-quiz__btn[hidden] {
  display: none;
}

/* Results section */
.ai-results {
  text-align: center;
  padding-top: 2rem;
}

.ai-results[hidden] {
  display: none;
}

.ai-results__score {
  margin-bottom: 2.5rem;
}

.ai-results__tier {
  display: inline-block;
  padding: 0.5rem 1.5rem;
  font-size: 1.25rem;
  font-weight: 700;
  border-radius: 999px;
  margin-bottom: 1rem;
}

.ai-results__tier[data-tier="exploring"] {
  background-color: #fef3c7;
  color: #92400e;
}

.ai-results__tier[data-tier="ready-to-pilot"] {
  background-color: #dbeafe;
  color: #1e40af;
}

.ai-results__tier[data-tier="ready-to-scale"] {
  background-color: #d1fae5;
  color: #065f46;
}

.ai-results__summary {
  font-size: 1.125rem;
  line-height: 1.7;
  color: #374151;
  max-width: 560px;
  margin: 0 auto;
}

.ai-results__recommendations {
  text-align: left;
  max-width: 560px;
  margin: 0 auto 2.5rem;
}

.ai-results__recommendations h3 {
  font-size: 1.125rem;
  margin-bottom: 1rem;
}

.ai-results__recommendations li {
  font-size: 1rem;
  line-height: 1.6;
  color: #374151;
  margin-bottom: 0.75rem;
  padding-left: 0.5rem;
}

.ai-results__cta {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 2.5rem;
}

.ai-results__btn {
  padding: 1rem 2rem;
  font-size: 1rem;
  font-weight: 600;
  border-radius: 8px;
  text-decoration: none;
  cursor: pointer;
}

.ai-results__btn--primary {
  background-color: #2563eb;
  color: #fff;
  border: none;
}

.ai-results__btn--primary:hover {
  background-color: #1d4ed8;
}

.ai-results__btn--secondary {
  background: #fff;
  color: #2563eb;
  border: 2px solid #2563eb;
}

.ai-results__btn--secondary:hover {
  background-color: #eff6ff;
}

.ai-results__btn:focus-visible {
  outline: 2px solid #2563eb;
  outline-offset: 2px;
}

/* Email capture */
.ai-results__email {
  max-width: 440px;
  margin: 0 auto;
  padding: 1.5rem;
  background-color: #f9fafb;
  border-radius: 12px;
}

.ai-results__email-form {
  display: flex;
  gap: 0.5rem;
  margin-top: 0.75rem;
}

.ai-results__email-form input {
  flex: 1;
  padding: 0.75rem 1rem;
  border: 1px solid #d1d5db;
  border-radius: 8px;
  font-size: 1rem;
}

.ai-results__email-form input:focus {
  outline: 2px solid #2563eb;
  outline-offset: -1px;
  border-color: #2563eb;
}

.ai-results__email-form button {
  padding: 0.75rem 1.5rem;
  background-color: #111827;
  color: #fff;
  border: none;
  border-radius: 8px;
  font-weight: 600;
  cursor: pointer;
}

.ai-results__privacy {
  font-size: 0.8125rem;
  color: #9ca3af;
  margin-top: 0.5rem;
}

.ai-results__privacy a {
  color: #6b7280;
  text-decoration: underline;
}

@media (max-width: 600px) {
  .ai-assessment {
    padding: 2rem 1rem 3rem;
  }

  .ai-assessment__header h1 {
    font-size: 1.5rem;
  }

  .ai-results__cta {
    flex-direction: column;
  }

  .ai-results__email-form {
    flex-direction: column;
  }
}
```

### Quiz JavaScript Logic

```javascript
class AIReadinessQuiz {
  constructor(formEl) {
    this.form = formEl;
    this.questions = this.form.querySelectorAll('.ai-quiz__question');
    this.prevBtn = this.form.querySelector('.ai-quiz__btn--prev');
    this.nextBtn = this.form.querySelector('.ai-quiz__btn--next');
    this.submitBtn = this.form.querySelector('.ai-quiz__btn--submit');
    this.progressBar = document.querySelector('.ai-assessment__progress-bar');
    this.progressEl = document.querySelector('.ai-assessment__progress');
    this.resultsSection = document.getElementById('ai-results');
    this.currentIndex = 0;
    this.totalQuestions = this.questions.length;

    this.scoringMap = {
      q1: { 'basic': 1, 'moderate': 2, 'advanced': 3, 'cutting-edge': 4 },
      q2: { 'data-entry': 2, 'decisions': 3, 'customer-service': 3, 'scaling': 4 },
      q3: { 'resistant': 1, 'mixed': 2, 'open': 3, 'eager': 4 },
      q4: { 'scattered': 1, 'partial': 2, 'organized': 3, 'excellent': 4 },
      q5: { 'exploring': 1, 'pilot': 2, 'committed': 3, 'scaling': 4 },
    };

    this.tiers = [
      {
        id: 'exploring',
        name: 'Exploring AI',
        range: [5, 10],
        summary: `Your business has real potential for AI, but there's groundwork
          to lay first. That's perfectly normal — most companies start here.
          Focus on organizing your data and identifying one high-impact process
          to automate.`,
        recommendations: [
          'Start by documenting your top 3 most time-consuming manual processes',
          'Invest in cleaning and centralizing your key business data',
          'Read our "AI for Business Leaders" guide to build your vocabulary',
          'Consider a Discovery engagement to map AI to your specific workflows',
        ],
      },
      {
        id: 'ready-to-pilot',
        name: 'Ready to Pilot',
        range: [11, 15],
        summary: `Your business has the foundation for a successful AI pilot.
          You have some digital infrastructure, a team that's at least open to
          change, and awareness of where AI could help. The next step is a
          focused proof-of-concept.`,
        recommendations: [
          'Identify one specific process to automate as a pilot (start small, prove value)',
          'Build an internal champion team — 2-3 people who will own the pilot',
          'Schedule a consultation to scope a 6-8 week proof-of-concept project',
          'Set clear success metrics before starting (hours saved, error rate, response time)',
        ],
      },
      {
        id: 'ready-to-scale',
        name: 'Ready to Scale',
        range: [16, 20],
        summary: `Your business is well-positioned for AI implementation at scale.
          You have strong data practices, an engaged team, and budget
          commitment. The opportunity now is to move from isolated tools to a
          strategic AI roadmap across your operations.`,
        recommendations: [
          'Create an AI roadmap that prioritizes initiatives by ROI and feasibility',
          'Evaluate enterprise AI platforms for your industry (not just point solutions)',
          'Establish an AI governance framework — data privacy, model monitoring, compliance',
          'Schedule a strategy session to identify your highest-ROI AI opportunities',
        ],
      },
    ];

    this.init();
  }

  init() {
    this.prevBtn.addEventListener('click', () => this.prev());
    this.nextBtn.addEventListener('click', () => this.next());
    this.form.addEventListener('submit', (e) => {
      e.preventDefault();
      this.showResults();
    });

    this.form.querySelectorAll('input[type="radio"]').forEach((radio) => {
      radio.addEventListener('change', () => this.onAnswerSelected());
    });

    this.updateUI();
  }

  onAnswerSelected() {
    // Auto-advance after a short delay for a smoother experience
    // (do NOT auto-advance on the last question — let the user click Submit)
    if (this.currentIndex < this.totalQuestions - 1) {
      setTimeout(() => this.next(), 400);
    }
  }

  next() {
    const currentQ = this.questions[this.currentIndex];
    const selected = currentQ.querySelector('input:checked');
    if (!selected) {
      this.showValidation(currentQ);
      return;
    }

    if (this.currentIndex < this.totalQuestions - 1) {
      this.currentIndex++;
      this.updateUI();
    }
  }

  prev() {
    if (this.currentIndex > 0) {
      this.currentIndex--;
      this.updateUI();
    }
  }

  updateUI() {
    this.questions.forEach((q, i) => {
      q.hidden = i !== this.currentIndex;
      q.classList.toggle('ai-quiz__question--active', i === this.currentIndex);
    });

    this.prevBtn.hidden = this.currentIndex === 0;
    const isLast = this.currentIndex === this.totalQuestions - 1;
    this.nextBtn.hidden = isLast;
    this.submitBtn.hidden = !isLast;

    const progress = ((this.currentIndex) / this.totalQuestions) * 100;
    this.progressBar.style.width = `${progress}%`;
    this.progressEl.setAttribute('aria-valuenow', this.currentIndex);

    const srText = this.progressEl.querySelector('.sr-only');
    if (srText) {
      srText.textContent = `Question ${this.currentIndex + 1} of ${this.totalQuestions}`;
    }

    this.questions[this.currentIndex].querySelector('legend')?.focus();
  }

  showValidation(questionEl) {
    const legend = questionEl.querySelector('.ai-quiz__legend');
    if (!legend.querySelector('.ai-quiz__error')) {
      const error = document.createElement('span');
      error.className = 'ai-quiz__error';
      error.setAttribute('role', 'alert');
      error.textContent = 'Please select an option to continue';
      legend.appendChild(error);
    }
  }

  calculateScore() {
    let total = 0;
    for (let i = 1; i <= this.totalQuestions; i++) {
      const selected = this.form.querySelector(`input[name="q${i}"]:checked`);
      if (selected) {
        total += this.scoringMap[`q${i}`][selected.value] || 0;
      }
    }
    return total;
  }

  getTier(score) {
    return this.tiers.find(
      (t) => score >= t.range[0] && score <= t.range[1]
    ) || this.tiers[0];
  }

  showResults() {
    const score = this.calculateScore();
    const tier = this.getTier(score);

    this.form.hidden = true;
    document.querySelector('.ai-assessment__progress').hidden = true;
    this.resultsSection.hidden = false;

    const tierEl = this.resultsSection.querySelector('.ai-results__tier');
    tierEl.dataset.tier = tier.id;
    tierEl.textContent = tier.name;

    this.resultsSection.querySelector('.ai-results__summary').textContent = tier.summary;

    const recList = this.resultsSection.querySelector('#recommendations-list');
    recList.innerHTML = tier.recommendations
      .map((r) => `<li>${r}</li>`)
      .join('');

    this.resultsSection.scrollIntoView({ behavior: 'smooth', block: 'start' });
    this.resultsSection.querySelector('h2').focus();

    this.trackCompletion(tier.id, score);
  }

  trackCompletion(tierId, score) {
    if (typeof gtag === 'function') {
      gtag('event', 'ai_readiness_complete', {
        event_category: 'engagement',
        event_label: tierId,
        value: score,
      });
    }
  }
}

document.addEventListener('DOMContentLoaded', () => {
  const quizForm = document.getElementById('ai-quiz');
  if (quizForm) new AIReadinessQuiz(quizForm);
});
```

### Downloadable Guide — Landing Section

For the PDF guide, add a gated download section on the results page and link it from other pages:

```html
<section class="guide-download" aria-labelledby="guide-heading">
  <div class="guide-download__content">
    <div class="guide-download__text">
      <h2 id="guide-heading">Free Guide: AI for Business Leaders</h2>
      <p>
        A plain-language guide for executives who want to understand AI
        without the hype. Covers what AI actually does, how to evaluate if
        it's right for your business, the questions to ask vendors, and a
        glossary of terms you'll actually encounter.
      </p>
      <ul class="guide-download__toc">
        <li>What AI is (and isn't) — in plain English</li>
        <li>5 real business processes AI can automate today</li>
        <li>How to evaluate AI readiness at your company</li>
        <li>10 questions to ask any AI vendor</li>
        <li>Glossary: 30 AI terms every executive should know</li>
      </ul>
    </div>
    <form class="guide-download__form" id="guide-form">
      <label for="guide-email">Get the free guide:</label>
      <div class="guide-download__input-group">
        <input
          type="email"
          id="guide-email"
          name="email"
          placeholder="you@company.com"
          required
          autocomplete="email"
        />
        <button type="submit">Download PDF</button>
      </div>
      <p class="guide-download__privacy">
        No spam, ever. <a href="/privacy/">Privacy policy</a>
      </p>
    </form>
  </div>
</section>
```

### Homepage / Service Page CTA Banner

Link the assessment prominently from high-traffic pages:

```html
<aside class="ai-cta-banner" aria-label="AI Readiness Assessment">
  <div class="ai-cta-banner__content">
    <h2>Not sure if AI is right for your business?</h2>
    <p>
      Take our free 2-minute assessment and get a personalized recommendation
      — no technical knowledge required.
    </p>
    <a href="/ai-readiness/" class="ai-cta-banner__btn">
      Take the AI Readiness Assessment
      <span aria-hidden="true">→</span>
    </a>
  </div>
</aside>
```

```css
.ai-cta-banner {
  background: linear-gradient(135deg, #1e3a5f, #2563eb);
  color: #fff;
  padding: 3rem 2rem;
  border-radius: 16px;
  margin: 3rem 0;
  text-align: center;
}

.ai-cta-banner h2 {
  font-size: 1.5rem;
  font-weight: 700;
  margin: 0 0 0.75rem;
}

.ai-cta-banner p {
  font-size: 1.0625rem;
  opacity: 0.9;
  max-width: 480px;
  margin: 0 auto 1.5rem;
  line-height: 1.6;
}

.ai-cta-banner__btn {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 1rem 2rem;
  background-color: #fff;
  color: #1e3a5f;
  font-weight: 700;
  font-size: 1rem;
  border-radius: 8px;
  text-decoration: none;
  transition: background-color 0.15s, transform 0.15s;
}

.ai-cta-banner__btn:hover {
  background-color: #f0f7ff;
  transform: translateY(-1px);
}

.ai-cta-banner__btn:focus-visible {
  outline: 2px solid #fff;
  outline-offset: 2px;
}
```

### WCAG References

- **WCAG 2.1 SC 1.3.1 Info and Relationships (A):** Quiz questions use `<fieldset>` and `<legend>` to associate labels with radio groups; progress bar uses `role="progressbar"` with `aria-valuenow`
- **WCAG 2.1 SC 1.3.5 Identify Input Purpose (AA):** Email input uses `autocomplete="email"`
- **WCAG 2.1 SC 2.4.3 Focus Order (A):** Focus moves logically from question to question, and to the results section upon completion
- **WCAG 2.1 SC 3.3.1 Error Identification (A):** Validation errors are announced via `role="alert"` and describe the error
- **WCAG 2.1 SC 3.3.2 Labels or Instructions (A):** Every form control has a visible label or instructions
- **WCAG 2.1 SC 4.1.3 Status Messages (AA):** Progress updates are communicated via `aria-valuenow` and screen reader-only text

### Components to Audit

| Component / Section | Page(s) | What to Build/Fix |
|---|---|---|
| AI Readiness Assessment | New page (`/ai-readiness/`) | Build interactive 5-question quiz with results engine |
| CTA banner | Homepage, AI Automation page | Add prominent link to assessment |
| Navigation CTA | Global nav | Add "AI Assessment" or "Is AI Right for You?" link |
| Guide download form | Assessment results, Homepage, AI pages | Build gated PDF download with email capture |
| PDF guide | New asset | Create accessible PDF guide (tagged, with bookmarks) |
| Analytics events | Assessment page | Track quiz starts, completions, tier results, email captures |
| CRM integration | Email form | Connect email capture to HubSpot/Mailchimp for nurture sequence |

---

## Examples from Other Sites

### HubSpot (hubspot.com/marketing-grader)
HubSpot's "Website Grader" is the gold standard for self-service assessment tools. Enter your URL, answer a few questions, and get a scored report with specific recommendations. It's been a top lead-generation tool for over a decade. The key: it provides genuine value (a real analysis) while capturing leads.

### McKinsey (mckinsey.com/capabilities/quantumblack/our-insights/ai-readiness)
McKinsey published an "AI Readiness" framework with a self-assessment component. It asks questions about data maturity, organizational readiness, and strategic alignment. The output maps to their consulting engagement tiers. Importantly, it uses executive-level language — no developer jargon.

### Salesforce (salesforce.com/form/ai-assessment)
Salesforce offers an "AI Maturity Assessment" that categorizes businesses into four stages: Aware, Experimenting, Operationalizing, and Transforming. Results include a maturity score and tailored recommendations. The quiz is short (6 questions) and uses plain language.

### IBM (ibm.com/watson)
IBM's Watson pages include an "AI Use Case Explorer" that helps visitors discover relevant AI applications by industry. While not a quiz, it serves the same educational purpose — helping AI-curious visitors find relevant information without needing prior knowledge.

### Drift / Salesloft (salesloft.com)
Their "Revenue Maturity Assessment" follows the same pattern: a short quiz, personalized results, and a gated guide download. The quiz doubles as lead qualification — sales teams know exactly where the prospect is in their journey before the first call.

### Key Patterns
1. **Keep it short** — 5-7 questions maximum. Every additional question reduces completion rate.
2. **Use plain language** — The target audience doesn't know AI terminology. Write for a smart 12-year-old.
3. **Provide real value** — Results should teach something, not just say "contact us." Specific recommendations build trust.
4. **Gate the guide, not the quiz** — Let people complete the quiz without an email. Ask for email to get the guide or results via email.
5. **Link everywhere** — The assessment should be discoverable from the homepage, service pages, blog posts, and navigation. It's both an educational tool and a top-of-funnel conversion path.
