# Customization

[← Previous: Contact Form](03-contact-form.md) · [Back to README](../README.md) · [Next: Roadmap →](05-roadmap.md)

The site is split across four pages, all hand-written:

| Page | Edit here for… |
| --- | --- |
| `index.html` | Hero copy, featured services, managed-support teaser |
| `services.html` | Service categories, deliverables, starting rates |
| `pricing.html` | Package tiers, labor rates, billing policies |
| `contact.html` | Form fields, service area, hours, response info |

Each page carries its own copy of the header and footer markup. When you change navigation or footer links, update **all four files**.

## Content

- **Copy / headline**: update text inside the `<h1>` and `<p>` tags in the hero sections.
- **Services**: edit the `<article>` cards in `services.html`; the home page shows a three-card preview. Keep the `NN / LABEL` eyebrow pattern consistent.
- **Pricing**: update the package cards and rate table in `pricing.html`.
- **Contact details**: add a phone number, email address, or business address in `contact.html` or the footer.
- **Form fields**: add inputs with a `name` attribute; Web3Forms forwards every field to the email.

## Navigation

The header contains two nav blocks: one for desktop (`hidden md:flex`) and one for mobile (`md:hidden`). The current page is marked by swapping `text-stone-300` for `text-amber-400` on its link. Remember to update both blocks and all four pages.

## Adding a page

1. Copy an existing page (e.g. `services.html`) as a starting point.
2. Update `<title>`, the meta description, and the `<h1>`.
3. Set the active nav link in both header nav blocks and the footer.
4. Add the new page to the nav on **every** page.
5. Update the page table in `README.md`, `docs/01-getting-started.md`, and the changelog.

## Colors

The palette uses Tailwind's `stone` (warm sandstone backgrounds/text) and `amber` (sunset-yellow accents), plus a thin amber-to-orange gradient bar and a soft radial glow in the hero.

| Role | Classes |
| --- | --- |
| Page background | `bg-stone-900` |
| Section band | `bg-stone-950/50` |
| Cards / surfaces | `bg-stone-800/70`, `border-stone-700/80` |
| Body text | `text-stone-100`, `text-stone-400` |
| Accent / CTA | `bg-amber-500`, `hover:bg-amber-400` |
| Logo accent | `text-amber-400` |
| Eyebrow labels | `text-amber-500` |
| Selection | `selection:bg-amber-500` |

Swap `amber-*` classes for another hue to rebrand.

## Typography & Layout

The layout is a centered `max-w-6xl` container with `px-6` gutters. The services grid collapses from three columns to one below the `md` breakpoint. Adjust the `grid md:grid-cols-3` class to change the column count.

## Production note on Tailwind

The `cdn.tailwindcss.com` build is intended for prototyping. It compiles styles in the browser, which adds a small runtime cost and a flash of unstyled content on slow connections. For production, consider generating a static stylesheet:

```bash
npx tailwindcss -i ./src/input.css -o ./dist/output.css --minify
```

Then link `output.css` in `<head>` instead of the CDN script.

---

[← Previous: Contact Form](03-contact-form.md) · [Back to README](../README.md) · [Next: Roadmap →](05-roadmap.md)
