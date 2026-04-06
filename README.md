# alex-blog

Personal site and blog built with **[Hugo](https://gohugo.io/)** (no third-party theme). Layout and typography take inspiration from [Gregory Gundersen’s site](https://gregorygundersen.com/): narrow measure, simple nav, understated links. The site splits **technical writing** (**Blog**) from lighter **Personal** notes, each with its own taxonomy and topic navigation.

Live configuration uses **Libre Franklin** by default (a classic, readable sans). Other presets are available via `hugo.toml` (see below).

---

## Requirements

- **Hugo** `0.120+` (tested on `0.160.x`). [Install Hugo](https://gohugo.io/installation/).

---

## Quick start

```bash
git clone https://github.com/alexwangjiaqi/alex-blog.git
cd alex-blog
hugo server
```

Open the URL Hugo prints (usually `http://localhost:1313/`).

**Production build** (writes to `public/`):

```bash
hugo --minify
```

Before deploying, set **`baseURL`** in `hugo.toml` to your real domain (or hosting URL).

---

## Repository layout

| Path | Purpose |
|------|--------|
| **`hugo.toml`** | Site title, `baseURL`, taxonomies, permalinks, math (KaTeX), Goldmark (`unsafe` HTML, math passthrough), nav tag lists, **font preset** (`params.site_font`). |
| **`content/`** | All Markdown pages and posts. |
| **`layouts/`** | HTML templates: base layout, section lists, tag pages, partials (head, nav, math, intros). |
| **`static/`** | Static assets copied verbatim; site CSS lives in `static/css/blog.css`. |
| **`data/site_fonts.yaml`** | Google Fonts URLs and family names for each `site_font` key. |
| **`archetypes/`** | Front-matter templates for `hugo new`. |
| **`.gitignore`** | Ignores `public/`, `resources/`, `.hugo_build.lock` (build output stays local). |

### `content/` in more detail

```
content/
├── _index.md           # Home page front matter (body optional; home layout is custom)
├── about-me.md         # About page → /about-me/
├── blog/
│   ├── _index.md       # Blog section landing
│   └── *.md            # Posts → /blog/YYYY/MM/DD/slug/
└── personal/
    ├── _index.md       # Personal section landing
    └── *.md            # Posts → /personal/YYYY/MM/DD/slug/
```

- **Blog** posts use taxonomy **`tags`** (URLs under `/tags/...`).
- **Personal** posts use **`personal_tags`** (URLs under `/personal/topic/.../`).

---

## Adding a Blog post

1. Create a file under **`content/blog/`** (or use the archetype):

   ```bash
   hugo new content blog/my-post-title.md
   ```

2. Edit front matter. Important fields:

   - **`title`**, **`date`**, **`draft`** (`false` when ready to publish).
   - **`subtitle`** (optional) — shown under the title.
   - **`tags`** — list of strings; should match labels you want under **Blog** topic navigation.

   Topic bars on list/tag pages are driven by **`params.tag_nav`** in `hugo.toml`. Use those exact strings (or update `hugo.toml` when you introduce new topics).

3. Write the body in **Markdown**. **Math**: KaTeX is enabled; use `$...$` / `$$...$$` (see `hugo.toml` `passthrough` delimiters).

Example (minimal):

```yaml
---
title: My note
date: 2026-04-10
draft: false
subtitle: Optional line under the title
tags:
  - Machine Learning
  - Misc
---

Your **markdown** here.
```

**Permalink pattern** (from `hugo.toml`): `/blog/:year/:month/:day/:slug/`.

---

## Adding a Personal post

1. Create Markdown under **`content/personal/`**:

   ```bash
   hugo new content personal/my-note.md
   ```

2. Use **`personal_tags`** (not `tags`):

   ```yaml
   ---
   title: Saturday sketch
   date: 2026-04-10
   draft: false
   subtitle: Optional
   personal_tags:
     - Travel
     - Notes
   ---
   ```

   Align tag names with **`params.personal_tag_nav`** in `hugo.toml` for the Personal topic bar.

**Permalink pattern**: `/personal/:year/:month/:day/:slug/`.

---

## About page

- File: **`content/about-me.md`**
- Rendered with **`layouts/_default/about.html`** (About layout, no “post” chrome if configured that way).

---

## Customisation

### Fonts

1. Set **`site_font`** in `hugo.toml` under `[params]` to a key defined in **`data/site_fonts.yaml`** (e.g. `libre-franklin`, `public-sans`, `source-sans-3`).
2. To add a new face, append an entry in **`site_fonts.yaml`** (`family` + Google Fonts `href`), then reference its key in `hugo.toml`.

The active family is injected as **`--font-sans-primary`** in **`layouts/partials/site-font.html`**; **`static/css/blog.css`** uses it on `html`.

### Topic navigation (Blog / Personal)

- **Blog** topics: `[params.tag_nav]` in `hugo.toml`.
- **Personal** topics: `[params.personal_tag_nav]`.

These control the nav bars on section and listing pages; your post `tags` / `personal_tags` should stay consistent with those labels (or extend the lists).

### Style

- Global rules: **`static/css/blog.css`**.

---

## Features (summary)

- **KaTeX** for math (`layouts/partials/math.html`, CSS from CDN in head).
- **Chroma**-friendly code blocks (if you enable highlighting in `hugo.toml` later).
- **RSS** is disabled (`disableKinds = ['RSS']` in `hugo.toml`); remove or adjust if you want a feed.

---

## License

Site content and templates are yours to license as you prefer. Hugo and third-party assets (e.g. fonts, KaTeX) follow their respective licenses.
