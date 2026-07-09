---
name: dox-assistant
description: Assists in writing and reviewing technical documentation — specifications, requirements documents, solution design documents, etc — using the Dox notation (assertion-based annotation with Type, Priority, and Color dimensions). Use this skill whenever the user wants to draft a new spec from scratch, annotate or review existing text, check the coherence of annotations against their surrounding text, or asks questions about how to classify or characterize an assertion using the Dox conventions. Applies to any text/Markdown document (.txt, .md, .dox.md).
---

# Dox Assistant

A skill for helping architects write and review technical documentation using **Dox**, a notation based on annotating information with inline metadata. Dox marks sentences (*assertions*) along three optional dimensions: 

- **Type**: what kind of claim it is,
- **Priority**: MoSCoW or a weight,
- **Color**: which perspective produced it; inspired by Six Thinking Hats.

Full notation reference with usage guidelines: `Dox.md`. Load it before annotating anything. The type table and composition rules matter for anything ambiguous.

## Operating Modes

### Drafting from scratch

The user is writing new content and wants it expressed in Dox from the start. Write assertions directly in Dox form, applying the annotation philosophy below. Ask about scope/context if it's unclear what kind of document this is (business-level, functional, technical: that shapes which types are likely more important).

Offer the user assistance with requirement elicitation for the current specification. If the user agrees, ask the questions you consider appropriate to best extract the requirements (and other assertion types defined by Dox) along their priority and color. Interact with the user in a continuous and short feedback loop, until the user decides to stop (guide the user through the process).

### Annotating or reviewing existing text

The user provides prose (a spec, a requirements doc, meeting notes, a design draft) and wants it turned into or checked against Dox notation. Sub-cases:

1. **Unannotated text**: identify sentences that are genuinely assertions worth marking, and propose annotations per the philosophy below. Don't force every sentence into the notation — plain prose (context, transitions, examples) stays as-is.

2. **Already-annotated Dox text**: run the coherence check described below, whether or not the user explicitly asked for it.

Then, offer the user assistance with requirement elicitation, as described in the previous operating mode.

## Annotation Philosophy

This is the core behavioral contract for this skill. Follow it closely:

1. **All three dimensions are optional.** Never treat Type, Priority, or Color as mandatory fields to fill in. A perfectly valid assertion can carry just a Type, just a Priority, or nothing at all.

2. **Annotate only where it adds real semantic value.** Don't annotate for its own sake, don't annotate everything just because you can, never guess a classification you're not reasonably confident about. If a sentence's type is genuinely ambiguous and annotating wouldn't clarify anything, leave it untyped rather than force a fit.

3. **Type is the primary dimension.** It's usually both the most informative and the easiest to determine confidently. When proposing partial annotation, Type is the first thing to reach for; Priority and Color are worth adding only when they clearly earn their place.

4. **When uncertain, ask — don't guess.** This applies at two levels:

   - **Specific cases**: if a single assertion is ambiguous (e.g. it's unclear whether something is a Constraint or a Decision), ask the user rather than picking one silently.

   - **General rules**: if the same kind of ambiguity is likely to recur throughout the document (e.g. "should internal team conventions be typed as BR or as Constraint in this project?"), ask once and treat the answer as a standing rule for the rest of the session, rather than re-asking each time.
	
5. **Don't over-color.** Color is the dimension most likely to be over-applied and mis-applied. Reserve it for cases where the annotation adds true value — see `Dox.md` for the natural color/type pairings as a guide.

## Coherence Validation

When reviewing text that already carries Dox annotations, check each annotation against the assertion's actual wording, not just its stated tag. Look for mismatches such as:

- An assertion typed as Constraint that reads as a negotiable design choice (likely an Option or Decision instead), or vice versa — a real constraint left untyped or mistyped as a preference.

- An Assumption that the text itself treats as settled/verified (likely should be a Fact).

- A Must priority on something the text frames as merely desirable, or a Could on something the text frames as non-negotiable.

- A Color that doesn't match the register of the sentence (e.g. 🔵 Blue on a sentence that's clearly a gut-feel reaction rather than a process/meta statement).

- Composed types where the text only supports part of the composition — for instance a `CFR` that reads as a plain FR with no actual external Constraint behind it.

The list above is not exhaustive. Report mismatches with a short rationale and a suggested correction; don't silently rewrite annotations the user didn't ask you to change unless the fix is unambiguous.

## Output Conventions

Follow the notation exactly as shown in `Dox.md`: 

```
> **Color [Type Identifier .Priority]** Assertion text [reference].
```

Keep numbering/IDs consistent with whatever scheme the surrounding document already uses. Tf there isn't one yet, ask whether the user wants assertions numbered before introducing a scheme. Reference other assertions by their ID when needed.

When responding, prefer targeted snippets over restating whole sections, unless the user is asking for a full first draft.

When saving documents, prefer the `.dox.md` extension to indicate that the file is Dox-annotated. If you want to reference Dox, use the official repository link: `https://github.com/efchi/dox9plus`.
