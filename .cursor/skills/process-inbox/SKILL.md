---
name: process-inbox
description: >-
  Processes course notes and materials dumped in inbox/ into _sources and
  assets/sources, then updates session and curriculum pages with cited compiled
  notes. Use when the user adds files to inbox/, asks to process the inbox,
  process notes, file source material, or ingest classmate/handout dumps.
---

# Process inbox

Turn whatever landed in `inbox/` into proper sources and updated compiled pages.

## When to run

- User says process inbox / file these notes / ingest material
- `inbox/` contains anything other than `README.md`
- User attaches course notes and points at this repo’s workflow

## Checklist

Copy and track:

```
Inbox processing:
- [ ] Inventory inbox (group into packets)
- [ ] Resolve author, received date, format per packet
- [ ] Create assets/sources/<id>/ and copy originals
- [ ] For non-text media: write transcription.md (own file) before compiling
- [ ] Create _sources/<id>.md (raw + front matter)
- [ ] Update _sessions and/or _places with compiled notes + cite includes
- [ ] Adjust _data/program.yml places: links if coverage is newly clear
- [ ] Remove processed files from inbox/
- [ ] Summarise for the user what was filed and which pages changed
```

## Step 1 — Inventory

List `inbox/` recursively. Ignore `README.md`.

Treat as one **packet**:

- A single file, or
- One subfolder, or
- Files clearly belonging together (same author/date in names)

If multiple unrelated packets exist, process each separately (separate source ids).

## Step 2 — Metadata

For each packet gather:

| Field | How to get it |
| --- | --- |
| `author` | Filename, `meta.md`, folder name, or ask once |
| `author_role` | `self` \| `classmate` \| `teacher` \| `handout` |
| `received` | Filename date, `meta.md`, file mtime, or today (`YYYY-MM-DD`) |
| `format` | `handwritten-photo` \| `scan` \| `text` \| `typed` \| `mixed` |
| `sessions` / `places` | Content + `_data/program.yml` slugs; ask if ambiguous |

**Source id** (also folder name): `YYYY-MM-DD-author-slug`  
Examples: `2026-09-26-anna-latin-quarter`, `2026-09-23-steffen-harbor`

`cite` label: short author surname or clear short name for superscripts.

Template: `_templates/source.md`

## Step 3 — File the source (as received)

1. Create `assets/sources/<id>/`.
2. Copy every original file there. Keep original filenames when sensible; fix only if unsafe/colliding.
3. **Non-text media (required before Step 4):** For photos, scans, PDFs, audio, or other non-text files, create `assets/sources/<id>/transcription.md` **before** compiling anything into session/place pages.
   - One file for the whole packet (preferred), with a heading per media file.
   - Transcribe as faithfully as possible (language as written; mark `[illegible]` / `[unclear: …]` rather than guessing).
   - Do not synthesise or rewrite into guide prose here — that is Step 4.
   - Plain text packets: skip this file; the `_sources` body *is* the transcription.
4. Create `_sources/<id>.md`:
   - Front matter: `title`, `source_id`, `cite`, `author`, `author_role`, `received`, `format`, `format_label`, `sessions`, `places`, `media`, `summary`
   - `media[]` lists **original media only** (images, PDFs, etc.) — not `transcription.md`
   - **Body:** paste the same transcription markdown (so it renders on the source page). For plain text packets, the body is the verbatim text.
   - Keep `assets/sources/<id>/transcription.md` in sync when the body is a transcription of media.

Readers see images + transcription on the source page; the `transcription.md` file remains the editable raw reading next to the originals.

**Note:** Use front matter key `source_id` (not `id` — Jekyll reserves `id`). Cite with that same string: `{% include cite.html id="<source_id>" %}`. Put sentence periods *before* the cite include so they stay with the text.

## Step 4 — Compile into site pages

Only after Step 3 is complete (including `transcription.md` for non-text media).

Update the matching `_sessions/<session-slug>.md` and/or `_places/<place-slug>.md` **below** the front matter.

- Write clear compiled notes for readers from the transcription + context (structure, headings OK).
- After each factual claim: `claim.{% include cite.html id="<source_id>" %}` (period before the include).
- Merge with existing compiled notes; do not wipe prior cited content.
- If several sources disagree, say so and cite both.
- Do not add maintainer instructions on public pages.

Session slugs live under `_sessions/` (e.g. `02-cathedral-latin-quarter`).  
Place slugs live under `_places/` and in `_data/program.yml` `places:`.

If this packet shows a session covers places not yet listed, add those slugs to that session’s `places:` array in `_data/program.yml`.

## Step 5 — Clear inbox

After successful filing, delete the processed files/folders from `inbox/` (originals now live under `assets/sources/`). Leave `inbox/README.md`.

## Step 6 — Report

Tell the user:

- Source id(s) created
- Author / format
- Which session and place pages were updated
- Anything skipped or needing their input

## Do not

- Publish `inbox/` (excluded from Jekyll)
- Put only a summary in `_sources` and discard the raw files
- Compile session/place notes from non-text media without first writing `transcription.md`
- Cite a source id that was not created
- Commit or push unless the user asks

## Details

- Front matter and cite examples: [reference.md](reference.md)
