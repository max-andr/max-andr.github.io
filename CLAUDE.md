# CLAUDE.md

## Project Overview

Personal academic website for Maksym Andriushchenko, built on the **al-folio** Jekyll theme.
- **Live site**: https://www.andriushchenko.me
- **Theme**: [al-folio](https://github.com/alshedivat/al-folio)

## Build & Serve

```bash
# Install dependencies
bundle install

# Local development server (http://localhost:4000)
bundle exec jekyll serve

# Production build
JEKYLL_ENV=production bundle exec jekyll build

# Docker alternative
docker compose up
```

**Requirements**: Ruby 3.0.2, Bundler, ImageMagick (for responsive images)

## Deployment

- **Source branch**: `master`
- **Deploy branch**: `gh-pages` (auto-built static site)
- Push to `master` triggers GitHub Actions → runs `bin/deploy` → force-pushes built site to `gh-pages`
- Manual deploy: `bin/deploy`

## Key Directory Structure

```
_bibliography/    # BibTeX files (papers.bib) — publications data
_data/            # YAML data: coauthors.yml, cv.yml, repositories.yml, venues.yml
_includes/        # Reusable HTML partials (header, footer, figure, news, etc.)
_layouts/         # Page templates (about, page, post, distill, bib, cv)
_news/            # News/announcement markdown items
_pages/           # Main content pages (about.md = homepage, publications.md)
_posts/           # Blog posts (YYYY-MM-DD-slug.md)
_projects/        # Project items (numbered: 1_project.md, 2_project.md)
_plugins/         # Custom Jekyll plugins (external-posts.rb, hideCustomBibtex.rb)
_sass/            # SCSS stylesheets (_base, _layout, _themes, _variables)
assets/img/       # Images and PDFs
assets/css/       # Compiled CSS (main.css)
assets/js/        # JavaScript files
bin/              # Build/deploy scripts
```

## Content Conventions

### Pages (`_pages/`)
Front matter must include `layout`, `permalink`. Add `nav: true` and `nav_order: N` to show in navbar.

### About page (`_pages/about.md`)
Homepage. Uses `layout: about`, `permalink: /`. Profile image, news, selected papers, and social toggles in front matter.

### News (`_news/`)
Short announcements. Use `inline: true` for compact display. Format: `layout: post`, `date: YYYY-MM-DD`.

### Projects (`_projects/`)
Numbered files for ordering. Front matter: `title`, `description`, `img`, `importance`, `category`.

### Blog Posts (`_posts/`)
Standard Jekyll naming: `YYYY-MM-DD-slug.md`. Layouts: `post` or `distill`.

### Publications (`_bibliography/papers.bib`)
BibTeX entries with custom fields: `abbr`, `abstract`, `arxiv`, `html`, `pdf`, `code`, `poster`, `slides`, `blog`, `website`, `preview`, `selected`, `bibtex_show`, `supp`.
- Co-authors linked via `_data/coauthors.yml`
- Venue abbreviations in `_data/venues.yml`
- Style: APA, processed by jekyll-scholar

## Configuration

Main config: `_config.yml`. Key settings:
- `max_width: 800px` — content container width
- `navbar_fixed: true`, `footer_fixed: true`
- Feature toggles: `enable_math`, `enable_masonry`, `enable_medium_zoom`, `enable_darkmode` (off), etc.
- Library versions with SRI hashes defined at bottom of config

## Tech Stack

- Jekyll 4.2.2, Ruby, kramdown (GFM)
- Bootstrap 4.6.1, jQuery 3.6.0, MathJax 3.2.0
- Rouge syntax highlighting (light: github, dark: native)
- jekyll-scholar for bibliography, jekyll-imagemagick for responsive images
