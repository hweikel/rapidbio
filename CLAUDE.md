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

Hosted on **Netlify** (free tier), deployed from the `main` branch
root via `netlify.toml` (`publish = "."`, no build command — this is
still a plain static site, no bundler). Pushing to `main` deploys
immediately — there is no staging/preview step, though Netlify does
generate deploy previews for PRs if/when a PR workflow is adopted.
`.nojekyll` is a holdover from the prior GitHub Pages host and is
harmless to leave in place.

The site previously lived on GitHub Pages at
`https://hweikel.github.io/rapidbio/`; that is no longer the
canonical deploy.

## Running locally

No build needed. From the repo root:
```
python3 -m http.server 8000
```
then open `http://localhost:8000/index.html`.

## Known outstanding work

- **Contact form uses Netlify Forms.** `contact.html` has
  `data-netlify="true"` plus a hidden `form-name` field, and submits
  via `fetch` to `/` with a Netlify-detected honeypot (`_gotcha`
  field, `netlify-honeypot="_gotcha"`). Netlify detects the form by
  parsing the static HTML at deploy time — no backend/build step
  needed. After the first deploy, go to Site configuration → Forms in
  the Netlify dashboard and add a notification (email-to, Slack,
  etc.) so submissions actually reach someone — by default Netlify
  just stores them silently. Verify a real test submission shows up
  before considering this done.
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
