# Deployment

[← Previous: Getting Started](01-getting-started.md) · [Back to README](../README.md) · [Next: Contact Form →](03-contact-form.md)

The site is deployed through **Cloudflare** and is live at [https://plateauit.com](https://plateauit.com). Response headers confirm the site is served from Cloudflare's edge (`Server: cloudflare`, `CF-Cache-Status: HIT`).

## Cloudflare Pages Settings

The typical configuration for a static repo like this is:

| Setting | Value |
| --- | --- |
| Framework preset | None |
| Build command | *(none)* |
| Build output directory | `/` |
| Production branch | `main` |

Pushing to `main` triggers a new deployment. Changes are live once Cloudflare finishes the build.

## Domain & DNS

- `plateauit.com` is managed by Cloudflare DNS.
- The apex domain serves the site directly; TLS is provisioned automatically by Cloudflare.
- Caching is handled at the edge. HTML is served with `Cache-Control: public, max-age=0, must-revalidate`, so content updates appear immediately after deployment.

## Notes

- No `CNAME` file is required in the repository — the custom domain is configured in the Cloudflare dashboard.
- Because the build output directory is the repository root, files such as `README.md` and `LICENSE` are technically published too. This is harmless, but they can be excluded with a `_redirects` rule or by moving site assets into a subfolder if that ever matters.
- All four HTML pages are served from the root and linked with relative URLs, so no routing rules are required. Cloudflare serves `/services.html`, `/pricing.html`, and `/contact.html` directly.

---

[← Previous: Getting Started](01-getting-started.md) · [Back to README](../README.md) · [Next: Contact Form →](03-contact-form.md)
