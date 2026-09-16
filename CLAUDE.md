# RapidBio Systems — marketing/investor site

Static marketing site for RapidBio Systems, Inc. (handheld bacterial
pathogen detection for food safety). No build step, no framework,
no backend — plain HTML/CSS/JS deployed as-is.

## Stack & structure

- 4 pages: `index.html`, `technology.html`, `team.html`, `contact.html`
- `css/styles.css` — single stylesheet, no preprocessor
- `js/nav.js` — mobile nav toggle only
- `assets/` — images/logos. `assets/*.pdf` is gitignored on purpose:
  source slide exports with "Confidential" footers get kept locally
  for extracting artwork but must never be committed, since the whole
  repo is served publicly (see `.gitignore` comment).
- `fonts/` — self-hosted Inter woff2
- No `package.json`, no bundler, no test suite, no README.

## Deployment

Hosted on **GitHub Pages**, legacy build (no Actions workflow),
serving directly from the `main` branch root. Live at
**https://hweikel.github.io/rapidbio/**. `.nojekyll` is present so
Pages skips Jekyll processing. Pushing to `main` deploys immediately
— there is no staging/preview step.

## Running locally

No build needed. From the repo root:
```
python3 -m http.server 8000
```
then open `http://localhost:8000/index.html`.

## Known outstanding work

- **Contact form is not wired up yet.** `contact.html` posts to
  Formspree (`action="https://formspree.io/f/FORMSPREE_ENDPOINT"`),
  but `FORMSPREE_ENDPOINT` is a literal placeholder, not a real form
  ID. The inline script in `contact.html` detects this
  (`form.action.indexOf("FORMSPREE_ENDPOINT") === -1`) and shows an
  error telling visitors to email John directly instead of POSTing.
  To finish this: create a form at formspree.io, swap the placeholder
  for the real endpoint (`https://formspree.io/f/xxxxxxxx`), and
  verify a real submission arrives before removing this note.
- No analytics/tracking is wired up anywhere on the site.
- No custom domain (`CNAME`) is configured — site lives at the
  `github.io` subpath, not `rapidbiosystems.com` or similar.

## Conventions seen in the code

- Every page repeats the same header/footer markup by hand (no
  templating) — if you edit nav or footer, update all four HTML
  files identically.
- CTAs consistently point to `contact.html` ("Request the Investor
  Deck").
- Copy changes have historically been done as direct commits to
  `main` (see `git log`) — no branch/PR workflow in use so far.
