# NGA Aarhus 2026 Notes

Student-compiled notes site for **Nordic Guide Academy · Aarhus 2026**, published with GitHub Pages (Jekyll).

## Two layers

1. **Sources** (`_sources/` + `assets/sources/`) — raw material as received (photos of handwriting, dumps, typed notes), always with **who** provided it.
2. **Compiled pages** (`_sessions/`, `_places/`) — synthesised notes, reached from **Program** and **Curriculum**. Each claim should cite a source.

Cite in compiled markdown:

```liquid
The cathedral tower is the meeting point{% include cite.html id="handout-fall-2026" %}.
```

## Publish on GitHub Pages

1. Push this repo to GitHub.
2. In **Settings → Pages**, set Source to **GitHub Actions**.
3. The workflow in `.github/workflows/pages.yml` builds and deploys on push to `main` / `master`.

## Local preview (Docker)

```bash
docker run --rm \
  --name nga-2026-notes \
  -v "$PWD:/srv/jekyll" \
  -p 4000:4000 -p 35729:35729 \
  jekyll/jekyll:4 \
  bash -lc 'bundle install && bundle exec jekyll serve --host 0.0.0.0 --baseurl "" --livereload --force_polling'
```

Open http://127.0.0.1:4000

(Production uses `baseurl: "/nga-2026-notes"` for GitHub Pages; local serve overrides it to empty.)

## Where things live

| What | Where |
| --- | --- |
| Raw source entries | `_sources/*.md` |
| Original files (photos, PDFs) | `assets/sources/<slug>/` |
| Compiled session notes | `_sessions/*.md` (linked from Program) |
| Compiled place notes | `_places/*.md` (linked from Curriculum) |
| Program / schedule data | `_data/program.yml` |
| Course handout images | `assets/handouts/` (also linked from Sources) |

Copy `_templates/source.md` into `_sources/` when filing a new contribution.
