# Projects

All active practices and one-off projects as graph-navigable nodes.

## How to use

Link to any project from a concept note using `[[project-slug]]`. Obsidian's graph and backlinks pane will surface the connections.

## Schema

- **type** — `practice` (ongoing ritual, series, playground) or `project` (self-contained, one-off)
- **category** — `computation` (keyboard work), `making` (hands on material), or `device` (both — own hardware + firmware)
- **tags** — domain + tool + format vocabulary, all lowercase kebab-case

## Source of truth

Canonical project data lives in `github.com/matthiasmeissen/projects/projects.json`. These markdown files are regenerated from it via `export_projects.py`.
