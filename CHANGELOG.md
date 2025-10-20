# Changelog

All notable changes to Foothills will be documented in this file.

The format is based on Keep a Changelog, and this project adheres to Semantic Versioning.

## [Unreleased]
### Added
- Google Fonts integration in preview (Cormorant Garamond for poetry, Inter for UI)
- Enhanced mobile menu with better accessibility and keyboard navigation
- Error handling and fallbacks for image loading
- Improved color palette toggle with localStorage persistence

### Fixed
- Fixed JavaScript errors in mobile menu implementation
- Resolved issues with drawer focus management
- Fixed duplicate event listeners in mobile navigation
- Addressed linting and syntax issues in theme JavaScript
- Fixed image loading errors with proper fallbacks

### Changed
- Refactored JavaScript for better performance and maintainability
- Improved mobile menu animations and transitions
- Updated preview to be fully static with hardcoded content
- Enhanced error handling throughout the codebase

## [0.2.0] - 2025-09-14
### Added
- Mobile drawer refinements:
  - Drawer title centered with separators and blog blurb
  - Palette toggle inside drawer, styled like other items
  - Denser spacing and better scrolling behavior
- SEO options in `<head>` (Theme Options):
  - Title/description overrides, OG image URL, Twitter username, Canonical URL
  - theme-color meta and optional JSON-LD `Blog` schema
- Pinned post treatment:
  - `pinned-post` class with accent top bar and soft `pinned-badge`
- CTA buttons micro-interactions (hover lift, press)

### Changed
- Header alignment: site title and nav chips share a clean baseline
- Sidebar section headings larger and centered
- Footer (mobile): extra padding; footer nav 2-per-row and centered
- Search results meta moved to bottom of page; search input is overlay-only
- Hover states unified via `--hover` token; strengthened visibility in dark palettes
- Organized CSS with section dividers and TOC

### Fixed
- UA margin reset to remove default `body { margin: 8px; }` white border
- Drawer/search close buttons now inherit theme text color for dark palettes

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
- External stylesheet `assets/foothills.css` implementing layout, typography, poetry formatting, and responsive behavior
- `README.md` with installation and asset hosting guidance

### Changed
- None

### Fixed
- None

[0.2.0]: https://github.com/brennanbrown/foothills/releases/tag/v0.2.0
[0.1.0]: https://github.com/brennanbrown/foothills/releases/tag/v0.1.0
