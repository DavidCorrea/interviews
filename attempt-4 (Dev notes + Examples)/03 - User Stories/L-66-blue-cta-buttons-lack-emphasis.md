# L-66: Blue CTA Buttons Lack Non-Color Emphasis

**Issue ID:** L-66
**Priority:** Low
**WCAG Criteria:** 1.4.1 Use of Color (A)
**Affected Personas:** Blue-Yellow Color Blind

---

## User Story

As a **user with tritanopia (blue-yellow color blindness)**, I want CTA buttons to have visual emphasis beyond just their blue background color so that I can identify them as prominent calls-to-action, even when the blue appears as a muted gray in my perception.

---

## Acceptance Criteria

- [ ] Primary CTA buttons have at least one additional non-color visual indicator that distinguishes them from secondary buttons and surrounding content. Acceptable indicators include:
  - Increased font weight (bold/semi-bold)
  - A visible border (2px+ solid border)
  - Larger size relative to secondary buttons
  - An icon or arrow glyph
  - Drop shadow or elevation effect
  - Distinct shape (e.g., rounded pill vs. sharp rectangle)
- [ ] The CTA buttons remain visually prominent when viewed through a color blindness simulator (tritanopia/deuteranopia mode).
- [ ] The visual emphasis is consistent across all CTA instances site-wide.
- [ ] The non-color indicator does not rely on motion or animation.
- [ ] Secondary/ghost buttons are visually distinct from primary CTAs through means other than color alone.

---

## How to Test the Change

### Manual Testing
1. Navigate to launchpadlab.com.
2. Install a color blindness simulator browser extension (e.g., [Colorblindly](https://chrome.google.com/webstore/detail/colorblindly), [NoCoffee](https://chrome.google.com/webstore/detail/nocoffee), or use Chrome DevTools > Rendering > Emulate vision deficiencies > Tritanopia).
3. Enable **Tritanopia** simulation.
4. Scroll through the homepage and identify all CTA buttons:
   - Confirm each CTA is still visually prominent and identifiable as a button/call-to-action.
   - Confirm CTAs are distinguishable from secondary links and non-interactive elements.
5. Compare primary CTAs with ghost/outline buttons — confirm they are visually distinct even without color perception.
6. Repeat on the Contact page and a Services page.
7. Test in **Deuteranopia** (red-green) mode as well to ensure broad coverage.

### Automated Testing
1. Check button styling for non-color indicators:
   ```javascript
   const ctaButtons = await page.$$('.cta-btn, .btn-primary, a.button');
   for (const btn of ctaButtons) {
     const styles = await btn.evaluate(el => {
       const cs = getComputedStyle(el);
       return {
         fontWeight: parseInt(cs.fontWeight),
         borderWidth: parseFloat(cs.borderWidth),
         boxShadow: cs.boxShadow,
         fontSize: parseFloat(cs.fontSize),
       };
     });
     // Should have at least one non-color emphasis
     const hasEmphasis =
       styles.fontWeight >= 600 ||
       styles.borderWidth >= 2 ||
       styles.boxShadow !== 'none' ||
       styles.fontSize >= 18;
     expect(hasEmphasis).toBe(true);
   }
   ```
2. Use `axe-core` with the `color-contrast` rule to verify buttons remain perceivable.

---

## Developer Notes

### General Explanation
The primary CTA buttons use a blue background (`#2949E5` or similar) as their main visual differentiator. For users with tritanopia (blue-yellow color blindness), this blue appears as a desaturated gray, losing its visual prominence. Adding non-color emphasis ensures the buttons remain identifiable as the primary action regardless of color perception.

### Code Examples

**Current state (color-only emphasis):**
```css
.cta-btn {
  background-color: #2949E5;
  color: #FFFFFF;
  padding: 12px 24px;
  border: none;
  border-radius: 4px;
  font-weight: 400;
}
```

**Fixed (multiple non-color indicators):**
```css
.cta-btn {
  background-color: #2949E5;
  color: #FFFFFF;
  padding: 14px 28px;
  border: 2px solid #1a3ab3; /* visible border adds structure */
  border-radius: 6px;
  font-weight: 600;           /* bold text for emphasis */
  font-size: 1.125rem;        /* slightly larger than body text */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.15); /* subtle elevation */
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

/* Arrow icon for additional emphasis */
.cta-btn::after {
  content: ' →';
  margin-left: 0.5em;
}
```

**Ensure secondary buttons are visually distinct:**
```css
.btn-secondary,
.btn-outline {
  background-color: transparent;
  color: #2949E5;
  border: 1px solid currentColor;
  font-weight: 400;          /* lighter than primary */
  font-size: 1rem;           /* same as body */
  box-shadow: none;           /* no elevation */
  text-transform: none;
}
```

### Visual Hierarchy Checklist
The primary CTA should differ from secondary buttons in **at least 3** non-color ways:

| Property | Primary CTA | Secondary Button |
|---|---|---|
| Font weight | 600 (semi-bold) | 400 (normal) |
| Border | 2px solid | 1px solid |
| Size/padding | Larger | Smaller |
| Shadow | Subtle elevation | None |
| Icon | Arrow/chevron | None |

### Components/Files to Audit
- Global button styles in the main stylesheet
- Button component/utility classes (`.btn`, `.cta-btn`, `.btn-primary`)
- Hero section CTA buttons
- In-section CTA buttons (Services, case studies)
- Footer CTA button
- Contact page CTA button
- Any theme builder (Divi, Elementor) button module styles

---

## Examples from Other Sites

- **Stripe:** Primary CTAs use a gradient background, bold text, slight elevation shadow, and an arrow icon — providing 4+ non-color indicators of prominence.
- **Slack:** CTA buttons are larger, bolder, and include a subtle shadow compared to secondary links. The visual hierarchy is maintained even in grayscale.
- **GOV.UK:** The green "Start" buttons use bold text, a right-facing arrow icon, and increased size — ensuring they remain the most prominent element even without color perception.
- **Material Design (Google):** The design system explicitly requires "contained buttons" (primary CTAs) to have elevation, increased font weight, and larger touch targets compared to "outlined" or "text" buttons.

---

## Additional Context

This issue is closely related to L-67 (Multiple Competing CTAs). Fixing both together creates an opportunity to establish a clear visual hierarchy: one primary CTA per section that is unmistakably the main action, with secondary links clearly subordinated through reduced visual weight. The non-color emphasis on primary CTAs helps all users (not just color-blind users) quickly identify the intended action.
