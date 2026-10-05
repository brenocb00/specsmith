# Rounds

The interview protocol used by `setup`, `grill`, and `plan`.
Adapted from Matt Pocock's `grilling` skill (MIT), with a persistent ledger added.

## The design tree

Interview the user relentlessly until you reach a shared understanding.
Map the topic as a **design tree**: every decision branches into the decisions that hang off it.

The **frontier** is every open decision whose prerequisites are already settled: the questions you can ask now without guessing at answers you have not heard yet.

## A round

Ask the whole frontier in one round.
Number the questions with the ledger IDs they will receive, and give your recommended answer for each.
Then wait for the user's answers.

```
❓ **D-07 - <question title>**: <question body, as long as it needs, including the options>

➡️ <your recommended answer and the one-line reason>

---

❓ **D-08 - <question title>**: <question body>

➡️ <your recommended answer>
```

A question whose answer depends on another question still open in this round belongs to a later round.

## After each round

1. Write every answer to the ledger as its own entry, in the format of `formats/decisions.md`, before anything else. "Recommended" or "yes" means the recommendation you stated becomes the decision.
2. Apply the domain-modeling moves in `grill.md` to the terms the answers introduced.
3. Recompute the frontier: settled decisions unblock the questions that depended on them.
4. Ask the next round.

When an answer is ambiguous, ask a short follow-up under the same ID.
When an answer contradicts an earlier decision, ask which one stands, then mark the loser `superseded by D-NN`.

## Facts versus decisions

Finding facts is your job.
When a frontier question needs a fact (how the code works today, what a config says, what a library supports, how other products solve it), look it up yourself or dispatch a subagent when your environment has them.
Only the questions downstream of a pending lookup wait for it; ask the rest of the frontier now.
Cite real sources for anything taken from the web.

Decisions belong to the user: put each one to them and wait.

## "Assume the rest"

The user may end the interview early at any time ("assume the rest", "good enough", "use your recommendations").
Record every remaining frontier question as an assumption (`A-NN`) holding your recommended answer, then close.
Assumptions stay visible: the spec lists them, and `tasks` flags every task that depends on one.

## Done

The interview is done when the frontier is empty, the ledger holds one entry per answered question, and the user confirms you reached a shared understanding.
The calling phase may add its own coverage bar on top.
