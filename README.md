# The Big Red Button (Senior-Friendly Audio Wrapper)

A single-page, no-backend web app that wraps a Dropbox audio link in a dead-simple UI: one giant red play/pause button.

## How it works

- The app stores the audio source in the URL fragment (hash):
  - `https://bigredbutton.online/#audio=[ENCODED_URL]`
- If the page URL has **no** `#audio=...`, you see the **Generator** view.
- If the page URL **has** `#audio=...`, you see only the **Player** view (the big red button).

## Dropbox link “cleaning”

In the Generator, pasted Dropbox share links are converted into a direct, stream-friendly link:

- `www.dropbox.com` → `dl.dropboxusercontent.com`
- Removes `dl=0/1`
- Preserves important parameters like `rlkey=...`
- Forces `raw=1`

This helps avoid Dropbox 404s and makes the link suitable for HTML5 audio playback.

## Run locally

This is a static site (one file: `index.html`).

Option A: open the file directly
- Double-click `index.html`.

Option B: serve with a local web server (recommended)

```bash
python3 -m http.server 8000
```

Then open:
- `http://localhost:8000/`

## Deploy

Deploy as a normal static site.

Key points:
- Ensure `index.html` is served at `/`.
- Use HTTPS in production (clipboard copy works best on HTTPS).
- No special routing/rewrite rules are needed because navigation uses the URL hash.

## Accessibility

- The big red button controls a standard HTML5 `<audio>` element.
- Clicking the button toggles play/pause via `audio.play()` / `audio.pause()`.

## Notes

- Google Drive/OneDrive are not supported right now. (Dropbox is the only supported source.)
