# Accessibility Technical Report: Senior Person (Elderly User)

**Persona:** Eleanor Morrison (Senior Person, 70+)  
**Website:** https://launchpadlab.com/  
**Date:** February 16, 2025  
**Testing Focus:** Conventional labels, text size/contrast, jargon clarity, contact path, and layout predictability for users aged 70+ with age-related vision decline and slower processing speed.

---

## Executive Summary

The LaunchPad Lab website presents significant accessibility barriers for senior users (70+). Unconventional navigation labels ("Connect with an Expert" instead of "Contact"), small/low-contrast text, jargon-heavy content, testimonials above the contact form, and form-only contact with no prominent phone/email create confusion and frustration. Users can complete core tasks but require disproportionate effort. WCAG 2.1 criteria 2.4.4, 3.2.4, 1.4.3, 1.4.4, and 3.1.3 are implicated.

---

## Issues Identified

### 1. Unconventional Link Purpose — "Connect with an Expert" vs "Contact"

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.4 Link Purpose (In Context) — Level A |
| **Severity** | High |
| **Finding** | Primary contact CTA is labeled "Connect with an Expert" rather than "Contact" or "Contact Us." Senior users expect conventional navigation labels. The link purpose is not clear from the link text alone; users must decode that "Connect with an Expert" leads to the contact page. |
| **Impact** | Users hesitate, second-guess, or search for "Contact" before recognizing the CTA. Cognitive load increases. Contact path is not obvious. Some users may abandon before finding how to reach the company. |
| **Fix** | Add "Contact" to primary navigation. Use "Contact Us" or "Contact" as the primary label. If "Connect with an Expert" is retained for marketing, pair it with "Contact" (e.g., "Contact — Connect with an Expert"). Ensure link purpose is unambiguous. |
| **WCAG Criterion** | 2.4.4 — "The purpose of each link can be determined from the link text alone or from the link text together with its programmatically determined link context." |

---

### 2. Inconsistent Component Identification

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 3.2.4 Consistent Identification — Level AA |
| **Severity** | Medium |
| **Finding** | Components that have the same functionality are not identified consistently. The contact path appears as "Connect with an Expert" in the nav, while the resulting page may be titled "Contact" or similar. Footer may use different phrasing. Inconsistent labels force users to re-learn what each component does. |
| **Impact** | Senior users rely on predictable patterns. When the same function (contact) appears under different labels across the site, confusion increases. Users who learned "Connect with an Expert" = contact on the homepage may not recognize equivalent links elsewhere if labeled differently. |
| **Fix** | Use consistent "Contact" labeling site-wide for the contact function. Ensure nav, page title, footer, and any CTAs that lead to contact use the same or clearly equivalent terminology. |
| **WCAG Criterion** | 3.2.4 — "Components that have the same functionality within a set of Web pages are identified consistently." |

---

### 3. Low Contrast (Body Text)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.3 Contrast (Minimum) — Level AA |
| **Severity** | High |
| **Finding** | Body text appears in light gray (#666–#777) on white backgrounds. Contrast ratio likely below 4.5:1 for normal text. Service descriptions, testimonials, form labels, and secondary content affected. Thin font weights exacerbate the issue. |
| **Impact** | Age-related vision decline makes low-contrast text difficult or impossible to read. Users squint, lean in, or increase zoom. Reading requires excessive effort; fatigue increases. Content may be skipped or misread. |
| **Fix** | Use text color of at least #595959 on white to achieve 4.5:1. For AAA (7:1), use #404040 or darker. Apply to all body text, labels, captions, testimonials, and form labels. Increase font weight to 500 minimum for body copy. |
| **WCAG Criterion** | 1.4.3 — "The visual presentation of text and images of text has a contrast ratio of at least 4.5:1." |

---

### 4. Small Text and Resize Behavior

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 1.4.4 Resize Text (Level AA), 1.4.8 Visual Presentation (Level AAA) |
| **Severity** | High |
| **Finding** | Body text may be below 16px at default zoom. Senior users require 16px minimum; 18px+ preferred for comfortable reading. Thin font weights reduce effective legibility. Some text may not scale adequately with user font-size preferences. |
| **Impact** | Users must increase browser zoom to 150–200% to read comfortably. Combined with low contrast and thin fonts, even zoomed text strains. Reading becomes a chore rather than a natural flow. |
| **Fix** | Set base body font size to 16px minimum (1rem). Use rem/em for scaling. Ensure text scales with user preferences. Use font-weight 500+ for body text. Support browser zoom and user font-size settings without layout breakage. |
| **WCAG Criterion** | 1.4.4 — "Except for captions and images of text, text can be resized without assistive technology up to 200 percent without loss of content or functionality." |

---

### 5. Unusual Words (Jargon) Without Definitions

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 3.1.3 Unusual Words (Level AAA) |
| **Severity** | High |
| **Finding** | The site uses industry and marketing jargon without definitions: "AI-centric," "digital product design," "development firm," "bespoke," "agentic," "agentic AI," "discovery process," "seamless handoff," "cross-functional," "proof of concept." Terms appear in hero, service descriptions, testimonials, and About page. |
| **Impact** | Senior users with slower processing speed cannot quickly decode abstract terms. Jargon creates skepticism and distrust. Core task ("find what they do") requires excessive effort. Users may leave before understanding the company's purpose. |
| **Fix** | Provide plain-language equivalents. Add hero summary: "We build websites and mobile apps for businesses. We help you add AI to your products." Expand first use of jargon: "AI-centric (focused on artificial intelligence)," "bespoke (custom-built for your needs)," "discovery process (we learn about your business before building)." |
| **WCAG Criterion** | 3.1.3 — "A mechanism is available for identifying specific definitions of words or phrases used in an unusual or restricted way, including idioms and jargon." |

---

### 6. Contact Form Buried Below Testimonials

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.1 Bypass Blocks (Level A), 2.4.6 Headings and Labels |
| **Severity** | Medium |
| **Finding** | Contact page displays five long testimonial blocks above the contact form. Users must scroll extensively to reach the form. No "Skip to contact form" link. Testimonials use same jargon as main copy. |
| **Impact** | Users who came to contact must wade through dense content first. Senior users read methodically; scrolling past five testimonials feels like a barrier. Frustration increases. Some may abandon. Form completion rate may drop. |
| **Fix** | Move contact form above testimonials. Or add "Skip to contact form" link at top of Contact page. Place form as primary content; testimonials below or in separate section. |
| **WCAG Criterion** | 2.4.1 Bypass Blocks — "A mechanism is available to bypass blocks of content that are repeated on multiple Web pages." |

---

### 7. Phone and Email Not Prominently Displayed

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.4 Link Purpose, 2.4.6 Headings and Labels |
| **Severity** | Medium |
| **Finding** | Phone number and email appear in footer but are not prominent. Senior users prefer direct communication (phone/email) over forms. Contact page emphasizes form; direct contact methods are secondary or buried. |
| **Impact** | Users who prefer to call or email must hunt. Trust in form submission is lower; users worry about whether message was received. Barrier for users who avoid or struggle with forms. |
| **Fix** | Display phone number and email prominently on Contact page, above or beside the form. Ensure footer contact info is clearly labeled and readable. Provide multiple contact paths. |
| **WCAG Criterion** | 2.4.4, 2.4.6 |

---

### 8. Too Many Options (Six Service Boxes)

| Attribute | Details |
|----------|---------|
| **WCAG Ref** | 2.4.6 Headings and Labels, 3.2.4 Consistent Identification |
| **Severity** | Medium |
| **Finding** | Homepage presents six service boxes with multiple "Learn more" links. Dense layout with many CTAs. Senior users with slower processing are overwhelmed by choice. |
| **Impact** | "Which one do I click?" confusion. Cognitive overload. Users may give up or choose incorrectly. Clear path is obscured. |
| **Fix** | Consolidate or prioritize services. Provide clear primary path (e.g., "Learn about our services" with single entry point). Reduce visual density. Use progressive disclosure. |
| **WCAG Criterion** | 2.4.6, 3.2.4 |

---

## Summary Table

| Issue | WCAG Ref | Severity | Priority |
|-------|----------|----------|----------|
| "Connect with an Expert" vs "Contact" | 2.4.4 | High | P0 |
| Inconsistent contact labeling | 3.2.4 | Medium | P1 |
| Low contrast (body text) | 1.4.3 | High | P0 |
| Small text / resize | 1.4.4 | High | P0 |
| Jargon without definitions | 3.1.3 | High | P0 |
| Form buried below testimonials | 2.4.1 | Medium | P1 |
| Phone/email not prominent | 2.4.4, 2.4.6 | Medium | P1 |
| Too many options | 2.4.6, 3.2.4 | Medium | P1 |

---

## Recommended Remediation Order

1. **Add "Contact" to navigation** — Replace or supplement "Connect with an Expert" with conventional "Contact" label. Ensure link purpose is clear.
2. **Increase contrast** — Darken all body text to meet 4.5:1 minimum (7:1 preferred). Apply to testimonials, form labels, footer.
3. **Increase text size and font weight** — Body text 16px minimum, 18px preferred. Font weight 500+ for body copy.
4. **Add plain-language hero summary** — "We build websites and mobile apps for businesses. We help you add AI to your products. Contact us to discuss your project."
5. **Move contact form above testimonials** — Or add "Skip to contact form" link. Put form first on Contact page.
6. **Display phone and email prominently** — On Contact page, above or beside form. Clear labeling in footer.
7. **Consistent contact identification** — Use "Contact" consistently site-wide for contact function.
8. **Reduce option overload** — Simplify service presentation; provide clearer primary path.

---

## References

- [WCAG 2.1 Success Criterion 2.4.4 Link Purpose (In Context)](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
- [WCAG 2.1 Success Criterion 3.2.4 Consistent Identification](https://www.w3.org/WAI/WCAG21/Understanding/consistent-identification.html)
- [WCAG 2.1 Success Criterion 1.4.3 Contrast (Minimum)](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
- [WCAG 2.1 Success Criterion 1.4.4 Resize Text](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
- [WCAG 2.1 Success Criterion 3.1.3 Unusual Words (Level AAA)](https://www.w3.org/WAI/WCAG21/Understanding/unusual-words.html)
