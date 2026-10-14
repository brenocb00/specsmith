# Phase: plan

Decide how the change will be built, inside the project's existing architecture.
The output is `plan.md`, plus `data-model.md` when the change touches data.

## 1. Load

- `spec.md` (root) and the active change's ledger;
- `rules.md`, the glossary, and the ADRs;
- the code: for every layer the change touches, find the closest **analogue** already in the codebase (a similar module, route, screen, or test) and read it.

The analogues set the patterns; the plan replicates them.

## 2. Settle technical decisions

List every technical question the change raises: where it lives, which layers it touches, data shape and storage, contracts, libraries, migrations, risks.
Answer each from the code, `rules.md`, the ADRs, or documentation first.
Put the questions that remain genuine choices to the user in rounds (`rounds.md`), recorded in the same ledger.
Offer an ADR only for a decision that passes the three gates in `grill.md`.

## 3. Write

Write `<change>/plan.md` from `formats/plan.md`.

- Name every file to create or modify, with the analogue it follows.
- Write `<change>/data-model.md` when the change adds or alters entities, fields, states, or indexes.
- Add a `contracts/` section or folder only when the change exposes an interface to other systems.
- Fill the rules check: every relevant rule in `rules.md` and every relevant ADR, each marked complies or deviates. A deviation needs a ledger decision that justifies it; without one, ask before writing the plan.

## 4. Close

The phase is done when every technical question is answered by a source or a ledger entry, and the rules check has no unjustified deviation.

1. Set the ledger status to `planned`.
2. Verify on disk: `plan.md`, `data-model.md` when written, the ledger, any ADRs.
3. Report, in the conversation language, the files the change will touch, the new decisions, and suggest `/specsmith tasks`.
