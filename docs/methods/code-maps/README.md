# Code maps and structural search

## Method

Use file maps, symbols, `rg`, language-server/AST search, ctags, imports/call graphs, and compact architecture docs to locate relevant code before reading full files.

## Best practice

Keep map entries short: purpose, public symbols, dependencies, and approximate size. Treat the map as a routing layer, not a source of truth—open precise source ranges before editing. Regenerate or update after architectural change.

## Caution

A giant map or stale summary can cost more than it saves and can mislead dynamic/reflection-heavy codebases.
