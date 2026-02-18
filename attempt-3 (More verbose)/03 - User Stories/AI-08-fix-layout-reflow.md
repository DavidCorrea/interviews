# AI-08: Fix Layout Reflow at High Zoom (200-400%)

## Metadata
- **ID:** AI-08
- **Priority:** 1 Critical
- **Personas Affected:** 2 of 16 personas (Low Vision Screen Magnifier critical)
- **WCAG Criteria:** 1.4.10 Reflow (AA)
- **Effort:** Large (8–16 hours)

---

## User Story

**As a** user with low vision who uses screen magnification at 200–400% or a narrow viewport,

**I want** all content to reflow into a single column without horizontal scrolling,

**So that** I can read and interact with the entire page without losing content, panning horizontally, or needing to scroll in two dimensions.

---

## Acceptance Criteria

- [ ] All content reflows at 320px viewport width (equivalent to 400% zoom on 1280px screen)
- [ ] No horizontal scrollbars appear at any zoom level (200%, 300%, 400%)
- [ ] Service boxes (6 items) stack vertically in a single column
- [ ] Statistics section stacks vertically
- [ ] Logo carousel wraps or displays in single column within container
- [ ] Testimonials section reflows without horizontal overflow
- [ ] No fixed widths force content beyond viewport
- [ ] All interactive elements remain accessible and usable at narrow widths
- [ ] Images scale with `max-width: 100%` and do not cause overflow

---

## Test Plan

### Method 1: Responsive Viewport (Chrome DevTools)
1. Open `https://launchpadlab.com/` in Chrome
2. Open DevTools (F12 or right-click → Inspect)
3. Toggle device toolbar (Ctrl+Shift+M or Cmd+Shift+M) for responsive mode
4. Set viewport width to **320px**
5. **Expected:** No horizontal scrollbar at bottom of viewport
6. Scroll through entire page and verify:
   - [ ] Hero section: content fits, no overflow
   - [ ] Services grid (6 boxes): stacks vertically, single column
   - [ ] Statistics: numbers and labels stack vertically
   - [ ] Logo carousel: single column or horizontal scroll within container (no page-level overflow)
   - [ ] Testimonials: stack vertically
   - [ ] Case study cards: stack vertically
   - [ ] Footer: content wraps, no horizontal scroll

### Method 2: Browser Zoom
1. Set browser window to 1280px width (or use full screen on 1280px monitor)
2. Zoom to **200%** (Ctrl/Cmd + +)
3. **Expected:** No horizontal scrollbar; content reflows
4. Repeat at **300%** and **400%** zoom
5. **Expected:** Same behavior; all content readable without horizontal panning

### Method 3: Section-by-Section Audit
- Test each section independently by temporarily isolating it
- Use DevTools to identify any element with `overflow-x: scroll` or `overflow: auto` that causes page-level scroll
- Check computed widths: no element should have width exceeding 320px at narrow viewport

---

## Developer Notes

### Audit All CSS for Fixed Widths
- Search for `width: XXXpx` (e.g., 400px, 600px, 1200px) — replace with `max-width: 100%` or fluid units
- Search for `min-width` that exceeds 320px — adjust or remove
- Check `flex` and `grid` for `minmax()` values that force wide columns

### Services Grid
```css
.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1rem;
}

@media (max-width: 320px) {
  .services-grid {
    grid-template-columns: 1fr;
  }
}
```

### Statistics Section
- Stack vertically at narrow widths
- Use `flex-direction: column` or `grid-template-columns: 1fr` at 320px

### Logo Carousel
- Option A: Single column layout at 320px
- Option B: Horizontal scroll within a container with `overflow-x: auto` — ensure container has `max-width: 100%` so scroll is internal, not page-level
- Ensure carousel wrapper does not force page overflow

### General Patterns
- Use `flex-wrap: wrap` on flex containers
- Use `grid-template-columns: 1fr` or `repeat(1, 1fr)` at 320px
- Replace `width` with `max-width: 100%` on images and containers
- Consider CSS Container Queries (`@container`) if supported for component-level reflow

### Files to Modify
- Global layout CSS
- Services section styles
- Statistics/counter section
- Logo carousel component
- Testimonials section
- Case study cards
- Footer layout

---

## Examples

| Site | Approach |
|------|----------|
| **GOV.UK** | Fully responsive to 320px; single column at narrow widths; no horizontal scroll |
| **BBC.com** | Content reflows to single column at high zoom; clean breakpoints |
| **WebAIM.org** | Clean reflow; all sections stack vertically; accessibility-focused layout |
