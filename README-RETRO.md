
# Retro Pro Theme Pack (minima override)

This pack makes your GitHub Pages Jekyll (minima) blog look professional with a clean, retro-futuristic style.

## How to install (drop-in)

1. Copy the contents of this zip into your repo, keeping the same folders:
   - `_includes/head-custom.html`
   - `assets/css/style.scss`
   - `index.html` (replaces your index.md to add a hero + post grid)
   - `archive.md`
   - `assets/img/og-image.png`
   - `assets/favicon.svg`

2. In `_config.yml`, confirm these settings (add if missing):
```yml
title: Levelyn
description: Music • Growth • Tech
url: "https://levelyn.blog"
baseurl: ""

theme: minima
plugins:
  - jekyll-feed
  - jekyll-seo-tag
  - jekyll-paginate

paginate: 10
paginate_path: "/page:num/"

minima:
  social_links:
    - platform: github
      user_url: https://github.com/<your-username>
    - platform: linkedin
      user_url: https://www.linkedin.com/in/<your-handle>/
    - platform: x
      user_url: https://x.com/<your-handle>
```

3. Commit & push. In 1–2 minutes, refresh your site.

## Notes
- The theme uses Google Fonts **Syne** (headings) and **IBM Plex Mono** (code).
- `index.html` adds a hero section and a responsive post grid.
- `archive.md` lists posts grouped by year.
- The OG/Twitter preview image is in `assets/img/og-image.png`.
