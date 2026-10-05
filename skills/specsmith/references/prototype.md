# Phase: prototype (optional)

Make the grilled decisions tangible as a clickable HTML prototype, and catch the decisions the interview missed.
Worth running when the feature introduces a new or complex screen; skip it otherwise.

## 1. Load

Read the active change's ledger and the glossary.
For an evolution, look at the screens the feature already has in the code, so the prototype shows the change in context.

## 2. Build

Write `<change>/prototype.html`: one self-contained file with inline CSS and JS.
Use a folder `<change>/prototype/` only when one file becomes unwieldy.

- Reflect every product decision in the ledger, and only those.
- Use realistic mock data in the artifact language.
- Simulate the interactions: navigation, dialogs, form validation, and the loading, empty, error, and success states the ledger decided.
- Follow the project's visual identity (colors, components, density) when the code or `rules.md` defines one.
- Build for the screen sizes the ledger requires.

Give the user the absolute path to open in a browser, and summarize the interactions to try.

## 3. Iterate

Ask what to change, apply it, and repeat until the user approves the prototype.
Each change of behaviour, content, or flow is a decision: record it in the ledger (new entry, or supersede an old one) before editing the HTML.
Purely cosmetic tweaks need no entry.

## 4. Close

The phase is done when the user approves the prototype and every behaviour it shows traces to a ledger entry.

1. Set the ledger status to `prototyped`.
2. Verify on disk: the prototype and the ledger.
3. Report the path, the decisions added during iteration, and suggest `/specsmith spec`.
