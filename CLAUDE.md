# CLAUDE.md

## Dox9+ Framework

This repository uses the Dox9+ Framework, composed of Dox notation,
the Dox9+ Solution Design template, and DoxOps agents — a set of Claude Code
skills that support the authoring, validation and maintenance of
Solution Design documents written with the Dox9+ template and using
Dox notation.

### Custom Skills Directory

Skills for this framework are not located in `.claude/skills/`. They
live in: `.dox/skills/`.

Treat this directory as an additional skills source, equivalent to
`.claude/skills/`. Each subdirectory contains a `SKILL.md` file
following the standard Agent Skills format (YAML frontmatter with
`name` and `description`, followed by instructions).

### Framework Context

Two reference documents define the conventions used throughout this
repository and should be treated as authoritative context whenever a
Dox9+ skill is invoked:

- `.dox/Dox.md` — the Dox notation framework (assertion types,
  priority, color)
- `.dox/Dox9+.md` — the Dox9+ Solution Design template (chapter
  structure and content guidelines, maturity models)

Skills under `.dox/skills/` may reference these files directly by
relative path. When working on any Dox9+ related task, consult these
files for naming conventions, chapter codes, and structural rules
before generating or editing content.

### Solution Design Location

Solution Design documents produced by these skills are expected to
live in a `solution-design/` folder at the repository root, with a
matching cover page file (`solution-design.md`) at the same level —
see the Dox9+ Bootstrapper skill for details.
