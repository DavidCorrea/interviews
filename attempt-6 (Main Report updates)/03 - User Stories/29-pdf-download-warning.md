# PDF Download Warning

## Priority
**Low**

## User Story
As a user clicking "Download Overview" on the AI Automation page, I want to know the file type and size before the download starts, so that I am not surprised by an unexpected PDF download and can make an informed decision.

## Acceptance Criteria

- [ ] "Download Overview" link indicates file type (PDF) in visible text
- [ ] File size is displayed when known (e.g., "2.4 MB")
- [ ] Link uses `aria-label` that includes file type and size for screen reader users
- [ ] Format is consistent: "Download Overview (PDF, 2.4 MB)" or similar
- [ ] Optional: Add a download icon (📄 or SVG) for visual clarity
- [ ] `download` attribute is used if the file should be saved rather than opened in browser

## How to Test

1. Navigate to the AI Automation page on https://launchpadlab.com/.
2. Locate the "Download Overview" link.
3. Verify visible text includes "PDF" and file size (e.g., "Download Overview (PDF, 2.4 MB)").
4. Inspect the link element — verify `aria-label` includes file type and size.
5. Use a screen reader — confirm the full description is announced (file type, size).
6. Click the link — verify the PDF downloads or opens as expected.
7. Check that file size is accurate (compare with actual file size).

## Developer Notes

### General Explanation
The "Download Overview" link on the AI Automation page links directly to a PDF without indicating file type or size. Users are surprised by an unexpected download. Indicating file type and size helps users with slow connections, limited storage, or assistive technology make informed decisions.

**Solution:** Add file type and size indicators to the link text. Example: "Download Overview (PDF, 2.4 MB)". Use `aria-label` or visible text. Consider adding the `download` attribute and an icon for clarity.

### Code Examples

**Basic implementation:**
```html
<a
  href="/agentforce-overview.pdf"
  download="Agentforce-Overview.pdf"
  aria-label="Download Agentforce Overview (PDF, 2.4 MB)"
>
  Download Overview (PDF, 2.4 MB)
</a>
```

**With icon:**
```html
<a
  href="/agentforce-overview.pdf"
  download="Agentforce-Overview.pdf"
  aria-label="Download Agentforce Overview (PDF, 2.4 MB)"
  class="download-link"
>
  <span class="icon" aria-hidden="true">
    <svg><!-- PDF icon --></svg>
  </span>
  Download Overview (PDF, 2.4 MB)
</a>
```

**React component with dynamic file size:**
```jsx
const DownloadLink = ({ href, label, fileSize, fileName }) => (
  <a
    href={href}
    download={fileName}
    aria-label={`${label} (PDF, ${fileSize})`}
  >
    {label} (PDF, {fileSize})
  </a>
);

<DownloadLink
  href="/agentforce-overview.pdf"
  label="Download Overview"
  fileSize="2.4 MB"
  fileName="Agentforce-Overview.pdf"
/>
```

**Fetching file size dynamically (optional):**
```javascript
async function getFileSize(url) {
  const response = await fetch(url, { method: 'HEAD' });
  const bytes = parseInt(response.headers.get('Content-Length') || 0, 10);
  return bytes >= 1024 * 1024
    ? `${(bytes / (1024 * 1024)).toFixed(1)} MB`
    : `${(bytes / 1024).toFixed(1)} KB`;
}
```

### Components to Audit
- AI Automation page download link
- Any other PDF or document download links across the site
- Shared link/button component used for downloads

## Examples from Other Sites

- **GOV.UK** — Always shows file type and size for document downloads (e.g., "Download form (PDF, 245 KB)"). Accessible and user-friendly.
- **BBC.com** — Document downloads are clearly labeled with file type and size.
- **W3C** — Technical documents often include "(PDF)" or "(HTML)" in link text.
