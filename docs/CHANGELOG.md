# Changelog

All notable changes to Foothills will be documented in this file.

The format is based on Keep a Changelog, and this project adheres to Semantic Versioning.

## [0.2.0] - 2025-09-14
### Added
- Color Palette system with one‑click switcher (Prairie, River, Night, Burnt) and header palette toggle
- Compact mobile drawer that mirrors the desktop nav (icons) and overlays header
- Social links widget now uses full URLs; default set: Email, Instagram, Bluesky, Goodreads, RSS; optional: Twitter, AO3
- Featured Tags moved to a dedicated sidebar widget with chips
- Donate widget (Ko‑fi by default) enabled via Theme Options
- Exact date format on posts (e.g., “Monday, January 1st, 2025 at 12:59PM”) linking to permalink
- Font Awesome visuals for reblog (retweet) and like (heart) while preserving Tumblr button functionality
- GUIDE.md with full documentation; README Quick Start trimmed and linked to docs

### Changed
- Tag pills have accent‑tinted backgrounds for clarity
- Sidebar social links shown as a centered 2‑per‑row grid
- Mobile: sidebar remains below posts; drawer contains nav only

### Fixed
- Drawer hidden state allowed “ghost” clicks; now blocks pointer events when hidden
- Drawer now slides in/out and sits above header (z‑index)
- Hero text color uses palette text; removed dark‑hero override
- Dark palettes use a darker page background
- Scoping of quote styles to quote posts only (metadata unaffected)
- Stray block before DOCTYPE removed; added concise Quick Start and docs link

## [0.1.0] - 2025-09-13
### Added
- Initial theme scaffold `theme/foothills.html` with:
  - Configurable header links (up to 5) via Theme Options
  - Featured Tags row using `{block:HasFeaturedTags}` and `{block:FeaturedTags}`
  - Posts rendering for NPF + legacy types with reblog trails
  - Sidebar widgets (About, Social, Substack, Blogroll x5, Write Club)
  - Pagination with jump pages
  - Accessibility basics (skip link, focus states, landmarks)
  - Mobile drawer (hamburger) that consolidates nav + sidebar widgets
- External stylesheet `assets/foothills.css`
- README with installation and asset hosting guidance

[0.2.0]: docs/CHANGELOG.md
[0.1.0]: docs/CHANGELOG.md
