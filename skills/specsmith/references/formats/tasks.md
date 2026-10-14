# Tasks format (`tasks.md`)

Lives in the change directory.
Translate the section titles into the artifact language; keep the line format and fixed tokens.

```markdown
---
feature: <feature path>
change: root | evolutions/NNN-<slug>
---

# Tasks: <feature title>

## Foundation (only when a prerequisite blocks every story)
- [ ] T001 <description> in <path>
- Commit: refactor: <proposed message>

## US-1 - <title> (P1)
Goal: <what works when this phase is done>

- [ ] T002 [US1] Test (red) US-1/1 in <test path> → FR-001
- [ ] T003 [P] [US1] <layer task> in <path> → FR-001
- [ ] T004 [US1] <layer task> in <path> → FR-001, FR-002 (needs A-05)
- [ ] T005 [US1] Verify US-1/2 by <E2E run or manual walkthrough>

## US-2 - <title> (P2)
...

## Consistency
| ID | Pass | Severity | Where | Finding | Recommendation | State |
|----|------|----------|-------|---------|----------------|-------|
| C1 | Coverage | CRITICAL | spec FR-004 | No task serves FR-004 | Add a layer task in US-2 | open |

Coverage: <requirements with at least one task> / <total requirements>; `[auto]` scenarios with a test task: <n> / <total>.

## Baseline (written by implement before any change)
<date>, <commit>: <test, lint, and typecheck commands> - <n> passed, <n> failed.
- <test file> › <test name>: <one-line failure reason>

## Coverage matrix (written by implement)
| Scenario | Requirement | Test or verification | Status |
|----------|-------------|----------------------|--------|
| US-1/1 | FR-001 | <test file> › <test name> | pass |
| US-1/2 | FR-002 | manual walkthrough, <date> | pass |
```

## Line format

`- [ ] T<NNN> [P]? [US<N>]? <description with exact path> → <FR list>? (needs A-NN)?`

- Task IDs are sequential in execution order and unique within the feature.
- `[US<N>]` appears on every task inside a story phase and nowhere else.
- One task per architecture layer per story; a layer task may create several files in one folder.
- A checkpoint line `- Commit: <proposed message>` has no checkbox and no ID; it closes the unit of work above it, back to the previous checkpoint or the start of its phase.
