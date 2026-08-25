# InnovateSim Technologies Inc. — Website

A single-page static website for InnovateSim Technologies Inc. (healthcare simulation
products and simulation facility consultancy). No build step, no framework, no backend —
plain HTML/CSS/JavaScript in one file (`index.html`).

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

Because this is a static file with no `package.json`, Vercel serves it directly —
there is nothing to install and nothing to build.

## Environment variables / API configuration

None are required. There is no backend and no third-party API key used anywhere in
this project:

- The **contact form / chatbot** uses a `mailto:` link and a small rule-based
  (keyword-matching) script — no AI API, no server.
- The **WhatsApp link** is a plain `wa.me` link — no API key needed.
- Google Fonts is loaded from its public CDN (`fonts.googleapis.com`) — no key required.

## Important: how "Add Product" actually works

The **Add Product** feature in the Products section is client-side only:

- Products you add are saved in **your own browser's local storage**, protected by a
  password check that also runs entirely in the browser (`Sim@123` — change it in the
  `PRODUCT_PASSWORD` constant near the bottom of `index.html`).
- This means: products you add are only visible **on the device/browser you added
  them from** — they are **not** saved to a shared database, so other visitors to the
  live site will not see products you've added, and the password is a soft deterrent
  (visible in page source), not real authentication.
- If you need products to be added once and shown to every visitor, that requires a
  real backend (a small database + an API route) — for example Vercel's own
  Serverless/Edge Functions with a database like Vercel Postgres, Supabase, or
  similar. That's a larger change than this static file can do on its own; let me
  know if you'd like that built.

## What was checked for this production review

- ✅ HTML structure: all tags balanced, no duplicate element IDs.
- ✅ All internal nav links (`#products`, `#consultancy`, `#about`, `#why`, `#contact`)
  resolve to a matching section — no broken anchors.
- ✅ No external dependencies beyond the Google Fonts stylesheet (no npm packages,
  no build tooling, nothing that can go out of date or fail to install).
- ✅ No API keys or secrets anywhere in the code — nothing to configure as an
  environment variable.
- 🔧 **Fixed:** the mobile navigation menu (under ~900px width) had no way to open —
  the nav links were hidden by CSS with no working hamburger button. Added a
  functional mobile menu (tap the ☰ icon, links close the menu after navigating).
- 🔧 **Fixed:** added a favicon (inline SVG, no extra file/request needed) and
  meta description / Open Graph tags for link previews and SEO.
- ✅ Re-tested: add product (with and without photo), password-protected product
  removal, chatbot quick replies and free-text, mobile menu, desktop nav — all pass
  with zero JavaScript console errors.

## Files

```
index.html     the entire site
vercel.json    security headers + clean URLs (optional but included)
.gitignore     standard ignores
README.md      this file
```
