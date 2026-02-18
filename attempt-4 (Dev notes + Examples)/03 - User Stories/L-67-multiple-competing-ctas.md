# L-67: Multiple Competing CTAs Create Choice Overload

**Issue ID:** L-67
**Priority:** Low
**WCAG Criteria:** N/A (UX / cognitive load concern)
**Affected Personas:** Senior Person, ADHD

---

## User Story

As a **senior user** visiting the homepage, I want a clear, singular call-to-action per section so that I can understand what the company wants me to do next without being overwhelmed by 15+ competing buttons and links that all demand my attention.

---

## Acceptance Criteria

- [ ] Each homepage section contains **at most two** call-to-action elements: one primary CTA and optionally one secondary link.
- [ ] The total number of CTA buttons on the homepage is reduced to a maximum of 6–8 (from the current 15+).
- [ ] There is a clear visual hierarchy between primary CTAs (high prominence) and secondary actions (lower prominence).
- [ ] The primary CTA in each section relates directly to that section's content (e.g., the case study section's CTA leads to case studies, not a generic contact form).
- [ ] Removed or demoted CTAs are relocated to dedicated landing pages where they are more contextually appropriate.
- [ ] The homepage has one dominant CTA that appears in the hero section and is reinforced (not competed with) by CTAs in subsequent sections.
- [ ] Senior users and users with ADHD can identify the "main next step" within 5 seconds of viewing any section.

---

## How to Test the Change

### Manual Testing
1. Navigate to the launchpadlab.com homepage.
2. Count all CTA buttons and links:
   - Confirm the total is 8 or fewer.
   - Confirm no single viewport (one screenful of content) shows more than 2 CTA-styled elements.
3. For each section, identify the primary CTA:
   - It should be visually obvious which action is the main one.
   - Secondary links should be clearly subordinated (smaller, less prominent, text-style).
4. Perform a **five-second test** with 3–5 participants:
   - Show each section for 5 seconds.
   - Ask: "What is this section asking you to do?"
   - At least 4 of 5 should identify the same action.
5. Test the full page flow:
   - Scroll from top to bottom.
   - The CTAs should create a logical progression, not a random scatter.
6. Test with a senior user (or persona simulation) to confirm the experience feels focused rather than overwhelming.

### Automated Testing
1. Count CTA elements programmatically:
   ```javascript
   // Playwright example
   const ctaButtons = await page.$$('.cta-btn, .btn-primary, a.button, .hero-cta');
   expect(ctaButtons.length).toBeLessThanOrEqual(8);
   ```
2. Check for visual hierarchy (primary vs. secondary):
   ```javascript
   const primaryCTAs = await page.$$('.btn-primary, .cta-btn');
   const secondaryCTAs = await page.$$('.btn-secondary, .btn-outline, .text-link');

   for (const primary of primaryCTAs) {
     const pStyle = await primary.evaluate(el => {
       const cs = getComputedStyle(el);
       return { fontWeight: parseInt(cs.fontWeight), fontSize: parseFloat(cs.fontSize) };
     });
     // Primary should be visually dominant
     expect(pStyle.fontWeight).toBeGreaterThanOrEqual(600);
   }
   ```

---

## Developer Notes

### General Explanation
The homepage currently contains 15+ CTA elements across 11+ sections. This volume of calls-to-action creates **choice overload** (Hick's Law) — the more options presented, the longer it takes to make a decision, and the more likely a user is to make no decision at all. This is especially problematic for senior users and users with ADHD who are more susceptible to decision fatigue.

The fix involves reducing the number of CTAs, establishing a clear hierarchy, and creating a focused conversion path.

### Recommended CTA Strategy

**Before (current state — 15+ CTAs):**
| Section | CTAs |
|---|---|
| Hero | "Connect with an Expert" + "View Our Work" |
| Services | 6× "Learn More" links |
| Case Studies | "Cameo" + "GoHealth" + "View All" |
| Stats | "About Us" |
| Testimonials | "Read More" |
| Blog | "Read More" × 3 |
| Footer CTA | "Let's Build Something Great" |

**After (recommended — 6 CTAs):**
| Section | Primary CTA | Secondary |
|---|---|---|
| Hero | "Start a Project" (primary) | "See Our Work" (text link) |
| Services | — (cards link to service pages, no separate CTA) | — |
| Case Studies | "Explore Case Studies" | — |
| Social Proof / Stats | — (no CTA needed) | — |
| Blog | "Read Our Blog" | — |
| Footer | "Start a Project" (reinforces hero CTA) | — |

### Implementation Approach

**1. Reduce per-section CTAs:**
```html
<!-- BEFORE: section with multiple CTAs -->
<section class="case-studies">
  <a href="/case-studies/cameo/" class="cta-btn">Cameo</a>
  <a href="/case-studies/gohealth/" class="cta-btn">GoHealth</a>
  <a href="/case-studies/other/" class="cta-btn">Other</a>
  <a href="/case-studies/" class="cta-btn">View All Case Studies</a>
</section>

<!-- AFTER: single focused CTA -->
<section class="case-studies">
  <!-- Case study cards link naturally, one section CTA -->
  <a href="/case-studies/" class="cta-btn">Explore Case Studies</a>
</section>
```

**2. Establish visual hierarchy:**
```css
/* Primary CTA — one per section maximum */
.cta-primary {
  background-color: #2949E5;
  color: #fff;
  font-weight: 600;
  padding: 16px 32px;
  font-size: 1.125rem;
  border-radius: 6px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.15);
}

/* Secondary action — clearly subordinated */
.cta-secondary {
  background: transparent;
  color: #2949E5;
  font-weight: 400;
  padding: 8px 0;
  font-size: 1rem;
  text-decoration: underline;
  border: none;
  box-shadow: none;
}
```

**3. Consistent CTA text (relates to H-22):**
Choose one primary CTA phrase and use it consistently:
- Hero: "Start a Project"
- Footer: "Start a Project" (same phrase, reinforcing the hero)
- Avoid: "Connect with an Expert," "Let's Build," "Reach Out," "Let's Connect" — pick one.

### Components/Files to Audit
- Homepage template (`front-page.php`)
- Each section partial/template
- Service card component template (remove or demote individual "Learn More" CTAs)
- Case study carousel/card templates
- Footer CTA section template
- Global button/CTA style definitions

---

## Examples from Other Sites

- **Basecamp:** The homepage has exactly 2 CTAs — "Try it free" in the hero and "Try it free" in the closing section. Every other section uses descriptive content with no competing buttons.
- **Stripe:** Despite having extensive product offerings, the homepage uses a single "Start now" CTA in the hero, with section-specific CTAs that are clearly subordinated (text links, not buttons).
- **Linear:** The homepage features one "Get started" CTA that appears twice (hero and closing). All other content is informational with no competing buttons.
- **Notion:** Uses a maximum of 2 CTAs per viewport — one "Get Notion free" button and one "Request a demo" text link — maintaining clear hierarchy throughout the page.

---

## Additional Context

This issue is deeply connected to several other findings:
- **H-22 (Inconsistent CTA Terminology):** Reducing the number of CTAs inherently reduces inconsistency.
- **L-66 (Blue CTA Buttons Lack Non-Color Emphasis):** Establishing a clear primary/secondary visual hierarchy solves both issues.
- **L-48 (Excessive Homepage Length):** Reducing sections also reduces the number of CTAs.

The recommended approach is to address these three issues together as a homepage CTA strategy rework, ensuring the result is focused, consistent, and accessible.
