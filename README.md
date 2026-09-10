# InnovateSim Technologies Inc. — Website

A static website for InnovateSim Technologies Inc. (healthcare simulation
products and simulation facility consultancy). No build step, no framework,
no backend — plain HTML/CSS/JavaScript in a single file (`index.html`),
including the logo, which is embedded directly in the page.

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

## Editing content

All content (hero text, products, consultancy list, why-us items, about
section, contact details) is plain static HTML directly inside `index.html`.
To update anything, open the file, find the relevant text, and edit it
directly — then redeploy (push to GitHub if using the Vercel Git
integration, or re-upload the file).

There is no external content source (like a spreadsheet or CMS) connected to
this site — everything lives in the one file.

## Environment variables / API configuration

None are required. There is no backend and no third-party API key used anywhere in
this project:

- The **chatbot** in the Contact section is a small rule-based (keyword-matching)
  script with fixed responses — no AI API, no server.
- The **WhatsApp link** is a plain `wa.me` link — no API key needed.
- Google Fonts is loaded from its public CDN (`fonts.googleapis.com`) — no key required.

## Logo

The logo is embedded directly in `index.html` (as a base64-encoded image), so
it displays correctly no matter how the file is opened, previewed, or
shared — there's no separate image file that can go missing. It appears in
three places:

- Header (next to the "InnovateSim" wordmark and tagline)
- Footer, inside a small light badge so it stays visible against the dark
  footer background
- Browser tab favicon

To replace it with a different logo later, you'll need to re-encode a new
image to base64 and swap the `data:image/png;base64,...` value in the
`<img class="logo-mark" ...>` tags (header and footer) and the favicon
`<link>` tag.

## Files

```
index.html       the entire site (including the logo, embedded as base64)
vercel.json      explicit build/output config + security headers
.gitignore       standard ignores
README.md        this file
DEPLOYMENT.md    detailed Vercel deployment spec (framework/build/env answers)
```
