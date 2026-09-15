# christiancollet.github.io

Personal-professional academic website. **al-folio** Jekyll theme, deployed via
GitHub Pages.

## Scope

In scope: site structure and content, publications, CV, teaching pages, theme
customisation, deployment.

Out of scope: research and course development. This repo publishes finished
outputs — a bib entry, a deck, a paper — and is not where that work happens.

## Where things live

- `_config.yml` — site config; the Jekyll Scholar block controls publication sorting
- `_pages/about.md` — landing page; the `profile` block in its front matter
  controls the sidebar
- `_bibliography/papers.bib` — the publications page is generated from this
- `_data/cv.yml` — CV content (fallback when no JSON resume is configured)
- `_data/coauthors.yml` — coauthor metadata, auto-links names
- `_news/`, `_projects/` — default collections; news appears on the home page,
  projects render as a grid
- New collections are declared in `_config.yml` with a matching folder and a
  landing page in `_pages/`
- `assets/pdf/` — papers, slides, posters
- `assets/img/prof_pic.jpg` — profile image

Local preview: `docker compose up`, then http://localhost:8080.
Changes to `_config.yml` need a full restart; everything else rebuilds on save.

## Conventions

### Hosting

Stay on `github.io`. No custom domain.

### BibTeX

`papers.bib` follows the JPOP BibTeX Normalization Standard, so entries move
between the site and the lit archive without reformatting.

al-folio supports these entry fields: `abstract`, `arxiv`, `bibtex_show`, `code`,
`doi`, `html`, `pdf`, `poster`, `slides`, `supp`, `video`, `website`.

### Language — selective Japanese

English is the default throughout. Japanese appears where it carries information
English can't: source titles, institution and publication names, survey
instrument wording, and terms whose English rendering is a translation rather
than a name.

Body text: paired on first mention — `Yomiuri Nenkan (読売年鑑)` — bare or
English-only thereafter within the same page.

Bibliography: follows the JPOP standard's title conventions, not this rule.

No language switcher, no parallel page tree.

### Look and feel

"Ink": accent `$ink-blue` (`#2c5282` light, `#7ba7d4` dark), Inter throughout,
light-grey footer instead of the stock near-black band. Palette variables live in
`_sass/_variables.scss`; the font stack is `$ink-font-stack` in `_sass/_base.scss`.
Any colour change must be made in BOTH the light and dark blocks of
`_sass/_themes.scss` — the theme has a working dark mode.

### Project instructions

This file lives in the repo, not in claude.ai project storage. It loads
automatically with the folder, carries override authority as project
instructions, and versions alongside the site. Project storage is for session
handoffs and drafts, not for these rules.

### Contact

`collet@icu.ac.jp` is published in the site footer via `_data/socials.yml`.

### Teaching materials

Courses are a collection: one page per course, with a landing page listing them.
Declared in `_config.yml` with a matching folder and a landing page in `_pages/`.

### File destinations

- Default to this repo for anything that becomes part of the built site: pages,
  posts, collection entries, `_data` files, bib entries, publish-ready assets.
- Default to `~/Projects/WIP/website/` for raw or unfinished source material: drafts, PDFs
  awaiting cleanup, unprocessed images, notes. That folder is Syncthing-synced;
  this repo is not, and must never be moved into it.
- **Ask first** when the destination is genuinely ambiguous, when a file would
  create a new directory in this repo, or when introducing an asset type the site
  doesn't already use.

## Working rules

- **Never commit or push without asking.** Show the diff and wait.
- Don't make design changes I didn't ask for while doing something else.
- Prefer proposing options over rewriting.
- Never write into `.git/`.
- **Grep before deleting any stock theme file.** al-folio pages reference one
  another — a page you delete may be included by a layout. Check
  `grep -rn "<filename>" _pages/ _layouts/ _includes/ _config.yml` first.
- This repo is public. Nothing private goes in this file — that belongs in
  `CLAUDE.local.md`, which is gitignored.

## Session protocol

Sessions are numbered `s1`, `s2`, … Branch sessions are `s1b1`; checkpoints are
`c1`, `c2`.

At the end of every session: update `site_state.md`, write the next session's
handoff into `~/Projects/WIP/website/s<N+1>/`, and add a one-line entry to the
session log below. Update THIS file only when a convention actually changes, and
show me the diff.

## Working notes

State, the phase plan and per-session handoffs live outside this repo, in
`~/Projects/WIP/website/`:

- `site_state.md` — what is done, what is still stock, current open items
- `build_plan.md` — the phased plan and its open questions
- `s<N>/` — per-session summaries and handoffs

Connect that folder at the start of a session and read `site_state.md` first.
Keep this file generic: scope, conventions and working rules only.

## Session log

- s1 — 2026-09-10 to 09-15 — Identity and landing page, "Ink" theme, first six
  publications, template cleanup, CV page removed in favour of external profile
  links.
