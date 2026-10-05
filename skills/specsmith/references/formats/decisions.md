# Ledger format (`decisions.md`)

One ledger per change: in the feature directory for the root change, in `evolutions/NNN-<slug>/` for an evolution.
Front matter keys and field labels (`**Decision:**`, `**Why:**`, `**Rejected:**`, `**Assumption:**`, `**Kind:**`, `**Status:**`) and status values stay in English, so every phase can parse them; titles and content use the artifact language.

```markdown
---
feature: <feature path relative to the spec root>
change: root | evolutions/NNN-<slug>
status: grilling | grilled | prototyped | specified | planned | tasked | implemented | done
language: <artifact language, only when no rules.md exists>
---

# Decisions: <feature title>

<One or two sentences: the idea as the user first stated it.>

## D-01 - <short title>
**Decision:** <what was decided, precise enough to test>
**Why:** <the reason the user gave, or the one they accepted>
**Status:** decided

## D-02 - <short title>
**Decision:** ...
**Why:** ...
**Rejected:** <alternatives worth remembering, only when the rejection is non-obvious>
**Status:** superseded by D-09

## A-01 - <short title>
**Assumption:** <the recommended answer adopted without the user deciding>
**Status:** unconfirmed
```

## Rules

- One entry per answered question. Write it the moment the answer arrives.
- `D-NN` and `A-NN` share one sequence per feature: `D-01, D-02, A-03, D-04`. An evolution continues the feature's highest number.
- Keep the precise answer: numbers, orderings, negatives ("never", "only"), and defaults survive verbatim.
- A changed mind supersedes; it never edits or deletes. The old entry gets `superseded by D-NN`, the new one explains why.
- Confirming an assumption keeps its ID and sets `**Status:** confirmed`; changing it adds a new `D-NN` that supersedes it.
- Technical decisions from `plan` and `implement` go in the same ledger, with `**Kind:** technical` under the title.
- Only decisions go here. Terms go to the glossary; long rationale for a hard-to-reverse decision goes to an ADR that the entry links.
