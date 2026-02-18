# Technical Report: Skeptical User — Trust, Transparency & Clarity

**Website:** https://launchpadlab.com/  
**Persona:** Jordan Reyes (Skeptical User)  
**Test Date:** February 16, 2025  
**Test Task:** Find what the company does and how to contact them

---

## Executive Summary

LaunchPad Lab's website presents significant trust and transparency barriers for skeptical users who value evidence, specificity, and honest communication. The persona (Jordan Reyes) completed the task of understanding what the company does and finding contact information, but reported low trust and would not engage without additional verification. The primary issues center on **vague marketing language**, **lack of measurable evidence in case studies**, **no pricing information or framework**, **testimonials without full attribution**, **contact information buried below testimonials**, and **no explicit process description or scope limitations**. The site avoids obvious dark patterns (fake urgency, pre-checked opt-ins) but prioritizes persuasion over utility, which backfires for evidence-seeking buyers. Implementing case studies with measurable outcomes, a pricing framework, clearer process steps, and prominent contact placement would substantially improve credibility for skeptical users.

**Key findings:**
- Vague claims ("Results that Matter," "Your Strategic AI Partner") without evidence or quantification
- Client logos present but lacking project context or measurable outcomes
- Only one specific metric found across all testimonials (7% increase in sales)
- No pricing information—not even a framework or typical project range
- Contact information (email, phone) buried below multiple testimonials on Contact page
- No dedicated case studies section with named clients, deliverables, and outcomes
- "Connect with an Expert" CTA feels sales-first; "Contact" would be more transparent
- No "we don't do" or scope limitations—reduces perceived honesty

---

## Issues (Trust, Transparency, Clarity)

### Critical

#### 1. No Pricing Information or Framework

| Field | Detail |
|-------|--------|
| **Description** | The site provides no pricing information. No ranges, no typical project examples, no framework for how costs are determined. The only path is "Contact us for a quote," which forces engagement before the user knows if the vendor is in their budget. |
| **Location** | Site-wide; Services page, Contact page |
| **Impact** | Skeptical users cannot compare vendors or assess fit without disclosing themselves. This obscures transparency and increases perceived risk. Many users will abandon before contacting. |
| **Recommended Fix** | Provide a pricing framework: "Typical discovery: 2–4 weeks, $X–$Y. Full projects typically range from $Z to $W depending on scope." If pricing is highly custom, explain why and what factors affect cost. Offer a "typical project" example with deliverables and approximate cost. |

---

#### 2. Lack of Case Studies with Measurable Outcomes

| Field | Detail |
|-------|--------|
| **Description** | Client names (Prosci, CDK Global, Millennium Trust) appear, but there is no dedicated case studies section with detailed project descriptions, deliverables, timelines, and measurable outcomes. The only specific metric found is in a testimonial: "7% increase in online membership sales and general admission tickets." |
| **Location** | Work page, homepage, Contact page (testimonials) |
| **Impact** | Skeptical users cannot verify claims or assess whether the vendor delivers real results. Logos without context are weak evidence. Absence of quantified outcomes reduces trust and differentiates poorly from competitors who overpromise. |
| **Recommended Fix** | Create case studies with: client name (with permission), project type, problem/solution, deliverables, timeline, and measurable outcomes (e.g., "reduced load time by 40%," "increased conversions by 23%"). Link case studies from client logos. Ensure at least 3–5 detailed case studies are easily discoverable. |

---

#### 3. Contact Information Buried Below Testimonials

| Field | Detail |
|-------|--------|
| **Description** | The Contact page leads with multiple long testimonials. Email (contact@launchpadlab.com) and phone ((312) 888-9651) appear below the fold, after the user scrolls past several quote blocks. The primary task—reaching the company—is secondary to social proof. |
| **Location** | Contact page (https://launchpadlab.com/contact) |
| **Impact** | Users seeking contact details must scroll past persuasion content. For skeptical users, this signals that the site prioritizes selling over helping. It also creates friction for users who prefer to call or email rather than fill out a form. |
| **Recommended Fix** | Restructure Contact page: (1) Clear "Contact Us" heading, (2) Phone, email, and address prominently at top, (3) Contact form, (4) Testimonials in a separate section below or on a different page. Repeat contact info in header/footer site-wide. |

---

### High

#### 4. Vague Marketing Language Without Evidence

| Field | Detail |
|-------|--------|
| **Description** | Claims such as "Results that Matter," "Your Strategic AI Partner," "AI-Powered Digital Solutions for the Modern Enterprise," "Driving ROI with AI," and "Make AI Your Competitive Advantage" appear without quantification, definition, or evidence. "AI-centric" and "AI-focused" are used repeatedly without explaining what the company actually does with AI (custom models, integrations, chatbots, etc.). |
| **Location** | Homepage, Services page, About page |
| **Impact** | Skeptical users treat unsubstantiated claims as red flags. Vague language reduces credibility and makes the company indistinguishable from vendors who overpromise. |
| **Recommended Fix** | Replace buzzwords with specific language. "We build custom web and mobile applications, integrate AI/LLM tools, and implement Salesforce solutions." Add quantified claims where possible: "We've delivered 730+ projects with an average X% improvement in [metric]." Define "AI-focused" with concrete examples. |

---

#### 5. Testimonials Lack Full Attribution

| Field | Detail |
|-------|--------|
| **Description** | Testimonials on the Contact page may lack full names, company affiliations, roles, or photos. Anonymous or partially attributed testimonials are not verifiable and carry less weight for skeptical users. |
| **Location** | Contact page |
| **Impact** | Unverifiable testimonials do not build trust. Skeptical users assume bias until evidence is provided. Full attribution (name, company, role, photo) increases credibility. |
| **Recommended Fix** | Ensure all testimonials include: full name, company name, role/title, and photo where possible. Consider video testimonials for higher trust. Link to case studies when the testimonial references a specific project. |

---

#### 6. No Explicit Process Description

| Field | Detail |
|-------|--------|
| **Description** | The site describes services (discovery, design, development, managed services) at a high level but does not provide a numbered process with steps, deliverables, and typical timelines. Users cannot evaluate what they will receive or when. |
| **Location** | Services page, About page |
| **Impact** | Without a clear process, users cannot assess whether the vendor's approach matches their needs. It also raises questions about scope creep and project management. Transparent process descriptions build trust. |
| **Recommended Fix** | Add a "Our Process" section with numbered steps: (1) Discovery (2–4 weeks, deliverables: X, Y, Z), (2) Design (timeline, deliverables), (3) Development (sprints, milestones), (4) Launch & Support. Include typical timelines and what the client receives at each stage. |

---

#### 7. "Connect with an Expert" Instead of "Contact"

| Field | Detail |
|-------|--------|
| **Description** | The primary contact CTA in navigation is "Connect with an Expert" rather than "Contact." This is marketing language that implies a sales conversation rather than a straightforward way to reach the company. |
| **Location** | Main navigation, site-wide |
| **Impact** | Skeptical users prefer direct, transparent language. "Connect with an Expert" feels like a soft sell and may deter users who want to ask a simple question or request a quote without committing to a "connection." |
| **Recommended Fix** | Use "Contact" or "Contact Us" as the primary label. If "Connect with an Expert" is retained for marketing, offer "Contact" as an alternative in the same menu or ensure the destination is clearly a contact page. |

---

### Medium

#### 8. No Acknowledgment of Scope or Limitations

| Field | Detail |
|-------|--------|
| **Description** | The site does not state what the company does *not* do. There is no "We focus on X; we don't do Y" section. This is common among vendors who claim to do everything, which skeptical users interpret as unrealistic or evasive. |
| **Location** | Services page, About page |
| **Impact** | Honest limitations build trust. Absence of scope acknowledgment raises questions about what is being hidden or overstated. |
| **Recommended Fix** | Add a brief "What We Focus On" or "Our Scope" section. Example: "We specialize in custom web and mobile applications for mid-market and enterprise. We don't do off-the-shelf product sales or simple WordPress sites." Acknowledge industries or project types that are a better fit. |

---

#### 9. Statistics Without Source or Context

| Field | Detail |
|-------|--------|
| **Description** | "12+ Years in Business," "730+ Projects," "240+ Clients" are displayed but without context: when last updated, how defined (e.g., are "clients" one-time or ongoing?), or link to verification (e.g., Clutch, case studies). |
| **Location** | Homepage, possibly other pages |
| **Impact** | Numbers are better than no numbers, but unverifiable statistics can be questioned. Skeptical users may discount them without source or context. |
| **Recommended Fix** | Add "as of [date]" or "updated [date]." Link to third-party verification (Clutch, G2) if available. Define terms briefly: "240+ clients we've partnered with" vs. "240+ projects delivered." |

---

#### 10. Cookie Consent and Privacy Transparency

| Field | Detail |
|-------|--------|
| **Description** | If a cookie banner or consent mechanism exists, skeptical users will evaluate whether it clearly explains what is collected, offers granular controls, and avoids dark patterns (e.g., pre-selected marketing cookies, unclear "Accept All" vs. "Reject"). |
| **Location** | Site-wide (on first visit) |
| **Impact** | Privacy-conscious users notice consent UI. Unclear or manipulative consent reduces trust. |
| **Recommended Fix** | Ensure cookie consent: (1) Clearly states what cookies are used for, (2) Offers granular controls (essential, analytics, marketing), (3) Does not pre-check marketing/optional cookies, (4) Links to privacy policy. Make "Reject non-essential" as easy as "Accept All." |

---

### Low

#### 11. Form Fields and Data Use

| Field | Detail |
|-------|--------|
| **Description** | Contact form fields should be minimal and necessary. If the form requests unnecessary information (e.g., company size, budget range) without explanation, or if there is no clear privacy notice about how data is used, skeptical users may hesitate. |
| **Location** | Contact page form |
| **Impact** | Overly invasive forms or unclear data use reduce trust. Users may abandon the form or provide false information. |
| **Recommended Fix** | Request only necessary fields for initial contact. Explain why each field is needed. Add a brief privacy notice: "We use this information to respond to your inquiry. We do not share it with third parties." Link to full privacy policy. |

---

## Priority Recommendations

### Phase 1 (Critical — Address First)

1. **Add pricing framework** — Provide a range, typical project example, or clear explanation of why pricing is custom and what factors affect it. Avoid "Contact us" as the only pricing information.
2. **Create case studies with measurable outcomes** — At least 3–5 detailed case studies with client name, project type, deliverables, timeline, and quantified results (e.g., "increased conversions by 23%").
3. **Restructure Contact page** — Place phone, email, and address at the top. Move testimonials below contact details or to a separate section.

### Phase 2 (High — Next)

4. **Replace vague language with specifics** — Define "AI-focused" with concrete examples. Replace "Results that Matter" and similar phrases with quantified claims or remove them.
5. **Add full attribution to testimonials** — Full name, company, role, photo. Link to case studies when relevant.
6. **Publish explicit process description** — Numbered steps, deliverables, typical timelines. Make it clear what the client receives and when.
7. **Rename "Connect with an Expert" to "Contact"** — Or offer both; ensure the primary path is transparent.

### Phase 3 (Medium — Follow-Up)

8. **Acknowledge scope and limitations** — "We focus on X. We don't do Y." Build trust through honesty.
9. **Add context to statistics** — Date, definition, link to verification.
10. **Review cookie consent** — Clear language, granular controls, no dark patterns.

### Phase 4 (Low — Ongoing)

11. **Minimize contact form fields** — Only necessary fields. Clear privacy notice and link to policy.

---

*This report is based on accessibility testing performed from the perspective of the skeptical user persona (Jordan Reyes) and focuses on trust, transparency, and clarity. Implementation should be validated with user testing involving evidence-seeking, skeptical buyers.*
