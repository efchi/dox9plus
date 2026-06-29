# Dox9+ Framework

The **Dox9+ Framework** is an agile system for writing and maintaining solution
design documentation. It combines a lightweight notation for expressing design
information, a structured template for solution design documents, and an agentic process that support writing and validating them.

The project is composed of three parts:

- **[Dox](#dox)**, the foundational notation used to express requirements, decisions and other types of assertions.
- **[Dox9+](#dox9)**, a Solution Design template built on Dox
  and inspired by [arc42](https://arc42.org), which includes conventions to guide document writing and evaluate the soundness of a specification over time.
- **[DoxOps](#doxops-agents)** agents, a set of agent skills for compiling
  the Dox9+ template following a well-established documentation
  process.

Dox, Dox9+ and DoxOps are distributed under CC BY-SA 4.0 — see [LICENSE.md](./LICENSE.md).

## Getting Started

To use the framework in a project:

1. Copy the entire `.dox` folder into your project root.
2. Instruct Claude Code (or any other agent of your choice) to look for skills inside `.dox/skills/`. You can do this by embedding the contents of [CLAUDE.md](./CLAUDE.md) into the CLAUDE.md file inside your project root.
3. Start with the Bootstrapper agent, which creates a
   `solution-design/` workspace with an empty, ready-to-fill Dox9+
   template inside.
4. From there, use the other agents to support the writing, maintenance
   and evaluation of your project's Solution Design — see [DoxOps](./.dox/DoxOps.md).

## Framework Components

### Dox

**Dox** is a documentation notation that establishes meaningful
conventions for writing specifications, enabling leaner solution design
for both humans and machines. It follows a convention-over-prescription
principle: rather than imposing formal rules, it encourages best
practices and applies Edward de Bono's *Six Thinking Hats* method to
surface implicit perspectives and bias in design documentation.

The latest version is [Dox v1.7.6](./.dox/Dox.md).

### Dox9+

**Dox9+** is a Solution Design template inspired by [arc42](https://arc42.org),
built on Dox notation. Unlike arc42, it is organized around a
chronological flow that mirrors the design process: from business
context, to functional definition, to technical strategy, to
implementation specification. Reading the document from beginning to
end should tell a coherent story of how a problem was understood and
how a solution was shaped to address it.

Dox9+ is primarily focused on the technical dimension of a solution.
Business and functional chapters are treated as prerequisites and
context, while the core design effort documented is architectural and
systemic. The framework defines a maturity model — available in two
variants, Top-Down and Bottom-Up — to calibrate documentation effort to
the actual needs of a project, and to support incremental, agile
solutioning.

The latest version is [Dox9+ v0.7.9](./.dox/Dox9+.md).

### DoxOps Agents

**DoxOps** is the agentic process built around Dox9+: a set of skills that turn the template into a working framework for writing,
maintaining, and validating Solution Design documentation, in support
of developers and architects working in enterprise and non-enterprise
contexts alike.

See [DoxOps](./.dox/DoxOps.md) for a description of available agents and related process.
