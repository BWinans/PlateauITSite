# Roadmap

[← Previous: Customization](04-customization.md) · [Back to README](../README.md) · [Next: Changelog →](06-changelog.md)

Suggested improvements, roughly in priority order.

## SEO & Discoverability

- Add Open Graph / Twitter card tags for better social previews (page descriptions are already in place).
- Add structured data (`LocalBusiness` JSON-LD) to improve local SEO for "Winslow IT support".
- Add a `robots.txt` and `sitemap.xml`.

## Performance

- Replace the Tailwind CDN with a compiled, minified stylesheet (see [Customization](04-customization.md#production-note-on-tailwind)).
- Provide larger favicon sizes (32×32, 180×180, and `.ico`) for crisper rendering across devices.

## Trust & Conversion

- Surface a phone number and email prominently; many local service customers prefer calling.
- Add a privacy policy page, particularly since the contact form collects personal data.
- Add customer testimonials or service-area details to build local credibility.

## Polish

- Consider a custom 404 page on Cloudflare Pages.
- Add a `noindex` or redirect for repository files (e.g. `README.md`) that are published alongside the site.
- Reduce duplicated header/footer markup across the four pages, either with a tiny build step or a shared JS include.

---

[← Previous: Customization](04-customization.md) · [Back to README](../README.md) · [Next: Changelog →](06-changelog.md)
