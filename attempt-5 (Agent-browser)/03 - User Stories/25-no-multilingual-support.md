# No Multilingual Support

**Priority:** Low
**Location:** Sitewide
**WCAG:** [3.1.1 Language of Page (A)](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page), [3.1.2 Language of Parts (AA)](https://www.w3.org/WAI/WCAG21/Understanding/language-of-parts)

---

## User Story

> As a **non-native English speaker or international prospective client**,
> I want **the option to view the site in my preferred language or to easily use automated translation**
> so that **I can understand LaunchPad Lab's services and evaluate whether to engage them, without a language barrier.**

---

## Problem

The LaunchPad Lab website is available only in English, with no language selection, multilingual content, or acknowledgment of international visitors. This is particularly notable because:

- The site references **global client metrics** and international work, suggesting an international audience.
- Prospective clients from non-English-speaking markets may struggle to evaluate services, case studies, and expertise.
- Automated browser translation tools (like Chrome Translate) work poorly on sites that don't follow plain-language principles or use heavy JavaScript rendering.
- The `<html>` element may lack a `lang` attribute, preventing assistive technology and translation tools from correctly identifying the page language.

While full professional translation may be out of scope, even a lightweight integration (Google Translate widget + plain language writing) significantly improves accessibility for international users.

---

## Acceptance Criteria

- [ ] The `<html>` element has a `lang="en"` attribute on all pages.
- [ ] A language selector or "Translate this page" widget is available in the header or footer.
- [ ] If using Google Translate or similar, the widget is keyboard accessible and labeled.
- [ ] Body copy follows plain-language guidelines to improve automated translation quality (short sentences, common words, active voice).
- [ ] Any content in a language other than the page's primary language is wrapped in a `lang` attribute (e.g., `<span lang="es">Hola</span>`).
- [ ] The site includes a brief note (e.g., in About or Contact) acknowledging the ability to work with international clients.
- [ ] The language selector does not break the page layout or obscure content.

---

## How to Test

1. **`lang` attribute check:** Inspect the `<html>` element in DevTools. Confirm `lang="en"` is present.
2. **Automated translation test:** Use Google Chrome's built-in "Translate this page" feature. Navigate through key pages (Home, About, Services, Contact). Verify the translation is reasonably accurate — if it isn't, the source text likely needs simplification.
3. **Widget test (if added):** Click the language selector. Choose a language (e.g., Spanish). Confirm the page translates and the widget remains accessible.
4. **Keyboard test:** Tab to the language selector. Confirm it can be opened and operated with keyboard alone.
5. **Screen reader test:** Navigate to the language selector with VoiceOver/NVDA. Confirm it announces its purpose (e.g., "Translate this page" or "Select language").
6. **Plain language audit:** Paste key page copy into [Hemingway Editor](https://hemingwayapp.com/). Sentences at grade 8 or below translate better with automated tools.

---

## Developer Notes

### Strategy

Implement a three-part approach:
1. **Set the `lang` attribute** on `<html>` — a one-line fix that helps all assistive tech and translation tools.
2. **Add a Google Translate widget** — low-effort, high-impact for international visitors.
3. **Write in plain language** — improves both accessibility and automated translation quality.

### 1. Set the `lang` attribute

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <!-- ... -->
  </head>
</html>
```

### 2. Google Translate widget integration

```html
<!-- In the header or footer -->
<div id="google-translate" class="translate-widget">
  <div id="google_translate_element"></div>
</div>

<script>
  function googleTranslateElementInit() {
    new google.translate.TranslateElement(
      {
        pageLanguage: 'en',
        includedLanguages: 'es,fr,de,ja,zh-CN,pt,ko,ar',
        layout: google.translate.TranslateElement.InlineLayout.HORIZONTAL,
        autoDisplay: false,
      },
      'google_translate_element'
    );
  }
</script>
<script src="https://translate.google.com/translate_a/element.js?cb=googleTranslateElementInit"></script>
```

### CSS for the translate widget

```css
.translate-widget {
  display: flex;
  align-items: center;
}

/* Override Google Translate default styles for better integration */
.goog-te-gadget {
  font-family: inherit !important;
  font-size: 0.875rem !important;
}

.goog-te-gadget-simple {
  border: 2px solid #767676 !important;
  border-radius: 6px !important;
  padding: 0.25rem 0.5rem !important;
  background: #fff !important;
}

.goog-te-gadget-simple:focus-within {
  border-color: #1a73e8 !important;
  box-shadow: 0 0 0 3px rgba(26, 115, 232, 0.3) !important;
}

/* Hide the Google Translate banner that appears at the top */
.goog-te-banner-frame {
  display: none !important;
}

body {
  top: 0 !important;
}
```

### 3. Custom language selector (alternative to Google Translate)

```html
<div class="language-selector" role="navigation" aria-label="Language selection">
  <button
    type="button"
    class="language-toggle"
    aria-expanded="false"
    aria-controls="language-menu"
    aria-label="Select language — current: English"
  >
    <svg aria-hidden="true" width="20" height="20" viewBox="0 0 24 24">
      <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10
               10-4.48 10-10S17.52 2 12 2zm-1 17.93c-3.95-.49-7-3.85-7-7.93
               0-.62.08-1.21.21-1.79L9 15v1c0 1.1.9 2 2
               2v1.93zm6.9-2.54c-.26-.81-1-1.39-1.9-1.39h-1v-3c0-.55-.45-1-1-1H8v-2h2c.55
               0 1-.45 1-1V7h2c1.1 0 2-.9 2-2v-.41c2.93 1.19 5 4.06
               5 7.41 0 2.08-.8 3.97-2.1 5.39z" />
    </svg>
    <span>English</span>
  </button>

  <ul id="language-menu" class="language-menu" role="menu" hidden>
    <li role="none">
      <a role="menuitem" href="/" lang="en" hreflang="en" aria-current="true">English</a>
    </li>
    <li role="none">
      <a role="menuitem" href="/es/" lang="es" hreflang="es">Español</a>
    </li>
    <li role="none">
      <a role="menuitem" href="/ja/" lang="ja" hreflang="ja">日本語</a>
    </li>
  </ul>
</div>
```

### Marking language changes in content

```html
<p>
  We've worked with clients across the globe, including teams in
  <span lang="ja">東京</span> (Tokyo) and
  <span lang="de">München</span> (Munich).
</p>
```

### Components to audit

| Component / Section | Page(s) | What to fix |
|---|---|---|
| `<html>` element | All pages | Add `lang="en"` attribute |
| Header or footer | All pages | Add translate widget or language selector |
| Body copy throughout | All pages | Simplify language for better automated translation |
| About page — international references | About | Acknowledge multilingual capability |
| Contact page | Contact | Note ability to accommodate international clients |

---

## Examples from Other Sites

### Shopify (shopify.com)
- Full language selector in the footer with 20+ languages.
- Professional translations for key markets.
- Language/region selector also adjusts currency and support links.

### W3C (w3.org)
- Content available in multiple languages.
- Each page has a proper `lang` attribute.
- Content in other languages is marked with appropriate `lang` attributes on inline elements.

### Airbnb (airbnb.com)
- Language and region selector in the footer.
- Automatically detects user's browser language and offers to switch.
- Clean, accessible dropdown for language selection.
- Demonstrates that even complex UIs can support many languages effectively.
