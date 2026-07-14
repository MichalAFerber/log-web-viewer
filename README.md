# Log Viewer

A fast, mobile-first, **single-file** log viewer. Drag & drop a `.log` (or any
text file) and read it with **search, log-level filtering, and virtualized
scrolling** — so even a multi-hundred-megabyte log stays smooth. It's a
**viewer** — no accounts, no uploads. Everything runs locally in your browser.

🔗 **Live:** <https://log-viewer.us/>

![Single file](https://img.shields.io/badge/build-single%20HTML%20file-success) ![No build step](https://img.shields.io/badge/build%20step-none-success) ![License](https://img.shields.io/badge/license-MIT-blue)

> Part of the **[File Viewer](https://file-viewer.us/) family** — HTML, Markdown,
> ePUB, PDF, Data, DOCX, Sheets, EML, PPTX, and Log each have their own
> dedicated viewer. Use the **☰ menu** in the header to jump between them.

## Features

- ⚡ **Virtualized scrolling** — only the visible lines are ever in the DOM, so
  huge logs (millions of lines) scroll smoothly instead of freezing the tab.
- 🎚️ **Level filters** — lines are auto-classified (**ERROR / WARN / INFO /
  DEBUG / other**) and color-coded; tap a chip to show or hide that level, with
  a live count per level.
- 🔎 **Instant search** — type to filter to matching lines, with the matches
  **highlighted** in place.
- #️⃣ **Line numbers** kept from the original file, so a match's position is
  always clear.
- ☰ **Family menu** · 🫥 **auto-hiding header** · 🎨 **pick any background color**.
- 🪶 **One file, no build, no dependencies** — `index.html` is self-contained,
  works offline, even from `file://`.
- 📊 **Privacy-friendly analytics** — self-hosted, cookieless
  [Plausible](https://plausible.io/); your logs never leave your device.

## Supported file types

`.log` `.txt` `.out` `.err` `.trace` `.syslog` — and pasted text.

## Quick start

**Just open it.** Download [`index.html`](index.html), double-click it — no
server, no build, no internet needed.

```sh
python3 -m http.server 8080   # then open http://localhost:8080
```

## Deploy to Cloudflare Pages

Connect the repo (**Workers & Pages → Create → Pages → Connect to Git**),
framework preset **None**, build command blank, output directory `/`. The
[`_headers`](_headers) file applies a strict CSP automatically. Add the custom
domain **log-viewer.us** under the project's Custom domains tab.

## How it works

Everything is in [`index.html`](index.html) — **no third-party libraries.** The
file is split into lines once; each line is classified by a level regex; a
windowed renderer keeps only the on-screen rows (plus a small overscan) in the
DOM and repositions them on scroll, so memory and layout stay flat regardless of
file size. Search and level filters rebuild the visible index in a single pass.
The viewer's CSP stays strict (`default-src 'none'`, no external assets).

**Note:** rows use a fixed line height for virtualization, so extremely long
lines scroll horizontally rather than wrapping. Level detection is heuristic
(common `ERROR/WARN/INFO/DEBUG` tokens); unrecognized lines are grouped as
"other".

## Credits

No bundled libraries — the viewer is original to this project. The terminal icon
is by the author. Analytics by [Plausible](https://plausible.io/).

## License

[MIT](LICENSE) © 2026 Michal Ferber, aka **TechGuyWithABeard**.
