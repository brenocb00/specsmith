# Phase: spec

Synthesize the ledger into `spec.md`: what the feature does and why, for a reader who never saw the interview.
Every statement in the spec traces to a ledger entry.

## 1. Load

- the active change's ledger, and for an evolution the ledgers of earlier changes;
- `prototype.html` when it exists, as the reference for flows and states;
- the glossary;
- for an evolution, the current root `spec.md`.

## 2. Check for gaps

Walk the spec format (`formats/spec.md`) section by section and list every statement you would need that no ledger entry decides.
Wording choices and restatements of decided facts are not gaps.
An interpretation is a gap: when a ledger entry admits two readings with different behaviour, or a case falls between entries, the user picks the reading.
Keeping today's behaviour in an uncovered case is also a decision, and gets asked.

When the list is not empty, close the gaps with rounds (`rounds.md`) before writing, recording each answer in the ledger as usual.
When the gaps reveal that a whole coverage category of `grill.md` was never explored, stop instead and suggest `/specsmith grill` to resume the full interview.

## 3. Write

- **Root change**: create `spec.md` in the feature directory from `formats/spec.md`.
- **Evolution**: edit the root `spec.md` in place. Revise the sections the change affects, keep everything still valid, and add a line to the evolution history. Remove requirements or scenarios only when a ledger entry decides their removal.

Traceability, applied to every requirement:

- each `FR-NNN` names at least one ledger entry it comes from (`D-NN` or `A-NN`);
- each `FR-NNN` points to the scenarios that cover it, and each scenario points to the requirements it covers;
- a requirement no scenario covers gets a scenario, or leaves the spec;
- scenarios that exercise an API, a business rule, a calculation, or a permission carry `[auto]`; purely visual or gesture-driven scenarios do not.

Add a flow diagram (Mermaid) only when the main flow has three or more decision points or branches.
Leave implementation out: no frameworks, file paths, schemas, or API shapes.

## 4. Validate

Check the spec against each item below, fix what fails, and re-check, up to three passes:

- every section required by `formats/spec.md` and by `rules.md` is present;
- every requirement is testable and unambiguous, with no vague adjective left unquantified;
- the traceability rules above hold for every requirement and scenario;
- success criteria are measurable and free of implementation detail;
- every `A-NN` the spec relies on is listed under assumptions;
- every term matches the glossary.

Report anything still failing after three passes.

## 5. Close

The phase is done when the validation passes or its remaining failures are reported.

1. Set the ledger status to `specified`.
2. Verify on disk: `spec.md`.
3. Report the counts of user stories, requirements, `[auto]` scenarios, and open assumptions, and suggest `/specsmith plan`.
