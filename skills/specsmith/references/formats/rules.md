# Rules format (`docs/specsmith/rules.md`)

Written by `setup`, read by every phase.
Every section is present; a section with nothing to say holds "none".
Each rule carries its reason, so a future reader can tell a rule from an accident.

```markdown
# Specsmith rules

## Language
Artifacts: <language>

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
