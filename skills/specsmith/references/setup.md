# Phase: setup

Capture the project-specific rules every other phase obeys, in `docs/specsmith/rules.md`.
Run it once per project, and again whenever the rules change.

## 1. Language

Ask the first question alone, before anything else: which language the artifacts (ledgers, specs, plans, tasks, glossary, ADRs) are written in.

## 2. Read the environment

Gather the facts yourself:

- environment selection: env files and their variable names (never their values), flags such as `--env` or `--production`, and the code paths that send email, messages, payments, or other effects outside the machine;
- manifests and scripts (`package.json`, `pyproject.toml`, `Makefile`, `*.csproj`, and the like) for the test, lint, typecheck, and build commands;
- test configs and test directories, to learn the test layout and naming;
- the source layout, plus two or three representative modules, to infer architecture layers and conventions;
- existing agent rules: `AGENTS.md`, `CLAUDE.md`, `.github/copilot-instructions.md`, `.cursor/rules`, `.agents/rules/`, `CONTRIBUTING.md`;
- existing `specs/` and `docs/` trees, and any earlier spec-driven tooling (`.specify/`).

Existing agent rules decide the **authority** question first:

- When the project already keeps its rules in an agent file every session loads (`AGENTS.md`, `CLAUDE.md`, and the like), that file stays the authority. `rules.md` names it and holds only what is specific to specsmith, so the project keeps one source of truth.
- When no such file exists, or the user wants `rules.md` to become the source, import each existing rule as a candidate for `rules.md`.

## 3. Run rounds

Follow `rounds.md`, recording answers straight into `rules.md` rather than a ledger (setup belongs to the project, not to a feature).
Cover every section of `formats/rules.md`:

- **Authority**: which existing rule files `rules.md` defers to, decided as above. Every later section skips what those files already say.
- **Environments**: which environments exist (development, test, staging, production), how the project selects one (env files, flags, variables), and which side effects reach the outside world (databases, payment or bank APIs, email and messaging, paid APIs, storage). Ask what each phase may touch. When the authority file says nothing about production, propose the rule for it there, not here.
- **Spec paths**: flat `specs/<feature>/`, or a hierarchy that mirrors the product (for example `specs/<system>/<module>/<scope>/`). Ask how to classify a feature when it is hierarchical.
- **Commands**: present the commands you found and ask which are canonical.
- **Architecture and conventions**: present each inferred pattern as a finding and ask "rule or accident?". A rule enters `rules.md` with its reason.
- **Workflow constraints**: task kinds `tasks` never generates, sections every spec must include, manual steps the user must be told about.
- **Documentation targets**: extra docs `doc` keeps in sync, each with its purpose.
- **Suggestion hook**: whether to add one line to the project's `AGENTS.md` or `CLAUDE.md` so the agent suggests `/specsmith grill` when the user asks for a significant feature.

Write into `rules.md` only what the agent cannot find by looking: conventions, reasons, constraints.
Leave anything a single file read reveals to the environment.

## 4. Write

Write `docs/specsmith/rules.md` from `formats/rules.md`.
On a re-run, edit the existing file in place and summarize what changed.
Add the suggestion hook line only when the user said yes.

## 5. Close

The phase is done when every section of `rules.md` holds content or an explicit "none", and the user confirmed it.
Verify the file on disk, report its sections in one line each, and suggest `/specsmith grill <idea>`.
