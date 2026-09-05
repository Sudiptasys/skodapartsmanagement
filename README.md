# ŠKODA Parts Desk — Spare Parts Order Management

A self-contained, single-file web app for managing spare-parts orders at a ŠKODA dealership: an order register, parts master/stock list, dashboard with reporting, admin-gated editing, and JSON backup/restore.

This is an **internal working tool**, not an official Škoda Auto product.

## What's included

- **`index.html`** — the entire application: markup, styles, and logic in one file. No build step, no framework, no npm install required.

That's it — there is no separate CSS, JS, or asset folder. Two things are loaded from a CDN at runtime in the browser (not needed to run the app locally as static files):
- Google Fonts (Space Grotesk / IBM Plex Sans / IBM Plex Mono)
- [SheetJS](https://sheetjs.com/) (`xlsx.full.min.js` from cdnjs) — used only when you click Export, or use the Parts Master bulk Excel upload tools

## Features

- **Order Register** — log spare-parts orders with order type, part category, supplier, status, and a locked/admin-edit workflow
- **Parts Master** — stock list with reorder-level tracking, bulk Excel upload for current stock, and 6-month movement upload that auto-calculates Max/Reorder/Min stock levels
- **Dashboard** — KPIs, Order Type and Part Category breakdowns, month-wise report, all filterable by month
- **Admin tab** — password-gated editing/deletion of register entries (see limitation below)
- **Backup tab** — download/restore a full JSON snapshot of all data
- **Export tab** — download the register as an Excel file with separate Open Cases / Closed Cases sheets

## Running it

Just open `index.html` in a browser — no server, no install, no build step.

To deploy on GitHub Pages:
1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Under "Build and deployment", set **Source** to "Deploy from a branch", pick your default branch and the `/ (root)` folder.
4. Save — GitHub will publish `index.html` at `https://<your-username>.github.io/<repo-name>/`.

## Important limitations (please read before relying on this for real data)

This is a static HTML page with **no backend, database, or server** — everything happens in your browser.

- **Data is session-only.** All orders and stock data live in the page's memory. Refreshing the page, closing the tab, or navigating away **loses everything** unless you've downloaded a backup first. Use the **Backup tab** regularly.
- **The Admin password is not real security.** It's a plain-text constant in the HTML source (`ADMIN_PASSWORD`, near the bottom of the `<script>` block) meant only to stop accidental edits by counter staff. Anyone who views the page source can read it. Don't use this to protect data you actually need to keep private — for that you'd need a real backend with authentication.
- **Excel import/export needs internet.** The Export tab and the two Parts Master upload tools load a small spreadsheet library from `cdnjs.cloudflare.com` the first time they're used in a session. Everything else works fully offline.
- **Multi-user use is not supported.** Since there's no shared server, two people with the page open at once are working with two independent, disconnected copies of the data — changes in one browser tab are never seen by another.

If you need persistent storage, multi-user access, or real authentication, this file would need to be paired with a backend (a small API + database) — the current version intentionally keeps things to a single static file for simplicity and easy deployment.

## License

No license file is included. Add one (e.g. via GitHub's "Add file → Create new file → LICENSE" template picker) if you plan to make this repository public and want to specify usage terms.
