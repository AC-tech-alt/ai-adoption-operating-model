# Pressure test: quarter-end, four stresses at once

A live scenario designed to show where the model bends. It is illustrative. The point is the method: stress-test your own rollout before leadership does it for you.

## Setup

Six months after rollout, the operations organization looks healthy on paper.

- The executive reporting assistant is deployed.
- Intake first-pass triage is deployed and widely used.
- The status slide says both initiatives are "Live."

It is quarter-end. Volume is high and leadership is watching.

## Four things happen in the same week

### Stress 1: a confident summary that is out of date (Workflows 2 and 3)

The executive reporting assistant produces a clean summary for a leadership meeting. It does not reflect a change a regional lead made the day before. The summary reads confidently and a leader nearly acts on it.

**Root cause:** the retrieval index refreshes overnight, and the change arrived after the last refresh. The output showed no indication of how fresh its data was, and the golden set had no "late-breaking change" cases, so evaluation never tested for this.

**Where the model bends:** it required a review step but did not require freshness to be visible, and the evaluation set did not cover the case.

**Fix:** a visible "data as of" stamp on every output, a maximum-lag alert from the data contract, and "late-breaking change" cases added to the golden set.

### Stress 2: reviewers start skipping review (Workflows 3 and 5)

With the intake queue backed up, reviewers begin accepting first-pass triage without reading it. Override rate drops sharply. On the dashboard, this looks like the model improving.

**Where the model bends:** the monthly override review treated a falling rate as good news. Nothing separated "the model got better" from "people stopped checking."

**Fix:** read the override rate next to sampled review results, add canary items to measure real attention, and treat a sudden drop in overrides during a volume spike as a warning, not a win.

### Stress 3: the old spreadsheet comes back (Workflow 4)

Under deadline pressure, one team reverts to the old spreadsheet because they trust it more. Two other teams notice and start keeping a copy "just in case."

**Where the model bends:** the old path had a retirement date, but no one owned enforcing it, and nothing in the reporting made the parallel version visible. The "Relied on" column quietly went back to "No" without anyone seeing it.

**Fix:** a named owner for retiring each old path, and a standing question in the four-column review: "Is a parallel version being maintained?"

### Stress 4: a silent change shifts behavior (Workflows 2 and 5)

Mid-quarter, the underlying model version is updated and a prompt is lightly edited to shorten summaries. No one re-runs the evaluation set. Summaries become shorter and begin dropping caveats. The change is noticed only when a weekly sample review flags several omissions in a row.

**Where the model bends:** change control existed on paper, but nothing forced a re-test when a version changed, and the provider-side update was not treated as a change at all.

**Fix:** pin model versions where possible, require the evaluation gate on any change to the model, prompt, retrieval, or schema, and compare results to the last passing run before release. The kill switch stays available while the fix is tested.

## What the pressure test shows

| Stress | Workflow | Assumption that failed | Change made |
|---|---|---|---|
| Out-of-date summary | 2 and 3 | A review step is enough, and evaluation covers real-world timing | Data-as-of stamp, max-lag alert, late-change cases in the golden set |
| Skipped reviews | 3 and 5 | Falling overrides means improvement | Sampled audit, canary items, read overrides with review results |
| Return of the spreadsheet | 4 | A retirement date enforces itself | Named owner and a standing parallel-path check |
| Silent change | 2 and 5 | Change control works without enforcement | Version pinning and a required re-test gate |

## The takeaway

None of the four problems was a failure of model intelligence. All four were operating failures: freshness, attention under pressure, an unenforced retirement date, and uncontrolled change. That is the point of this model. Whether AI sticks is decided less by the model and more by the operating system around it.

## Your turn

Run your own rollout through these four stresses. If you find a fifth that breaks this model, I want to hear about it.
