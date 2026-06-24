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
- **Blog** — Markdown posts rendered to committed static HTML by a small generator (no CMS, no build server, no CI); see [Writing (Blog)](#writing-blog)

## Structure

```
index.html                  Homepage (hero, services, work, pricing, calendar, contact)
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
calendar/                   Legacy-compat redirects → Cal.com (see Scheduling)
archive/                    Legacy assets (not linked from live site)
blog/                       GENERATED blog — listing, per-post pages, RSS (do not hand-edit)
content/blog/               Blog post sources (Markdown + YAML frontmatter)
templates/blog/             Blog templates (post.html, index.html)
blog.config.json            Blog generator config (paths + site metadata)
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

## Scheduling (Cal.com)

Booking is handled by [Cal.com](https://cal.com) on the shared `jasoncookdesign` account ([cal.com/jasoncookdesign](https://cal.com/jasoncookdesign)). This replaces the previous Google Appointments redirect pages.

The homepage carries an always-visible inline Cal.com **profile** embed (all event types) in the `#calendar` section, between `#pricing` and the FAQ. It uses the official `embed.js` snippet with `calLink: "jasoncookdesign"` and `layout: "month_view"`. The section is anchor-reachable at [jasoncookdesign.com/#calendar](https://jasoncookdesign.com/#calendar) — there is no nav entry.

The six live event types are: `meeting` (15m / 30m / 60m), `coffee` (30m), `breakfast` (60m), `lunch` (60m), `dinner` (90m), and `studio` (120m / 180m / 240m). The `studio` event is shared with dysonhope.com.

### Legacy `/calendar/` redirects

The old `/calendar/` pages are retained only as legacy-compatibility redirects (`<meta http-equiv="refresh" content="0; ...">` plus a `window.location.replace()` JS fallback). The hub returns visitors to the on-site embed; per-type routes go straight to their specific Cal.com event to preserve booking intent from bookmarked or shared links. No Google Appointments URLs remain.

| Page | Redirect target |
|---|---|
| `calendar/index.html` | `/#calendar` |
| `calendar/30min/index.html` | `https://cal.com/jasoncookdesign/meeting` |
| `calendar/60min/index.html` | `https://cal.com/jasoncookdesign/meeting` |
| `calendar/coffee/index.html` | `https://cal.com/jasoncookdesign/coffee` |
| `calendar/breakfast/index.html` | `https://cal.com/jasoncookdesign/breakfast` |
| `calendar/lunch/index.html` | `https://cal.com/jasoncookdesign/lunch` |
| `calendar/dinner/index.html` | `https://cal.com/jasoncookdesign/dinner` |
| `calendar/studio/index.html` | `https://cal.com/jasoncookdesign/studio` |

## Adding a Case Study

1. Duplicate an existing `csNN.html` (e.g., `cp cs08.html cs09.html`)
2. Update the title, meta description, and all content sections in the new file
3. Add a card/link to the work grid in `index.html`
4. Open a PR from the `jcduser01` fork

## Writing (Blog)

The `/blog/` section is long-form writing on design, technology, and AI, reachable from the **Writing** link in the main navigation. It keeps the site's "commit static HTML, no server" model: posts are authored in Markdown and rendered to static HTML by a small generator, and the **rendered HTML is committed** — there is no CMS, build server, or CI.

### How it fits together

```
content/blog/<YYYY-MM-DD-slug>.md   Post source (Markdown + YAML frontmatter)
templates/blog/post.html            Per-post template (site chrome + typography)
templates/blog/index.html           Listing template; the card between
                                     <!-- BEGIN POST_CARD --> / <!-- END POST_CARD -->
                                     repeats once per published post
blog/index.html                     GENERATED listing
blog/<slug>/index.html              GENERATED post page
blog/feed.xml                       GENERATED RSS feed
blog.config.json                    Generator config (source/template/output paths + site metadata)
```

The `blog/` directory is generated output — do not hand-edit it. Edit the Markdown source or the templates, then regenerate.

### Post frontmatter

```yaml
title:         "Required — post title"
date:          2026-06-23          # required; ISO date; drives ordering + RSS
slug:          optional            # derived from the title if omitted
tags:          [design, ai]        # optional
excerpt:       "One-line summary"  # listing + meta description + og:description; auto-derived if omitted
draft:         false               # true = the post is skipped by the generator
cover_image:   assets/blog/x.jpg   # optional; used for the social/og:image
canonical_url: optional            # optional; set when the post is also published elsewhere
```

### Publishing a post

1. Add `content/blog/<YYYY-MM-DD-slug>.md` with frontmatter and a Markdown body.
2. Regenerate with the blog generator (Python; requires the `markdown` and `pyyaml` packages), pointing it at `blog.config.json`. It renders every non-draft post and (re)writes the `blog/` directory deterministically.
3. Commit the new Markdown **and** the regenerated `blog/` files, then open a PR from the `jcduser01` fork. Merging to canonical `main` publishes to [jasoncookdesign.com/blog/](https://jasoncookdesign.com/blog/).

### Local preview

Blog asset links are root-relative (`/assets/...`), so preview by serving the **repo root** and visiting `/blog/`:

```bash
python3 -m http.server 8000   # then open http://localhost:8000/blog/
```
