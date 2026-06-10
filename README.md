# Jason Cook Design — Portfolio Site

Source code for [jasoncookdesign.com](https://jasoncookdesign.com), the professional portfolio and consulting brand website for Jason Cook Design. Deployed via GitHub Pages from the `main` branch of this repository.

## About the Site

Jason Cook Design is an Austin-based consultancy offering experience design, UX/UI, software architecture, business strategy, and interface engineering. This site serves as the primary inbound channel for consulting engagements.

## Tech Stack

- **Static HTML5** — no build step, no framework, no CMS
- **Bootstrap** (bundled locally) — responsive grid and components
- **jQuery + plugins** — Owl Carousel, Magnific Popup
- **Font Awesome + Themify Icons** — icon sets (bundled locally)
- **Custom CSS** — `assets/css/app.css`
- **Google Analytics (GA4)** — tag `G-2ECQP0N7FX`

## Structure

```
index.html                  Homepage (hero, services, work, pricing, contact)
cs01.html                   Case study: OSIsoft Enterprise UI Framework
cs02.html                   Case study: Ford Build and Price
cs03.html                   Case study: Qu POS
cs04.html                   Case study: Banco Azteca Network Operations Center
cs05.html                   Case study: Millennium Meevo
cs06.html                   Case study: Microsoft Surface
cs07.html                   Case study: Leading Hotels of the World
cs08.html                   Case study: Dell Unified Contact Us Experience
resume.pdf                  General resume
resume_designproduction.pdf Design production resume
404.html                    Custom 404 page
CNAME                       GitHub Pages custom domain config
assets/                     CSS, JS, images, bundled plugin assets
calendar/                   Scheduling/calendar page
archive/                    Legacy assets (not linked from live site)
```

## Development

There is no build process. Edit HTML files directly.

All dependencies are bundled under `assets/plugins/` — no npm, no package manager.

To preview locally, open any `.html` file in a browser or serve the directory:

```bash
python3 -m http.server 8000
```

## Deployment

This repo is deployed via **GitHub Pages**. Merging to `main` on the canonical repo (`jasoncookdesign/jasoncookdesign.github.io`) publishes immediately to [jasoncookdesign.com](https://jasoncookdesign.com).

**Contribution model:** Submit PRs from the `jcduser01` fork to the canonical `jasoncookdesign` upstream. Do not push directly to canonical `main`.

## Adding a Case Study

1. Duplicate an existing `csNN.html` (e.g., `cp cs08.html cs09.html`)
2. Update the title, meta description, and all content sections in the new file
3. Add a card/link to the work grid in `index.html`
4. Open a PR from the `jcduser01` fork
