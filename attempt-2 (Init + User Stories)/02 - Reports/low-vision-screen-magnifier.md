# Technical Report: Low Vision Screen Magnifier Accessibility

**Website:** https://launchpadlab.com/  
**Persona:** Thomas Rodriguez (Low Vision Screen Magnifier User)  
**Test Date:** February 16, 2025  
**Test Task:** Find what the company does and how to contact them  
**Zoom Levels Tested:** 200%, 300%, 400%

---

## Executive Summary

LaunchPad Lab's website presents **critical accessibility barriers** for users who rely on screen magnification (200–400% zoom). The primary failure is **layout reflow**: content does not reflow to a single column at high zoom, forcing users to pan horizontally in addition to scrolling vertically. This violates WCAG 1.4.10 Reflow (Level AA) and creates an exhausting, disorienting experience for users like Thomas Rodriguez.

**Key findings:**
- **Critical:** Horizontal scrollbars appear at 200%, 300%, and 400% zoom. Content extends beyond viewport width.
- **Critical:** Multi-column layouts (services, logos, case studies, statistics) do not collapse to single column—users must pan 15+ times on homepage alone.
- **High:** Sticky header consumes 30–40% of visible viewport at 300% zoom.
- **High:** No skip links ("Skip to main content," "Skip to contact")—users must scroll through all content.
- **High:** Contact information (phone, email) not prominently visible; obscured by testimonials.
- **Medium:** Headings separated from content by viewport boundaries, causing context loss.
- **Medium:** Large images dominate viewport and obscure surrounding content.

---

## Accessibility Issues

### Critical

#### 1. Horizontal Scrolling Required at High Zoom (Layout Reflow Failure)

| Field | Detail |
|-------|--------|
| **Description** | At 200%, 300%, and 400% browser zoom, horizontal scrollbars appear. Content does not reflow to fit viewport width. Users must pan left and right to read content. |
| **Location** | Homepage, About, Services, Contact, Work pages |
| **Impact** | Screen magnifier users see only ~25–33% of typical viewport. Horizontal panning is exhausting and indicates layout failure. Users cannot complete tasks using only vertical scrolling. |
| **Recommended Fix** | Ensure all content reflows at 320px viewport width (equivalent to 400% zoom on 1280px). Use flexible layouts, `max-width: 100%`, `flex-wrap`, `grid-template-columns: 1fr` at narrow widths. Remove fixed-width containers. Test at 320px viewport in DevTools. |
| **WCAG** | **1.4.10 Reflow (Level AA)** — Content can be presented without loss of information or functionality, and without requiring scrolling in two dimensions. |

---

#### 2. Multi-Column Grids Do Not Reflow to Single Column

| Field | Detail |
|-------|--------|
| **Description** | Services section (6 boxes), logos section (12+ logos), "Problems We Solve," case studies, and statistics ("12+ Years," "730+ Projects," "240+ Clients") remain in 2–3 column layouts at high zoom. They do not stack vertically. |
| **Location** | Homepage (services, logos, case studies, statistics), Services page, Work page |
| **Impact** | Users must pan right 8+ times to see all logos, 6+ times for services. Navigation pattern: pan right, right, right, scroll down, pan left, left, right. Extremely fatiguing. |
| **Recommended Fix** | Use CSS media queries or container queries to collapse grids to single column at `max-width: 480px` (200% zoom) and below. Use `flex-wrap: wrap` and `grid-template-columns: 1fr` for narrow viewports. |
| **WCAG** | **1.4.10 Reflow (Level AA)** |

---

#### 3. Content Cut Off at Viewport Edges

| Field | Detail |
|-------|--------|
| **Description** | Text, buttons, and images are cut off at viewport edges when zoomed. Headlines may be split across viewport. "Learn More" buttons may be invisible until user scrolls. Words split at viewport edge. |
| **Location** | Hero section, service boxes, CTA buttons, footer |
| **Impact** | Users may miss critical content. Buttons and links may be undiscoverable. Reading is fragmented and confusing. |
| **Recommended Fix** | Ensure no fixed-width elements prevent reflow. Use `overflow: visible`. Avoid `overflow: hidden` on containers with critical content. Ensure buttons and text wrap within viewport. |
| **WCAG** | **1.4.10 Reflow (Level AA)** — No loss of content or functionality. |

---

### High

#### 4. Sticky Header Consumes Excessive Viewport Space

| Field | Detail |
|-------|--------|
| **Description** | Fixed/sticky header remains at top of viewport. At 300% zoom, the header occupies approximately 30–40% of visible area. |
| **Location** | All pages (global header) |
| **Impact** | Users see very little content below the header. Valuable viewport space is consumed by navigation that could be collapsed or minimized at high zoom. |
| **Recommended Fix** | Consider collapsible header at narrow viewport widths. Reduce header height when viewport is below 480px. Or provide option to minimize header. Ensure header does not use fixed pixel heights that scale poorly. |
| **WCAG** | **1.4.10 Reflow (Level AA)** — Content should be usable. **2.4.1 Bypass Blocks (Level A)** — Skip link helps bypass repeated content. |

---

#### 5. No Skip Links

| Field | Detail |
|-------|--------|
| **Description** | No "Skip to main content" or "Skip to contact" links. Users must scroll through entire page (header, hero, testimonials, etc.) to reach target content. |
| **Location** | All pages |
| **Impact** | Magnifier users expend significant effort scrolling past repeated and non-essential content. Contact page requires scrolling past multiple testimonials before reaching form or contact details. |
| **Recommended Fix** | Add visible or focusable "Skip to main content" link at top of each page. On Contact page, add "Skip to contact form" or "Skip to contact details." Ensure skip links are keyboard-accessible and visible on focus. |
| **WCAG** | **2.4.1 Bypass Blocks (Level A)** — A mechanism is available to bypass blocks of content that are repeated on multiple pages. |

---

#### 6. Contact Information Not Prominently Displayed

| Field | Detail |
|-------|--------|
| **Description** | Phone number, email, and address are not immediately visible on Contact page. Testimonials occupy prominent space. Contact form and/or direct contact details may be below the fold or require extensive scrolling. |
| **Location** | Contact page (https://launchpadlab.com/contact) |
| **Impact** | Users who prefer to call or email (rather than use a form) may not find direct contact details. Magnifier users must scroll and pan extensively to locate them. |
| **Recommended Fix** | Display phone number, email, and address at top of Contact page, in large, readable text. Repeat contact info in footer on every page. Ensure visibility without scrolling on initial load at 300% zoom. |
| **WCAG** | **2.4.6 Headings and Labels (Level AA)** — Headings should describe topic. **2.1 Operable** — Multiple ways to complete tasks. |

---

### Medium

#### 7. Headings Separated from Content by Viewport Boundaries

| Field | Detail |
|-------|--------|
| **Description** | When magnified, section headings may appear at bottom of viewport while content appears at top of next "screen." Users lose the connection between heading and content. |
| **Location** | All pages with sectioned content |
| **Impact** | Context loss. Users cannot easily associate headings with their content. Confusion about which section they are in. |
| **Recommended Fix** | Use `scroll-margin-top` or ensure sufficient spacing so headings and content stay visually grouped when possible. Consider `break-inside: avoid` for heading+content blocks. Provide clear section structure with aria landmarks. |
| **WCAG** | **2.4.6 Headings and Labels (Level AA)** — Headings describe topic. **1.3.1 Info and Relationships (Level A)** — Structure preserved. |

---

#### 8. Large Images Dominate Viewport

| Field | Detail |
|-------|--------|
| **Description** | Case study screenshots, decorative graphics, and hero images fill the entire viewport when zoomed. Users cannot see surrounding content or context. |
| **Location** | Homepage hero, case studies, About page, Work page |
| **Impact** | Users lose context. Large images obscure content above and below. Decorative images waste viewport space. |
| **Recommended Fix** | Ensure images scale appropriately and do not force horizontal overflow. Use `max-width: 100%` and `height: auto`. Consider reducing decorative image size at narrow viewports. Use `object-fit` for responsive images. |
| **WCAG** | **1.4.10 Reflow (Level AA)** — Content reflows. **1.1.1 Non-text Content (Level A)** — Decorative images should not obstruct content. |

---

#### 9. Testimonials on Contact Page Obscure Primary Task

| Field | Detail |
|-------|--------|
| **Description** | Contact page leads with multiple long testimonials. Users must scroll past them to reach contact form or contact details. |
| **Location** | Contact page |
| **Impact** | Magnifier users expend significant scrolling to complete primary task (find contact info). Increases fatigue and task completion time. |
| **Recommended Fix** | Move testimonials below contact form and contact details. Or move to separate Testimonials page. Prioritize: (1) Contact heading, (2) Phone, email, address, (3) Contact form, (4) Testimonials. |
| **WCAG** | **2.4.6 Headings and Labels (Level AA)** — Content should be findable. |

---

### Low

#### 10. Hamburger Menu or Navigation Visibility

| Field | Detail |
|-------|--------|
| **Description** | At high zoom, full navigation may not be visible. Hamburger menu or collapsed menu may require additional interaction. Users may not see all nav options until they pan or interact. |
| **Location** | Header/navigation |
| **Impact** | Users may miss navigation options. Requires extra panning or clicks to discover "Contact" or other links. |
| **Recommended Fix** | Ensure navigation is fully visible or clearly accessible at 320px viewport. Test hamburger menu with keyboard and screen magnifier. Ensure menu is announced and usable. |
| **WCAG** | **2.1.1 Keyboard (Level A)** — All functionality via keyboard. **4.1.2 Name, Role, Value (Level A)** |

---

## WCAG References

| Success Criterion | Level | Relevance |
|------------------|-------|-----------|
| **1.4.10 Reflow** | AA | Content must reflow at 320px width without horizontal scrolling. Primary failure. |
| **1.4.4 Resize Text** | AA | Text must be resizable to 200% without loss of content or functionality. |
| **2.4.1 Bypass Blocks** | A | Skip links required to bypass repeated content. |
| **2.4.6 Headings and Labels** | AA | Headings describe topic; content is findable. |
| **1.4.3 Contrast (Minimum)** | AA | Text contrast important when magnified. |
| **1.3.1 Info and Relationships** | A | Structure and relationships preserved. |

---

## Priority Recommendations

### Phase 1 (Critical — Address First)

1. **Fix layout reflow** — All content must fit within viewport at 320px width. No horizontal scrollbars at 200%, 300%, or 400% zoom. Use flexible layouts, `max-width`, `flex-wrap`, single-column grids.
2. **Collapse multi-column layouts** — Services, logos, case studies, and statistics must stack in single column at narrow viewports. Test at 320px and 480px.
3. **Eliminate content cutoff** — Ensure no text, buttons, or images are cut off at viewport edges. Remove fixed-width containers that prevent reflow.

### Phase 2 (High — Next)

4. **Add skip links** — "Skip to main content" on all pages. "Skip to contact form" or "Skip to contact details" on Contact page.
5. **Display contact information prominently** — Phone, email, address at top of Contact page and in footer site-wide. Visible without scrolling at 300% zoom.
6. **Reduce sticky header impact** — Collapsible or smaller header at narrow viewports. Ensure header does not consume >25% of viewport at 300% zoom.

### Phase 3 (Medium — Follow-Up)

7. **Improve heading-content grouping** — Prevent headings from separating from content at viewport boundaries. Use appropriate spacing and `break-inside: avoid`.
8. **Optimize images for reflow** — Ensure images scale and do not dominate viewport. Use `max-width: 100%`. Consider reducing decorative image size at narrow widths.
9. **Reorganize Contact page** — Move testimonials below contact form and contact details. Prioritize primary task.

### Phase 4 (Low — Ongoing)

10. **Verify navigation at all zoom levels** — Ensure hamburger menu and all nav links are accessible and visible at 320px viewport.

---

## Validation Approach

- **Browser zoom test:** Chrome/Firefox/Safari at 200%, 300%, 400% — verify no horizontal scrollbar.
- **Viewport test:** Chrome DevTools, set viewport to 320px width — verify all content reflows, no horizontal scroll.
- **Real tools:** Test with ZoomText, Windows Magnifier, or macOS Zoom at 300%+ and navigate the site.
- **WCAG 1.4.10:** Content must reflow without loss of information or functionality, and without requiring scrolling in two dimensions.

---

*This report is based on accessibility testing performed from the perspective of the low vision screen magnifier persona (Thomas Rodriguez) and aligns with WCAG 2.1 guidelines. Implementation should be validated with user testing involving people who use screen magnification.*
