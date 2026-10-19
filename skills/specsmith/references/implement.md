# Phase: implement

Execute `tasks.md` story by story, test-first, until every story is green.

## 1. Gate

Read `tasks.md`, `plan.md`, `data-model.md` when present, the spec scenarios, and `rules.md`.
When the consistency section has open CRITICAL findings, list them and stop, unless the user waives them; record a waiver in the ledger.
When tasks still carry `(needs A-NN)`, ask the user to confirm or change those assumptions first, and update the ledger.

**Resume.** This phase runs in several turns: it stops for questions, commit checkpoints, and failures.
When some tasks are already `[X]`, continue from the first unchecked task and keep the existing baseline.
This holds whether the turn starts with the command or with a plain request to continue.

## 2. Guards

Every run of a command from `rules.md` (tests, lint, typecheck, build) goes through these guards, in the baseline and in every story.

- **Irreplaceable data.** Before the run, check the guard of each store under "Data that cannot be regenerated" in `rules.md`. When a guard fails or cannot be checked, do not run the command: report it and stop.
- **Backup.** Before the baseline run, run the backup command of each store that has one, and report where the copy went.
- **Working tree.** Snapshot the working tree's content before and after the run: the diff against the last commit (`git diff HEAD --binary`) plus every untracked, non-ignored file with a hash of its content. Comparing content, not the list of changed files, also catches a write to a file that was already modified. When the snapshot changed, stop: a command writes instead of checking. Report the command and the changed files, leave them as they are for the user to inspect, and ask for a checking variant to record in `rules.md`.

## 3. Baseline

Before changing any code, run the full test suite, lint, and typecheck from `rules.md`, through the guards.
Write every failure to the baseline section of `tasks.md` (`formats/tasks.md`): these are the failures the change did not cause.
An empty baseline is written too, as "no failures".

## 4. Work each story phase

Take the Foundation phase first when it exists, then the story phases in order.
Inside a phase, run `[P]` tasks together when your environment allows; run the rest in order.

For each story:

1. **Red.** Write the test tasks. Run them with the project's test command and watch each fail for the reason the scenario describes. A test that passes before the implementation exists tests nothing: fix the test.
2. **Green.** Before creating any file, read the analogue the plan names and follow its structure, naming, and helpers. Implement the layer tasks until the story's tests pass.
3. **Verify.** Run the story's verification task. For scenarios without `[auto]`, drive the feature as an end user would (E2E tooling or the running app) and record the outcome next to the task.
4. **Check.** Run the full test suite, lint, and typecheck from `rules.md`. The story is done when nothing fails outside the baseline.

Mark each task `[X]` in `tasks.md` the moment it completes, and report progress per task.

Tests, assertion messages, and logs never print credentials, tokens, or connection strings; mask them.

## 5. Commit checkpoints

A `Commit:` line in `tasks.md` marks work that must land in its own commit.
When every task above it is `[X]` and the checks pass, stop: list the files for that commit with the proposed message, and end the turn.
Continue from the next task once the user has committed or told you to commit.

## 6. When something fails

- A failing test reveals a bug or a wrong test. Change a test only when the spec shows the test expects the wrong behaviour; otherwise fix the code.
- A failure outside the baseline is a regression until shown otherwise. When it passes when run alone, run it alone three more times and the full suite once more. Report it as flaky, with that evidence, only when it passes alone every time and the change touches nothing it exercises; the user decides whether to accept it.
- Stop on a failed sequential task and report the error with its context. For `[P]` tasks, finish the others and report the failures together.
- An unfixable failure ends the phase early: report what is done, what failed, and what the user must decide.

## 7. Decisions during implementation

Implementation keeps meeting small questions the plan did not answer.

- A question with one obvious answer from the code or `rules.md` is a fact: follow it.
- A choice nobody can observe from outside the code (where a helper lives, how a module is imported) is a technical decision: record it in the ledger with `**Kind:** technical` and list it in the report.
- A question with real alternatives that change behaviour (what the user sees, what is stored, what an API returns) is the user's decision. Write the question with your recommendation, leave the remaining tasks unchecked, and end the turn. The next turn records the answer in the ledger and resumes.

`implement` never writes `A-NN` entries: an assumption adopted here is a decision the user never made.

When the code must diverge from the plan in a way that changes behaviour or contradicts a ledger entry, that is the user's decision too.
List structural deviations (an extra helper, a refactored test) in the final report; `doc` reconciles the plan with them.

Tell the user explicitly about every manual step the change needs (a migration to run, a secret to set, a service to enable), as `rules.md` requires.

## 8. Close

End every turn of this phase with this check: when every task is `[X]`, every story's tests are green, and nothing fails outside the baseline, close the phase.
A turn that stops early (a question, a checkpoint, a failure) does not close.

1. Append the coverage matrix to `tasks.md` from `formats/tasks.md`: one row per scenario, with its requirement, its test (file and test name) or verification outcome, and its status.
2. Set the ledger status to `implemented`.
3. Verify on disk: `tasks.md` and the files the plan named.
4. Report, in the conversation language, the test totals against the baseline, the coverage matrix gaps, the manual steps pending, and suggest `/specsmith doc`.
