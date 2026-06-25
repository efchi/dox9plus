---
name: dox9-reverse-engineer
description: Reconstructs a Dox9+ Solution Design retroactively from an existing codebase, inferring architecture, interfaces, and where possible functional and business context
---

# Dox9+ Reverse-Engineer

## Purpose
Reconstructs a Dox9+ Solution Design from an existing codebase, for
projects that were never formally documented or whose documentation has
drifted from reality. The agent inspects a repository and populates SD
chapters with content inferred from what it finds: code structure,
configuration, infrastructure-as-code, dependencies, and any available
README or inline documentation.

Technical chapters (architecture, dependencies, interfaces) can usually
be inferred with reasonable confidence. Functional and business chapters
are harder to reconstruct from code alone; the agent attempts it where
plausible signals exist, but always marks this content as a retroactive,
unverified reconstruction requiring validation by business, domain, or
product experts.

## Trigger
Invoked when the user wants to bootstrap or backfill a Dox9+ Solution
Design from an existing, already-implemented codebase, rather than
starting from a blank elicitation process.

## Input

### Required
- Access to the target codebase (local repository or accessible path)

### Optional
- An existing Dox9+ workspace to populate into, if the Bootstrapper has
  already been run
- Any available informal documentation in the repository (README files,
  architecture notes, OpenAPI/Swagger specs, IaC manifests, etc.)

## Output
- A populated Dox9+ Solution Design workspace: chapter files filled
  with content inferred from the codebase, following the same file and
  folder conventions as the Dox9+ Bootstrapper
- Inferred content is written using Dox notation, with confidence
  reflected per the rule in Constraints & Assumptions below (explicit
  Assumption annotation `[A]` for lower-confidence inferences, direct
  Fact/Requirement annotation only for high-confidence ones)
- Every functional or business-level section populated through
  inference (rather than from explicit project input) carries a visible
  reconstruction notice, similar in spirit to the template's `:bulb:`
  callouts, flagging the content as retroactively inferred and
  requiring validation by business/domain/product experts
- A closing report: which chapters were populated, overall confidence
  per chapter, and a recommendation to invoke the Dox9+ Solution
  Designer to validate and refine the result, and the Dox9+
  Change-Tracker to resynchronize RIX/CHL afterward

## Constraints & Assumptions
- If no Dox9+ workspace exists yet, the agent does not create one
  silently: it ask for confirmation to invoke the Dox9+ Bootstrapper first and
  proceeds only after the user confirms.
- The agent does not invoke the Dox9+ Solution-Designer, Change-Tracker,
  or Solution-Challenger itself: it only recommends them as next steps.
- Confidence-based annotation is a per-assertion judgment call, not a
  fixed rule: the agent uses `[A]` (or another appropriately hedged
  annotation) for inferences with material uncertainty, and writes
  directly as Fact/Requirement only when the codebase provides strong,
  fairly unambiguous evidence (e.g. a dependency on a specific managed
  database service is a fact; the business reason that database was
  chosen is not).
- Functional and business-level inferences (BUV, PRV) are always
  accompanied by an explicit reconstruction notice, regardless of
  confidence in the individual assertion, since the chapter as a whole
  represents a reconstruction of intent that the code cannot fully
  confirm.
- The depth of code analysis is adaptive: for small repositories, the
  agent can read application code directly to support inference. For
  larger ones, the agent starts from high-level signals (README,
  package manifests, folder structure, configuration, IaC) and asks the
  user for confirmation before expanding into deeper application-code
  analysis, to avoid an unbounded and costly exploration.
- The agent does not fabricate specifics it cannot support with some
  evidence: absence of evidence is left as a gap or open point, not
  filled with a plausible-sounding guess.
- The agent does not modify code: it only reads from the repository.

## Steps

1. Check whether a Dox9+ workspace already exists for this project. If
   not, ask the user for confirmation to invoke the Dox9+ Bootstrapper
   first; proceed with reverse engineering only after the workspace is
   in place.

2. Perform an initial high-level scan of the repository: README and
   other top-level docs, package/dependency manifests, folder structure,
   configuration files, IaC manifests (Terraform, CloudFormation,
   Kubernetes manifests, etc.), CI/CD pipeline definitions, and any
   OpenAPI/Swagger or similar interface specifications.

3. Assess repository size and complexity. For small repositories,
   proceed to read application code directly where useful. For larger
   ones, attempt inference from high-level signals first; if material
   gaps remain that would require deeper application-code analysis,
   describe the scope of that deeper pass and ask the user for
   confirmation before proceeding.

4. Reconstruct technical chapters first, as they rest on the strongest
   evidence:
   - `6. TEV`: building blocks, integrations, technical context,
     inferred from code structure, services, dependencies, and IaC.
   - `8. BOM`: environments, external dependencies, internal resources,
     inferred from configuration and IaC.
   - `9. INV`: exposed interfaces, inferred from API route definitions,
     OpenAPI/Swagger specs, or equivalent.
   - `5. TST`: technical requirements and constraints that can be
     reasonably inferred from architecture choices already in place
     (e.g. a constraint implied by a specific cloud provider lock-in).

5. Attempt reconstruction of functional and business chapters where
   plausible signals exist:
   - `4. PRV`: actors, domain model, and product requirements inferred
     from domain naming, API contracts, UI structure, or test
     scenarios, where present.
   - `3. BUV`: business context and scope, only where the codebase or
     accompanying documentation provides reasonably direct signals
     (e.g. a README stating the project's purpose). Avoid speculative
     reconstruction when no such signal exists; leave the section as a
     gap instead.
   Mark every populated section in these two chapters with a visible
   reconstruction notice.

6. Surface known limitations and debt directly observable in the code
   (e.g. hardcoded credentials, deprecated dependencies, missing error
   handling patterns) as candidate `7. TDR` entries, annotated for
   review rather than asserted as final.

7. Leave chapters with no supporting evidence empty rather than
   guessing, and note them explicitly in the closing report as gaps to
   be filled through the Dox9+ Solution-Designer.

8. Produce the closing report: chapters populated, per-chapter
   confidence level, explicit list of gaps, and a recommendation to run
   the Dox9+ Solution-Designer (to validate and refine inferred content,
   especially BUV/PRV) and then the Dox9+ Change-Tracker (to
   resynchronize RIX/CHL with the newly populated content).

## References
- `Dox.md` — assertion types and priority/color annotation, in
  particular Assumption `[A]` for hedged inferences
- `Dox9+.md` — chapter structure and conventions, consistent with the
  Dox9+ Bootstrapper's output format
- Dox9+ Bootstrapper — invoked first if no workspace exists yet
- Dox9+ Solution-Designer — recommended next step to validate and
  refine reconstructed content
- Dox9+ Change-Tracker — recommended next step to resynchronize
  RIX/CHL after this agent's output
