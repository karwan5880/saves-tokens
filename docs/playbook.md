# Token-saving playbook

## 1. Baseline

Run 5–10 representative tasks before changes. Record billed input, cached input, output, reasoning when available, turns, tool calls, latency, and cost per successful task. Use native usage/billing data; local estimates are secondary.

## 2. Bound task

```text
Goal: fix timeout handling in src/api/client.ts.
Evidence: inspect relevant file first.
Done when: retry handling matches intended behavior.
Constraints: no API change; no unrelated refactor.
Output: changed files, risks.
```

Use paths/symbols instead of dumps. Split work at real boundaries; do not create new sessions or agents for trivial steps.

## 3. Discover cheaply

1. Tree or compact architecture map.
2. `rg`, LSP, AST, or graph search.
3. Relevant ranges.
4. Targeted trace or diff.

Ignore generated output, dependencies, vendor files, coverage, and secrets unless they are the source of truth.

## 4. Keep tools useful

- Search symbols, not whole trees.
- Cap logs; disable color/progress.
- Keep exit status, filenames, assertions, and stack traces on failure.
- Fetch IDs/summaries first from web, database, or MCP tools; fetch detail on demand.

## 5. Reset stale context

Clear unrelated work. Before reset or compaction, save goal, facts, changed files, decisions, open question, and next action. Compaction is lossy; persist contracts if they must survive exactly.

## 6. Control output and scope

Request concise status: changed files and risks. Use output caps only for summaries or classification. Ask for minimal correct patches; never omit required validation, security, accessibility, migrations, or compatibility.

## 7. Add advanced methods last

Try maps, retrieval, compression, output skills, model routing, proxies, or hooks only after baseline workflow is solid. These add setup, security, and failure modes. Cache stable prompts; append volatile task data.

## 8. Validate

Compare baseline and one intervention on the same revision, prompt, model, reasoning level, permissions, and environment. Repeat because runs vary. Keep failures and cost-per-success; displayed compression alone is not savings.

Sources: [Claude costs](https://code.claude.com/docs/en/costs), [Kimi CLI](https://www.kimi.com/resources/kimi-code-introduction), [Cursor context](https://docs.cursor.com/en/guides/working-with-context), [Token Reduction Is Not Cost Reduction](https://arxiv.org/abs/2607.12161).
