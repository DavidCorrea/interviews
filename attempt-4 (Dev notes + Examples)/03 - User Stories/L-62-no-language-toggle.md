# L-62: No Language Toggle/Multilingual Support

**Issue ID:** L-62
**Priority:** Low
**WCAG Criteria:** 3.1.1 Language of Page (A)
**Affected Personas:** Non-Native Speaker

---

## User Story

As a **non-native English speaker** evaluating LaunchPad Lab's services, I want the site to offer a language toggle or multilingual support so that I can read about the company's offerings in my preferred language and make confident purchasing decisions without language barriers.

---

## Acceptance Criteria

- [ ] A visible language selector is accessible from a persistent location (e.g., site header or footer).
- [ ] At minimum, the language selector offers English as the default, with at least one additional language (e.g., Spanish, given the Chicago-area market).
- [ ] Selecting a language translates the primary content (navigation, headings, body text, CTAs, and form labels) into the chosen language.
- [ ] The `<html lang="">` attribute updates to reflect the selected language (e.g., `lang="es"` for Spanish).
- [ ] The language preference persists across page navigation and browser sessions.
- [ ] The language selector itself is accessible: keyboard operable, screen reader compatible, and labeled with `aria-label` or equivalent.
- [ ] If full translation is not feasible, at minimum a machine translation option (e.g., Google Translate widget) is provided with a clear disclaimer about translation quality.

---

## How to Test the Change

### Manual Testing
1. Navigate to launchpadlab.com.
2. Locate the language selector in the header or footer.
3. Change the language to Spanish (or the available alternative).
4. Verify:
   - Navigation labels are translated.
   - Hero headline and body text are translated.
   - CTA button text is translated.
   - Contact form labels are translated.
5. Navigate to at least 3 different pages — confirm translations persist.
6. Reload the page — confirm the language preference is retained.
7. Inspect the `<html>` element — confirm `lang="es"` (or appropriate value) is set.
8. Test the language selector with keyboard only (Tab to it, Enter/Space to activate, arrow keys to choose).
9. Test with a screen reader — confirm the language selector announces options correctly.

### Automated Testing
1. Verify `<html lang>` attribute matches the selected language:
   ```javascript
   // After selecting Spanish
   const lang = await page.getAttribute('html', 'lang');
   expect(lang).toBe('es');
   ```
2. Check that key content elements have translated text:
   ```javascript
   // Example: check nav item text changes
   await page.click('[data-lang="es"]');
   const navText = await page.textContent('nav .primary-menu li:first-child a');
   expect(navText).not.toBe('Services'); // Should be translated
   ```

---

## Developer Notes

### General Explanation
The site currently has no language selector or multilingual content. All content is in English only. For a company serving an international market from Chicago (a city with a large Spanish-speaking population), offering at least one additional language improves accessibility for non-native speakers and signals inclusivity.

### Implementation Options

**Option A: WordPress multilingual plugin (recommended for full translation):**

Use a plugin like WPML or Polylang:
```php
// Polylang — register languages in settings
// Then use the language switcher widget or shortcode:
<?php pll_the_languages(array('show_flags' => 1, 'show_names' => 1)); ?>
```

Or in a theme template:
```html
<!-- Language switcher in header -->
<nav aria-label="Language selector">
  <ul class="language-switcher">
    <li><a href="/" lang="en" hreflang="en" aria-current="true">English</a></li>
    <li><a href="/es/" lang="es" hreflang="es">Español</a></li>
  </ul>
</nav>
```

**Option B: Google Translate widget (quick interim solution):**
```html
<!-- Add to header or footer -->
<div id="google_translate_element" aria-label="Translate this page"></div>
<script>
  function googleTranslateElementInit() {
    new google.translate.TranslateElement({
      pageLanguage: 'en',
      includedLanguages: 'es,fr,de,zh-CN,ja,ko',
      layout: google.translate.TranslateElement.InlineLayout.SIMPLE,
      autoDisplay: false
    }, 'google_translate_element');
  }
</script>
<script src="//translate.google.com/translate_a/element.js?cb=googleTranslateElementInit"></script>
```

> **Note:** Machine translation has quality limitations. Add a visible disclaimer:
> ```html
> <p class="translation-disclaimer">
>   Translations are provided by Google Translate and may not be fully accurate.
> </p>
> ```

**Option C: Manual `hreflang` tags for SEO (even if translation is partial):**
```html
<head>
  <link rel="alternate" hreflang="en" href="https://launchpadlab.com/" />
  <link rel="alternate" hreflang="es" href="https://launchpadlab.com/es/" />
  <link rel="alternate" hreflang="x-default" href="https://launchpadlab.com/" />
</head>
```

### Components/Files to Audit
- Site header template (for language selector placement)
- `<html>` tag in `header.php` (for dynamic `lang` attribute)
- WordPress configuration (for multilingual plugin setup)
- All page templates (for translated content hooks)
- Contact form (Ninja Forms) — form labels need translation support

---

## Examples from Other Sites

- **Shopify:** Offers a language selector in the footer with 20+ languages. The selector uses a globe icon with visible text indicating the current language.
- **Stripe:** Provides full localization with dedicated subdomains (e.g., `stripe.com/es` for Spanish). Each localized page sets the correct `<html lang="">`.
- **HubSpot:** Offers content in 6+ languages via a header dropdown with flag icons and language names in their native script (e.g., "Deutsch," "Français").
- **W3C:** Provides every specification and guideline in multiple languages, with a language selector prominently placed in the header.

---

## Additional Context

Full multilingual support is a significant content and development effort. A phased approach is recommended:

1. **Phase 1 (quick win):** Add a Google Translate widget with a disclaimer. This provides immediate value for non-native speakers at minimal cost.
2. **Phase 2 (medium effort):** Translate the highest-traffic pages (homepage, services overview, contact) into Spanish using a professional translator.
3. **Phase 3 (full effort):** Implement a complete multilingual setup with WPML or Polylang, covering all pages and navigation.

Even Phase 1 alone addresses the core accessibility concern for non-native speakers.
