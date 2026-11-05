# Five workflows

Each workflow lists its Execution Plan, Field Readiness standard, Evidence, and Adoption threshold. Thresholds are illustrative starting points. The initiative owner sets the real ones before rollout.

Technical detail lives in the companion pages: [technical-architecture.md](technical-architecture.md), [evaluation.md](evaluation.md), [risk-tiers.md](risk-tiers.md), and [operations-monitoring.md](operations-monitoring.md).

---

## 1. Use-Case Selection and Intake

**Purpose:** decide what AI should and should not touch, and how much oversight it needs, before anything is built.

**Execution Plan**
- Collect candidate use cases through one intake form, not ad hoc requests.
- Score each against a short rubric: repeatable, measurable, has a named owner, has a safe human-review step, and the data it needs is available and trustworthy inside the system of record.
- Assign a risk tier (see [risk-tiers.md](risk-tiers.md)). The tier sets the controls for the rest of the workflows.
- Capture a baseline (time, rework, error rate, decision delay) for every approved use case before build starts. This is Gate 0.
- Write a data contract for each source the use case reads.
- Publish the decision, including use cases that were declined and why.

**Field Readiness standard**
- A team lead can explain, in one minute, why a given use case was approved or declined and which tier it sits in.

**Evidence**
- Scored intake records, an assigned tier, a baseline for each approved case, data contracts, and a published decision log.

**Adoption threshold**
- No use case enters build without a named owner, a recorded baseline, and an assigned risk tier.

---

## 2. Embedded Build in the System of Record

**Purpose:** put the capability where people already work, built so its quality can be proven before release.

**Execution Plan**
- Build inside the existing system of record (for example, the CRM or case system the team already uses). No new login, no separate tool.
- Follow the reference architecture: permission-filtered retrieval, versioned prompts, structured outputs with citations, a validation layer, and abstention routing.
- Show a "data as of" stamp on every output.
- Build the golden set and pass Gate 1 (offline evaluation) before any user sees the tool. See [evaluation.md](evaluation.md).
- Keep the old path available during transition, with a retirement date set at kickoff.

**Field Readiness standard**
- A user completes a real task, start to finish, without leaving the system or asking for help.
- The evaluation lead can show the latest gate results for this version.

**Evidence**
- Gate 1 results, task logs showing work starting in the embedded tool, and version records for the model, prompt, and retrieval settings.

**Adoption threshold (example)**
- Passed Gate 1, and 80% of eligible tasks start in the embedded tool for four consecutive weeks.

---

## 3. Human Review and Override

**Purpose:** make clear what the AI drafts, what a person decides, and what happens when the two disagree, in a way that holds up under pressure.

**Execution Plan**
- Define review rules by risk tier: what a person must always approve, what is sampled, and what runs without review.
- Design the review screen to show source evidence beside each claim, so reviewers check facts and not just wording.
- Allow and track abstention. The system may say it cannot answer reliably and route to a person.
- Log every override with a one-line reason.
- Use canary items (planted known errors) to measure whether reviewers are really checking.
- Review override, abstention, and canary-catch patterns monthly. A rising override rate may signal a model problem. A falling one may signal rubber-stamping. Treat both as questions, not goals.
- Provide a reporting path for AI errors that is easier than ignoring them.

**Field Readiness standard**
- A reviewer can explain why they accepted or overrode a specific output and can point to the source record they checked.

**Evidence**
- Override records with reasons, sampled review results, canary catch rate, and a log of reported errors and fixes.

**Adoption threshold (example)**
- Every in-scope output has a recorded review outcome, the canary catch rate stays above the agreed floor, and the monthly review actually happens.

---

## 4. Rollout and Field Readiness

**Purpose:** move people from "trained" to "actually working this way," in stages that match the evidence.

**Execution Plan**
- Run Gate 2 (shadow mode) and Gate 3 (limited release) on real work, not a demo environment.
- Name a champion on each team who handles day-to-day questions.
- Test readiness with unassisted real tasks, not attendance.
- Confirm monitoring and the rollback path work before retiring anything.
- Retire the old path on the date set at kickoff, with a named person responsible for enforcing it, and say so openly.

**Field Readiness standard**
- Each team passes an unassisted real-task check before the old path is retired.

**Evidence**
- Gate 2 and Gate 3 results, readiness check results by team, a tested rollback record, the retirement date for the old path, and confirmation that no parallel spreadsheet is being kept.

**Adoption threshold (example)**
- The old path is retired on schedule, no parallel version is maintained, and monitoring is live.

---

## 5. Adoption and Value Measurement

**Purpose:** keep deployed, used, relied on, and valued as separate columns, and keep quality and cost visible after launch.

**Execution Plan**
- Report all four columns for every initiative at every leadership review (see [adoption-and-value.md](adoption-and-value.md)).
- Compare results to the baseline captured in Workflow 1.
- Run the monitoring routine: weekly sampled quality checks, freshness, cost per task, and user feedback (see [operations-monitoring.md](operations-monitoring.md)).
- Re-run the evaluation gate on every change to the model, prompt, retrieval, or data definitions.
- Set sunset rules: an initiative that stays stuck for two quarters gets a decision to fix, narrow, or stop.

**Field Readiness standard**
- A leader can say which column an initiative is in, what evidence supports it, and what it costs per task.

**Evidence**
- The four-column report, the comparison to baseline, monitoring results, and change records.

**Adoption threshold (example)**
- Value is reported against baseline for every initiative, including the ones that did not work, and every change has a recorded evaluation result.
