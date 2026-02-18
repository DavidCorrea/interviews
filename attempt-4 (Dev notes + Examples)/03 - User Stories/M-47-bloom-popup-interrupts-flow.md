# M-47: Bloom Popup Interrupts User Flow

**Issue ID:** M-47
**Priority:** Medium
**WCAG Criteria:** 2.2.4 Interruptions (AAA)
**Affected Personas:** ADHD

---

## User Story

As a **user with ADHD**, I want **to read site content without being interrupted by unsolicited popup overlays** so that **I can maintain my focus and flow without being jarred by an unexpected modal that demands my attention at an arbitrary moment.**

---

## Acceptance Criteria

- [ ] The timed Bloom email opt-in popup no longer appears automatically during content consumption.
- [ ] If the popup is retained, it must be triggered only by a deliberate user action (e.g., clicking a "Subscribe" CTA) — not by a timer or scroll position.
- [ ] Alternatively, the popup is replaced with a non-intrusive inline email signup form (e.g., at the bottom of blog posts or in the footer).
- [ ] If the popup must appear timed, it includes a "Don't show again" option that persists across sessions (via cookie/localStorage).
- [ ] The popup does not appear on the Contact page or during active form completion.
- [ ] The popup's close button is keyboard-accessible, has a visible label, and returns focus to the previously focused element when dismissed.

---

## How to Test the Change

### Manual Testing

1. Open the homepage (and 2–3 other pages) in an incognito window.
2. Scroll and read for 2–3 minutes on each page.
3. Confirm no popup overlay appears during content consumption.
4. If the popup was converted to inline, verify the email signup form is present at the expected location (e.g., below blog content).
5. If a timed popup is retained with "Don't show again," verify:
   - The popup appears once.
   - Clicking "Don't show again" prevents it from reappearing.
   - Refreshing the page and returning later does not re-trigger the popup.
6. Test keyboard accessibility: Tab to the close button, press Enter — confirm the popup closes and focus returns.

### Automated Testing

1. Search for Bloom popup initialization code:
   ```bash
   grep -rn "bloom\|et_bloom\|popup.*trigger\|popup.*timer" path/to/theme/
   ```
2. Playwright test to verify no popup appears during a 3-minute browsing session:
   ```javascript
   await page.goto('/');
   await page.waitForTimeout(180000); // 3 minutes
   const popup = await page.$('.et_bloom_popup, .bloom-overlay, [class*="popup"]');
   expect(popup).toBeNull();
   ```
3. Lighthouse audit — check for modal-related accessibility issues.

---

## Developer Notes

### General Explanation

The Bloom plugin (by Elegant Themes) triggers a timed email opt-in popup as a modal overlay that interrupts the user's reading flow. For users with ADHD, unexpected interruptions break concentration and create frustration, especially when the popup demands attention (modal overlay that obscures content). WCAG 2.2.4 requires that interruptions can be postponed or suppressed. The best solution is to eliminate the timed popup entirely and replace it with an inline or end-of-content email signup form.

### Code Examples

**Option A — Disable Bloom popup entirely (WordPress):**

In the WordPress admin:
1. Navigate to Bloom > Optin Forms.
2. Select the popup form and either delete it or change the display type from "Pop Up" to "Below Post" or "Inline."

Or deactivate via code:
```php
// In functions.php — prevent Bloom popup from loading
function disable_bloom_popup() {
  if (class_exists('ET_Bloom')) {
    remove_action('wp_footer', array(ET_Bloom::instance(), 'display_popup'));
  }
}
add_action('wp_loaded', 'disable_bloom_popup');
```

**Option B — Replace with inline email signup:**
```html
<!-- Place at the bottom of blog posts or in a sidebar -->
<section class="email-signup" aria-label="Newsletter signup">
  <h2>Stay Updated</h2>
  <p>Get insights on digital product development delivered to your inbox.</p>
  <form action="/subscribe" method="POST">
    <label for="signup-email">Email address</label>
    <input type="email" id="signup-email" name="email"
           placeholder="you@company.com" required>
    <button type="submit">Subscribe</button>
  </form>
</section>
```

**Option C — If popup must stay, add "Don't show again" + focus management:**
```javascript
const popup = document.querySelector('.bloom-popup');
const closeBtn = popup?.querySelector('.close-btn');

// Check suppression cookie
if (localStorage.getItem('bloom_suppressed') === 'true') {
  popup?.remove();
}

closeBtn?.addEventListener('click', () => {
  popup.setAttribute('aria-hidden', 'true');
  popup.style.display = 'none';
  localStorage.setItem('bloom_suppressed', 'true');
  // Return focus to the element that was focused before popup appeared
  previouslyFocusedElement?.focus();
});

// Ensure popup traps focus correctly when open
popup?.addEventListener('keydown', (e) => {
  if (e.key === 'Escape') {
    closeBtn.click();
  }
});
```

### Components / Files to Audit

- Bloom plugin settings in WordPress admin (Bloom > Optin Forms)
- Bloom plugin popup configuration (trigger timing, display conditions)
- `footer.php` — where Bloom injects popup markup
- Any custom JavaScript that initializes or controls the popup
- Consider whether the Bloom plugin can be replaced with a lightweight inline form

---

## Examples from Other Sites

- **Basecamp.com:** No popups whatsoever. Email signup is a prominent but inline form on the homepage.
- **Smashing Magazine:** Uses an inline newsletter signup at the bottom of every article — no popup interruption.
- **GOV.UK:** Strictly prohibits popup overlays per their design system, citing both accessibility and user experience concerns.
- **A List Apart:** Includes a subtle, non-modal newsletter banner at the bottom of the page that does not interrupt content consumption.
- **Medium.com:** Moved away from timed popups in favor of inline signup prompts between articles, which are skippable and non-modal.
