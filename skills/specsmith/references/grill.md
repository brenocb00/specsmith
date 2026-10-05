# Phase: grill

Turn a raw idea into a complete ledger of decisions, a sharper glossary, and the ADRs that earn one.
This phase replaces both discovery and clarification: it interviews before anything is written as a spec.

## 1. Resolve the change

- **New feature**: derive a 2 to 4 word kebab-case slug from the idea. Place it with the spec path pattern from `rules.md`. When the placement is ambiguous (which module, which scope), make it the first question of the first round.
- **Existing feature** (its root `spec.md` exists): ask whether this is an evolution of it or a new, separate feature. For an evolution, scan `evolutions/` for the highest number and create `evolutions/NNN-<slug>/`.
- **Active change still in `grilling` or `grilled`**: resume it. Read the ledger and continue from its frontier.

Create the change directory and its ledger from `formats/decisions.md` with status `grilling` before the first round.

## 2. Gather context

Read before asking anything:

- the existing specs, to catch duplicates and overlaps with what already exists;
- for an evolution, the root `spec.md` and the ledgers of earlier changes;
- the code areas the idea touches;
- the glossary and ADR titles.

Report a duplicate or a trivial idea to the user plainly and let them decide whether to continue.

## 3. Run rounds

Follow `rounds.md`.
Seed the design tree from the idea, then grow it until every **coverage category** below is either decided, explicitly out of scope, or assumed:

| Category | Covers |
|----------|--------|
| Problem and outcome | whose pain, why now, what success looks like |
| Actors and permissions | user types, who may do what, data isolation |
| Scope | what is in, what is explicitly out, what is later |
| Behaviour and rules | flows, business rules, calculations, validations |
| Data | entities, identity and uniqueness, lifecycle and state transitions, volume |
| States and feedback | loading, empty, error, success, confirmation of destructive actions |
| Edge and failure cases | invalid input, concurrency, partial failure, external outages |
| Integrations | external services, imports and exports, their failure modes |
| Quality attributes | performance, security, privacy, accessibility, compliance, when relevant |
| Terminology | every domain term the feature introduces or reuses |

When a decision would benefit from how other products solve it, research real references as a fact lookup and bring the findings into the question.
Keep implementation choices (frameworks, file layout, schemas) for `plan`, unless one blocks a product decision.

## 4. Model the domain while you grill

Apply these moves during every round:

- **Challenge against the glossary.** When the user uses a term in a sense that conflicts with `GLOSSARY.md`, call it out at once and ask which sense holds.
- **Sharpen fuzzy language.** When a term is vague or overloaded, propose one precise canonical term.
- **Probe with scenarios.** Invent concrete edge-case scenarios that force precise boundaries between concepts.
- **Cross-check the code.** When the user states how something works today, check the code. Surface a contradiction as a question.
- **Update the glossary inline.** Write each resolved term to `GLOSSARY.md` the moment it resolves, in the format of `formats/glossary.md`. Create the file lazily, with the first term.
- **Offer ADRs sparingly.** Offer one only when the decision is hard to reverse, surprising without context, and the result of a real trade-off. Write accepted ADRs with `formats/adr.md`.

## 5. Close

The phase is done when `rounds.md` is done and every coverage category is decided, out of scope, or assumed.

1. Set the ledger status to `grilled`.
2. Verify on disk: the ledger, the glossary, any ADRs.
3. Report the counts of decisions, assumptions, glossary terms, and ADRs, plus any category marked out of scope.
4. Suggest `/specsmith spec`, or `/specsmith prototype` first when the feature introduces a new or complex screen.
