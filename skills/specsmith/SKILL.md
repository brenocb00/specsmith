---
name: specsmith
description: Spec-driven feature workflow built on relentless grilling. Phases - setup, grill, prototype, spec, plan, tasks, implement, doc.
disable-model-invocation: true
argument-hint: "<phase> [feature] [notes]"
---

# Specsmith

Specsmith turns a raw idea into shipped, tested, documented code through a fixed sequence of phases.
Every artifact traces back to a decision the user made, recorded in the feature's **ledger** (`decisions.md`).

## Invocation

`/specsmith <phase> [feature] [notes]`

| Phase | Reads | Writes | Sets status |
|-------|-------|--------|-------------|
| `setup` | codebase, existing agent rules | `docs/specsmith/rules.md` | - |
| `grill` | idea, codebase, glossary | ledger, `GLOSSARY.md`, `docs/adr/` | `grilled` |
| `prototype` (optional) | ledger | `prototype.html`, ledger | `prototyped` |
| `spec` | ledger, prototype | `spec.md` | `specified` |
| `plan` | spec, ledger, codebase | `plan.md`, ledger | `planned` |
| `tasks` | spec, plan | `tasks.md` with consistency report | `tasked` |
| `implement` | tasks, plan | code, tests, `tasks.md` | `implemented` |
| `doc` | change, code | spec, glossary, ADRs, doc targets | `done` |

Load `references/<phase>.md` and follow it step by step.
With no phase or an unknown one, print this table plus every feature whose status is not `done`, then stop.

## Before every phase

`setup` runs steps 1 and 2; the other phases run all five.

1. Read `docs/specsmith/rules.md` when it exists, plus every authority file it names. Their rules override the defaults in the references.
2. Read `GLOSSARY.md` (or `GLOSSARY-MAP.md` and the relevant context glossary) and the titles in `docs/adr/`. Use the glossary's terms in everything you write.
3. Resolve the **artifact language** from `rules.md`. When there is no `rules.md`, ask for it once, record it at the top of the ledger, and suggest `/specsmith setup`.
4. Resolve the feature and its active change (below).
5. Check the **gate**: the active change's status must be the one the previous phase sets (`prototype` is skippable). When it is not, tell the user which phase is pending and ask whether to proceed anyway.

**Conversation language.** Every message you write to the user (questions, round recommendations, progress notes, the final report) is in the language the user writes in; when their message is only a command, it is the artifact language.
These instructions are in English, and that never sets the conversation language.
Write artifacts in the artifact language.

## Features and changes

A **feature** is a directory under the spec root, located by the path pattern in `rules.md` (default `specs/<feature-slug>/`).
Its `spec.md` is the single source of truth for how the feature behaves now.

A **change** is one pass through the phases:

- The **root change** creates the feature. Its artifacts live in the feature directory.
- An **evolution** changes an existing feature. Its artifacts live in `evolutions/NNN-<slug>/` inside the feature directory, and it updates the root `spec.md` in place.

Each change has its own ledger, `plan.md`, optional `data-model.md`, and `tasks.md`.
The change's status lives in the front matter of its ledger.
The **active change** is the root change while its status is not `done`, otherwise the newest evolution whose status is not `done`.

Resolve the feature from the argument, then from the conversation.
When it stays ambiguous, list the features in progress and ask.
Hold no global "current feature" state: several sessions may work on different features at once.

## Fixed tokens

These tokens stay identical in every artifact language, so every phase can find them:

`D-NN` decision, `A-NN` assumption, `US-N` user story, `FR-NNN` functional requirement, `SC-NNN` success criterion, `TNNN` task, `[P]` parallelizable task, `[auto]` scenario that becomes an automated test.

IDs are unique within a feature, never reused, never renumbered.
An evolution continues the feature's numbering.

## Rules for every phase

- **Facts from the environment, decisions from the user.** Look up anything the codebase, docs, or web can answer. Put every choice between alternatives to the user, with your recommendation.
- **Stay inside the allowed environments.** Touch databases and external services only as the Environments section of `rules.md` allows. Without that section, only `implement` touches them, and only non-production ones. A fact only production can answer becomes a manual step for the user, with the exact command.
- **Record as you go.** Write each answer to the ledger, each resolved term to the glossary, and each qualifying ADR the moment it settles, before the next question.
- **Ledger first.** A decision reaches the spec, plan, tasks, or code only after it is in the ledger. When a later phase meets an undecided question, ask it, record it, then continue.
- **Stop at the phase boundary.** End the turn after the phase, naming the next command. The user starts the next phase.
- **Verify on disk.** Before the final report, list every file the phase wrote and confirm each exists with the expected content.

File formats live in `references/formats/`.
The interview protocol shared by `setup`, `grill`, and `plan` lives in `references/rounds.md`.
