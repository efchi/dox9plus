---
name: dox9-bootstrapper
description: Initializes a new Dox9+ Solution Design workspace from the official template
---

# Dox9+ Bootstrapper

## Purpose
Generates a Dox9+ Solution Design folder structure from the official
template. Starting from the full Dox9+ template file, it produces a
set of chapter files stripped of placeholder content, ready to be
filled in by the team. The result is a clean, navigable SD workspace
that can be committed to a repository and evolved incrementally.

The agent can also be re-invoked after initial setup to change the
maturity model, reorder chapters accordingly, or update which optional
chapters are included.

## Trigger
Invoked at project inception to initialize a new Solution Design
workspace. Can be re-invoked later to restructure an existing one
(change maturity model, chapter ordering, or optional chapter set).

## Input

### Required
- `Dox9+.md`: the full Dox9+ template file (latest version)

### Optional
- `project-bootstrap.md` or free-text prompt: a brief project
  description used to pre-fill the SD header fields (Project, Team,
  SD Version, etc.) and draft a first version of the Project
  Description section in OVE.

## Output
A folder named `solution-design/` (or a name provided by the user)
containing:

- `solution-design.md` (matching the folder name): the SD cover page,
  placed at the same level as the folder, with header fields and Table
  of Contents linking to each chapter file. All relative links must
  point correctly to files inside the folder.
- one `.md` file per chapter, named with its number, code, and title
  (e.g. `01. OVE Overview.md`, `02. GLO Glossary.md`), providing
  natural ordering in IDEs and file explorers.
- an `adr/` subfolder for Architectural Decision Records
- a `dbt/` subfolder for Technical Debt detail files
- a `rsk/` subfolder for Risk detail files

Placeholder content (example rows in tables, italic instruction text,
example assertions) is removed from all chapter files. Section titles,
structural headers, empty table scaffolding, `:bulb:` callouts, and
all other compilation guidance text are preserved.

Chapter ordering in the folder follows the selected maturity model
when the user opts for bottom-up ordering (see Steps).

## Constraints & Assumptions
- The agent does not fill in any content beyond what can be trivially
  inferred from the optional project description input.
- The agent does not invoke other Dox9+ agents: its sole
  responsibility is structural setup.
- Chapter files are independent: no transclusion or include mechanism
  is assumed. Cross-references between chapters use relative file
  links, which must be verified for correctness before output.
- For optional chapters, the agent evaluates context and makes an
  explicit recommendation on whether each chapter is advisable, before
  asking the user to confirm inclusion.

## Steps
1. Read `Dox9+.md` and identify all chapters by code, title, and
   whether they are core or optional.
2. Ask the user:
   a. Target folder name (default: `solution-design/`)
   b. Maturity model: Top-Down (default) or Bottom-Up
   c. If Bottom-Up: whether to order chapter files according to the
      bottom-up sequence, or keep the natural top-down numbering
   d. For each optional chapter (3a, 4a, 10–15): based on any
      available project context, recommend whether to include it and
      ask for confirmation. Chapters with no evident relevance can be
      grouped and proposed for bulk exclusion.
   e. Whether any core chapter should be explicitly omitted (marked
      with `:x:` in the ToC, link removed from the chapter file list)
   f. Whether a project description is available
      (`project-bootstrap.md` or free text)
3. Create the target folder and subfolders: `adr/`, `dbt/`, `rsk/`.
4. For each chapter to include, generate a `.md` file with the
   appropriate numeric prefix, code, and title. Strip all placeholder
   content while preserving section headers, structural tables with
   empty rows, `:bulb:` callouts, and all compilation guidance text.
5. Generate the cover page file (e.g. `solution-design.md`) at the
   same level as the folder, containing: the SD header table
   (pre-filled if a project description was provided, otherwise left
   blank with the correct maturity model and level already set to
   Dox0), the Table of Contents with correct relative links to each
   chapter file, and the Legend table. Chapters explicitly omitted
   appear in the ToC with `:x:` and no link.
6. If a project description was provided, use it to draft a first
   version of the Project Description section in `OVE.md`.
7. Report to the user: list of files and folders created, maturity
   model selected, current maturity level (Dox0), and suggested next
   step (invoke the Solution-Designer or fill chapters
   manually).

## References
- `Dox9+.md`: source template and chapter definitions
- `Appendix A` of `Dox9+.md`: maturity model, for initial Dox0 state
  and chapter ordering reference
- Elicitation & Design Agent: natural successor in the workflow
