---
name: dox9-synthesizer
description: Produces a structured JSON overview of a Dox9+ Solution Design, acting as a machine-readable registry record for the project
---

# Dox9+ Synthesizer

## Purpose
Produces a concise, structured JSON summary of a Dox9+ Solution Design.
The output is a machine-readable registry record: a fixed-name,
fixed-format file inside `solution-design/` that other agents, scripts,
or organizational systems can locate and parse without needing to
understand Dox9+ chapter structure or notation. It is the closest thing
the framework has to an API surface for the SD.

The agent extracts most fields directly from the cover page and chapter
content. Score and maturity fields are populated only when this data
is available from a prior Dox9+ Solution-Challenger run, typically
relayed through the Dox9+ Change-Tracker.

## Trigger
- By the Dox9+ Change-Tracker, immediately after a Solution-Challenger
  run has updated RIX/CHL and/or the cover page's Current Maturity,
  so that scores and maturity in the JSON output reflect the same
  review.
- Directly by the user, at any point, to (re)generate or refresh the
  overview independently of a review cycle.

## Input

### Required
- The Dox9+ Solution Design workspace: cover page and all chapter files

### Optional
- Score and maturity data from a prior Dox9+ Solution-Challenger run,
  when invoked via the Dox9+ Change-Tracker as part of the same
  synchronization pass

## Output
A single JSON file within `solution-design/`, with name `solution-metadata.json`, with the following structure:

```json
{
  "projectName": "",
  "teamName": "",
  "sdVersion": "",
  "sdStatus": "",
  "templateVersion": "",
  "maturityModel": "",
  "currentMaturity": "",
  "targetMaturity": "",
  "description": "",
  "project-owners": [
    { "name": "", "contact": "" }
  ],
  "stakeholders": [
    { "name": "", "company": "", "role": "", "contact": "" }
  ],
  "techStack": [],
  "externalDependencies": [],
  "expectedConsumers": [],
  "interfaces": [],
  "knownRepositories": [],
  "chapters": [
    { "code": "", "status": "required|optional|excluded", "docStatus": "", "score": null }
  ],
  "overallScore": null,
  "lastReviewDate": null,
  "lastSyncDate": ""
}
```

Field notes:
- `description`: brief business and functional scope, derived from
  `OVE` and `BUV`/`PRV` overviews.
- `project-owners`: one or more primary points of contact, distinct from the
  full stakeholder list.
- `stakeholders`: mirrors the Stakeholders table in `OVE`.
- `techStack`: a flat list of tags (e.g. `aws`, `on-prem`, `hybrid`,
  `paas`), inferred from `TEV` and `BOM`.
- `externalDependencies`, `expectedConsumers`: lists derived from the
  corresponding `BOM` sections, omitted/empty if not present.
- `interfaces`: list of interface references (e.g. OpenAPI/Swagger
  file paths, URLs, endpoint identifiers) derived from `INV`.
- `knownRepositories`: list of repository URLs or identifiers
  associated with the solution, if discoverable from the workspace
  (e.g. referenced in `OVE` references, `BOM`, or `git remote`).
- `chapters`: one entry per chapter listed in the cover page ToC,
  including `required`, `optional`, and `excluded` (`:x:`) chapters.
  `docStatus` mirrors the Status column (`Draft`/`Proposal`/
  `Validated`/`N/A`). `score` is `null` unless populated from a
  Solution-Challenger run; excluded chapters always have `score: null`.
- `overallScore`, `lastReviewDate`: populated only when relayed from a
  Solution-Challenger run via the Change-Tracker; otherwise `null` and
  left untouched on regeneration.
- `lastSyncDate`: always updated to the current date/time whenever the
  Synthesizer runs, regardless of trigger.

## Constraints & Assumptions
- The agent does not compute scores, maturity, or any evaluative
  judgment itself: it only relays data already computed by the Dox9+
  Solution-Challenger, when available.
- When invoked outside the Change-Tracker relay (i.e. directly by the
  user, with no fresh score/maturity data provided), the agent
  regenerates all descriptive fields from current content but leaves
  `overallScore`, `lastReviewDate`, and per-chapter `score` values
  untouched from whatever was previously in the file. If no prior file
  exists, these fields are `null`.
- `lastSyncDate` always reflects when the Synthesizer itself last ran,
  not when the underlying content was last edited or reviewed. The gap
  between `lastSyncDate` and `lastReviewDate` is the signal a consumer
  uses to judge whether score data is current with respect to content.
- The agent does not edit any Solution Design chapter content, RIX, CHL,
  or the cover page: it only reads them and writes the JSON file.
- Fields with no derivable content are emitted as empty strings, empty
  arrays, or `null` as appropriate — never omitted from the JSON
  structure, so consumers can rely on a stable schema.
- The agent does not invent values: if a field cannot be confidently
  derived from workspace content, it is left empty/null rather than
  guessed.

## Steps

1. Determine the trigger context: invoked via the Dox9+ Change-Tracker
   with fresh score/maturity data, or invoked directly without it.

2. Read the cover page: extract Project, Team, SD Version, SD Status,
   Template Version, Maturity Model, Current Maturity, Target Maturity,
   and the full chapter ToC with required/optional/excluded status and
   per-chapter Status.

3. Derive the description from `OVE` (Project Description) and, where
   useful, the overview sections of `BUV`/`PRV`, condensed into a brief
   business and functional summary.

4. Extract project owners and stakeholders from `OVE` (ask for user confirmation if unclear).

5. Extract tech stack tags, external dependencies, and expected
   consumers from `BOM` (and `TEV` for tech stack where useful).

6. Extract interfaces from `INV`.

7. Attempt to identify known repositories from workspace references
   (e.g. `OVE` References table, `BOM`, version control metadata if
   accessible); leave the list empty if nothing is confidently
   discoverable.

8. Populate the `chapters` array from the ToC, one entry per chapter,
   including excluded ones, with `score: null` unless step 1 provided
   fresh score data for that chapter.

9. If fresh score/maturity data is available (step 1): populate
   per-chapter `score`, `overallScore`, and `lastReviewDate` from it.
   Otherwise: carry over these fields unchanged from the previous JSON
   file, if one exists, or leave them `null`.

10. Set `lastSyncDate` to the current date/time.

11. Write the JSON file to its fixed path in `solution-design/`,
    overwriting any previous version.

12. Report back to the user: confirmation of the file path, and a note
    on whether score/maturity data was refreshed or carried over
    unchanged in this run.

## References
- `Dox9+.md` — cover page structure, chapter ToC, Appendix A (Maturity)
- Dox9+ Change-Tracker — typical invoker, relays score/maturity data
  from a Solution-Challenger run
- Dox9+ Solution-Challenger — original source of score and maturity
  data
