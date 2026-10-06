# Rules format (`docs/specsmith/rules.md`)

Written by `setup`, read by every phase.
Every section is present; a section with nothing to say holds "none".
Each rule carries its reason, so a future reader can tell a rule from an accident.

```markdown
# Specsmith rules

## Language
Artifacts: <language>

## Authority
<Existing rule files this file defers to, for example `AGENTS.md`, or "none: this file is the source".>
<A rule in an authority file wins over any default of the specsmith references; this file never repeats one.>

## Environments
<Where the environment rules live (an authority file section, or here), then what each phase may touch.>
- grill, spec, plan, tasks, doc: <for example "no database or external API; facts come from code and docs">
- implement: <for example "test database and sandbox APIs only, after checking the env file">
- Production checks: <for example "a manual step for <person>, with the exact command">

## Spec paths
Pattern: <specs/<feature>/ or a hierarchy such as specs/<system>/<module>/<scope>/>
<How to classify a feature into the hierarchy, when hierarchical.>

## Commands
- Unit tests: <command>
- Integration tests: <command or none>
- End-to-end: <command or none>
- Lint: <command>
- Typecheck: <command or none>
- Build: <command or none>

## Architecture and conventions
- <Rule, stated as a checkable fact.> Reason: <why>.
- Layer order for new code: <for example types → repository → service → route → components → page>

## Workflow constraints
- Tasks never generated: <kinds, with reason>
- Sections every spec includes: <for example "Mobile version", with reason>
- Manual steps to announce: <for example "every migration must be run by hand in the dashboard">

## Documentation targets
- `<path>`: <what it documents and for whom>
```
