# DoxOps

**DoxOps** is the agentic process layer of the Dox9+ Framework. It provides
a set of skills that support the full lifecycle of a Solution
Design document: from initial workspace setup, through requirement
elicitation and design, to validation, maintenance, and synthesis.

Each agent has a well-defined responsibility and interacts with the others
in a structured way. Some invocations are triggered by the user; others
are automatic, agent-to-agent, as part of a synchronization chain.

DoxOps is distributed under CC BY-SA 4.0 — see [LICENSE.md](./LICENSE.md) file.

:warning: **The agents and process described below have received limited testing.**

## Agents

- :warning: **[Bootstrapper](./skills/dox9-bootstrapper/SKILL.md)**. Initializes a new Dox9+ Solution Design workspace
  from the official template, stripped of placeholder content and
  ready to be filled in. Can also be re-invoked later to change the
  maturity model, chapter ordering, or optional chapter set.

- :warning: **[Reverse-Engineer](./skills/dox9-reverse-engineer/SKILL.md)**. Reconstructs a Dox9+ Solution Design
  retroactively from an existing codebase, inferring architecture,
  interfaces, and — where plausible signals exist — functional and
  business context, clearly flagged for validation.

- :warning: **[Solution-Designer](./skills/dox9-solution-designer/SKILL.md)** Guides requirement elicitation and design,
  following the Dox9+ logical flow (business → product → technical
  requirements), with an active technical solution architect's point of view.
  Can ingest existing documentation to bootstrap elicitation.
  
- :warning: **[Solution-Challenger](./skills/dox9-solution-challenger/SKILL.md)**. Critically evaluates a Solution Design for
  completeness, consistency, and technical soundness. Assigns a 1-10
  score per chapter and computes the document's actual maturity level.

- :warning: **[Change-Tracker](./skills/dox9-change-tracker/SKILL.md)**. Mechanically resynchronizes, after relevant changes to a Solution Design, the Requirements Index, Changelog and current maturity level. Always
  invokes the Synthesizer as its final action.

- :warning: **[Synthesizer](./skills/dox9-synthesizer/SKILL.md)**. Produces a structured JSON overview of a Solution
  Design, acting as a machine-readable registry record for the project.

## Process

The diagram below shows the ideal DoxOps workflow: solid arrows
represent user-triggered or agent-to-agent invocations, dashed arrows represent other operations.

```mermaid
flowchart TD
    U([User])

    U -->|new project| BST[Bootstrapper]
    U -->|existing codebase| REV[Reverse-Engineer]
    REV -->|"no workspace yet"| BST

    BST -.->|suggest using| SD

    U -->|elicitation <br> or design session| SD[Solution Designer]
    SD -.->|writes chapters| WS[(Solution Design <br> workspace)]
    SD -->|signals changes| CT

    U -->|review request| SC[Solution-Challenger]
    SC -.->|reads chaptes| WS
    SC -->|update status: <br> scores, maturity| CT

    CT[Change-Tracker] -.->|write RIX, CHL, <br> current maturity| WS
    CT -->|always, as final action| SY[Synthesizer]

    SY -.->|writes solution-design.json| WS

    U -->|direct invocation| CT
    U -->|direct invocation| SY
```

## Common Use Cases

### Starting a new project
The user invokes the Bootstrapper, which creates the workspace. The
Solution-Designer is then invoked to begin elicitation. After each
relevant session, the Solution Designer signals the Change-Tracker,
which resynchronizes RIX and CHL, then automatically
invokes the Synthesizer.

### Starting from an existing codebase
The user invokes the Reverse-Engineer, which inspects the repository
and populates technical chapters (and where possible functional and
business chapters, clearly flagged for validation). If no workspace
exists yet, the Reverse-Engineer asks for confirmation before invoking
the Bootstrapper. Afterward, the Solution-Designer or Solution-Challenger are recommended to evaluate, validate and refine the reconstructed content.

### Periodic quality review
The user invokes the Solution-Challenger at any point. It evaluates
the document, scores each chapter, and computes the actual maturity
level. It then passes this delta to the Change-Tracker, which updates
the cover page's current maturity, RIX and CHL accordingly, and
invokes the Synthesizer to keep the JSON registry current.
