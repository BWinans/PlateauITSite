# Getting Started

[← Back to README](../README.md) · [Next: Deployment →](02-deployment.md)

## Requirements

None. The site is pure static HTML — there is nothing to install, compile, or configure.

An internet connection is needed so the Tailwind CDN can load.

## Local Development

**Option 1 — Open the file directly**

Open `index.html` in any modern browser.

**Option 2 — Serve locally (recommended)**

Serving over HTTP more closely matches production behavior:

```bash
# Python 3
python -m http.server 8000

# or Node.js
npx serve .
```

Then visit [http://localhost:8000](http://localhost:8000).

> Tip: hCaptcha and other third-party scripts may behave differently on `file://` URLs, so prefer a local HTTP server when testing the contact form.

## Project Structure

```
PlateauITSite/
├── docs/                  # Documentation pages
├── favicon.png            # Site icon (38×38 PNG)
├── index.html             # The entire website (markup + Tailwind classes)
├── LICENSE                # Proprietary license — all rights reserved
└── README.md
```

Everything on the page lives in `index.html`: markup, Tailwind utility classes, the contact form, and the small inline validation script.

## A note on `CNAME`

Earlier revisions included a `CNAME` file containing `plateauit.com`, a **GitHub Pages** artifact from the project's original hosting. It has since been removed, as Cloudflare does not read it and the custom domain is configured in Cloudflare DNS instead. The domain record now lives in the Cloudflare dashboard, not in this repository.

---

[← Back to README](../README.md) · [Next: Deployment →](02-deployment.md)
