# Foothills Theme Guide

This document expands on the Quick Start note in `theme/foothills.html`. It explains installation, options, and customization.

## 1) Install

- Tumblr → Customize → Edit HTML → Paste the contents of `theme/foothills.html` → Save.
- Optional: Host `assets/foothills.css` and set the Theme Option `External Stylesheet URL`.
  - Personal blog: a GitHub raw URL is fine for testing.
  - Theme Garden: upload CSS to Tumblr Theme Assets (HTTPS) and use that URL.

## 2) Theme Options

- Colors: `Background`, `Text`, `Accent`, `Link`.
- Fonts: `Poetry Font`, `Headers Font`, `Body Font`, `UI Font`.
- Toggles:
  - `Show Calendly CTA`
  - `Show Current Reading`
  - `Enable Poetry Special Formatting`
  - `Use Chota CSS`
  - `Show Donate`
- Text fields:
  - `Email Address`
  - `Write Club Description`
  - `Current Reading`
  - `Footer SEO Blurb`
  - Social URLs (full URLs): `Instagram URL`, `Bluesky URL`, `Goodreads URL`, `Twitter URL`, `AO3 URL`
    - If `Instagram URL` isn’t set, the theme falls back to `Instagram Handle`.
- Header links: `Nav Link 1–5 Label/URL`
- Blogroll links (x5): `Blogroll Link {N} URL/Title/Description`

## 3) Palettes

- Select `Color Palette` (Prairie, River, Night, Burnt) in the editor.
- The palette button in the header cycles palettes and saves the choice in localStorage.

## 4) Mobile Drawer

- Compact, iconified nav showing Books, Contact, Ask, Submit, Random, Archive.
- About/Connect live in the sidebar on mobile, so they’re omitted from the drawer.
- Drawer overlays the header. ESC, overlay click, and ✕ close it.

## 5) Posts

- Dates: exact format, e.g., `Monday, January 1st, 2025 at 12:59PM`, linking to the permalink.
- Reblog/Like actions:
  - Reblog uses a Font Awesome retweet icon linking to `{ReblogURL}`.
  - Like overlays a Font Awesome heart on Tumblr’s `{LikeButton}` iframe for visuals while keeping functionality.
- Quote styling is scoped to quote posts and won’t affect other metadata.

## 6) Featured Tags / Donate

- Featured Tags render in the sidebar as chips when the blog has featured tags.
- Donate widget (Ko‑fi by default): configured by `Show Donate`, `Donate URL`, `Donate Button Label`, `Donate Blurb`.

## 7) Assets and Icons

- For Theme Garden, host CSS and images via Tumblr Theme Assets (HTTPS).
- This theme uses Font Awesome from a CDN for convenience. For now, install from GitHub as-is. If you plan to submit to Theme Garden later, consider replacing with SVGs/Tumblr-hosted icons.

## 8) Local Preview

- Open `preview/index.html` in a static server from the repo root.
- The preview mirrors the theme (hero, posts, sidebar, drawer, Featured Tags, Donate) and includes the palette toggle.

## 9) Dev Notes

- CSS relies on variables: `--bg`, `--text`, `--accent`, `--link`, and font tokens.
- Keep new UI consistent by reusing the existing card and button patterns.
- The mobile drawer is intentionally minimal to avoid duplicating sidebar content and to reduce complexity.

## 10) Troubleshooting

- Drawer not visible: ensure `.drawer[aria-hidden="true"]` toggles and that no other overlay has higher `z-index`.
- Palette button: it both registers click listeners and exposes `window.foothillsNextPalette()` for robustness.
- External CSS not applying in preview: serve from repo root so `/assets/foothills.css` resolves correctly.
