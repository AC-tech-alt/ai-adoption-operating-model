# AI Adoption Operating Model

A worked example: embedding AI into executive reporting and review workflows so it changes how the work gets done, not just how the demo looks. It covers the operating model and the technical controls underneath it: architecture, evaluation, risk tiers, and monitoring.

**Status:** early / worked example. This is a stress-test-me framework, not a finished standard. Push on it.

## The problem in one line

"We piloted AI" and "AI is how the work gets done" are constantly reported as the same milestone. They are not.

A pilot proves a tool can do something. It does not prove anyone's Monday changed, or that the output is reliable enough to act on. Most AI initiatives stall in that gap: a successful demo, a status field that says "deployed," and a team still doing the work the old way in a spreadsheet next to it.

## What this repo is

A plain-language operating model for taking an AI capability from idea to relied-upon, value-producing use inside an operations organization. It is built on the same backbone as my earlier models:

**Business Problem → Initiative → Workflow → Execution Plan → Field Readiness → Evidence → Adoption → Value Realization**

The worked example is an illustrative operations organization bringing AI into two places:

1. Executive reporting (recurring summaries that leaders use to make decisions)
2. Intake and review queues (high-volume work that needs consistent first-pass triage)

The scenario is illustrative. Numbers and thresholds are starting points to tune, not benchmarks.

## Two halves that have to work together

**The operating half** decides whether people actually change how they work.
**The technical half** decides whether the output deserves to be trusted.

| Question | Where it is answered |
|---|---|
| Is the output reliable enough to release? | [Evaluation](docs/evaluation.md) |
| How is it wired in, and what can go wrong? | [Technical architecture](docs/technical-architecture.md) |
| How much oversight does each use case need? | [Risk tiers](docs/risk-tiers.md) |
| How do we keep it good after launch? | [Operations and monitoring](docs/operations-monitoring.md) |
| Are people really working this way? | [Adoption and value](docs/adoption-and-value.md) |

## The core idea: four columns, not one

Most status reports collapse an AI initiative into a single field. This model keeps four separate:

| Column | Question it answers | Typical false signal |
|---|---|---|
| Deployed | Is it live in the system? | "Launched" on the status slide |
| Used | Are people starting real tasks in it? | Logins, training attendance |
| Relied on | Has the old path actually stopped? | Parallel spreadsheet still running |
| Valued | Did a decision or outcome improve? | Hours saved with no change in decisions |

A leader who cannot say which column an initiative is in does not know whether it worked.

## Five workflows

1. [Use-Case Selection and Intake](docs/workflows.md#1-use-case-selection-and-intake)
2. [Embedded Build in the System of Record](docs/workflows.md#2-embedded-build-in-the-system-of-record)
3. [Human Review and Override](docs/workflows.md#3-human-review-and-override)
4. [Rollout and Field Readiness](docs/workflows.md#4-rollout-and-field-readiness)
5. [Adoption and Value Measurement](docs/workflows.md#5-adoption-and-value-measurement)

Each workflow has its own Execution Plan, Field Readiness standard, Evidence, and an explicit Adoption threshold.

## Repo map

- [`docs/model.md`](docs/model.md): the problem, the initiative, and how the chain fits together
- [`docs/workflows.md`](docs/workflows.md): the five workflows in full
- [`docs/technical-architecture.md`](docs/technical-architecture.md): reference architecture, data contracts, and failure modes
- [`docs/evaluation.md`](docs/evaluation.md): golden sets, severity-weighted scoring, and staged release gates
- [`docs/risk-tiers.md`](docs/risk-tiers.md): matching controls to stakes, plus designing against automation bias
- [`docs/operations-monitoring.md`](docs/operations-monitoring.md): monitoring, incident response, change control, and ownership
- [`docs/adoption-and-value.md`](docs/adoption-and-value.md): the four columns, thresholds, and how to report them
- [`examples/pressure-test.md`](examples/pressure-test.md): a live scenario that stress-tests four stresses at once and shows where the model bends

## How to use it

- Read `docs/model.md` first (five minutes).
- Assign your use case a tier with `docs/risk-tiers.md`, then work through the gates in `docs/evaluation.md`.
- Run your initiative through the four columns in `docs/adoption-and-value.md`.
- Use `examples/pressure-test.md` as a template for stress-testing your own rollout before leadership does it for you.

## Scope and limits

- This is an operating and quality model, not legal, security, or regulatory advice.
- It is tool-agnostic. It does not recommend specific vendors or models.
- All figures are illustrative. Set real thresholds with the people who own the work.

## Related work

- [business-enablement-concept-model](https://github.com/AC-tech-alt/business-enablement-concept-model)
- [grant-operations-infrastructure-model](https://github.com/AC-tech-alt/grant-operations-infrastructure-model)
- [client-engagement-leadership-model](https://github.com/AC-tech-alt/client-engagement-leadership-model)

## Feedback wanted

If you run operations or lead AI programs, tell me where this breaks. Open an issue or message me. The pressure-test document is the best place to start.
