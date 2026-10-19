# Specsmith

Decision-driven specs workflow for coding agents, built on relentless grilling with end-to-end traceability.

Specsmith combines two ideas:

- the **grilling** interview from [mattpocock/skills](https://github.com/mattpocock/skills): a design tree asked in rounds, facts looked up by the agent, decisions put to you, a living glossary and gated ADRs;
- the **delivery pipeline** of GitHub's Spec Kit: spec, plan, tasks, implement, with traceability from requirement to scenario to test.

The glue is the **ledger** (`decisions.md`): every answer you give is written down the moment you give it, and every requirement, task, and test traces back to one.
Grilling alone leaves most decisions in the chat; Spec Kit alone assumes too much and asks too little.

## Flow

```
setup (once per project)
  ↓
grill → prototype (optional) → spec → plan → tasks → implement → doc
```

| Command | What it does |
|---------|--------------|
| `/specsmith setup` | Interviews you about the project and writes `docs/specsmith/rules.md`: artifact language, environments and irreplaceable data, spec layout, artifact locations, check-only commands, conventions, constraints, doc targets. |
| `/specsmith grill <idea>` | Interviews you until every decision is made, writing the ledger, `GLOSSARY.md`, and ADRs as you go. |
| `/specsmith prototype` | Builds a clickable HTML prototype from the ledger and iterates with you. |
| `/specsmith spec` | Synthesizes the ledger into `spec.md`, with user stories, scenarios, and requirements that trace to decisions. |
| `/specsmith plan` | Designs the build inside the existing architecture, following analogue code. |
| `/specsmith tasks` | Writes `tasks.md` story by story, test-first, then checks spec, plan, and tasks for consistency. |
| `/specsmith implement` | Executes the tasks red → green, story by story, and records the coverage matrix. |
| `/specsmith doc` | Reconciles the docs with the built code and closes the change. |

Each phase stops at its end; you start the next one.

## When not to use it

Specsmith pays off when a change carries decisions: behaviour someone will see, data that will be stored, rules others will rely on.
Skip it for a typo, a one-line fix with an obvious answer, a dependency bump, or a throwaway spike.
When you are unsure, start with `/specsmith grill`: it tells you when an idea is trivial and lets you stop there.

## What lands in your repo

```
GLOSSARY.md
docs/adr/0001-<slug>.md
docs/specsmith/rules.md
specs/<feature>/
  decisions.md        ledger of the root change
  spec.md             source of truth for the feature
  prototype.html
  plan.md
  data-model.md
  tasks.md
  evolutions/001-<slug>/
    decisions.md      ledger of a later change
    plan.md
    tasks.md
```

## Install

Copy `skills/specsmith/` into the skills folder your agent reads.

**Claude Code**, per project or for every project:

```bash
cp -r skills/specsmith .claude/skills/
```

```bash
cp -r skills/specsmith ~/.claude/skills/
```

**Antigravity** and other agents that read `.agents/skills/`:

```bash
cp -r skills/specsmith .agents/skills/
```

Then run `/specsmith setup` in the project.

## Design decisions

The reasoning behind the workflow lives in [docs/decisions.md](docs/decisions.md).

## License

MIT. Parts of the interview protocol, glossary format, and ADR format are adapted from [mattpocock/skills](https://github.com/mattpocock/skills) (MIT); see [LICENSE](LICENSE).
