# SI Rate Book — Geotechnical Quotation Tool

A single-page web tool for building a global geotechnical site-investigation rate
database, visualizing coverage on a world map, and generating cost estimates for
new bids using inflation-adjusted and regionally-derived pricing.

Everything runs in the browser — there is no backend, database, or server to set
up. Data is saved locally in the browser via the Storage API used by the page.

See **[USER_GUIDE.md](USER_GUIDE.md)** for a full step-by-step walkthrough of every
tab and feature.

---

## Publishing this on GitHub Pages (free hosting, ~5 minutes)

1. **Create a new repository** on GitHub (e.g. `si-rate-book`). Public or private
   both work; Pages is free either way on a personal account.
2. **Upload the files** in this folder to the repository:
   - `index.html` — the landing page (black/teal theme)
   - `app.html` — the tool itself
   - `README.md`
   - `USER_GUIDE.md`

   Easiest path if you're not familiar with git: on the repository page, click
   **Add file → Upload files**, drag in all three files, and click **Commit changes**.
3. **Turn on GitHub Pages:**
   - Go to the repository's **Settings** tab
   - In the left sidebar, click **Pages**
   - Under **Build and deployment → Source**, choose **Deploy from a branch**
   - Under **Branch**, choose **main** (or `master`) and folder **/ (root)**, then **Save**
4. Wait 1–2 minutes, then refresh the Pages settings page. You'll see a banner:
   *"Your site is live at `https://<your-username>.github.io/si-rate-book/`"*
   That link is now your permanent tool URL — bookmark it.

### Important note on data storage

This tool saves your quotations, countries, and settings **in your browser's local
storage** — no backend, database, or account needed. That means:

- Your data persists between visits, as long as you use the **same browser on the
  same device** and don't clear its site data/browsing data.
- It does **not** sync between devices (e.g. laptop and phone) or between different
  browsers on the same machine — each is a separate local store.
- If you need multiple people (or yourself across devices) sharing one live rate
  database, that requires a real backend (e.g. Firebase, Supabase, or a small API
  with a database behind it). That's a bigger step up from this static-file setup —
  ask if you want help scoping that out.
- Private/incognito windows typically clear this storage when closed.

For a single bid manager working from one main computer, the built-in local
storage is usually all you need.

## Files in this folder

| File | Purpose |
|---|---|
| `index.html` | Landing page — the site's front door, links into the tool |
| `app.html` | The tool itself |
| `README.md` | This file — publishing instructions |
| `USER_GUIDE.md` | Step-by-step usage guide for every tab |
