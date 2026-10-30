# Customization

[← Previous: Contact Form](03-contact-form.md) · [Back to README](../README.md) · [Next: Roadmap →](05-roadmap.md)

Everything lives in `index.html`; edit it and redeploy.

## Content

- **Copy / headline** — update text inside the `<h1>` and `<p>` tags in the Hero section.
- **Services** — duplicate or edit the three `<div>` cards in the `#services` section. Keep the `NN / LABEL` eyebrow pattern consistent.
- **Contact details** — add a phone number, email address, or business address near the form or in the footer.
- **Form fields** — add inputs with a `name` attribute; Web3Forms forwards every field to the email.

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
