# Plan format (`plan.md`)

Lives in the change directory.
Translate the section titles into the artifact language.
Drop an optional section entirely when it does not apply.

```markdown
---
feature: <feature path>
change: root | evolutions/NNN-<slug>
---

# Plan: <feature title>

## Approach
<Three to six sentences: how the change is built and why this shape. Cites D-NN.>

## Technical context
- **Stack touched**: <languages, frameworks, services involved>
- **Layers touched**: <in the project's layer order>
- **Analogues**: <existing code each new piece follows, with paths>

## Files
| File | Action | Follows | Serves |
|------|--------|---------|--------|
| <path> | create / modify | <analogue path> | FR-001, FR-002 |

## Data model (optional)
<Short summary, or "see data-model.md". Migrations listed here.>

## Contracts (optional)
<Interfaces exposed to other systems: endpoints, events, CLI, public API.>

## Technical decisions
- D-NN: <one line each; full entry in the ledger>

## Rules check
| Rule or ADR | Status | Note |
|-------------|--------|------|
| <rule from rules.md> | complies / deviates | <for a deviation, the justifying D-NN> |

## Risks (optional)
- <risk> → <mitigation>

## Manual steps (optional)
- <migration to run, secret to set, service to enable>
```

`data-model.md`, when written, lists each entity with its fields and types, constraints, relationships, state transitions, and indexes, in the project's own vocabulary.
