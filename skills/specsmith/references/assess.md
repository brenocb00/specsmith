# Command: assess

An honest assessment of one point, on demand: a ledger decision, a recommendation, an argument the user just made, or an idea nobody has discussed yet.
It runs at any time, inside a phase or outside any feature; it passes no gate and sets no status.

## 1. Identify the point

Take the point from the argument; with none, take the last decision, recommendation, or argument in the conversation.
State it in one line, with its `D-NN` or `A-NN` when it has one, plus the claim under assessment.
When it stays ambiguous, ask which point and stop.

## 2. Gather the facts

Look up every fact the point rests on: code, data, docs, the web.
A claim the environment can answer (a frequency, a cost, how the code behaves today) gets checked, never taken as given, whoever made it.
Stay inside the allowed environments.
A claim you cannot check is marked unverified, with the way to check it.

## 3. Weigh

State the criteria first: what the spec and ledger say matters for this point, then correctness, cost, risk, and reversibility.
Judge every alternative against the same criteria: the user's, your own earlier recommendation, and the obvious ones.
Who proposed an option is not a criterion.
Look for an option nobody considered.

## 4. Report

```
**Point:** <D-NN - title, or the claim>
**Strongest case:** <the argument under assessment, stated at least as well as its author stated it>
**Facts:** <what you checked, with sources>
**Unverified:** <claim - how to check it>
**For:** <what the position gets right>
**Against:** <what it gets wrong or leaves out>
**Unconsidered option:** <only when one exists>
**Verdict:** agree | disagree | agree if <condition> - <one-line reason>
**Would change my mind:** <the fact or argument that would flip the verdict>
**Remaining risk:** <the strongest risk left, also when you agree>
```

Agreeing is a valid verdict, and so is disagreeing with your own earlier recommendation.
Never soften a verdict because the user holds the other view, and never invent objections to look independent.
End by asking whether to keep, change, or adjust the point, then stop.

## 5. Record

`assess` writes nothing until the user answers.

- **Changed or newly decided, inside a feature:** record a new `D-NN` in the active change's ledger, superseding the old entry when there is one, as `formats/decisions.md` describes.
- **Kept, or outside a feature:** record nothing.

When the spec, plan, tasks, or code already reflect a changed decision, list them and name the phase that reconciles them; edit none of them here.
Then return to the phase in progress, when there is one.
