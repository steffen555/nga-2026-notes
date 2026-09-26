# Inbox processing reference

## Source front matter

```yaml
---
title: "Latin Quarter walking notes"
source_id: 2026-09-26-anna-latin-quarter
cite: Anna
author: Anna Jensen
author_role: classmate
received: 2026-09-26
format: handwritten-photo
format_label: Handwritten photo
sessions:
  - 02-cathedral-latin-quarter
places:
  - latin-quarter
  - vor-frue-kirke
media:
  - path: /assets/sources/2026-09-26-anna-latin-quarter/page1.jpg
    caption: Page 1
  - path: /assets/sources/2026-09-26-anna-latin-quarter/page2.jpg
    caption: Page 2
summary: Anna’s handwritten notes from the Saturday Latin Quarter demonstration.
---

Handwritten notebook pages…

## page1.jpg

…
```

After writing `assets/sources/<id>/transcription.md`, paste that same markdown into the `_sources/<id>.md` body (without a duplicate top-level `# Transcription` heading — the layout supplies it). List only image/PDF originals under `media:`.

## Transcription file (non-text media)

Path: `assets/sources/<id>/transcription.md`

Write this **before** compiling session/place pages.

```markdown
# Transcription

## page1.jpg

Longest church in Denmark
825 years. 1201, but actually a bit older…
[illegible]

## page2.jpg

…
```

- Match headings to media filenames.
- Keep original language; do not rewrite into compiled English here.
- Use `[illegible]` / `[unclear: …]` instead of inventing words.

## Citing on compiled pages

In `_sessions/*.md` or `_places/*.md`:

```markdown
## Latin Quarter

The walking tour used a viking theme and met at the cathedral tower.{% include cite.html id="2026-09-26-anna-latin-quarter" %}
```

Optional short label override:

```liquid
{% include cite.html id="2026-09-26-anna-latin-quarter" label="Anna" %}
```

## Optional inbox meta.md

```markdown
author: Anna Jensen
author_role: classmate
received: 2026-09-26
sessions: 02-cathedral-latin-quarter
places: latin-quarter, vor-frue-kirke
```

## Session slug cheat sheet

Fall examples (see `_data/program.yml` for full list):

| Slug | Topic |
| --- | --- |
| `01-welcome-harbor` | Welcome + harbor |
| `02-cathedral-latin-quarter` | Cathedral + Latin Quarter |
| `03-history-1` | History 1 |
| `06-old-town-tour` | Old Town tour |
| `07-old-town-class` | Old Town in class |
| `12-moesgaard` | Moesgaard |
| `13-old-town-exam` | Old Town exam |

Place slugs: `aarhus-cathedral`, `latin-quarter`, `vor-frue-kirke`, `the-old-town`, `dokk1`, `aros`, `moesgaard`, … (all under `_places/`).
