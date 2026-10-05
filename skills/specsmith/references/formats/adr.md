# ADR format (`docs/adr/NNNN-slug.md`)

Adapted from Matt Pocock's `domain-modeling` skill (MIT).
Number sequentially from the highest existing file; create `docs/adr/` lazily with the first ADR.
When the project already keeps decision records elsewhere, `rules.md` names that location and it wins.

```markdown
# <Short title of the decision>

<One to three sentences: the context, what was decided, and why.>
```

An ADR can be a single paragraph: its value is recording that a decision was made and why.
Add these only when they carry real value:

- **Status** front matter (`proposed | accepted | deprecated | superseded by ADR-NNNN`), when decisions get revisited;
- **Considered options**, when the rejected alternatives are worth remembering;
- **Consequences**, when non-obvious downstream effects need calling out;
- **Source**, the feature and `D-NN` the decision came from.

## The three gates

Offer an ADR only when all three hold:

1. **Hard to reverse**: changing your mind later has a meaningful cost.
2. **Surprising without context**: a future reader will wonder why it was done this way.
3. **A real trade-off**: there were genuine alternatives and one was picked for specific reasons.

Typical qualifiers: architectural shape, integration patterns between contexts, technology choices with lock-in, boundary and ownership decisions, deliberate deviations from the obvious path, constraints invisible in the code, and non-obvious rejections.
