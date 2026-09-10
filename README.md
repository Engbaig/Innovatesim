# InnovateSim Technologies Inc. — Website

A static website for InnovateSim Technologies Inc. (healthcare simulation
products and simulation facility consultancy). No build step, no framework,
no backend — plain HTML/CSS/JavaScript in a single file (`index.html`),
including the logo, which is drawn as inline SVG.

## Deploy to GitHub

```bash
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

## Deploy to Vercel

1. Go to https://vercel.com/new and import the GitHub repo.
2. Framework preset: choose **Other** (or leave auto-detected — there is no build step).
3. Build command: none / leave blank. Output directory: `.` (root).
4. Click **Deploy**. No environment variables are required (see below).

Because this is a static site with no `package.json`, Vercel serves it
directly — there is nothing to install and nothing to build. `vercel.json`
already sets `framework: null`, `buildCommand: null`, and
`outputDirectory: "."` explicitly so Vercel won't try to guess.

## Managing website content

This site pulls its content (hero text, products, consultancy list, why-us
items, about section, contact details) from a connected Google Sheet, so you
can update the live site without touching code. See **CONTENT-MANAGEMENT.md**
for the full setup guide and required tab structure.

There's also a private, hidden shortcut to jump straight to that sheet: visit
your live site with `#admin` at the end of the URL once (e.g.
`yoursite.com/#admin`) and a small panel appears in the corner showing live
sheet-sync status plus a "Manage Website Content" link straight to the sheet.
It's remembered on that browser until you dismiss it — regular visitors never
see it.

## Environment variables / API configuration

None are required. There is no backend and no third-party API key used anywhere in
this project:

- The **chatbot** in the Contact section is a small rule-based (keyword-matching)
  script that reads live from the page's own content — no AI API, no server.
- The **WhatsApp link** is a plain `wa.me` link — no API key needed.
- Google Fonts is loaded from its public CDN (`fonts.googleapis.com`) — no key required.
- The **Google Sheets content sync** uses a public, unauthenticated read
  endpoint (Google's `gviz` query interface) — no API key, no OAuth, nothing
  to configure as a secret. See CONTENT-MANAGEMENT.md for the one sharing
  setting it does require on the sheet itself.

## Important: how content sync actually works

The site's content (products, consultancy, why-us, about, hero text, contact
details) is read live from a Google Sheet by each visitor's browser on page
load — see CONTENT-MANAGEMENT.md for the full setup. Key things to know:

- This is **read-only from the website's side** — editing the sheet updates
  the site; editing the site's code does not update the sheet.
- It requires the sheet to be shared as "Anyone with the link — Viewer" (view
  access only — editing still requires your Google login).
- If the sheet is unreachable, misconfigured, or a tab is missing, that
  section simply falls back to its built-in default content — nothing on the
  site breaks.
- The hidden `#admin` panel shows live, per-tab sync status so you never have
  to guess whether it's working.

## Logo

The logo is drawn entirely in code (inline SVG) — a stylized "i" figure
merging into a swirling "S" with a heartbeat line through it, in the site's
orange-to-charcoal palette. It's fully self-contained inside `index.html`:
no external image files, so it can never fail to load or go missing
regardless of how or where the file is opened. Used in three places:

- Header (next to the "InnovateSim" wordmark)
- Footer, inside a small light badge (`logo-mark-badge`) so it stays visible
  against the dark footer background
- Browser tab favicon (embedded as an SVG data URI, same design)

To change it later, edit the SVG markup directly in `index.html` (search for
`logoGradHeader` and `logoGradFooter`), or replace it with a different design
entirely.

## Files

```
index.html       the entire site (including the logo, drawn in SVG)
vercel.json      explicit build/output config + security headers
.gitignore       standard ignores
README.md        this file
DEPLOYMENT.md    detailed Vercel deployment spec (framework/build/env answers)
CONTENT-MANAGEMENT.md   Google Sheet setup guide for content sync
```
