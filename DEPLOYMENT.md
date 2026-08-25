# Vercel Deployment Specification

## Framework
**None.** This is a plain static HTML/CSS/JavaScript site — one file (`index.html`),
no React/Next.js/Vite/etc. In Vercel's project settings, set:
- **Framework Preset: Other**

`vercel.json` in this repo also sets `"framework": null` explicitly, so Vercel will
not attempt to auto-detect a framework.

## Build command
**None.** There is nothing to compile or bundle.
- **Build Command:** leave blank (or `vercel.json`'s `"buildCommand": null` covers it)

## Output directory
**Project root (`.`).** `index.html` is served as-is from the root of the repo.
- **Output Directory:** `.` (already set in `vercel.json`)

## Install command
**None.** There is no `package.json`, no `node_modules`, nothing to install.
- **Install Command:** leave blank (`vercel.json`'s `"installCommand": null` covers it)

## Node.js requirements
**None at build/runtime.** Because there is no build step and no serverless
functions in this project, Vercel does not need to run Node.js to serve this
site at all — it's pure static file hosting. You can leave the Node.js Version
setting at its default in the Vercel dashboard; it has no effect here.

## Environment variables
**None required.** There are no API keys, secrets, or config values anywhere in
the code:
- Contact form → a `mailto:` link (client-side only).
- WhatsApp button → a plain `wa.me` link.
- Chatbot → a small rule-based (keyword-matching) script, no external AI API.
- Fonts → loaded from the public Google Fonts CDN, no key needed.

If you later add a real backend (see note below), that's when environment
variables would start to apply.

## Deployment instructions

### Option A — GitHub + Vercel dashboard (recommended)
1. Push this project to a new GitHub repository:
   ```bash
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo>.git
   git push -u origin main
   ```
2. Go to https://vercel.com/new and import that GitHub repo.
3. Confirm the settings Vercel shows match this document (Framework: Other,
   Build Command: none, Output Directory: `.`). Vercel should auto-read these
   from `vercel.json`.
4. Click **Deploy**. No environment variables to add.
5. Every future push to `main` will auto-deploy.

### Option B — Vercel CLI (no GitHub required)
```bash
npm install -g vercel   # one-time, requires Node.js only for the CLI itself
vercel                  # deploy a preview
vercel --prod           # deploy to production
```
The CLI will detect `vercel.json` and deploy the static file directly — it
won't ask for a build command.

## Post-deploy checklist
- [ ] Visit the deployed URL and click through all nav links (desktop and mobile
      menu — tested down to 390px width).
- [ ] Confirm the "Add Product" password still matches what you want live
      (`PRODUCT_PASSWORD` near the bottom of `index.html` — currently `Sim@123`).
- [ ] Confirm contact details are correct: emails, phone, WhatsApp link, address.
- [ ] If you want a custom domain, add it under Project Settings → Domains.

## Known architectural limitation (by design, not a bug)
"Add Product" and product removal use browser `localStorage` — products added
by one visitor are **not** shared with other visitors, since there's no
database or API. If you want products to persist for everyone site-wide,
that requires adding a real backend (e.g. a Vercel Serverless/Edge Function
plus a database like Vercel Postgres or Supabase) — that's a larger change
than this static file supports on its own. Let me know if you'd like that built.
