# Model: from business problem to value realized

This page walks the chain once, using the illustrative scenario.

## Scenario (illustrative)

An operations organization supports executive leadership across several regions. Two recurring pain points:

- Leaders receive recurring reports that take days of manual assembly and arrive after the moment to act has passed.
- A high-volume intake queue gets uneven first-pass review, so similar items are handled differently depending on who picks them up.

Leadership wants to use AI to improve both. The risk is the usual one: a pilot that demos well and changes nothing.

## 1. Business Problem

State the problem as a decision or outcome, not a tool.

- Weak: "We need an AI summarizer."
- Strong: "Leaders decide too late because reports take days to assemble, and the same request gets different answers depending on the reviewer."

If the problem statement names a technology, the initiative is already off course.

## 2. Initiative

The named, owned effort that addresses the problem. An initiative has:

- A single accountable owner (a person, not a team)
- A baseline measured before anything is built
- A defined end state described in terms of behavior ("the old report is retired"), not delivery ("the tool is live")

## 3. Workflow

The repeatable sequence of work the initiative changes. This model uses five (see [workflows.md](workflows.md)). A workflow is not adopted because it exists. It is adopted when people run it without being reminded.

## 4. Execution Plan

For each workflow: who does what, in what order, by when, with what dependencies. An execution plan that cannot name an owner for each step is a wish list.

## 5. Field Readiness

The standard the people closest to the work must meet before the workflow counts as ready. Training attendance is not field readiness. The test is whether someone can complete a real task, unassisted, using the new workflow.

## 6. Evidence

What proves each stage. Evidence is observed behavior or data, not a status update. Examples: task logs showing work starting in the tool, the date the old path was retired, override records with reasons.

## 7. Adoption

The explicit threshold at which a workflow counts as truly in use. Set it before rollout, with the owner, so it cannot be redefined afterward to look successful.

## 8. Value Realization

Whether a decision or outcome actually improved against the baseline. Hours saved is an input. A faster, better decision is the result.

## Where the technical controls fit

The chain above is the operating spine. Four technical pieces plug into it:

- **Risk tier** is assigned at Initiative intake and sets how much oversight the Workflows need ([risk-tiers.md](risk-tiers.md)).
- **Architecture and data contracts** shape the Workflow build ([technical-architecture.md](technical-architecture.md)).
- **Evaluation gates** are the Evidence required before Field Readiness can be declared ([evaluation.md](evaluation.md)).
- **Monitoring and change control** keep Adoption and Value Realization honest after launch ([operations-monitoring.md](operations-monitoring.md)).

## The rule that holds it together

Never let a later stage be reported as complete because an earlier stage is. Built is not ready. Ready is not adopted. Adopted is not valuable. Each gets its own evidence.
