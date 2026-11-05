# Operations and monitoring: keeping it good after launch

Launching is the start of the work. This page covers what to watch, who owns it, and what to do when something goes wrong. Thresholds are illustrative.

## What to monitor

| Area | Signal | Why it matters | Example alert (illustrative) |
|---|---|---|---|
| Quality | Weekly sampled accuracy against sources | Catches slow decline | Accuracy on sample drops below the agreed floor |
| Freshness | Data-as-of lag | Prevents confident, outdated output | Lag exceeds the maximum in the data contract |
| Attention | Override rate, abstention rate, canary catch rate | Shows whether reviews are real | Overrides fall sharply during a volume spike |
| Adoption | The four columns | Shows whether the work actually changed | "Used" stalls for several weeks |
| Experience | User feedback and reported errors | Surfaces problems metrics miss | Repeated reports about the same issue |
| Cost and speed | Cost per task, response time | Keeps unit economics honest | Cost per task exceeds the value of time saved |

## Cost: do the unit economics

Compare the cost per task (model usage plus review time) to the baseline cost of the manual process. An AI step that saves ten minutes but adds eight minutes of review is not a win. Track cost per task from the first week.

## Incident response

When an output is wrong in a way that matters:

1. **Detect.** Through sampling, a user report, or an alert.
2. **Contain.** Use the kill switch to fall back to the old path. This is why the old path is only retired once evaluation and monitoring are proven (Workflow 4), not before.
3. **Diagnose.** Use version records to identify what changed: model, prompt, retrieval, or data.
4. **Fix and re-test.** Re-run the golden set, including the new failure case.
5. **Communicate.** Tell affected users what happened and what changed.
6. **Review.** Hold a blameless post-incident review and add the case to the golden set.

## Change management

Any change to the model, prompt, schema, retrieval settings, or data definitions follows the same path:

- Record the change and the reason.
- Re-run the evaluation gate and compare to the last passing result.
- Release to a small group first.
- Tell users what changed and what to watch for.

A provider updating a model without notice is a change too. Pin versions where possible and re-test when a version changes.

## Who owns what

| Role | Responsibility |
|---|---|
| Initiative owner | Accountable for outcomes, thresholds, and the four-column report |
| Evaluation lead | Owns the golden set, labeling, and gate results |
| Data steward | Owns the data contract, definitions, and freshness |
| Platform engineer | Owns the build, versioning, logging, and rollback |
| Team champions | Support daily use and report issues |
| Leadership sponsor | Removes blockers; holds the sunset decision |

## Sunset rules

An initiative that stays stuck for two quarters gets a decision: fix it, narrow it, or stop it. Stopping is a legitimate outcome, and reporting it honestly is part of the model.
