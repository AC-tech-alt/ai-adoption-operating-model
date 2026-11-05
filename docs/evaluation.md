# Evaluation: evidence before rollout, not opinions after

A demo is not evidence. This page describes how to decide, with data, whether an AI capability is good enough to release and whether it stays good enough afterward. Numbers below are illustrative starting points. The initiative owner and the reviewers set the real thresholds before testing begins, so they cannot be moved afterward to fit the result.

## 1. Build a golden set from real work

- Collect a set of real past tasks (for example, 100 to 300 to start) with the correct outputs labeled by experienced reviewers.
- Cover normal cases, edge cases, and tricky ones: late-breaking changes, conflicting records, missing data, and items where the correct answer is "escalate to a person."
- Hold out a portion that is never used while tuning, so results are not overfit.
- Refresh the set every quarter so it reflects how the work actually changes.

## 2. Measure what matters for each use case

| Use case | Primary measures | Secondary measures |
|---|---|---|
| Executive reporting summary | Factual accuracy against sources; omission of material changes; citation validity; stale-data catch rate | Readability, length, consistency week to week |
| Intake first-pass triage | Agreement with senior reviewers; severity-weighted error rate; correct abstention on ambiguous items | Time to first-pass, cost per item |

**Severity-weighted scoring.** Not all errors are equal. Label each error critical, major, or minor, and set the release gate on critical and major errors, not on overall accuracy. A system that is 95% accurate can still be unusable if the 5% includes the cases that matter most.

## 3. Check that humans agree with each other

Have at least two reviewers label a sample independently and measure how often they agree. If experienced people disagree often, the problem is the task definition, not the model. Fix the rubric before trusting any score.

## 4. Use model-based grading carefully

Using one model to grade another can scale evaluation, but it has known biases. If used, calibrate it against human labels on a sample, re-check periodically, and never make it the only gate for higher-risk use cases.

## 5. Staged gates

| Gate | What happens | Pass criteria (set in advance, illustrative) |
|---|---|---|
| 0. Baseline | Measure the current process: time, error, rework, decision delay | Baseline recorded and signed off by the owner |
| 1. Offline evaluation | Run the golden set, including held-out cases | No unmitigated critical errors; major-error rate under the agreed limit; abstention works on "should escalate" cases |
| 2. Shadow mode | AI runs alongside the existing process; humans do the work as usual and compare | Results hold up on live volume; reviewers confirm output is useful |
| 3. Limited release | One or two teams use it for real work, with 100% review of outputs | Error and override patterns understood; field readiness check passed |
| 4. General release | Broader rollout with sampled review and monitoring | Monitoring in place and the rollback path tested |

An initiative does not advance to the next gate because the calendar says so. It advances because the evidence does.

## 6. Re-test on every change

Re-run the golden set whenever any of these change:

- The model or model version
- The prompt or output schema
- Retrieval settings or the data it draws on
- The underlying data definitions

Compare to the last passing result. A change that improves one measure but worsens another is a decision for the owner, not an automatic release.

## 7. Keep sampling in production

- Review a random weekly sample of live outputs against sources.
- Track the trend, not only the current number.
- Add every real failure to the golden set so the same mistake is caught next time.

## What evaluation does not replace

Evaluation tells you whether the output is good. It does not tell you whether people use it or whether decisions improved. That is the job of the four-column view in [adoption-and-value.md](adoption-and-value.md).
