---
title: "Foothills: Building a Modern, Accessible Tumblr Theme in 2025"
description: "A technical deep dive into designing and shipping a configurable, SEO-friendly Tumblr theme—with lessons learned about the Tumblr platform, CSP, caching, favicons, Open Graph, and progressive enhancement."
tags: [tumblr, webdev, css, html, accessibility, seo]
cover_image: https://raw.githubusercontent.com/brennanbrown/foothills/main/docs/screenshot.png
published: false
---

Tumblr’s theme system is both deceptively simple and surprisingly powerful. Over the past few years, Tumblr has quietly modernized a lot of their platform and documentation, but most theme development guides and popular themes haven’t kept up with current UX expectations: accessibility, responsive ergonomics, social metadata, and sensible customization.

I built Foothills to explore what a modern Tumblr theme could look like—one that’s accessible, configurable, and optimized for writers and small communities. This post documents the technical journey, the surprising challenges, and the pragmatic solutions that made it production-ready.

# Goals

- Accessible, mobile-first layout with generous typography and calm UI
- Configurable “one-click” color palettes with a front-end toggle
- Sensible SEO: canonical URLs, Open Graph, Twitter Cards, optional JSON‑LD
- Clean reblog trails and notes, with balanced hierarchy
- First-class mobile drawer that doesn’t duplicate sidebar content
- Favicon handling that doesn’t break on custom domains
- Progressive enhancement: graceful behavior if external CSS fails

Main files:
- `theme/foothills.html` — The Tumblr theme (HTML + Tumblr tags + inline safety styles)
- `assets/foothills.css` — The full CSS, shipped via CDN or Tumblr Theme Assets
- `preview/index.html` — Static preview of the theme head and favicons

# Tumblr Theme Constraints That Matter

Tumblr themes are a single HTML document with their own templating tags. You get:
- Blocks like `{block:PermalinkPage}` and variables like `{MetaDescription}`
- Buttons and widgets like `{LikeButton}` and `{ReblogButton}` that render iframes
- User-configurable Theme Options via `<meta name="text:Option Name">` and friends

Caveats you’ll want to design around:
- Content Security Policy and cross-domain iframes are strict; you cannot inject arbitrary third‑party JS
- Tumblr buttons render in iframes; style with a wrapper, not the iframe internals
- External CSS is allowed, but Tumblr’s `{CustomCSS}` is injected late—order matters

# Progressive Enhancement: Inline Safety Net

If you host CSS externally and the CDN hiccups, a blank page is a terrible first impression. Foothills embeds a tiny inline CSS safety net inside `theme/foothills.html`—only enough to respect tokens, show a usable header, and avoid a flash of unstyled content. Everything else lives in `assets/foothills.css`.

Key snippet in `theme/foothills.html`:

```html
<style>
  :root { /* bridged from Theme Options */
    --bg: {color:Background};
    --text: {color:Text};
    --accent: {color:Accent Color};
    --link: {color:Link Color};
    --font-poetry: {font:Poetry Font};
    --font-headers: {font:Headers Font};
    --font-body: {font:Body Font};
    --font-ui: {font:UI Font};
  }

  html { background: var(--bg); color: var(--text); }
  body { margin: 0; font-family: var(--font-body, serif); }

  /* Inline fallback palettes so the toggle still works even if CSS is cached */
  body[data-palette="Prairie"] { --bg:#FFFEF7; --text:#2F2F2F; --accent:#D2691E; --link:#B8860B; }
  body[data-palette="River"]   { --bg:#F8FAFD; --text:#232A31; --accent:#2A9D8F; --link:#1E6F77; }
  body[data-palette="Night"]   { --bg:#0b0e11; --text:#EDEDED; --accent:#E3985B; --link:#F2B679; }
  body[data-palette="Burnt"]   { --bg:#120c08; --text:#F6F1EB; --accent:#D2691E; --link:#E0AA72; }
</style>
```

This kept the palette toggle functional even when a CDN edge had stale CSS.

# One‑Click Palettes with a Toggle

In the Theme Options we expose this select multiple times to define choices:

```html
<meta name="select:Color Palette" content="Prairie" title="Prairie (light)">
<meta name="select:Color Palette" content="River" title="River (light, cool)">
<meta name="select:Color Palette" content="Night" title="Night Sky (dark)">
<meta name="select:Color Palette" content="Burnt" title="Burnt Umber (dark, warm)">
```

Then bind it to `body[data-palette]`:

```html
<body class="foothills" data-palette="{select:Color Palette}">
```

A tiny script cycles through the list and persists to `localStorage`:

```js
(function() {
  var palettes = ["Prairie", "River", "Night", "Burnt"]; // keep in sync with Theme Options
  var root = document.body;
  function setPalette(p){ root.setAttribute('data-palette', p); try{localStorage.setItem('foothills_palette', p);}catch(e){} }
  function nextPalette(){ var list = palettes, cur = root.getAttribute('data-palette')||list[0]; setPalette(list[(list.indexOf(cur)+1)%list.length]); }
  try { var saved = localStorage.getItem('foothills_palette'); if (saved && palettes.indexOf(saved) !== -1) setPalette(saved); } catch(e) {}
  document.querySelectorAll('.palette-toggle').forEach(function(b){ b.addEventListener('click', nextPalette); });
  window.foothillsNextPalette = nextPalette; // fallback for inline onclick
})();
```

In `assets/foothills.css`, each palette assigns color tokens which the rest of the theme uses.

# SEO: Canonical, OG/Twitter, JSON‑LD

Tumblr gives you `{MetaDescription}`, `{BlogURL}`, `{Permalink}`, and `{PostTitle}`. Foothills adds:
- Optional overrides: `SEO Title Override`, `SEO Description Override`, `OG Image URL`, `Twitter Username`, `Canonical URL`
- Defaults to Avatar as OG image if no override is provided
- Optional `Enable SEO JSON‑LD` to emit a small Blog schema block

Head excerpt (`theme/foothills.html`):

```html
<!-- Canonical -->
{block:IndexPage}
  {block:IfCanonicalURL}<link rel="canonical" href="{text:Canonical URL}">{/block:IfCanonicalURL}
  {block:IfNotCanonicalURL}<link rel="canonical" href="{BlogURL}">{/block:IfNotCanonicalURL}
{/block:IndexPage}
{block:PermalinkPage}
  <link rel="canonical" href="{Permalink}">
{/block:PermalinkPage}

<!-- Open Graph defaults with user overrides -->
<meta property="og:title" content="{Title}{block:PostTitle} — {PostTitle}{/block:PostTitle}">
{block:IfSEOTitleOverride}<meta property="og:title" content="{text:SEO Title Override}">{/block:IfSEOTitleOverride}
<meta property="og:description" content="{MetaDescription}">
{block:IfSEODescriptionOverride}<meta property="og:description" content="{text:SEO Description Override}">{/block:IfSEODescriptionOverride}
{block:IfOGImageURL}<meta property="og:image" content="{text:OG Image URL}">{/block:IfOGImageURL}
{block:IfNotOGImageURL}<meta property="og:image" content="{PortraitURL-128}">{/block:IfNotOGImageURL}
```

This nets clean link previews without needing custom code per post. Future work: use post‑type fallbacks for `og:image` on photo/video/link permalinks.

# Favicons: Avoid 404s on Custom Domains

On a custom domain, `/favicon/...` won’t exist unless you host it yourself. The fix was to:
- Always include Tumblr’s `{Favicon}` tag for a baseline
- Offer optional Theme Options for apple‑touch‑icon, 32×32, 16×16, and webmanifest URLs
- Wrap them in `{block:If...}` so nothing renders if left blank (no 404s)

```html
<link rel="icon" href="{Favicon}">
{block:IfAppleTouchIconURL}<link rel="apple-touch-icon" sizes="180x180" href="{text:Apple Touch Icon URL}">{/block:IfAppleTouchIconURL}
{block:IfFavicon32URL}<link rel="icon" type="image/png" sizes="32x32" href="{text:Favicon 32 URL}">{/block:IfFavicon32URL}
{block:IfFavicon16URL}<link rel="icon" type="image/png" sizes="16x16" href="{text:Favicon 16 URL}">{/block:IfFavicon16URL}
{block:IfWebmanifestURL}<link rel="manifest" href="{text:Webmanifest URL}">{/block:IfWebmanifestURL}
```

# CDN Realities: Don’t Use raw.githubusercontent.com for CSS

Browsers enforce `X-Content-Type-Options: nosniff`. `raw.githubusercontent.com` serves `text/plain`, so your stylesheet is blocked with a MIME mismatch. Use one of:
- jsDelivr: `https://cdn.jsdelivr.net/gh/OWNER/REPO@main/path/to.css`
- Tumblr Theme Assets: upload and paste the static HTTPS URL
- Your own server/CDN with proper `Content-Type: text/css`

If you use `@main` on jsDelivr, expect caching. Add a `?v=timestamp` cache‑buster or hit the purge endpoint:
`https://purge.jsdelivr.net/gh/OWNER/REPO@main/path/to.css`

For stability (Theme Garden), pin to tags like `@v0.2.1`.

# Reblog/Like Buttons and CSP

Tumblr provides `{LikeButton}` and `{ReblogButton}` as iframes. You can’t style the internals or rely on external scripts due to CSP. Foothills wraps the buttons with styled containers so they look like native controls:

```html
<div class="post-actions">
  {block:ReblogURL}<a class="btn-action" href="{ReblogURL}"><i class="fa-solid fa-retweet"></i></a>{/block:ReblogURL}
  {block:IfNotReblogURL}<span class="reblog-fallback">{ReblogButton color="grey" size="28"}</span>{/block:IfNotReblogURL}
  <span class="like-wrapper"><i class="fa-regular fa-heart"></i>{LikeButton color="grey" size="28"}</span>
</div>
```

Then in `assets/foothills.css`:

```css
.post-actions { display: inline-flex; gap: .5rem; align-items: center; }
.btn-action, .reblog-fallback, .like-wrapper {
  width: 28px; height: 28px; display: inline-grid; place-items: center;
  border: 1px solid var(--border); border-radius: 6px; background: var(--surface);
}
.like-wrapper iframe { opacity: 0; width: 100% !important; height: 100% !important; }
```

# Mobile Drawer: Ergonomics and Scroll Behavior

The drawer merges nav + a curated subset of sidebar content. Subtleties that mattered:
- Use `height: 100dvh` to avoid iOS viewport quirks
- Make the nav area the primary scroll surface and contain overscroll
- Respect safe‑area insets

```css
.drawer { position: fixed; inset: 0; display: grid; place-items: stretch; background: rgba(0,0,0,.35); }
.drawer-inner { position: fixed; top: 0; right: 0; width: min(92vw, 360px); height: 100dvh; padding: .75rem; padding-bottom: max(.75rem, env(safe-area-inset-bottom)); overflow: auto; overscroll-behavior: contain; }
.drawer-nav { flex: 1 1 auto; overflow: auto; }
```

# Notes, Related Posts, and Pinned Posts

Tumblr’s `{PostNotes}` renders server-side HTML. We added horizontal padding and border rhythm so it doesn’t feel cramped.

Related posts use `{block:RelatedPosts}` and show a small plaintext snippet below titles. Each card is centered with a max width for readability.

Pinned posts get a subtle top border and a badge with a Font Awesome pin:

```html
{block:PinnedPost}
  <div class="pinned-badge"><i class="fa-solid fa-map-pin"></i><span>{PinnedPostLabel}</span></div>
{/block:PinnedPost}
```

# Poetry Formatting: Opt‑In and Left‑Aligned

Initially, poems were centered when tagged `#poetry` or `#poem`. We made this fully opt‑in with a Theme Option and left‑aligned by default:

```html
{block:IfEnablePoetrySpecialFormatting}
<script>
  document.addEventListener('DOMContentLoaded', function () {
    document.querySelectorAll('.post').forEach(function (post) {
      var tags = post.querySelector('.post-tags');
      var body = post.querySelector('.post-body');
      if (!tags || !body) return;
      var t = tags.textContent.toLowerCase();
      if (t.includes('#poetry') || t.includes('#poem')) body.classList.add('poetry-formatting');
    });
  });
</script>
{/block:IfEnablePoetrySpecialFormatting}
```

In CSS:

```css
.poetry-formatting { line-height: 2; text-align: left; max-width: 42ch; margin: 0 auto; }
```

# Substack Embed: Be a Good Host

Third‑party embeds frequently assume full widths. The newsletter widget is wrapped in a `.substack-widget` and clamped:

```css
.substack-widget img,
.substack-widget iframe,
.substack-widget .embed-page,
.substack-widget .embed-page-inner,
.substack-widget form,
.substack-widget .container { max-width: 100% !important; width: 100% !important; }
```

# Debugging in Production: What the Console Told Us

On a live custom domain you’ll see noisy console messages:
- CSP report‑only logs about inline or third‑party scripts (Tumblr’s analytics stack)—ignore
- Partitioned cookie logs for Tumblr iframes—also expected
- The real problems were:
  - CSS blocked by MIME type when using `raw.githubusercontent.com`
  - Favicon 404s when `/favicon/...` paths weren’t hosted by the blog

Both issues were fixed by switching CSS hosting and gating favicon link tags behind optional Theme Options.

# Deployment, Caching, and Versioning

Options for CSS delivery:
- jsDelivr `@main` for fast iteration; add `?v=YYYYMMDD` while testing or purge the file
- Pinned tags (e.g., `@v0.2.1`) for stability
- Tumblr Theme Assets for fully controlled caching

I recommend `@main` during development and tags for public releases.

# Accessibility Touches

- Skip link, landmark roles, large hit targets on mobile
- Keyboard‑friendly drawer and search overlay with Escape to close
- Reasonable color contrast and hover/active states

# Lessons Learned

- Tumblr’s theme system remains viable for serious writing blogs if you embrace its constraints
- CSP and iframe buttons mean progressive enhancement—not control of everything
- Host CSS properly; avoid GitHub raw URLs for production assets
- Make SEO configurable but safe by default
- Provide toggles for taste (like poetry formatting) instead of assuming preferences
- Add inline fallbacks for critical UX like the palette so users aren’t blocked by CDN caches

# What’s Next

- Per‑post `og:image` fallbacks that pull first media on permalinks
- Replacing FA CDN icons with inline SVGs for Theme Garden submission
- Localizations for strings in the UI
- Stylelint/Prettier and a formal release workflow (tags + CHANGELOG + GitHub Releases)

If you want to try Foothills, the repository is here:

- GitHub: https://github.com/brennanbrown/foothills

I’d love feedback—especially from folks running Tumblr blogs for lit mags, reading groups, or community projects.
