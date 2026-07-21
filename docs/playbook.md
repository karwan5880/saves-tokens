# Token-saving playbook

## 1. Establish a baseline

Run 5–10 representative tasks before changing anything. Include bug fixes, feature work, tests, and unfamiliar-code exploration. Capture total tokens and final correctness, not just a compressor’s before/after text size.

Claude Code offers `/usage` and `/cost` (API billing); its [cost guide](https://code.claude.com/docs/en/costs) recommends clearing unrelated context, controlling compaction, using model selection, and preprocessing hooks. Kimi Code exposes `/usage`, `/clear`, and `/compact` in its [CLI overview](https://www.kimi.com/resources/kimi-code-introduction). Codex and Cursor usage displays vary by surface and plan; use their current account/IDE usage views and API billing records when applicable.

Useful measurements:

| Measure | Why it matters |
|---|---|
| billed input / cached input / output / reasoning tokens | identifies the real dominant component |
| turns, tool calls, repeated reads | exposes exploration loops and noisy tooling |
| task pass rate and cost per successful task | prevents false “savings” that cause rework |
| context size just before each turn | shows stale-history or over-injection problems |
| latency and human intervention | a cheap run that takes twice as long may not be a win |

## 2. Prevent context from entering in the first place

Use a task contract in the opening prompt:

```text
Goal: fix timeout handling in src/api/client.ts.
Evidence: inspect that file and its direct tests first.
Done when: retry policy has tests and `pnpm test client` passes.
Constraints: no API changes; do not refactor unrelated modules.
Output: concise summary, files changed, tests run, remaining risks.
```

This narrows autonomous exploration and makes success testable. Split a large objective at natural boundaries (reproduce → diagnose → plan → implement → verify), but do not turn every tiny substep into a separate agent session: each new agent has its own prompt/context overhead.

Prefer symbol/path references to content dumps. In Cursor, the official guidance is to use surgical `@` context; `@folder` can include its full contents and, especially in Max mode, can consume the model’s full context window and increase cost ([Cursor context guide](https://docs.cursor.com/en/guides/working-with-context), [folder docs](https://docs.cursor.com/context/%40-symbols/%40-folders)). In Claude Code, an `@` reference injects the full file and its `CLAUDE.md` tree, so a bare path is cheaper when full injection is not necessary ([Anthropic help](https://support.claude.com/en/articles/14552983-models-usage-and-limits-in-claude-code)).

Keep instruction files short and scoped. Put universal, stable conventions at the root; put domain-specific rules beside the relevant subtree; remove stale procedures and large examples. Referencing files from rules can itself inject them in Cursor ([rules docs](https://docs.cursor.com/context/rules)).

## 3. Use a cheap discovery funnel

Make the agent locate before it reads:

1. file tree / compact architecture map;
2. fast text or symbol search (`rg`, language server, AST/knowledge graph);
3. relevant function ranges, not every matching file;
4. targeted test, diff, or runtime trace.

For humans, the equivalent is: tell the agent where you believe the change belongs and what you already tried. This is usually more valuable than a prose-compression plugin.

Use ignore rules to exclude generated assets, dependencies, vendor directories, lockfiles (unless changing dependencies), minified bundles, coverage, screenshots, build output, and secrets. Do not exclude the actual source of truth merely to save tokens.

## 4. Make tool calls and results compact

Prefer commands designed to return decisions, not logs:

- `rg -n "symbol" src` instead of recursive directory dumps.
- run one affected test first; request full suite only after it passes.
- limit log lines, turn off color/progress, and preserve errors, failing assertions, filenames, stack frames, and exit status.
- inspect `git diff --stat` / a single hunk before a repository-wide diff.
- request summaries from database/web/MCP tools, then fetch the exact records needed.

Do not blindly strip test output. Verbose output is indispensable when a failure needs its assertion, snapshot, or stack trace.

## 5. Manage the session lifecycle

Long threads grow expensive because prior messages and tool results are repeatedly considered. Clear when changing projects or unrelated tasks. Before clearing, save a small handoff note containing: goal, confirmed facts, files changed, tests/results, decisions, open question, and exact next action.

Claude Code automatically uses prompt caching and auto-compaction, and supports manual `/compact` instructions; Anthropic recommends `/clear` between unrelated tasks ([official cost guide](https://code.claude.com/docs/en/costs)). Custom compaction instructions should specify what facts to preserve, e.g. “retain API contracts, changed files, test commands/results, decisions, and TODOs; discard command noise.” Kimi likewise provides `/compact` and `/clear` ([Kimi CLI commands](https://www.kimi.com/code/docs/en/kimi-code-cli/reference/kimi-command)).

Compaction is lossy. Save implementation plans, ADRs, and test status in files if they must survive exactly. Avoid repeatedly compacting a muddled thread; a fresh session plus a good handoff is often safer.

## 6. Control output and implementation scope

Ask for “no preamble; concise bullets; do the work; report only changed files/tests/risks.” This reduces natural-language output, which is then part of later context. A short output cap (`max_tokens` / `max_output_size`) is useful for classification, planning, and tool summaries, but can truncate code or an important warning.

Ask for the smallest correct patch: reuse existing patterns, avoid speculative abstractions, do not add optional features/tests/docs outside acceptance criteria. This saves output tokens and review/rework tokens. It is a quality discipline, not permission to omit validation, security checks, migrations, or user requirements.

## 7. Route models and reasoning deliberately

Use a capable model/reasoning effort for ambiguous design, deep debugging, and final verification; route mechanical transformations, classification, extraction, or summarization to a cheaper/faster model when quality is demonstrably adequate. Turn high reasoning off/down for straightforward edits if the product permits it.

Kimi Code’s configuration includes a per-request `max_output_size` and a setting controlling whether prior reasoning is retained ([configuration docs](https://www.kimi.com/code/docs/en/kimi-code-cli/configuration/config-files)). That makes the tradeoff explicit: retaining reasoning may help continuation but enlarges context. GLM/Kimi/OpenAI/Anthropic-compatible gateways can similarly expose model and output controls, but exact flags are client-specific.

## 8. Validate the intervention

Use a paired A/B design: same repository revision, task prompt, model, reasoning level, permissions, environment, and test command. Randomize order and repeat runs because agents are stochastic. Publish the raw trajectories or at least aggregate billed counts and failures.

Recent research stresses why: one large analysis found token usage varies dramatically between identical agentic tasks and higher spend does not reliably increase accuracy ([How Do AI Agents Spend Your Money?](https://arxiv.org/abs/2604.22750)). A separate 2,848-run study warns that context reducers can lower displayed token counts but raise cost per solved task or damage patch quality ([Token Reduction Is Not Cost Reduction](https://arxiv.org/abs/2607.12161)).
