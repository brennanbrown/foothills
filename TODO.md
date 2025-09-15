# Foothills TODO

## Completed (recent)
- [x] Color palette system and header palette toggle
- [x] Compact mobile drawer (icons) that mirrors desktop links
- [x] Social links grid and full URL fields (Instagram, Bluesky, Goodreads, Twitter, AO3)
- [x] Featured Tags sidebar widget and Donate widget
- [x] Exact date format on posts; FA visuals for Reblog/Like
- [x] Dark palette page background; quote styles scoped; hero text color fixed
- [x] Docs overhaul: concise Quick Start in `theme/foothills.html` and `docs/GUIDE.md`
- [x] Header/nav baseline alignment; remove UA `body` margin
- [x] Drawer title + separators + blurb; palette toggle inside drawer
- [x] Hover backgrounds unified via `--hover` and tuned for dark palettes
- [x] Footer mobile padding and 2‑per‑row centered nav
- [x] Sidebar headings centered and larger; About → Currently Reading styled
- [x] Pinned post styling (`pinned-post` + `pinned-badge`)
- [x] CTA button micro‑interactions and text color lock
- [x] SEO options (OG/Twitter/canonical/theme‑color + optional JSON‑LD)
- [x] Favicons wired for theme and preview
- [x] README beautified with logo/badges, screenshot; CHANGELOG v0.2.0

## Next
- [ ] Per‑post `og:image` fallbacks on permalinks (photo/link/video)
- [ ] Localization strings (`{lang:...}`) for UI labels (Menu, Connect, Newsletter, Random, Archive)
- [ ] Notes on permalinks using `{block:PostNotes}` (with optional FA icons)
- [ ] Search/404 states (use `{block:SearchPage}` and `{block:NoSearchResults}`)
- [ ] Optional Related Posts on permalinks (`{block:RelatedPosts}`)
- [ ] Replace FA CDN with SVGs/Tumblr‑hosted assets for Theme Garden
- [ ] Demo blog setup and link in README
- [ ] Stylelint + Prettier config and scripts; optional CSS split into partials

## Nice-to-have
- [ ] Layout density select (regular/compact)
- [ ] Optional header image via `{image:Header}` with toggle
- [ ] Optional Following/Likes widgets
- [ ] Enhanced NPF rendering using `{NPF}` JSON for fine-grained styling

## A11y
- [ ] Confirm WCAG AA contrast across palettes; tune defaults if needed
- [ ] Add focus trap to drawer and return-focus to menu button

## Performance
- [ ] Consider minifying CSS for production builds
- [ ] Defer non-critical JS or inline critical CSS if needed for Theme Garden

## QA
- [ ] Cross-browser/device test (Safari, Firefox, Chrome; iOS/Android)
- [ ] Test all legacy post types, reblog trails, and featured tags
- [ ] Validate against Tumblr Theme Garden checklist
