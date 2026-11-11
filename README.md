# Sara M. Jenkins Ministry Website

Current static website source exported from the existing ChatGPT Site on October 1, 2026.

## Files
- index.html: complete current content, responsive CSS, and scripts.
- assets/: all ten Site photo assets, web-optimized as WebP for GitHub hosting.

## Preview
Open index.html in a browser, or run `python3 -m http.server 8000` from this folder.

## GitHub replacement
Replace the temporary index.html and styles.css with the contents of this archive on the main branch of sjenkins-ministry/sj-ministry-website. Remove the old styles.css; styling is embedded in index.html.

## Hosting
This is a buildless static site. Publish this folder as the website root. Google Fonts are loaded remotely. Existing contact behavior is preserved. This export does not change the existing ChatGPT Site, DNS, or domain configuration.

Source commit: 51164255176ebd93d418a5676a04891aa5aa2ae6
## Guidance & Mentoring form (`mentoring/`)
- Emails each request to sara@sarajenkins.com through FormSubmit, then redirects to `mentoring/thank-you/`.
- Also logs to the Google Sheet "Sara Jenkins – Guidance & Mentoring Requests" once its Apps Script web app is deployed and its `/exec` URL is pasted into `SHEET_WEBHOOK_URL` in `mentoring/index.html`.

Apps Script (Sheet → Extensions → Apps Script; Deploy → Web app, Execute as: Me, Who has access: Anyone):

```js
function doPost(e) {
  const p = e.parameter;
  const clean = v => { v = String(v || ''); return /^[=+\-@]/.test(v) ? "'" + v : v; }; // block formula injection
  SpreadsheetApp.getActiveSpreadsheet().getSheets()[0].appendRow([
    new Date(), clean(p.name), clean(p.email), clean(p.phone),
    clean(p['meeting-preference'] || 'Not specified'), clean(p.guidance), clean(p['additional-details'])
  ]);
  return ContentService.createTextOutput('ok');
}
```
