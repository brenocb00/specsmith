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
- Data that cannot be regenerated: <every store that would lose real data if wiped, whatever its environment is called, or "none". No phase writes to these, and no command may overwrite or delete them.>
  - `<store>`: <what it holds>. Guard: <a check run before every command that proves the command cannot reach the store, for example "`DB_NAME` in `.env` ends in `_teste`" or "the app is stopped and `DATABASE_URL` points to a temporary file">. Backup: <a command that copies the store, or "none">.

## Artifact locations
- ADRs: <`docs/adr/` by default, an existing decision-record folder, or "none: no ADRs">
- Glossary: <`GLOSSARY.md` by default, or an existing glossary or glossary map>

## Spec paths
Pattern: <specs/<feature>/ or a hierarchy such as specs/<system>/<module>/<scope>/>
<How to classify a feature into the hierarchy, when hierarchical.>

## Commands
<Every command here only checks: it never writes source files, schema, or data beyond what the test itself creates and removes. Record the checking variant, for example `prettier --check`, not `prettier --write`.>
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
