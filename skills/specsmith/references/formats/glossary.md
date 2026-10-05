# Glossary format (`GLOSSARY.md`)

Adapted from Matt Pocock's `domain-modeling` skill (MIT).

```markdown
# <Context name>

<One or two sentences: what this context is and why it exists.>

## Language

**Order**:
<One or two sentences: what it is.>
_Avoid_: Purchase, transaction

**Customer**:
A person or organization that places orders.
_Avoid_: Client, buyer, account
```

## Rules

- **Be opinionated.** When several words name one concept, pick the best and list the rest under `_Avoid_`.
- **Keep definitions tight.** One or two sentences that say what the term is, not what it does.
- **Only project-specific terms.** General programming concepts stay out, however often the project uses them.
- **Vocabulary only.** Implementation details, decisions, and specs live elsewhere.
- **Group terms under subheadings** when natural clusters emerge.

## Single and multiple contexts

Most repos have one `GLOSSARY.md` at the root, created lazily with the first resolved term.
A `GLOSSARY-MAP.md` at the root marks a multi-context repo: it lists each context, where its `GLOSSARY.md` lives, and how the contexts relate.
In that case, write the term into the glossary of the context the feature belongs to, and ask when unclear.
