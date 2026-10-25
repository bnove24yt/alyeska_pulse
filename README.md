# alyeskapulse.com

Source for **Pulse · The Alaska Merchant Pulse** (https://alyeskapulse.com), served by the Cloudflare Pages project `alyeskapulse`.

## How this repo started

The site was originally uploaded to Cloudflare Pages directly, with no source repo. On 2026-10-25 this repo was rebuilt from the live deployment (`fa0fa7a1.alyeskapulse.pages.dev`) by crawling every page, stylesheet, image and data file it references. Everything the site serves publicly is here.

Not recoverable from the live site, because Cloudflare never serves them to visitors:
- `_redirects` / `_headers`, if the original upload had them
- any Pages Functions (none appear to be in use: every dynamic call goes to n8n)

## Layout

| Path | What it is |
|---|---|
| `index.html`, `how-it-works.html`, `lookup.html`, `claim.html`, `terms.html`, `privacy.html` | Public pages (also in `sitemap.xml`) |
| `signin.html`, `me.html`, `unsubscribe.html` | Owner pages, excluded in `robots.txt` |
| `b/preview/` | Owner-page previews, excluded in `robots.txt` |
| `404.html` | Not-found page |
| `assets/pulse.css` | Shared stylesheet |
| `assets/index.json` | Business index used by the lookup search |
| `assets/snapshots.json` | Score snapshots used by the owner pages |
| `assets/img/` | Page images |

Pages serves `lookup.html` at `/lookup`, `b/preview/index.html` at `/b/preview/`, and so on.

## Backend

The site is static. Sign-in, claims, the owner page and profile edits call n8n webhooks at `https://cl8.alyeskapos.com/webhook/` (workflows "Pulse — Claims" and "Pulse — Profile").

## Deploying

Changes are deployed to the Cloudflare Pages project `alyeskapulse`. Deploy to a preview first, check it, then promote.

`assets/index.json` and `assets/snapshots.json` are generated from the Pulse database; treat them as build output, not hand-edited files.
