# Phase: tasks

Break the plan into an ordered, executable `tasks.md`, then check spec, plan, and tasks for consistency before any code is written.

## 1. Load

`spec.md`, the active change's ledger, `plan.md`, `data-model.md` when present, and `rules.md`.

## 2. Generate

Write `<change>/tasks.md` from `formats/tasks.md`.

**Phases**

- **Foundation**, only when a real prerequisite blocks every story (a new dependency, a schema migration). Omit it otherwise.
- **One phase per user story**, in the spec's priority order. Each phase is a vertical slice: when it is done, its story works and its tests are green on their own.

**Order inside a story phase**

1. One test task per `[auto]` scenario of the story, written first: the test is expected to go red.
2. Implementation tasks, one per architecture layer the plan names, in the layer order of `rules.md` or the plan.
3. One verification task for the story's scenarios without `[auto]`, saying how to check them (E2E run, manual walkthrough).

**Every task**

- follows the line format of `formats/tasks.md`, with its exact file path;
- cites the requirements it serves (`→ FR-002, FR-004`);
- carries `[P]` only when it touches different files from every unfinished task it could run beside, and depends on none of them;
- carries `(needs A-NN)` when it depends on an unconfirmed assumption;
- is specific enough that an agent with no other context can complete it.

Generate only the task kinds the change needs; skip every kind `rules.md` lists under tasks never generated.

## 3. Check consistency

Run these passes over spec, ledger, plan, and tasks without editing any of them.
Cap the findings at 50 and summarize any overflow.

| Pass | Finds |
|------|-------|
| Coverage | an `FR` with no task; an `[auto]` scenario with no test task; a task with no `FR`; a ledger entry reflected nowhere in spec or plan |
| Assumptions | tasks marked `(needs A-NN)` |
| Rules | a requirement, plan item, or task that conflicts with `rules.md` or an ADR |
| Ambiguity | vague adjectives without a measure; leftover placeholders (TODO, ???, `<...>`) |
| Duplication | near-duplicate requirements or tasks |
| Terminology | one concept named differently across artifacts or against the glossary |
| Ordering | a task scheduled before a task it depends on |

Severity:

- **CRITICAL**: a rules or ADR conflict, an uncovered requirement that blocks a story, a missing core artifact.
- **HIGH**: a conflicting or duplicate requirement, an untestable scenario, a task depending on an assumption.
- **MEDIUM**: terminology drift, an under-specified edge case.
- **LOW**: wording.

Append the result to `tasks.md` as the consistency section of `formats/tasks.md`, listing every CRITICAL and HIGH finding as open.

## 4. Offer fixes

Propose concrete edits for the CRITICAL and HIGH findings and apply them only with the user's approval.
A fix that changes behaviour is a decision: record it in the ledger first.
Mark each fixed finding resolved in the consistency section.

## 5. Close

The phase is done when every story has its test, implementation, and verification tasks, and the consistency section is written.

1. Set the ledger status to `tasked`.
2. Verify on disk: `tasks.md`.
3. Report the task count per story, the parallel opportunities, and the open findings by severity, and suggest `/specsmith implement`. Open CRITICAL findings block `implement` until resolved or waived by the user.
