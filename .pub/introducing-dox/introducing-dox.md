# Introducing Dox: a lean notation to guide solution design, inspired by Six Thinking Hats

> ✨ This article was drafted and translated into English with the help of an AI. The content and related assets originate from the author's own ideas and experiences.

## Table of Contents

1. [Introduction](#introduction)
2. [Hello Dox](#hello-dox)
3. [Everything Is an Assertion](#everything-is-an-assertion)
4. [Classifying Assertions](#classifying-assertions)
5. [Prioritizing Assertions](#prioritizing-assertions)
6. [Putting On a Hat](#putting-on-a-hat)
7. [The Dox Assistant](#the-dox-assistant)
8. [From Dox to a Design Framework](#from-dox-to-a-design-framework)
9. [Try It Yourself](#try-it-yourself)

## Introduction

During my career as a software engineer, now over a decade long and preceded by many more years as a hobbyist programmer, a significant part of my time has been involved in requirements analysis and solution design.

A couple of years ago I had the chance to move into a solution architect role in an enterprise context, and that shift was both challenging and formative, giving me the opportunity to see firsthand how documentation is approached in more structured, formal settings.

Documentation has always been one of the less popular activities in software development. This was true in the past, when waterfall processes made it more or less mandatory, and is arguably even more so now that agile methodologies have [shifted the balance](https://agilemanifesto.org/#:~:text=Working%20software%20over%20comprehensive%20documentation) for good reasons.

Still, in regulated settings, where software and its evolution are governed by some central authority, agile has often been adopted more as a delivery framework than a genuine cultural shift, and a certain degree of documentation remains required in most cases.

With the rise of AI, we may now have the opportunity to finally close the documentation gap within the SDLC, leveraging agents to take care of the grunt work for us.

**Dox**, a notation for expressing requirements and other design concepts, is my attempt to reconcile two seemingly incompatible needs:

1. The need for meaningful documentation, or at least a minimum core of it;
2. The need to remain adaptable, without letting documentation overhead slow down development.

I originally came up with Dox as a convenient way to write baseline specifications for my hobby projects, used as a starting point for AI-assisted development in a vibe coding fashion. But then I realized it might have some real-world value, so I brought in the lessons learned from a few years of professional solutioning, and decided to publish it.

In this article, I'm going to describe the core principles underlying Dox.

## Hello Dox

Dox was designed with both AI agents and humans (me) in mind. It is based on plain text, embeddable in Markdown files, and deliberately avoids rigid hierarchies and rules, embracing ambiguity rather than forcing structure.

The most distinctive aspect of the notation, the one I find most interesting and fairly original, is its inspiration from the **[Six Thinking Hats](https://en.wikipedia.org/wiki/Six_Thinking_Hats)** model by Edward de Bono: a method for making explicit the perspective behind any information that shapes design choices. I use this method as a tool for surfacing bias that is often hidden throughout my design process.

This project is not limited to the conceptual level. In fact, after a first specification of the framework, I set up an agent skill called **[Dox Assistant](#the-dox-assistant)** to help me write and maintain Dox documents in a convenient way. Then, on top of Dox, I created a Solution Design template called **Dox9+** (Dox-nine-plus), inspired by [arc42](https://arc42.org) and intended as the foundation for a full-featured agentic documentation framework. 

You can find here the full [Dox specification](./../.dox/Dox.md) and the [Dox9+ template](./../.dox/Dox9+.md), which I'll cover in a separate article. For now, let's dive into the main concepts.

## Everything Is an Assertion

Any design documentation, no matter the field, is a collection of sentences that make claims about a system and its context. We call these sentences *assertions*. In general, the purpose, relevance and even the truth of each assertion are constantly evolving throughout the design process.

To capture this, Dox suggests a way to annotate assertions along three dimensions:

1. **Type**: what kind of sentence is this?
2. **Priority**: how important is it?
3. **Color**: which perspective produced it?

The notation is lightweight. A fully annotated assertion looks like one of the following examples.

> **⚪ [FR .M]** The system shall allow registered users to log in using their email and password.

> **⚪ [QFR .S]** The login process shall complete in under 2 seconds under normal network conditions.

> **⚪ [CTR Sec-1 .M]** As stated in our information security policy, the system must use OAuth 2.1.

> **🔵 [D NoSQL]** On 2026-01-15, after evaluating consistency and scalability trade-offs, we chose MongoDB over PostgreSQL to better handle the schema flexibility required by our domain model.

> **🔴 [Rsk Infra-1]** The platform team feels that our infrastructure may not scale properly, but this still needs to be investigated.

> **🟡 [O Cache]** Adding a caching layer could tactically mitigate the scalability concern in [Rsk Infra-1] while a more structural solution is evaluated.

> **🟢 [FR Coffee .C]** Our onboarding flow could automatically order a coffee for the new user upon completion, as a memorable first impression.

> **⚫ [Rsk Coffee]** Automating a physical coffee order introduces a dependency on a third-party delivery service, adding costs, operational complexity and potential failure points outside our control.

In the examples above, you can see a color, a type, an assertion identifier and a priority annotation, any of which may be omitted. Let's walk through each syntax component to make sense of them.

## Classifying Assertions

Dox defines sixteen assertion types. Rather than organizing them into a strict hierarchy, we treat them as composable attributes, like mixins or traits in object-oriented design. There are no fixed composition rules: the writer's common sense is the only guide.

| Type | Symbol | Description |
|---|---|---|
| **Assumption** | `A` | Something believed to be true, but not yet verified. Includes hypotheses, premises, preconditions. |
| **Fact** | `F` | Something known to be true with near-absolute confidence. Often a validated assumption. |
| **Constraint** | `C` | A fact that limits design freedom. Typically imposed from outside: regulations, policies, dependencies. |
| **Option** | `O` | A directional assumption representing something we could pursue. Implies a genuine free choice. |
| **Decision** | `D` | A commitment to pursue an option, at a given time and under specific circumstances. Should be tracked explicitly. |
| **Strategy** | `S` | A coherent ensemble of decisions oriented toward a specific outcome. |
| **Requirement** | `R` | Something considered necessary to achieve a result. A generic supertype. |
| **Functional Requirement** | `FR` | A product-level requirement describing behavior: what the system does and for whom. |
| **Technical Requirement** | `TR` | An implementation-level requirement describing how the system fulfills other requirements. |
| **Quality Requirement** | `QR` | A requirement describing a quality property of the system, whether functional or technical in nature. |
| **Business Requirement** | `BR` | A higher-level organizational need: economics, compliance, resources, methodology, stakeholder expectations. |
| **Goal** | `G` | A SMART objective tied to measurable outcomes. A specific subtype of BR. |
| **Debt** | `Dbt` | A known suboptimal situation accepted to meet a requirement under specific circumstances. Something to pay back later. |
| **Risk** | `Rsk` | A potential future problem to be aware of and mitigated. Often tied to debt, but can also arise from uncertainty. |
| **Open Point** | `Opn` | An unresolved issue that needs addressing before a decision can be made. |
| **Untyped** | `X` | Any useful assertion that doesn't fit neatly elsewhere. Can carry a freely chosen sub-type, eg. `[X-Idea]`. |

When we say that types are composable, it means that we can combine multiple symbols to express more complex types. For instance, in the example above, `QFR` equals `QR` + `FR`, which indicates a Functional Requirement that is also a Quality concern. Likewise, `CTR` equals `C` + `TR`, indicating a Technical Requirement that is also a Constraint.

By using these types Dox encourages making the lifecycle of assertions explicit, as a best practice. An assumption that gets validated becomes a fact. An option that gets chosen becomes a decision. An open point that gets resolved can become a requirement. These transitions should be tracked, so that the reasoning behind every design choice can be reconstructed over time.

Typing matters especially for constraints and assumptions: it is surprisingly common to mistake a design choice for a settled constraint, or to mistake an unvalidated assumption for a proven fact. Dox nudges you to be explicit, which helps you reason about the source of every claim.

## Prioritizing Assertions

This is probably the least innovative part of Dox: we rely on the well-known MoSCoW method for requirements prioritization.

> **⚪ [FR 1 .M]** The system must allow registered users to log in.

> **⚪ [FR 2 .S]** The system shall allow users to reset their password.

> **⚪ [FR 3 .C]** The system could support single sign-on.

> **⚪ [FR 4 .W]** The system will not support offline mode in the first release.

> **🟢 [FR Coffee ?]** The system could support remotely controllable coffee preparation.

Priority annotation is encouraged but not mandatory; when unspecified, we default to *should*. We can use the `?` marker to signal that priority is still under discussion, which is itself useful information.

For non-requirement assertions, a custom weight can express likelihood, confidence, or importance — whatever is meaningful in context.

> **🔴 [O Migration-1 .2]** Migrate the entire codebase to a microservices architecture.

> **🟡 [O Migration-2 .8]** Extract only the billing module as a first, isolated service.

> **⚫ [Dbt Secrets-1 .High]** Hardcoded API keys in the deployment scripts, accepted to speed up the initial release, now must be resolved with maximum priority before going to production.

## Putting On a Hat

This is the most interesting part of Dox — where Six Thinking Hats comes in.

This method, developed by [Edward de Bono](https://en.wikipedia.org/wiki/Edward_de_Bono), is a thinking methodology that separates different cognitive modes into six hats of different colors. The idea is that when a group discusses a problem, multiple thinking modes are in play simultaneously, and this collision often produces confusion rather than clarity. Wearing one hat at a time makes the thinking more structured and productive. 

If you've never come across this method before I encourage you to read the author's [wonderful book](https://en.wikipedia.org/wiki/Six_Thinking_Hats). It's something that anyone engaged in intellectual or knowledge work should do to sharpen their thinking (and relational) skills.

In practice, I find the method just as useful for individuals as for teams: it forces you to step back and ask the right questions about your own perspective and tendencies at the time.

Dox borrows this model not as a meeting facilitation technique, but as an annotation system for design information. Every assertion has a thinking mode that generated it; making that mode explicit adds a layer of meaning that neither the type nor the priority captures.

| Color | Mode | Best suited for |
|---|---|---|
| ⚪ **White** | Factual, objective, data-driven | Facts, constraints, mature requirements |
| ⚫ **Black** | Critical, cautious, risk-focused | Risks, debt, assertions that challenge others |
| 🔴 **Red** | Intuitive, emotional, instinctive | First impressions, gut-feel design choices |
| 🟡 **Yellow** | Optimistic, opportunity-focused | Options with strong potential upside |
| 🟢 **Green** | Creative, lateral, exploratory | Novel ideas, unconventional alternatives |
| 🔵 **Blue** | Structural, meta, process-oriented | Decisions about process, tracking, summaries |

Here are a few examples showing the visual gain that color annotation provides. It's the kind of insight you get at a glance.

> **🟡 [O]** We should consider replacing the synchronous API with an event-driven architecture. Even if it sounds like overkill for now, it would decouple our services and make it easier to scale as new consumers onboard.

> **⚫ [Rsk 1]** The third-party payment provider may introduce breaking changes within a short notice period.

> **🔴 [Opn 1]** This data model feels wrong, but I can't articulate why yet.

> **🔵 [D SSO]** On 2026-03-15 we decided to close this open point and mark the SSO requirement as Wont for v1.

> **🟢 [X-Idea]** What if the system had no login at all, and instead recognized users by how they type — their rhythm, their typos, their habits?

Color annotation gives us the opportunity, and the legitimacy, to formalize things that would normally go unwritten, bringing into the light what would otherwise stay invisible in the minds of the people designing the solution.

Colors are also particularly powerful as a diagnostic tool for our design process. A specification with too many ⚫ Black assertions may reflect excessive pessimism, or a team stuck in risk-avoidance mode. Too many 🔴 Red assertions signal that decisions are being driven by instinct rather than analysis. An abundance of 🟡 Yellow with few ⚪ White assertions suggests optimism that hasn't been validated yet.

That said, colors aren't mandatory, and shouldn't be used indiscriminately; consider reserving them for cases where they add real semantic value. 

As for types, Dox doesn't prescribe strict rules on how to use colors: everything is left to the designer's common sense. There are, however, some natural color/type mappings you may want to follow to ensure a minimum level of consistency (check out the full spec linked below for details).

## The Dox Assistant

At this point you should have a good grasp of the Dox principles. You may want to check out the full [Dox specification](./../.dox/Dox.md) for the complete usage guidelines.

Now it's time to put Dox into practice. You probably don't want to write Dox specifications manually. In that case, you can use the **[Dox Assistant](./../.dox/skills/dox-assistant/SKILL.md)** skill to help you write and maintain your documentation. You should be able to install the skill in any agent of your choice: please find some instructions in the related [Getting Started](./../.dox/DoxOps.md) section.

## From Dox to a Design Framework

As a simple notation, Dox is self-contained. You can use it in any Markdown file or document, without any additional tooling or process. But since the start of the project, it was clear to me that it could be used as the foundation to build something larger and potentially more valuable.

In real-world scenarios, the solution design process is usually more structured than a free-form collection of sentences. It typically involves multiple stages and follows well-defined flows and ceremonies, including the use of official templates, checklists, and documentation artifacts.

That is why I created **Dox9+** (Dox-nine-plus), a solution design template built on Dox notation and principles, inspired by [arc42](https://arc42.org) but organized differently — around a chronological flow that mirrors a standard design process, from business context, to functional definition, to technical strategy, to implementation specification. A full article covering Dox9+ in depth is coming soon. Meanwhile, you can find here the full **[Dox9+ template](./../.dox/Dox9+.md)**.

As the next step of this project, **DoxOps** is meant to be an agentic layer built around Dox: a set of agent skills for compiling, validating, and maintaining solution design documents throughout a project's lifecycle. The idea is that a specification written in Dox notation and structured according to Dox9+ is a natural fit for AI-assisted documentation workflows, in formal enterprise contexts as much as in individual projects. You can find an initial implementation of [DoxOps](./../.dox/DoxOps.md) here.

## Try It Yourself

Thank you for reading this far! 

I invite you to try using Dox on your own projects, leveraging it as a conceptual support throughout your design process, alone or alongside your AI agents of choice. If you'd like, you can contribute or leave feedback by opening an issue on the [GitHub](https://github.com/efchi/dox9plus) repo. It's much appreciated!

Dox, Dox9+ and DoxOps are open source, released under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).
