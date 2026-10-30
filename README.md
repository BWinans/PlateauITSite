# PlateauIT Website

The official marketing site for **PlateauIT LLC**, an on-site IT support and network services business serving Winslow and Northern Arizona.

**Live site:** [https://plateauit.com](https://plateauit.com)

---

## Overview

A single-page, fully static website. There is no framework, build step, package manager, or backend — just one self-contained `index.html` file styled with the Tailwind CSS CDN and deployed to Cloudflare.

The page is organized into four sections:

| Section | Content |
| --- | --- |
| **Header** | Sticky navigation with the PlateauIT wordmark and a "Request Support" call-to-action |
| **Hero** | Headline, service-area badge, and primary CTAs |
| **Services** | Three cards: Network & Wi-Fi Systems, Storage & Samba Servers, Systems Administration |
| **Contact** | Web3Forms-powered inquiry form (name, email, message) with hCaptcha |

---

## Tech Stack

- **HTML5** — semantic, single-file layout
- **Tailwind CSS** (CDN: `cdn.tailwindcss.com`) — utility-first styling, no compiled stylesheet
- **Web3Forms** — serverless form submission endpoint
- **hCaptcha** — spam protection on the contact form, loaded via the Web3Forms client script
- **Cloudflare** — hosting, CDN, TLS, and DNS for `plateauit.com`

JavaScript use is minimal: Tailwind loads at runtime, Web3Forms loads hCaptcha, and a short inline script blocks form submission until the captcha is solved.

---

## Project Structure

```
PlateauITSite/
├── index.html   # The entire website (markup + Tailwind classes)
├── LICENSE      # Proprietary license — all rights reserved
└── README.md
```

### A note on `CNAME`

Earlier revisions included a `CNAME` file containing `plateauit.com`, a **GitHub Pages** artifact from the project's original hosting. It has since been removed, as Cloudflare does not read it and the custom domain is configured in Cloudflare DNS instead. The domain record now lives in the Cloudflare dashboard, not in this repository.

---

## Local Development

Because the site is pure static HTML, there is nothing to install or compile.

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

> An internet connection is required locally so the Tailwind CDN can load.

---

## Deployment

The site is deployed through **Cloudflare** and is live at `https://plateauit.com`. Response headers confirm the site is served from Cloudflare's edge (`Server: cloudflare`, `CF-Cache-Status: HIT`).

The typical Cloudflare Pages configuration for a repo like this is:

| Setting | Value |
| --- | --- |
| Framework preset | None |
| Build command | *(none)* |
| Build output directory | `/` |
| Production branch | `main` |

Pushing to `main` triggers a new deployment. Changes are live once Cloudflare finishes the build.

### Domain & DNS

- `plateauit.com` is managed by Cloudflare DNS.
- The apex domain serves the site directly; TLS is provisioned automatically by Cloudflare.
- Caching is handled at the edge. HTML is served with `Cache-Control: public, max-age=0, must-revalidate`, so content updates appear immediately after deployment.

---

## Contact Form

The form in `index.html` posts to `https://api.web3forms.com/submit`:

```html
<form id="contact-form" action="https://api.web3forms.com/submit" method="POST">
    <input type="hidden" name="access_key" value="...">
    <input type="hidden" name="subject" value="New Inquiry from PlateauIT.com">
    ...
    <div class="h-captcha" data-captcha="true" data-theme="dark"></div>
</form>

<script src="https://web3forms.com/client/script.js" async defer></script>
```

Submissions are emailed to the address associated with the Web3Forms access key.

**About the access key:** Web3Forms access keys are designed to be public — they identify the destination inbox, not authorize an account. They are safe to commit. If the inbox changes or the key is abused, generate a new key in the Web3Forms dashboard and update the hidden input.

### hCaptcha

The form is protected by **hCaptcha**, using Web3Forms' zero-config integration — no hCaptcha account, site key, or secret key is required. Two pieces make it work:

1. The `<div class="h-captcha" data-captcha="true" data-theme="dark">` placeholder inside the form.
2. The `<script src="https://web3forms.com/client/script.js" async defer>` tag before `</body>`, which renders the widget and injects the `h-captcha-response` field.

An inline script also validates the challenge client-side before allowing submission:

```js
document.getElementById('contact-form').addEventListener('submit', function (e) {
    const hCaptchaResponse = this.querySelector('textarea[name="h-captcha-response"]');

    if (!hCaptchaResponse || !hCaptchaResponse.value.trim()) {
        e.preventDefault();
        alert('Please complete the captcha before submitting.');
    }
});
```

> **Required dashboard step:** hCaptcha must also be enabled for the form at [app.web3forms.com](https://app.web3forms.com) (open the form → spam protection settings → select hCaptcha). Without that, the widget renders but submissions are not actually verified.

`data-theme="dark"` matches the site's dark palette; other hCaptcha options can be passed as `data-*` attributes (for example `data-lang="es"` or `data-size="compact"`).

---

## Customization Guide

Everything lives in `index.html`; edit it and redeploy.

- **Copy / headline** — update text inside the `<h1>` and `<p>` tags in the Hero section.
- **Services** — duplicate or edit the three `<div>` cards in the `#services` section. Keep the `NN / LABEL` eyebrow pattern consistent.
- **Contact details** — add a phone number, email address, or business address near the form or in the footer.
- **Colors** — the palette uses Tailwind's `slate` (backgrounds/text) and `cyan` (accents). Swap `cyan-*` classes for another hue to rebrand.
- **Form fields** — add inputs with a `name` attribute; Web3Forms forwards every field to the email.

### Production note on Tailwind

The `cdn.tailwindcss.com` build is intended for prototyping. It compiles styles in the browser, which adds a small runtime cost and a flash of unstyled content on slow connections. For production, consider generating a static stylesheet:

```bash
npx tailwindcss -i ./src/input.css -o ./dist/output.css --minify
```

Then link `output.css` in `<head>` instead of the CDN script.

---

## Suggested Improvements

- Add `<meta name="description">` and Open Graph / Twitter card tags for better search and social previews.
- Add a favicon and `apple-touch-icon`.
- Add structured data (`LocalBusiness` JSON-LD) to improve local SEO for "Winslow IT support".
- Surface a phone number and email prominently — many local service customers prefer calling.
- Add a privacy policy page, particularly since the contact form collects personal data.
- Consider a custom 404 page on Cloudflare Pages.
- Optimize the Tailwind delivery (see above) and add a `robots.txt` / `sitemap.xml`.

---

## Changelog

- **2026-10-30** — Added hCaptcha spam protection to the contact form (Web3Forms integration plus client-side validation).
- **2026-10-29** — Added a proprietary `LICENSE` (all rights reserved).
- **2026-10-29** — Removed the `CNAME` file; the custom domain is now managed entirely through Cloudflare DNS. Added this README.
- **2026-10-29** — Replaced the original `page/page.html` with a redesigned root `index.html` (dark theme, services grid, Web3Forms contact form).

---

## Repository

- **GitHub:** [github.com/BWinans/PlateauITSite](https://github.com/BWinans/PlateauITSite)
- **Branch:** `main`
- **License:** Proprietary — all rights reserved by PlateauIT LLC. See [LICENSE](LICENSE) for terms.
