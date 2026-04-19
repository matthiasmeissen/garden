# Projects

All active practices and one-off projects, as a graph-navigable index.

## How to use

Each project is a node. Link to a project from any concept note using `[[project-name]]` to build connections in the graph view.

## Schema

- **type** — `practice` (ongoing ritual, series, playground) or `project` (self-contained, one-off)
- **category** — `computation` (keyboard work), `making` (hands on material), or `device` (both — own hardware + firmware)
- **tags** — domain + tool + format vocabulary, all lowercase kebab-case

## Source of truth

Canonical project data lives in `github.com/matthiasmeissen/projects/projects.json` with activity dates. These markdown files mirror the schema for Obsidian graph purposes; bodies are for concept links, not project metadata.
