# Documentation

| Folder / file | What |
|---|---|
| [`docs/`](docs) | **the documentation site** (Markdown, built with MkDocs + Material for MkDocs). Start at [`docs/index.md`](docs/index.md) |
| `mkdocs.yml` | site settings: navigation (page order), theme, colours, extensions |
| `requirements-docs.txt` | what's needed to build the site |
| [`samples/`](samples) | curated real outputs from the acceptance runs (camera photos, report CSVs); see its README |
| `oshe-pnp-docs/` | the **old** hand-written HTML site (superseded on 2026-11-18, kept for reference) |
| `site/` | build output, not in git |

The pages read fine on GitHub too, but the site adds search, navigation, the results videos and
the theme.

## Read it locally

Needs Python **3.14 or older** (3.15 can't install MkDocs' YAML library yet). In PowerShell, from
the repository folder:

```powershell
py -3.14 -m pip install -r Documentation/requirements-docs.txt
py -3.14 -m mkdocs serve -f Documentation/mkdocs.yml
```

Open **http://127.0.0.1:8000/**. Saving a page reloads the browser. `Ctrl+C` stops it.

## Publish it (GitHub Pages): not switched on yet

`.github/workflows/docs.yml` builds the site with `--strict` on every change to `Documentation/`
(a check), and publishes it only once publishing is switched on. To publish, a repository admin of
**OSHE-Github/OSHE-PnP**:

1. **Settings -> Pages -> Build and deployment -> Source: GitHub Actions**.
2. **Settings -> Secrets and variables -> Actions -> Variables**: add `PUBLISH_DOCS` = `true`.
3. Custom domain **pnp.oshe.io** (planned; `site_url` in `mkdocs.yml` is already set to it):
   - **Before asking for DNS**, claim the domain for the org: OSHE-Github **organisation**
     Settings -> Pages -> **Add a domain** -> `oshe.io`. GitHub shows a TXT record
     (`_github-pages-challenge-OSHE-Github` with a code). This stops anyone else's GitHub Pages
     site from using pnp.oshe.io.
   - Ask whoever runs oshe.io's DNS (campus IT) for two records:
     `CNAME  pnp  ->  oshe-github.github.io`  and that TXT record.
   - When they're in: back in the org Pages settings click **Verify**; then in the
     **repository** Settings -> Pages enter `pnp.oshe.io` as custom domain, wait for the
     certificate, and tick **Enforce HTTPS**.

Until the DNS exists, a published site is at `https://oshe-github.github.io/OSHE-PnP/` (it works
there too; only the "canonical" address in the page headers already says pnp.oshe.io).

## Writing pages

- One task per page, numbered steps, short sentences, "you".
- Callouts: `!!! warning "Title"`, `!!! tip`, `!!! danger`, `!!! note` (indented body).
- Images go in `docs/assets/`; videos and GIFs in `docs/assets/media/`.
- A new page must be added to `nav:` in `mkdocs.yml` (and to the table on the home page).
- Before committing: `py -3.14 -m mkdocs build --strict -f Documentation/mkdocs.yml` must pass
  (it fails on broken links and anchors).
- Mark unfinished things with an **Ongoing** warning box, never with placeholders like `xxxx`.
