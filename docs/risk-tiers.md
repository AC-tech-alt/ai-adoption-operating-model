# Risk tiers: match the controls to the stakes

Not every AI use case needs the same level of oversight. Treating them all the same either slows low-risk work to a crawl or under-protects high-stakes work. Assign a tier at intake (Workflow 1) and let the tier set the controls.

## The tiers

| Tier | What the AI does | Human role | Example | Evaluation gate | Rollback |
|---|---|---|---|---|---|
| 1. Assist | Drafts or summarizes for internal reading | Reads before use | First draft of a weekly summary for an internal team | Gates 0 to 2 | Switch off; old path still available |
| 2. Recommend | Suggests a classification or priority | Decides; AI never acts alone | First-pass triage on an intake queue | Gates 0 to 4 with sampled review | Switch off; revert to manual triage |
| 3. Act (narrow) | Takes a defined, reversible action automatically | Monitors; samples results | Auto-routing an item to a queue based on clear rules | All gates, strict thresholds, tested rollback | One-step revert of the action plus kill switch |
| Out of scope | Not for AI to decide | Person decides | Irreversible or high-consequence decisions | Not applicable | Not applicable |

Move a use case up a tier only after it has earned it through evidence, never because volume pressure makes automation tempting.

## Designing for human attention

People reviewing AI output tend to over-trust it, especially under time pressure. This is called automation bias. Design against it:

- **Evidence first.** Show the source records beside each claim so the reviewer checks facts, not just wording.
- **Require an active confirmation** for higher tiers, not a default "approve all."
- **Use canary items.** Occasionally insert outputs with a known, planted error and measure whether reviewers catch them. A low catch rate means reviews have become a formality.
- **Rotate and sample.** Pull random items for a second look, and treat a sudden drop in overrides during a volume spike as a warning.

## Abstention

Allow and measure "I can't answer this reliably." Track the abstention rate and read it next to evaluation results. Too low can mean the model is guessing. Too high can mean it is not useful. The goal is correct abstention on the cases that should be escalated.

## Informal mapping to a common risk framework

This model's controls line up with the four functions of the NIST AI Risk Management Framework. This is an informal orientation aid, not a compliance claim.

| NIST AI RMF function | Where it shows up here |
|---|---|
| Govern | Named owner, risk tiers, decision log (Workflow 1) |
| Map | Use-case intake, context, and baseline (Workflow 1) |
| Measure | Golden set, staged gates, sampled review ([evaluation.md](evaluation.md)) |
| Manage | Monitoring, incident response, change control ([operations-monitoring.md](operations-monitoring.md)) |
