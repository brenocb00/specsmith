# Phase: implement

Execute `tasks.md` story by story, test-first, until every story is green.

## 1. Gate

Read `tasks.md`, `plan.md`, `data-model.md` when present, the spec scenarios, and `rules.md`.
When the consistency section has open CRITICAL findings, list them and stop, unless the user waives them; record a waiver in the ledger.
When tasks still carry `(needs A-NN)`, ask the user to confirm or change those assumptions first, and update the ledger.

## 2. Work each story phase

Take the Foundation phase first when it exists, then the story phases in order.
Inside a phase, run `[P]` tasks together when your environment allows; run the rest in order.

For each story:

1. **Red.** Write the test tasks. Run them with the project's test command and watch each fail for the reason the scenario describes. A test that passes before the implementation exists tests nothing: fix the test.
2. **Green.** Before creating any file, read the analogue the plan names and follow its structure, naming, and helpers. Implement the layer tasks until the story's tests pass.
3. **Verify.** Run the story's verification task. For scenarios without `[auto]`, drive the feature as an end user would (E2E tooling or the running app) and record the outcome next to the task.
4. **Check.** Run the full test suite, lint, and typecheck from `rules.md`. The story is done when all are green.

Mark each task `[X]` in `tasks.md` the moment it completes, and report progress per task.

## 3. When something fails

- A failing test reveals a bug or a wrong test. Change a test only when the spec shows the test expects the wrong behaviour; otherwise fix the code.
- Stop on a failed sequential task and report the error with its context. For `[P]` tasks, finish the others and report the failures together.
- An unfixable failure ends the phase early: report what is done, what failed, and what the user must decide.

## 4. Decisions during implementation

Implementation keeps meeting small questions the plan did not answer.
A question with one obvious answer from the code or `rules.md` is a fact: follow it.
A question with real alternatives that change behaviour is a decision: stop, ask, record it in the ledger, then continue.
When the code must diverge from the plan in a way that changes behaviour or contradicts a ledger entry, record why in the ledger.
List structural deviations (an extra helper, a refactored test) in the final report; `doc` reconciles the plan with them.

Tell the user explicitly about every manual step the change needs (a migration to run, a secret to set, a service to enable), as `rules.md` requires.

## 5. Close

The phase is done when every task is `[X]`, every story's tests are green, and lint and typecheck pass.

1. Append the coverage matrix to `tasks.md` from `formats/tasks.md`: one row per scenario, with its requirement, its test (file and test name) or verification outcome, and its status.
2. Set the ledger status to `implemented`.
3. Verify on disk: `tasks.md` and the files the plan named.
4. Report the test totals, the coverage matrix gaps, the manual steps pending, and suggest `/specsmith doc`.
