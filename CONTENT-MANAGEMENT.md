# Managing Website Content via Google Sheets

Your website is connected to this Google Sheet:
https://docs.google.com/spreadsheets/d/1HuH1YsDudYqJF067FLnSfPGgk3vkzJHtE9YkfH-pb30/edit

Every visitor's browser reads directly from this sheet when the page loads, so
edits you make show up for everyone the next time they load the site — no
code changes needed.

## Step 1 — Required: share the sheet correctly

Click **Share** (top right of the sheet) → under "General access" change it
from "Restricted" to **"Anyone with the link"** → set the role to **"Viewer"**.

This is required because it's each visitor's browser doing the reading, not a
server you control — it has no way to log in as you. "Viewer" access means
people can only ever *see* the data if they have the exact link; only you can
edit it, since only you are logged into your Google account.

If you skip this step, every section below simply keeps showing its built-in
default content — nothing on the site breaks, it just won't reflect your edits.

## Step 2 — Set up the 5 tabs

Create tabs (the little labels at the bottom of the sheet) with these **exact
names** (case-sensitive). Right-click a tab to rename it, or click the **+**
to add a new one.

### Tab: `Content`
Single text fields, one per row. Columns: **Key | Value**

| Key | Value (example) |
|---|---|
| hero_eyebrow | Healthcare Simulation & Facility Consultancy |
| hero_headline | Clinical training environments where <em>competence comes before the real patient.</em> |
| hero_lead | InnovateSim Technologies provides healthcare simulation products and advises hospitals... |
| stat_years | 14+ |
| stat_facilities | 25+ |
| stat_countries | 6+ |
| about_heading | We build the environments where clinical skills are earned safely. |
| about_paragraph1 | (first About paragraph) |
| about_paragraph2 | (second About paragraph) |
| contact_email | alidawoodian@yahoo.com, bahatomah@yahoo.com |
| contact_phone | +1 (647) 949-5728 |
| contact_whatsapp_number | +16479495728 |
| contact_whatsapp_display | +1 (647) 949-5728 |
| contact_address | 572 Laughren Cres, Milton, Ontario, L9T 0G5 |

Notes:
- `hero_headline` accepts basic HTML — wrap text in `<em>...</em>` to get the
  orange emphasis styling.
- `contact_email` accepts multiple addresses separated by commas — each shows
  on its own line.
- `contact_whatsapp_number` should be digits only (with country code, no
  spaces/dashes/plus needed, though a leading `+` is fine — it gets stripped).
- Any row you leave out keeps that field's current default — you don't need
  to fill in every key if you only want to change one or two things.

### Tab: `Products`
Columns: **Name | Tag | Description | ImageURL**

One row per product. `ImageURL` is optional — leave blank to show a default
icon instead of a photo.

### Tab: `Consultancy`
Columns: **Title | Description**

One row per consultancy service. Cards are numbered automatically in the
order the rows appear.

### Tab: `WhyUs`
Columns: **Title | Description**

One row per "Why InnovateSim" item.

### Tab: `About`
Single column: **Text**

One row per bullet point in the About section's numbered list.

## Step 3 — Confirm it's live

The easiest way: visit your site with `#admin` at the end of the URL (e.g.
`yoursite.com/#admin`). A small panel appears in the bottom-right corner with
a **live sync status** — it will tell you plainly:

- **"Sheet sync: all 5 tabs connected ✓"** — everything is working.
- **"Sheet sync: not connected (...)"** — nothing is reachable yet; the
  reason is shown in plain English (e.g. "sheet not shared publicly, or tab
  missing").
- **"Sheet sync: 3/5 tabs connected — check: Consultancy, About"** — most
  tabs are fine, but specific ones need attention. Hover over the status
  text for a per-tab breakdown (row counts or failure reasons).

If something's still not right after checking that message:
- Double-check the tab name matches exactly (including capitalization).
- Double-check the sharing setting from Step 1.
- Open the browser's developer console (F12) for the same diagnostic detail
  in log form.

## What this does NOT do

- This is **one-way**: the website reads from the sheet. Editing the website
  itself doesn't write anything back to the sheet.
- There's no login/authentication built into the website for this — anyone
  who knows the sheet's link could view (not edit) it, per Step 1.
- Product images must be links to images hosted elsewhere (e.g. uploaded to
  Google Drive with public sharing, Imgur, or your own hosting) — you can't
  paste an image directly into a sheet cell for this purpose.

## Built-in safety nets

- If an `ImageURL` in the Products tab is broken or unreachable, the site
  automatically falls back to the default icon instead of showing a broken
  image.
- Consultancy cards synced from the sheet automatically cycle through a set
  of 7 icons in order, so a long list doesn't repeat the same icon over and
  over.
- Every tab is fetched independently — if one tab fails (wrong name, sheet
  not shared yet, etc.), only that section falls back to defaults; every
  other section still updates normally.
- The chatbot's answers about products and consultancy services are
  generated live from whatever is actually displayed on the page — so if you
  update the sheet, the chatbot's answers update too, automatically.
- The hidden admin panel (`#admin`) shows real-time sync status per tab, so
  you never have to guess whether it's working.
