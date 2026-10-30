# PlateauIT Website

The official marketing site for **PlateauIT LLC**, an on-site IT support and network services business serving Winslow and Northern Arizona.

**Live site:** [https://plateauit.com](https://plateauit.com) · **Repo:** [github.com/BWinans/PlateauITSite](https://github.com/BWinans/PlateauITSite)

---

## Overview

A single-page, fully static website. There is no framework, build step, package manager, or backend — just one self-contained `index.html` file styled with the Tailwind CSS CDN and deployed to Cloudflare.

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

## Documentation

| # | Page | What it covers |
| --- | --- | --- |
| 1 | [Getting Started](docs/01-getting-started.md) | Running the site locally and understanding the layout |
| 2 | [Deployment](docs/02-deployment.md) | Cloudflare Pages settings, DNS, and caching |
| 3 | [Contact Form](docs/03-contact-form.md) | Web3Forms setup, access keys, and hCaptcha |
| 4 | [Customization](docs/04-customization.md) | Editing copy, colors, services, and form fields |
| 5 | [Roadmap](docs/05-roadmap.md) | Suggested improvements for SEO, performance, and trust |
| 6 | [Changelog](docs/06-changelog.md) | History of notable changes |

A full index of the docs folder is also available at [`docs/README.md`](docs/README.md).

---

## Project Structure

```
PlateauITSite/
├── docs/                  # Documentation pages (see index above)
├── favicon.png            # Site icon (38×38 PNG)
├── index.html             # The entire website (markup + Tailwind classes)
├── LICENSE                # Proprietary license — all rights reserved
└── README.md
```

---

## License

Proprietary — all rights reserved by PlateauIT LLC. See [LICENSE](LICENSE) for terms.
