---
feature: specsmith
change: root
status: implemented
---

# Decisions: specsmith

Build one generic, reusable skill that runs a spec-driven workflow on top of Matt Pocock's grilling, keeping the strengths of a project-specific Spec Kit fork (originally written for Copilot and ported to Antigravity).

## D-01 - Target platforms
**Decision:** Any agent that reads the Agent Skills format (`SKILL.md`), tested on Claude Code and Antigravity.
**Why:** The skill must outlive any one tool, so it names no tool-specific functions, uses no `handoffs:`, and never needs one skill to load another.
**Status:** decided

## D-02 - Packaging
**Decision:** One user-invoked skill with phase subcommands (`/specsmith <phase>`); each phase lives in its own reference file loaded on demand.
**Why:** The most reported failure of `grill-with-docs` is a skill that fails to load the skills it delegates to. One skill removes that failure, and per-phase files keep later steps out of view.
**Status:** decided

## D-03 - Optional phases
**Decision:** Market research becomes a fact lookup inside `grill`; `prototype` stays as an optional phase between `grill` and `spec`.
**Why:** Validating a new screen before the spec is a genuine strength of the original fork; a separate discovery phase duplicated the interview.
**Status:** decided

## D-04 - Grilling is vendored
**Decision:** The grilling protocol and the glossary and ADR formats are adapted into the skill, with MIT attribution.
**Why:** A runtime dependency on another skill reproduces the loading failure D-02 avoids.
**Status:** decided

## D-05 - Assumption policy
**Decision:** Grill until the frontier is empty; the user may say "assume the rest" at any time, and each remaining question becomes an `A-NN` entry with the recommended answer, listed in the spec and flagged on dependent tasks.
**Why:** Spec Kit caps questions and assumes silently; grilling forbids silent assumptions. Visible assumptions keep the speed without the silence.
**Status:** decided

## D-06 - Language
**Decision:** Skill instructions in English. The artifact language has no default: it is the first question of `setup`, or of the first phase when `setup` never ran.
**Why:** English makes the skill shareable; the artifact language belongs to each project.
**Status:** decided

## D-07 - Name and location
**Decision:** `specsmith`, in its own git repository.
**Why:** Chosen by the user among anvil, crucible, temper, whetstone, specsmith, crossexam.
**Status:** decided

## D-08 - Artifact layout
**Decision:** `GLOSSARY.md` at the root, ADRs in `docs/adr/`, rules in `docs/specsmith/rules.md`, features under a spec root whose path pattern comes from `setup` (flat by default, hierarchical when the project needs it).
**Why:** A configurable pattern lets a product hierarchy (system, module, tab) fit without hard-coding it.
**Status:** decided

## D-09 - Ledger format
**Decision:** `decisions.md` per change, with `D-NN` decisions and `A-NN` assumptions in one sequence per feature; superseded entries stay; each requirement cites its source entry.
**Why:** It closes grilling's documented gap: decisions that never leave the chat.
**Status:** decided

## D-10 - No global state
**Decision:** The active feature comes from the argument or the conversation, never from a global state file.
**Why:** Parallel sessions on different features break a single `feature.json`, as the original fork itself admitted.
**Status:** decided

## D-11 - What setup records
**Decision:** Artifact language, spec path pattern, canonical commands, architecture and conventions with reasons, workflow constraints, documentation targets, and an optional suggestion hook in `AGENTS.md` or `CLAUDE.md`.
**Why:** These are what an agent cannot find by looking; one-lookup facts stay in the environment.
**Status:** decided

## D-12 - Invocation and gates
**Decision:** The skill fires only when the user types it, and every phase stops at its end and names the next command. Interception of natural-language feature requests becomes an optional one-line suggestion hook.
**Why:** The original fork's forced interception hijacked every request; a suggestion keeps the user in charge.
**Status:** decided

## D-13 - Spec content
**Decision:** Keep user stories with Given/When/Then scenarios, two-way links between scenarios and requirements, the `[auto]` tag, success criteria, edge cases, out of scope, and evolution history. Validate inside the phase instead of a separate checklist file. The flow diagram is optional.
**Why:** Traceability was the fork's strongest asset; the checklist file and the mandatory tab-based diagram were overhead or product-specific.
**Status:** decided (gap handling superseded by D-22)

## D-14 - Test order
**Decision:** Test-first per user story for `[auto]` scenarios (red, then green); scenarios without `[auto]` are verified end to end or by hand and recorded.
**Why:** The fork contradicted itself (tests last in tasks, TDD in implement); the scenarios already exist, so test-first is nearly free.
**Status:** decided

## D-15 - Task format
**Decision:** Keep the strict checklist line (`- [ ] T001 [P] [US1] description in path`) and one task per layer per story, adding the requirements each task serves.
**Why:** Requirement references make the coverage check mechanical.
**Status:** decided

## D-16 - Consistency check
**Decision:** The former analyze step runs automatically at the end of `tasks`, read-only, with open CRITICAL findings blocking `implement`. It adds two passes: every ledger entry reflected, and tasks depending on unconfirmed assumptions.
**Why:** A separate command was easy to skip; the new passes tie the check to the ledger.
**Status:** decided

## D-17 - Plan artifacts
**Decision:** Everything goes in `plan.md` sections; `data-model.md` only when data changes, contracts only for external interfaces. Unresolved technical choices get a short grilling round recorded in the same ledger.
**Why:** Fewer files, one place for every decision.
**Status:** decided

## D-18 - Doc scope
**Decision:** `doc` always reconciles spec, plan, data model, tasks, glossary, and ADRs with the built code; other documentation targets come from `rules.md`. Every divergence is asked, never silently edited.
**Why:** The fork's doc targets were product-specific folders.
**Status:** decided

## D-19 - Distribution
**Decision:** Repository in the Agent Skills layout (`skills/specsmith/SKILL.md` plus `references/`), installed by copying into `.claude/skills/` or `.agents/skills/`. A Claude Code plugin manifest may come later.
**Why:** Copying a folder works in every agent that reads skills.
**Status:** decided

## A-20 - Status lives in the ledger
**Assumption:** A change's status lives in the front matter of its ledger, not of `spec.md`.
**Why:** Supersedes the earlier choice of `spec.md`: `grill` runs before any spec exists, and an evolution needs a status of its own while the spec stays shared.
**Status:** confirmed

## A-21 - Fixed tokens
**Assumption:** IDs and tags (`D-NN`, `A-NN`, `US-N`, `FR-NNN`, `SC-NNN`, `TNNN`, `[P]`, `[auto]`) stay in English in every artifact language; headings are translated.
**Why:** Every phase must find them reliably regardless of language.
**Status:** confirmed

## D-22 - Spec closes small gaps itself
**Decision:** When `spec` finds ledger gaps, it closes them with rounds before writing, recording each answer in the ledger; it sends the user back to `grill` only when a whole coverage category was never explored.
**Why:** In the end-to-end test, four small gaps cost a full extra grill session; asking in place keeps the ledger-first rule without the round trip.
**Status:** decided

## D-23 - Existing agent rules stay the authority
**Decision:** When a project already keeps its rules in an agent file every session loads (`AGENTS.md`, `CLAUDE.md`), `setup` records that file as the authority in a new `Authority` section of `rules.md` and writes only specsmith-specific rules; it imports rules into `rules.md` only when no such file exists or the user asks.
**Why:** Testing `setup` on a real production project showed that copying `AGENTS.md` into `rules.md` creates two sources of truth that drift, which that project's `CLAUDE.md` explicitly forbids.
**Status:** decided

