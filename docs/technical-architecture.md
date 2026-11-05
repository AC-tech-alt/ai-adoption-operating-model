# Technical architecture: how the AI is actually wired in

The operating model only works if the technical design supports it. This page describes a reference architecture for embedding AI into executive reporting and intake review inside an existing system of record. It is deliberately tool-agnostic.

## Design principles

1. **Ground answers in the system of record.** The model should answer from the organization's own current records, not from general knowledge. Retrieval-grounded generation comes first. Fine-tuning is considered only after evaluation shows a gap that grounding and better prompts cannot close.
2. **Respect the source system's permissions.** If a user cannot see a record in the system of record, the AI must not surface it to them. Retrieval is filtered by the requesting user's access, not by a shared service account.
3. **Show the evidence.** Every claim in an output points to the source record it came from, and every output carries a "data as of" timestamp.
4. **Structured outputs, validated.** The model returns a defined schema (fields, citations, confidence flags), and a validation layer checks it before a human sees it.
5. **Allow abstention.** The system may say "insufficient or conflicting information" and route to a person. A model that must always answer will sometimes answer wrongly with confidence.
6. **Version everything.** Prompts, model versions, retrieval settings, and data schemas are versioned so a change in behavior can be traced to a change in the system.
7. **Keep the human step inside the same system.** Review happens where the work already happens (see Workflow 2).

## Reference flow

```
System of record (CRM / case system)
        |
        v
Data contract + freshness check   <- field definitions, owners, refresh schedule
        |
        v
Permission-filtered retrieval     <- only what the requesting user may see
        |
        v
Model call                        <- versioned prompt, structured output schema
        |
        v
Validation layer                  <- schema check, citation check, rules,
        |                            data-as-of stamp, abstention routing
        v
Review surface (in the same system)
        |
        v
Action / write-back (by risk tier)   <- see risk-tiers.md
        |
        v
Logging + feedback  ->  Evaluation + monitoring loop  (see evaluation.md and operations-monitoring.md)
```

## Data contract

A data contract is a short agreement for each data source the AI reads:

- Field definitions, including one agreed definition for every metric leaders see (for example, what counts as an "active" case)
- A named data steward
- Refresh schedule and the maximum acceptable lag
- Known quality issues and how they are handled

Many "AI errors" are data errors. If two teams define the same metric differently, the model will confidently report whichever it retrieved.

## Key design choices

| Choice | Default in this model | Why | When to revisit |
|---|---|---|---|
| Grounding vs. fine-tuning | Retrieval grounding | Easier to keep current and to cite sources | Evaluation shows consistent style or format failures grounding cannot fix |
| Where the model runs in the workflow | Inside the system of record | Avoids a second place to check | Not applicable for most operations use cases |
| Output format | Structured schema with citations | Enables automatic validation and clean review | Free-text drafts only for low-risk Tier 1 uses |
| Model selection | Smallest model that passes the evaluation gate | Controls cost and latency | A new model passes the gate at lower cost, or the use case changes tier |
| Build vs. buy | Decide per use case, after the baseline | Avoid committing before the problem is measured | Requirements shift |

## Failure modes and controls

| Failure mode | What it looks like | Primary control |
|---|---|---|
| Fabricated detail | A figure or fact not in any source | Citation check: every claim must map to a retrieved record |
| Material omission | A summary leaves out an important change | Evaluation set with "must mention" cases; sampled review |
| Stale data | Output reflects yesterday's records | Data-as-of stamp; maximum-lag alert |
| Permission leakage | A user sees something they should not | Permission-filtered retrieval; test with restricted-access cases |
| Prompt injection via record text | Text inside a record tries to instruct the model | Treat retrieved text as untrusted data, not instructions; keep tool and write access minimal |
| Over-reliance | Reviewers accept outputs without reading | Evidence-first review layout; canary items (see risk-tiers.md) |
| Silent behavior change | A model or prompt update shifts outputs | Version control and re-running the evaluation gate on every change |

## Data handling notes

- Send the model only the fields the task needs.
- Logs of inputs and outputs may contain sensitive business data. Control access to them and set a retention period.
- Keep a human-readable record of which model and prompt version produced each output.
