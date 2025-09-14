# Foothills — A Tumblr Theme for Poetry & Community

Foothills is a Tumblr theme designed for writers and community builders. It emphasizes breathable typography, warm colors, and first-class support for reblogs and poetry formatting.

This repo contains:
- `theme/foothills.html` — the complete single‑file Tumblr theme for Tumblr’s Custom HTML editor.
- `assets/foothills.css` — optional external stylesheet you can host and reference in Theme Options.
- `docs/` — documentation and change history (`GUIDE.md`, `CHANGELOG.md`).
 - Optional demo hosting via Netlify.

## Quick Start

1) Open Tumblr → Customize → Edit HTML.
2) Paste the entire contents of `theme/foothills.html`.
3) Save and exit HTML editor.
4) In Customize → Theme Options, set:
   - Colors, fonts, palette
   - Nav links, Social URLs (full URLs), Write Club description, Calendly link
   - Toggles (poetry formatting, hero CTA, Use Chota CSS, Donate)
   - Optional: set `External Stylesheet URL` to your hosted `assets/foothills.css`

## External Stylesheet Options

There are two supported ways to host `assets/foothills.css`:

- GitHub Raw (good for development and personal use)
  - Example URL: `https://raw.githubusercontent.com/brennanbrown/foothills/MAIN_OR_TAG/assets/foothills.css`
  - Replace `MAIN_OR_TAG` with your default branch (e.g., `main`) or a version tag.

- Tumblr Static Assets (required for Theme Garden submission)
  - In Customize → Theme → Theme Assets (Upload), upload `foothills.css`.
  - Copy the uploaded file URL and paste into the `External Stylesheet URL` theme option.

Note: Tumblr Theme Submission Guidelines require hosting assets on Tumblr's static uploader for themes listed in the Theme Garden. For your own blog, GitHub Raw is fine, but Tumblr may cache differently.

## Theme Options (Customizer)

- Colors: `Accent Color`, `Link Color`, `Background`, `Text`
- Fonts: `Poetry Font`, `Headers Font`, `Body Font`, `UI Font`
- Palette: `Color Palette` (Prairie, River, Night, Burnt)
- Toggles:
  - `Show Calendly CTA`
  - `Show Current Reading`
  - `Enable Poetry Special Formatting`
  - `Use Chota CSS` (loads `https://unpkg.com/chota@latest`)
- Text fields:
  - `Calendly Link`
  - `Substack Embed Code` (paste iframe/embed)
  - `Email Address`
  - `Write Club Description`
  - `Current Reading`
  - Social URLs (full): `Instagram URL`, `Bluesky URL`, `Goodreads URL`, `Twitter URL`, `AO3 URL`
  - `Instagram Handle` (fallback if Instagram URL not set)
  - `External Stylesheet URL`
  - Blogroll entries (x5)

## Structure

- Header with nav: About, Books, Contact, Ask, Submit, Random, Archive (icons)
- Optional hero on index with CTA (Calendly)
- Main content with full reblog trail support for NPF and legacy post types
- Sidebar widgets: About, Social (2‑per‑row links), Substack, Blogroll, Featured Tags, Write Club, Donate
- Pagination with jump pages
- Accessibility basics: skip link, focus styles, semantic landmarks

## Poetry Formatting

If `Enable Poetry Special Formatting` is on, `.post-body` for original text posts applies `.poetry-formatting` styles. Additionally, any post tagged `#poetry` or `#poem` gets the class via a small script, improving display on reblogs too.

## Live Demo

View the theme demo on Netlify:

- https://foothills-tumblr.netlify.app/preview/

Netlify builds serve the `/preview/` page and load `../assets/foothills.css` directly from the repo.

## Documentation & Changes

- Full guide: [`docs/GUIDE.md`](docs/GUIDE.md)
- Changelog: [`docs/CHANGELOG.md`](docs/CHANGELOG.md)

## Development Notes

- CSS variables are set inline in the HTML `<style>` block, exposing theme option values to the external CSS: `--bg`, `--text`, `--accent`, `--link`, `--font-poetry`, `--font-headers`, `--font-body`, `--font-ui`.
- If you prefer a micro framework, toggle `Use Chota CSS` in options.
- For Theme Garden submission, ensure all assets (CSS, images) are uploaded via Tumblr Theme Assets and URLs updated in options. Replace Font Awesome CDN with Tumblr‑hosted SVGs.

## License

See `LICENSE` in the repository.
