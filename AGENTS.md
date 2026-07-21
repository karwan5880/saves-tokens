# saves-tokens agent guide

## Purpose

This repository researches practical ways to reduce token use without reducing correctness, safety, or maintainability. The canonical research entry points are:

- `docs/README.md` — overview
- `docs/playbook.md` — recommended workflow
- `docs/catalog.md` — comparison and caveats
- `docs/methods/` — one note per project or technique
- `graphify-out/GRAPH_REPORT.md` — generated navigation map; use it to locate relevant docs before broad reads

## Token-efficient working agreement

1. Start from Graphify’s report, the methods index, or `rg` to locate a relevant note; read only the files needed for the current task.
2. Keep work scoped: state goal, target paths, acceptance criteria, and non-goals before making a change.
3. Prefer focused, quiet diagnostics: targeted searches/tests and compact diffs. Preserve raw output whenever a failure needs exact evidence.
4. Make the smallest correct change. Do not remove tests, security checks, accessibility, migrations, compatibility behavior, or explicit requirements to save tokens.
5. For unrelated work, use a fresh session and save the compact template in `docs/templates/session-handoff.md` first.
6. Avoid parallel agents unless their work is genuinely independent and worth the duplicated context cost.
7. Do not install proxies, hooks, or tools that can access project content, credentials, or network traffic without explicit user approval and a source/security review.

## Documentation changes

- Add a focused README under `docs/methods/<slug>/README.md` for a newly researched named tool or distinct method.
- Update `docs/methods/README.md` and `docs/catalog.md` when adding an entry.
- Label project-reported savings as claims; do not present them as universal facts. Prefer official sources and reproducible, end-to-end evaluations.
