# alyeskapulse.com

Source for **Pulse · The Alaska Merchant Pulse** (https://alyeskapulse.com), served by the Cloudflare Pages project `alyeskapulse`.

## How this repo started

The site had no source repo. On 2026-10-25 this repo was rebuilt from the live deployment (`fa0fa7a1.alyeskapulse.pages.dev`) and checked file by file against the deploy record n8n keeps (`app_blob` key `pages_manifest_alyeskapulse`): all 36 files match byte for byte. `_redirects` and `_headers` come from that same record. There are no Pages Functions; every dynamic call goes to n8n.

## Layout

| Path | What it is |
|---|---|
| `index.html`, `how-it-works.html`, `lookup.html`, `claim.html`, `terms.html`, `privacy.html` | Public pages (also in `sitemap.xml`) |
| `signin.html`, `me.html`, `unsubscribe.html` | Owner pages, excluded in `robots.txt` |
| `b/preview/` | Owner-page previews, excluded in `robots.txt` |
| `404.html` | Not-found page |
| `open.html` | One-tap opening-date page from the new-business email |
| `preview/email/` | Previews of the owner emails |
| `_redirects`, `_headers` | Clean URLs, www redirect, security headers |
| `assets/pulse.css` | Shared stylesheet |
| `assets/index.json` | Business index used by the lookup search |
| `assets/snapshots.json` | Score snapshots used by the owner pages |
| `assets/img/` | Page images |

Pages serves `lookup.html` at `/lookup`, `b/preview/index.html` at `/b/preview/`, and so on.

## Backend

The site is static. Sign-in, claims, the owner page and profile edits call n8n webhooks at `https://cl8.alyeskapos.com/webhook/` (workflows "Pulse — Claims" and "Pulse — Profile").

## Deploying

Deploys go through the n8n workflow **APOS — Cloudflare Pages deploy** (webhook `apos-pages-deploy`, project `alyeskapulse`). It keeps the site's file list in `app_blob`, so an `incremental` deploy only needs the files that changed. Send `branch: "preview"` (or any name other than `main`) for a preview URL; `main` is production. Deploy to a preview first, check it, then promote.

`assets/index.json` and `assets/snapshots.json` are generated from the Pulse database; treat them as build output, not hand-edited files.
