# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static portfolio website for Ali Ullah (Data Scientist / ML Engineer), hosted on GitHub Pages at Ali623.github.io. No build process — changes to files are deployed by pushing to the `main` branch.

## Development

There are no build tools, package managers, or test suites. To preview locally, open `index.html` directly in a browser or use a simple static file server:

```bash
# Python
python -m http.server 8000

# Node (if available)
npx serve .
```

Deployment is automatic via GitHub Pages on push to `main`.

## Architecture

Single-page application — all portfolio content lives in `index.html` (~840 lines). The page is divided into named sections: `#header`, `#about`, `#work`, `#education`, `#portfolio`, `#contact`.

**CSS load order matters** (defined in `<head>`):
1. `lib/bootstrap/` — Bootstrap grid and utilities
2. Third-party plugin CSS (`owl-carousel`, `magnific-popup`, `hover`, `ionicons`)
3. `css/style.css` — primary custom styles (color scheme, typography, layout)
4. `css/responsive.css` — responsive breakpoints and mobile overrides
5. `css/blog.css` — blog-specific styles (currently minimal)

**JS load order matters** (defined at bottom of `<body>`):
1. `lib/jquery/jquery.min.js` + `jquery-migrate.min.js`
2. `lib/bootstrap/js/bootstrap.bundle.min.js`
3. Third-party plugins: `typed.js`, `owl-carousel`, `magnific-popup`, `isotope`
4. `js/main.js` — custom initialization and event handlers

All third-party libraries are vendored under `lib/` — no CDN dependencies for JS (Google Fonts and Font Awesome are CDN-loaded in `<head>`).

## Key Customization Points

**Content** lives entirely in `index.html`:
- Hero typing animation strings → `js/main.js` `typed` options (`strings` array)
- Work experience slides → `.work-slide` elements inside `#work` section
- Portfolio projects → `.portfolio-item` elements inside `#portfolio`; each has `data-filter` attribute (`data-science` or `machine-learning`) used by Isotope for filtering
- Profile photo → `images/me.png`; hero background → `images/home-bg.png`
- Company logos → `images/work/`; project screenshots/GIFs → `images/portfolio/`
- Resume PDF → `documents/Aliullah-resume-heds00.pdf`

**Color scheme** is defined via CSS variables / repeated values in `css/style.css`:
- Navy: `#112A46`
- Gold/Tan: `#b8a07e`

**Fonts** — Poppins (body) and Playfair Display (headings) loaded via Google Fonts in `<head>`.

## Branch Strategy

- `main` — production branch served by GitHub Pages
- `refacter_UI` — current active development branch; open PRs against `main`
