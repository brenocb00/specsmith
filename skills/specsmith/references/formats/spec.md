# Spec format (`spec.md`)

Lives in the feature directory, one per feature, edited in place by each evolution.
Translate the section titles into the artifact language; keep the fixed tokens.
Drop an optional section entirely when it does not apply.

```markdown
---
feature: <feature path relative to the spec root>
title: <feature title>
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
---

# <Feature title>

## Context
<The problem, who has it, and why it matters now. Cites D-NN.>

## Actors
- **<Actor>**: <who they are and what they may do> (D-NN)

## User stories

### US-1 - <title> (P1)
As <actor>, I want <capability>, so that <outcome>.

**Scenarios**
1. Given <state>, when <action>, then <observable result>. → FR-001 [auto]
2. Given ..., when ..., then .... → FR-001, FR-002

## Functional requirements
- **FR-001**: <The system must ...> ← US-1/1, US-1/2 (D-03)
- **FR-002**: <...> ← US-1/2 (D-04, A-05)

## Edge cases
- <Situation> → <expected behaviour> (D-NN). Covered by US-N/M.

## Out of scope
- <What this feature deliberately does not do> (D-NN)

## Key entities (optional)
- **<Entity>**: <what it represents, key attributes, lifecycle states>. No storage detail.

## Success criteria
- **SC-001**: <measurable, technology-free outcome>

## Assumptions (optional)
- A-NN: <assumption the spec relies on, still unconfirmed>

## Flow (optional)
<Mermaid flowchart, only for three or more decision points or branches.>

## Evolution history (optional)
- **NNN - <slug>** (YYYY-MM-DD): <one line: what changed>
```

## Rules

- User stories are ordered by priority (P1 first); each one is independently testable.
- `US-1/2` means scenario 2 of user story 1.
- Every scenario has an observable result; every requirement has a covering scenario and a source entry.
- `[auto]` marks scenarios that become automated tests: API behaviour, business rules, calculations, validations, permissions.
- Sections that `rules.md` declares mandatory are always present.
