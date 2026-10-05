# Phase: doc

Bring every document in line with what was actually built, then close the change.

## 1. Gather what changed

- the change's ledger, `plan.md`, and `tasks.md`;
- the code diff since the change began (version control when available, otherwise the files named in the plan and tasks);
- decisions and rules stated in the conversation that the ledger may lack.

## 2. Reconcile

Compare the built code with the spec, plan, and ledger.
Every divergence is a question, never a silent edit: ask whether the code or the document is right.

- **The code is right**: record the decision in the ledger (superseding the old entry), then update the spec and plan.
- **The document is right**: the code has a bug; report it and leave the change at `implemented`.

## 3. Update

Edit surgically: touch only the affected sections and keep each document's structure and tone.

| Document | Update |
|----------|--------|
| `spec.md` | scenarios and requirements as built; the evolution history line for an evolution |
| `plan.md` | file list and decisions as built |
| `data-model.md` | entities, fields, states, indexes as built |
| `tasks.md` | every task status |
| `GLOSSARY.md` | terms the implementation introduced or renamed |
| `docs/adr/` | decisions made during implementation that pass the three gates |
| documentation targets in `rules.md` | each target according to its stated purpose |

When the change established a new project-wide convention, propose the line for `rules.md` and add it only with the user's approval.

## 4. Close

The phase is done when every divergence is resolved and every document in the table reflects the built code.

1. Set the ledger status to `done`.
2. Verify on disk: every file updated.
3. Report the files updated with one line each, the files checked and left unchanged, and any follow-up.
