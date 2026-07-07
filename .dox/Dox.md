# Dox

| | |
|---|---|
| **Version** | 1.8.1 |

**Dox** is a lean documentation notation that aims to establish meaningful conventions for writing specifications, enabling lightweight solution design for both humans and machines.

Dox follows a convention-over-prescription principle, encouraging best practices rather than imposing formal rules. What makes it distinctive is the application of Edward de Bono's *Six Thinking Hats* method to information that emerges during the design process, making implicit perspectives explicit and surfacing bias in documentation.

Dox is distributed under CC BY-SA 4.0 — see [LICENSE.md](./LICENSE.md)

## Table of Contents

1. [Introduction](#introduction)
1. [Type](#type)
1. [Priority](#priority)
1. [Color](#color)
1. [Conclusion](#conclusion)
1. [Appendix A. Concept Tree](#appendix-a-concept-tree)
1. [Appendix B. Design Process](#appendix-b-design-process)
1. [Appendix C. Requirements Dimensions](#appendix-c-requirements-dimensions)
1. [Appendix D. Color Mapping](#appendix-d-color-mapping)
1. [Appendix E. Questions](#appendix-e-questions)

## Introduction

Specifications are generally built around sentences that express claims about the system or its context. We call these sentences *assertions*.

In Dox, assertions can be annotated in meaningful ways to express their value across different dimensions. We are mainly interested in three dimensions:

1. **Type**: which is the function of an assertion?
2. **Priority**: how important is an assertion?
3. **Color**: which perspective does an assertion come from?

Following the [Show, don't tell](https://en.wikipedia.org/wiki/Show,_don%27t_tell) principle, we'll walk through each dimension by example, favoring concrete usage over abstract definitions.

## Type

We use the following types to classify assertions:

1. **Assumption**. Something that is believed to be true, but needs to be verified. Often used as a starting point for reasoning, or as a time saver to avoid research that can be deferred. Assumptions include hypotheses, conjectures, premises, preconditions and so on.

	> **[A]** The user has an internet connection.

2. **Fact**. Something that is known to be true without any doubt, or at least with a near-absolute level of confidence. A validated assumption.

	> **[F]** A minute is 60 seconds.

3. **Constraint**. A fact that limits our degrees of freedom when formulating a solution. Constraints are often imposed from the outside and include rules, regulations, policies and anything which is not under our control or negotiable. It is important to distinguish between real constraints and those which are actually assumptions.

	> **[C]** We must comply with the GDPR when handling user data.
 
4. **Option**. A directional assumption representing something that we can choose to pursue or not. These include possibilities, opportunities, alternatives, candidates, etc. Options are always on the table, but they should be checked against facts and constraints to determine whether they are viable or not. It is important to distinguish between real options and those which are actually constraints (an option implies a free choice). Pursuing an option can lead to new assumptions, facts, constraints, etc.

	> **[O 1]** We could outsource our data to a third party.

	> **[O 2]** We could keep our data on our own servers.
	
5. **Decision**. A fact stating that we have committed to pursuing an option, at a given time and under specific circumstances. Decisions are driven by assumptions, facts and constraints; they are the result of a decision-making process and they should be tracked properly, ie. using *decision records*.

	> **[D 1]** After thoughtful consideration of all legal aspects, we decided to outsource our data to a third party.

	> **[D 2]** We decided to build our app using a proprietary no-code tool in order to speed up development, in spite of potential vendor lock-in and additional costs.

6. **Strategy**. An ensemble of cohesive decisions towards a specific result, also known as a *plan*. Often, we use the term *tactic* when pursuing a short-term solution.

	> **[S]** In order to achieve a successful product launch, we decided to narrow our application scope to focus on a specific niche market. We decided to **[D 1]** target independent coffee shop owners as our primary user base, and to **[D 2]** exclude enterprise clients from the first release.

7. **Requirement** or *solution requirement*. Something that we consider necessary to achieve a specific result. We classify requirements in sub-categories as follows, but we prefer to be flexible and pragmatic: our classification is neither mandatory nor mutually exclusive, and we leave space for interpretation and other categories as well. Note that constraints are requirements too.

	> **[R]** The application should do/be something.

8. **Functional Requirement**. A requirement that describes a specific behavior or function of the system. This includes features, use cases, user stories, etc. FRs are *product requirements*: they generally originate from a design and discovery process focusing on interactions with external actors, such as users or other systems. FRs focus on the *who* and *what*.

	> **[FR 1]** The application shall allow plumbers to register.

	> **[FR 2]** The application shall notify our CRM whenever a new user completes the registration process.

	Some constraints can be classified as FRs: we call them *functional constraints*.

	> **[CFR 3]** As stated by our GDPR policy, the application must provide a user-consent management UI.

	When useful, we encourage the use of Gherkin notation (BDD) to effectively express FRs.

	> **[FR Pwd]** Given a registered user | when they request a password reset | then the system shall send a reset link to their email.

9. **Technical Requirement**. A requirement that describes a technical aspect of the system, such as architecture, infrastructure, tools, technologies, etc. TRs are *implementation requirements*: they typically originate from an implementation strategy and exist to fulfill requirements from other categories. TRs focus on the *how*.

	> **[TR 1]** The application shall use an IPaaS to send notifications to our CRM.

	> **[TR 2]** The application shall use serverless architecture to satisfy the high-concurrency requirement expressed in [QTR 3].

	Some constraints can be classified as TRs: we call them *technical constraints*.

	> **[CTR 3]** As stated in our information security policy, the application must use OAuth 2.1.

10. **Quality Requirement**. A requirement that describes a quality or property of the system, also known as a non-functional or cross-functional requirement. QRs can be *product requirements* (functional quality requirements) or *implementation requirements* (technical quality requirements) depending on their subject.

	> **[QR 1]** The application should be fast and easy to use.

	> **[QFR 2]** The password reset procedure shall take no longer than 2 minutes.

	> **[QTR 3]** The system shall be able to handle 1000 concurrent users without performance degradation.

	Some constraints can be classified as QRs: we call them *quality constraints*.

	> **[CQR 4]** As stated in our content policy, the application must comply with WCAG 2.1 accessibility standards.

11. **Business Requirement**. A requirement that describes a non-functional and non-technical need that the system, product, project or process should satisfy. BRs span a wide range of concerns, including economics, compliance, resources, timeline, methodology, stakeholder expectations, etc. Some BRs can involve quality as well.

	> **[BR 1]** The system shall be developed by a team of 3 people max.	

	> **[QBR 2]** As stated in our guidelines, we should use the Dox framework to write documentation in a clear and effective way.

	Some constraints can be classified as BRs: we call them *business constraints*.

	> **[CBR 3]** The system must cost no more than $10,000 to develop and maintain.
	
12. **Goal**. A specific, measurable, achievable, relevant and time-bound (SMART) objective that we want to achieve. A goal helps us to set realistic expectations on the outcomes of our project and to keep track of progress. Goals are BRs, but not all BRs are goals.
	
	> **[G 1]** Launch the MVP within 3 months.

	> **[G 2]** Generate at least $100,000 in revenue within the first year of launch.

13. **Debt**. A situation that we know is suboptimal, but we are willing to accept it in order to meet one or more requirements under specific circumstances. Debt can arise from inside (eg. tactical decisions, changing requirements, missing documentation, etc) or from outside (deprecated dependencies, security updates, etc). It is something that we know we'll have to pay back in the future.

	> **[Dbt 1]** Unsecure storage of secret keys, in order to speed up development.

14. **Risk**. A potential problem that could arise in the future, which we should be aware of and try to mitigate. Risks are deeply tied to debt, but not every risk comes from debt: some can arise from uncertainty (unvalidated assumptions, changing requirements, dependency on third parties, etc) or other factors.
	
	> **[Rsk 1]** The third-party API may introduce latency issues that we don't control.
	
	> **[Rsk 2]** The required service may be not available 100% of the time.
	
	> **[Rsk 3]** If we don't fix the security issue from [Dbt 1] before launch, our compliance department will not approve our product.

15. **Open Point**. An unresolved issue that needs to be addressed before we can move forward with a specific decision or strategy. Open points generally arise from unvalidated assumptions and options.
	
	> **[Opn 1]** Evaluate the viability of using server-based architecture given the high concurrency requirement (QTR 3) and budget allocation policies.

16. **Untyped**. Any useful assertion that doesn't fall into any of the previous categories. It could be a thought, idea, citation, sensation, unanswered question, event, achievement, etc. It can be annotated with any freely chosen sub-type.

	> **[X]** This is an unnamed and untyped assertion.

	> **[X-Sec 1]** John thinks that it's a good idea to prioritize time-to-market over security, but I'm not sure about it.
	
	> **[X-Quote 1]** A good specification is not one that cannot be added to, but one that cannot be taken away from. — Claude, 2026.

### Notes on Type Usage

As shown above:

1. Numbering assertions is not mandatory, but helps to reference them across the documentation. We can use nested numbering for a more structured format. Use the notation you prefer: `[C 1.2.3]` `[R 1/2/3]` `[FR Gui.X.Y]` etc.

2. We can combine types together to express more complex ideas. Treat assertions like mixins that can have multiple traits. There are no strict rules for this, try to keep consistency though: use common sense to avoid ambiguity (use the symbol `+` when useful).

	> **[CQBR]** The application must comply to ISO 27001: this is a mandatory quality requirement coming from our business.

	> **[CQFR]** As stated in our SLA, the onboarding process must be completable by a new user in less than 5 minutes. This is an essential functional quality constraint.
	
	> **[Dbt+Rsk]** Unsecure storage of user credentials.

	See [Appendix A](#appendix-a-concept-tree), [Appendix B](#appendix-b-design-process) and [Appendix C](#appendix-c-requirements-dimensions) for more indications on how to compose requirements.

3. Use untyped assertions when not yet sure which type to assign. Types can always be refined later.

## Priority

In our specs, we are interested in capturing the importance of an assertion. This is especially true for requirements, which should be prioritized to streamline the design process.

For requirements, we use the **MoSCoW** method to express priority:

1. **Must** and **must not**. The requirement is non-negotiable and must be satisfied. Constraints always fall in this category, but not every must-have is a constraint: some are deliberate design choices.

	> **[FR .M]** The system must allow registered users to log in.

	> **[FR .M]** The system must not allow unregistered users to log in.

2. **Should** or shall. Important and expected, but not critical. Should be satisfied if possible.

	> **[FR .S]** The system shall allow users to reset their password.

3. **Could (C)**. Desirable but not necessary, nice-to-have. Could be satisfied if time and resources allow.

	> **[FR .C]** The system could support single sign-on (SSO).

4. **Wont (W)**. Explicitly out-of-scope for now, but may be reconsidered in the future.

	> **[FR .W]** The system will not support offline mode in the first release.

For other types of assertions, we may want to assign a score or weight denoting priority, importance, likelihood, confidence, etc.

> **[O .2]** Use a local in-memory DB to store user data.

> **[O .6]** Use a SaaS DB to store user data.

> **[O .8]** Use a cloud-based distributed DB to store user data.

> **[Dbt .High]** Hardcoded API keys are to be removed ASAP.

### Notes on Priority Usage

1. Priority annotation is encouraged but not mandatory. When unspecified, the priority for a requirement should be inferred from the assertion itself. If the assertion does not explicitly state a priority, we assume Should (S).

2. Use the symbol `?` to handle cases where priority is still under evaluation.

	> **[FR Ux-Bio ?]** The application might allow users to log in via biometric authentication, but we are still discussing it for budget reasons.

3. Wont (W) helps to clearly identify the solution boundary during the design phase. Use it to communicate the scope of the project and to align stakeholder expectations.

4. A constraint should always be a Must (M). Use this heuristic to tell real constraints from ones which are actually choices.

5. Again, there are no strict rules: use common sense to maximize meaning and effectiveness.

## Color

We draw inspiration from the **Six Thinking Hats** method by Edward de Bono to characterize sentences, focusing on the *thinking mode* that generated them. These annotations can be used freely for any assertion type.

1. **White**. Factual and objective: based on data, information, or evidence. Suited for facts, constraints and other assertions that emerged as established outcomes of the design process.

	> **⚪ [F]** Statistical analyses show that 70% of our users access the platform via mobile.

2. **Black**. Critical and cautious: focusing on problems and reasons why something may go wrong. Suited for risks, debt, and any assertion that is meant to challenge another.

	> **⚫ [Rsk]** The third-party API may introduce latency issues that we don't control.

3. **Red**. Intuitive and emotional: expressing a feeling, instinct, or reaction without the need for justification. Suited for representing first impressions and intuitive or impulsive design choices.

	> **🔴 [A]** This approach feels overly complex for our use case.

4. **Yellow**. Optimistic and constructive: looking for benefits, opportunities and reasons why something could work. Suited for spotlighting options that could provide a tactical or strategic added value.

	> **🟡 [O]** Outsourcing data storage could significantly reduce our infrastructure costs.

5. **Green**. Creative, introducing new ideas and possibilities — even if they sound absurd or contradict assumptions, facts, and constraints. This mode enables *lateral thinking*, innovation and exploration.

	> **🟢 [O]** We could consider a hybrid architecture involving pigeons to deliver asynchronous messages.

6. **Blue**. Structural and meta, these assertions are about the process itself: organizing thinking, setting goals, summarizing conclusions, etc. Suited for reflective statements about the design process as a whole, eg. for requirements tracking.

	> **🔵 [D]** On 1/1/2026 we decided to discard the password reset FR, marking it as a Wont.

### Notes on Color Usage

1. Color is particularly useful to surface cognitive bias in a document. A spec with too many Blacks may reflect excessive pessimism, too many Yellows may signal overconfidence, too many Reds may imply uninformed decisions.

2. Some combinations feel natural (see [Appendix D](#appendix-d-color-mapping)) but trying to assign the right color to every assertion is not really needed. Use color where it adds genuine semantics or value. As always, rely on common sense.

## Conclusion

Now that we have shown Dox usage by example, let us conclude with a recap of its core principles.

1. **Design agility**. Dox is intentionally non-prescriptive, favoring meaning and effectiveness over formality. Use it as a thinking tool, not as a self-imposed constraint or dogma.

2. **Information usability**. Our ultimate goal is to keep information in a convenient semi-structured format, ready to communicate, query and navigate.

3. **Decision tracking**. Like source code, software specifications are alive: requirements and decisions are always changing. We commit to tracking all changes to Dox files, so that the reasoning behind every design choice can be traced and reconstructed over time.

4. **Solution-oriented**. Dox can be used to help designers and architects write Solution Design documents as an alternative to other notations or templates, such as UML or arc42. Check out the [Dox9+ Template](./Dox9+.md) as a reference for applying Dox to enterprise-grade specifications.

## Appendix A. Concept Tree

The following tree organizes the types of Dox into a hierarchy. It is meant as a 2D conceptual map rather than a strict taxonomy, our types can in fact behave as attributes rather than classes — see [Appendix B](#appendix-b-design-process) and [Appendix C](#appendix-c-requirements-dimensions).

```
Assertion
├── Untyped
├── Assumption
│   └── Option
├── Fact
│   ├── Constraint
│   ├── Decision
│   │   └── Strategy
│   ├── Debt
│   ├── Risk
│   └── Open Point
└── Requirement
    ├── Business
    │   └── Goal
    ├── Product
    ├── System
    └── Quality
```

## Appendix B. Design Process

In general, requirements don't appear all at once: they emerge gradually through a design process that typically unfolds in *phases*. Each phase has a natural focus, but any type of assertion can surface at any point. Here we attempt to describe the mental and organizational model that underlies the requirements lifecycle.

### Phase 1: Business Analysis

The process usually starts with some business ideas, often accompanied by a cloud of immature assertions. This phase is meant to identify BRs and set the project goals. This is the fuzziest phase, where the problem space is being defined rather than solved. In fact, a key activity here is pruning, starting from unvalidated assumptions and options about our problem/solution and deciding which ones are worth promoting to formal requirements.

> **[AG]** Our system should make an enormous amount of money.

### Phase 2: Functional (or Product) Analysis 

Once the business landscape is clearer, assumptions and options get transformed into FRs. This phase focuses on defining what the system should do and for whom, typically involving product designers and users. Here too, implicit assumptions and options are constantly being evaluated and resolved.

> **[AFR]** Our system should be able to make coffee.

### Phase 3: Technical (or System) Analysis

Once core FRs are established, the team moves to defining how to technically satisfy them. This phase is where a *solution strategy* emerges and where TRs are produced. Here, architectural and implementation choices are made, and explicitly documented as ADRs (Architectural Decision Records).

> **[DTR]** On 1/1/2026 we decided to use AWS to host our infrastructure.

> **[ATR]** Our system should use S3 to store coffee pods.

### Notes on Requirement Lifecycle

1. Assertions of any type can emerge at *any* phase of the process. This is especially true for constraints and QRs, which are cross-cutting and not tied to a specific phase or requirement type.

2. Note how, in the previous examples, we freely mixed assumption and decision annotations with requirements, treating them as traits like we did before with constraints and QRs.

3. The process described above is intended to be iterative. There is no fixed path: we know that we will have to proceed back and forth as unforeseen issues arise.

### Example: From Assumptions to Requirements

Formalizing assumptions into requirements is a design decision itself. These choices don't always need to be maintained inline in the spec, but they should be recorded in a changelog for traceability.

> **[ABR ?]** Our system is meant to solve the chicken and egg problem.

> **[Opn]** Validate assumption [ABR].

> **[DBR]** On 1/1/2026 we decided to give up on the chicken and egg problem.

> **[BR .W]** Solve the chicken and egg problem.

## Appendix C. Requirements Dimensions

In Dox, requirements are treated along three independent dimensions, across all the design phases:

1. **Nature**. What does a requirement describe?

	1. A behaviour or functionality (FR)
	1. A technical or architectural aspect (TR)
	1. A quality property or attribute (QR)
	1. A higher-level request from our organization (BR)
	
2. **Ownership**. Who owns a requirement? Where is it located in the process? 
	
	1. Business stakeholders: *business requirement* (BR)
	1. Product designers and users: *product requirement* (PR)
	1. Developers, engineers and architects: *implementation requirement* (IR)

3. **Degree of freedom**. Was the requirement imposed or chosen?

	1. Imposed. The requirement is a constraint (C)
	1. Chosen. The requirement is not a constraint, but an implicit or explicit decision made during the design process.

For *business requirements*, (1.iv) and  (2.i) are essentially the same — that's why we tolerate the naming overlap — but in general the three dimensions are independent. 

For instance, a QR can describe a desirable functional property available to the user, making it a product-level concern, or a purely technical one like throughput or uptime, placing it at the system-level. Likewise, any requirement can be a constraint, independently of other types involved.

This means that our types are not really *types* in a strict hierarchical sense, but rather *orthogonal attributes* that any assertion can present. That's why we made an analogy with mixin/traits before.

The following table shows how QR and C can compose with the primary types:

| | Business (BR) | Product (PR) | Implementation (IR) |
|---|---|---|---|
| **Primary Type** | BR | FR | TR |
| **+ Quality (QR)** | QBR | QFR | QTR |
| **+ Constraint (C)** | CBR | CFR | CTR |
| **+ Both (QR, C)** | CQBR | CQFR | CQTR |

But again, the naming does not follow strict rules. We could annotate an assertion using just QR or C when the underlying functional or technical nature is still unclear, or even using PR or IR when the same uncertainty applies to quality or constraint aspects, without specifying the full and exact requirement type.

The same composition principles apply to other types as well, as long as consistency is maintained and valuable meaning is added.

## Appendix D. Color Mapping

This section contains a table mapping the most natural color/type pairings, as a quick guide for annotation. 

During the design process, we should sometimes stop and ask ourselves: which thinking mode produced this assertion? It can be a useful heuristic to better understand the origin of certain choices.

| | White | Black | Red | Yellow | Green | Blue |
|---|---|---|---|---|---|---|
| Untyped		|⚪	|⚫	|🔴	|🟡	|🟢	|🔵 |
| Fact			|⚪	|⚫	|🔴 |	|	|	|
| Constraint	|⚪	|⚫	|🔴 |	|	|	|
| Assumption	|	|	|🔴	|🟡	|🟢	|	|
| Option		|	|	|🔴	|🟡	|🟢	|	|
| Requirement	|⚪	|	|🔴 |	|	|	|
| Goal			|⚪	|	|🔴	|🟡	|	|	|
| Decision		|	|	|🔴	|	|	|🔵 |
| Strategy		|	|	|🔴	|	|	|🔵 |
| Open Point	|	|	|🔴	|	|	|🔵 |
| Debt			|⚪	|⚫	|🔴 |	|	|	|
| Risk			|⚪	|⚫	|🔴 |	|	|	|

Color annotation is especially useful for assumptions and options, which are often implicit and unspoken, but also to spot unvalidated facts, false constraints and requirements introduced without a proper discussion. 

Our map is meant to highlight that:

1. 🟡 Yellow and 🟢 Green modes propose assertions that eventually need to be validated.

2. ⚫ Black mode doesn't propose anything: it only questions and challenges existing assertions.

3. 🔴 Red mode can impact any aspect of the process: instinct can influence goals, decisions and strategies. Make sure that such assertions are evaluated with a neutral disposition and in an informed way.

4. Ideally, approaching the end of the process, requirements should tend toward ⚪ White as an indicator of maturity and analysis effort, while the spec gets enriched with 🔵 Blue assertions.

## Appendix E. Questions

### Can Dox be used for non-software projects?
 
Yes, and this is encouraged. Dox should apply to virtually any design or decision-making process. The framework aims to be domain-agnostic by nature.
 
### Can I invent new types?
 
Yes, try to follow the [open-closed principle](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle). Feel free to introduce new types but avoid redefining or overloading the core types defined in this document. Use the Untyped type as an alternative approach (eg. `[X-MyType]`).
 
### How granular should assertions be?
 
There is no fixed rule: this is left to the designer's judgement and context. A useful heuristic: an assertion should express one coherent claim. When in doubt, split.
 
### Do I need to use the full notation (eg. CQFR)?
 
Not really, you can keep it simple, especially in early phases. The full notation is most useful when a requirement is consolidated and its attributes are well understood. Start with primary types and refine later.
 
### How do I handle conflicting assertions?

You probably want to treat them as mutually exclusive options and surface the conflict explicitly. Annotate them as `[O ALT.A]` and `[O ALT.B]` documenting the trade-offs, resolve the conflict through a decision `[D]` when ready.
 
### How do I know when a spec is done?
 
Dox does not prescribe a Definition of Done. However, you are encouraged to formalize your own criterion based on your context. You could also treat it as a `[G]` — a meta-requirement on the design process.

### Is ambiguity an issue?
 
Not necessarily. Dox relies on the reader's (human or machine) ability to resolve ambiguity from context. Forcing excessive precision too early can hinder our design process: embrace ambiguity where it is productive, reduce it where it matters.
