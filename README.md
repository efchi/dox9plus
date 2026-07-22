# Dox9+ Framework

The **Dox9+ Framework** is a lean system for writing and maintaining solution design documentation. It combines a lightweight notation for expressing design information, a structured template for solution design documents, and an agentic process that support writing and validating them.

The project is composed of three parts:

- **[Dox](#dox)**, the foundational notation used to express requirements, decisions and other types of assertions, inspired by the *Six Thinking Hats* method
- **[Dox9+](#dox9)** (Dox-nine-plus), a Solution Design template built on Dox
  and inspired by [arc42](https://arc42.org), which includes conventions to guide document writing and evaluate the soundness of a specification over time.
- **[DoxOps](#doxops-agents)** agents, a set of agent skills for compiling the Dox9+ template following a well-established documentation process.

Dox, Dox9+ and DoxOps are distributed under CC BY-SA 4.0 — see [LICENSE.md](./LICENSE.md).

## Getting Started

To start using the framework with the help of agent skills, please follow the instructions available in the [DoxOps](./.dox/DoxOps.md) page. You can also use the framework manually, following the conventions described in the [Dox specification](./.dox/Dox.md) and the [Dox9+ template](./.dox/Dox9+.md).

## Framework Components

### Dox

**Dox** is a documentation notation that establishes meaningful conventions for writing specifications, enabling leaner solution design for both humans and machines. It follows a convention-over-prescription principle: rather than imposing formal rules, it encourages best practices and applies Edward de Bono's *Six Thinking Hats* method to surface implicit perspectives and bias in design documentation.

The latest version is [Dox v1.8.1](./.dox/Dox.md).

### Dox9+

**Dox9+** is a Solution Design template inspired by [arc42](https://arc42.org), built on Dox notation. Unlike arc42, it is organized around a chronological flow that mirrors the design process: from business context, to functional definition, to technical strategy, to implementation specification. Reading the document from beginning to end should tell a coherent story of how a problem was understood and how a solution was shaped to address it.

The framework defines a maturity model — available in two variants, Top-Down and Bottom-Up — to calibrate documentation effort to the actual needs of a project, and to support incremental, agile solutioning.

The latest version is [Dox9+ v1.0.4](./.dox/Dox9+.md).

### DoxOps Agents

**DoxOps** is the agentic process built around Dox9+: a set of skills that turn the template into a working framework for writing, maintaining, and validating Solution Design documentation, in support of developers and architects working in enterprise and non-enterprise contexts alike.

See [DoxOps](./.dox/DoxOps.md) for a description of available agents and related process.

## Writings

- July 2026: *[Introducing Dox: a lean notation to guide solution design, inspired by Six Thinking Hats](./.pub/introducing-dox/introducing-dox.md)* — [Hashnode](https://efchi.hashnode.dev/introducing-dox-a-lean-notation-to-guide-solution-design-inspired-by-six-thinking-hats), [Medium](https://medium.com/@efchi/introducing-dox-a-lean-notation-to-guide-solution-design-inspired-by-six-thinking-hats-0caa54ce528a)
- July 2026: *[Vibecoding a browser-game PoC in less than 3 hours, aided by Dox](./.pub/vibecoding-bsj/vibecoding-bsj.md)*
