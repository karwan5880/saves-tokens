# saves-tokens

A research corpus, **not an app**: a source-linked map of techniques for reducing tokens / cost / quota / context in coding agents (Claude Code, Codex, Cursor, Kimi, …). All Markdown — no build step, no tests to run.

## Layout & contribution convention
- `docs/README.md` — entry map · `docs/playbook.md` — the workflow · `docs/catalog.md` — every technique/tool with its caveats.
- `docs/methods/<name>/README.md` — one folder per method/tool/project.
- **Adding a method:** create its folder here **and** link it from `catalog.md` + `README.md`. An unlinked doc becomes an isolated node in the graph.

## Query the graph — don't re-read 39 docs
A knowledge graph lives in `graphify-out/` (`GRAPH_REPORT.md` is the human summary). Ask it first:
- `graphify query "<question>"` · `graphify explain "<node>"` · `graphify path "<A>" "<B>"`
- After edits: `graphify update .` (structural, no LLM). Full re-extract runs an LLM step — use Haiku on the subscription, no API key: `export GRAPHIFY_CLAUDE_CLI_MODEL=haiku` then `graphify extract . --backend claude-cli --model haiku`.
- A `.graphifyignore` is already in place.

## Evidence discipline (the whole point of this repo)
- Keep distinct: **token count ≠ price ≠ subscription quota.** Prompt caching lowers price, not usually quota.
- Vendor/repo percentages are **claims, not proof** — label them, and prefer independent tests and cost-per-*successful*-task over raw compression ratios.
- Never document techniques for evading provider limits, billing, or policy.
