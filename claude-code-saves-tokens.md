# Claude Code token-saving methods, tools, and skills

This is a research catalog of methods people use to reduce Claude Code context growth, billed tokens, subscription usage, or output. It is not a list of guaranteed savings: those four outcomes are different, and most published percentages are project claims.

## Evidence labels

- **Official:** Anthropic documents the behavior, but does not promise a universal saving.
- **Project claim:** measured or estimated by the tool's authors.
- **Independent test:** evaluated by someone other than the project author; inspect the task set and metric.
- **Research:** result from a paper or benchmark; transfer to Claude Code may be limited.
- **Community practice:** repeated user technique without controlled evidence.

## Claude Code's built-in controls

| Method | What it targets | Evidence and limits |
|---|---|---|
| `/clear` between unrelated tasks | stale conversation resent on later turns | **Official.** Anthropic calls clearing between tasks a high-impact habit. Save a handoff first if facts must survive. |
| `/compact <focus>` at natural breaks | old messages and tool results | **Official.** Compaction replaces history with a shorter summary and costs a summarization call. It is lossy; use `/rewind` when the branch should be discarded instead. |
| `/context` | hidden startup and session context | **Official diagnostic.** Shows contributions from instructions, tools, memory, messages, and other context. It measures before you optimize. |
| `/usage` and provider billing | token and cost visibility | **Official diagnostic.** Local dollar figures can be estimates; API/provider billing is authoritative. Subscription users should not equate an API cost estimate with plan quota. |
| Prompt caching | repeated, unchanged prompt prefixes | **Official.** Claude Code manages it automatically. Cache reads can reduce price and latency, but do not remove the content from the context window. Model, effort, tool-set, or prefix changes can rebuild the cache. |
| Model and effort selection | per-token price and reasoning spend | **Official.** Route bounded mechanical work to an adequate cheaper model; a failed attempt plus a retry can cost more than one capable run. |
| Disable unused MCP servers | tool-definition/context overhead and tool confusion | **Official.** Claude Code defers MCP definitions by default, but enabled servers still have names and can expand when used. Inspect with `/context` and `/mcp`. |
| Code-intelligence plugins | broad grep/read exploration | **Official mechanism.** Symbol navigation can reduce unnecessary file reads. The actual saving depends on index quality and the task. |
| Focused subagents | verbose research or logs entering the main conversation | **Official mechanism.** Only the result returns to the parent, but the subagent has its own system prompt, tools, context, and bill. Isolation can save main-context space while increasing total tokens. |

Sources: [cost management](https://code.claude.com/docs/en/costs), [context window](https://code.claude.com/docs/en/context-window), [prompt caching](https://code.claude.com/docs/en/prompt-caching), and [extension context costs](https://code.claude.com/docs/en/features-overview).

## Repository maps, retrieval, and memory

These tools try to replace repeated repository archaeology with compact, queryable structure.

| Project | Claude Code method | Reported evidence | Main caveat |
|---|---|---|---|
| [Graphify](https://github.com/safishamsi/graphify) | Builds a graph over code/docs/schemas; query the graph before opening exact source ranges. | **Project/community claim:** examples include a 71× reduction. | Indexing costs time/tokens; stale graphs and lost literal anchors can cause rework. [Research note](docs/methods/graphify/README.md). |
| [Repowise](https://github.com/repowise-dev/repowise) | Local code graph, git history, generated docs, ADRs, and task-shaped MCP retrieval. | **Project claim:** early paired SWE-QA runs report up to 70% fewer tool calls, 89% fewer file reads, and 36% lower cost/query at comparable answer quality. | Authors say a more rigorous benchmark is still in progress; AGPL-3.0; index freshness and generated docs need checking. [Research note](docs/methods/repowise/README.md). |
| [OpenWolf](https://github.com/cytostack/openwolf) | Hooks maintain project anatomy, preferences, fixes, and read history to avoid rediscovery. | **Project claim:** 65.8% average reduction across its own sessions. | Its ledger is estimation-based; hooks read repository activity and add instructions; AGPL-3.0. [Research note](docs/methods/openwolf/README.md). |
| [ContextSniper](https://github.com/Calluking/ContextSniper) | Hybrid retrieval and an intention-aware gate return small evidence packets while raw evidence remains recoverable. | **Research/pilot:** reports 38.9% lower Claude Code tokens and 27.3% lower estimated cost. | Recent preprint and pilot, not broad independent validation; exact identifiers and edit anchors must survive. [Research note](docs/methods/contextsniper/README.md). |
| Code maps, LSP, AST, ctags, `rg` | Locate symbols, callers, imports, and relevant ranges before reading files. | **Community practice;** also consistent with Anthropic's recommendation to use code intelligence. | A stale or oversized map may cost more than direct search. [Research note](docs/methods/code-maps/README.md). |
| Compact handoff files | Persist goal, facts, changed paths, decisions, failures, and next action before clearing. | **Community practice** built on official `/clear` and `/compact` behavior. | Summaries are lossy; contracts and code remain the source of truth. [Template](docs/templates/session-handoff.md). |

## Tool-output and context compressors

These target file reads, command output, web/MCP responses, or conversation payloads. Compression ratio is not the same as task-level cost reduction.

| Project | Mechanism | Reported evidence | Main caveat |
|---|---|---|---|
| [Context Mode](https://github.com/mksglu/context-mode) | Claude Code plugin/hooks route large tool work through a local sandbox and SQLite FTS5 store; only summaries or selected records enter context. | **Project claim:** 315 KB became 5.4 KB in its demonstration, described as 98% context saving for those payloads. | This is selected raw-output compression, not 98% off a complete task. Hooks/MCP can change routing and command behavior; Elastic License 2.0. [Research note](docs/methods/context-mode/README.md). |
| [RTK](https://github.com/rtk-ai/rtk) | Rewrites supported shell commands and filters progress, repeated lines, and routine output. | **Project claim:** 60–90% compression on supported output. **Independent test:** real compression, but +7.6% modeled task cost at low reasoning and roughly neutral at high reasoning. | Keep a raw-output bypass; never compress away failure, migration, security, or patch diagnostics. [Research note](docs/methods/rtk/README.md). |
| [Tamp](https://github.com/sliday/tamp) | Local HTTP proxy applies lossless and optional lossy transforms to accumulated agent payloads. | **Project claim:** 45% fewer tokens with no quality regressions in 216 author-run A/B tasks at its tested setting. | A proxy sees prompts, code, tool data, and credentials and may alter caching/protocol semantics. Some modes are lossy. [Research note](docs/methods/tamp/README.md). |
| [Headroom](https://github.com/chopratejas/headroom) | API proxy compresses context before provider requests. | **Project mechanism;** no independently verified universal saving recorded here. | Same proxy trust boundary; measure provider-billed totals, not the proxy's counter. [Research note](docs/methods/headroom/README.md). |
| Quiet command design | Use targeted `rg`, line ranges, focused tests, `git diff --stat`, no ANSI/progress, and bounded logs. | **Community practice.** Low-risk because no middleware is required. | Preserve exit status, assertions, stack traces, filenames, error text, and diff anchors; rerun raw on failure. [Research note](docs/methods/command-design/README.md). |
| Filtered MCP/API retrieval | Return IDs and compact summaries first; filter by path/date/fields and paginate; fetch selected details later. | **Engineering technique.** Directly bounds tool results. | Tool schemas also cost tokens; overly vague schemas cause bad calls and retries. [Research note](docs/methods/mcp-payloads/README.md). |

## Skills and instruction pruning

| Project or method | Mechanism | Reported evidence | Main caveat |
|---|---|---|---|
| [Caveman](https://github.com/juliusbrussee/caveman) | Claude Code skill asks for terse, telegraphic responses and removes conversational filler. | **Project claim:** roughly 65% fewer output tokens. **Independent test:** 8.5% lower modeled cost on paired real agentic tasks. | It mainly affects assistant prose, not file/tool input or hidden reasoning. Preserve decisions, failures, and risks. [Research note](docs/methods/caveman/README.md). |
| [Ponytail](https://github.com/DietrichGebert/ponytail) | Skill pushes Claude toward the smallest sufficient implementation and away from speculative abstraction. | **Community/project method;** no direct task-level percentage established here. | Indirect saving only; must not remove tests, validation, security, accessibility, migrations, or compatibility. [Research note](docs/methods/ponytail/README.md). |
| [Skillreaper](https://github.com/thousandflowers/skillreaper) | Audits Claude Code transcripts to find skills, agents, and MCP servers that are loaded but unused, then supports reversible pruning. | **Project/community claim:** users may carry thousands of tokens of unused descriptions; the tool reports estimates from local configuration and transcripts. | Absence in past transcripts does not prove future irrelevance. Review the prune plan and keep backups; MIT. [Research note](docs/methods/skillreaper/README.md). |
| Short `CLAUDE.md` plus scoped rules/skills | Keep universal rules always loaded; move specialized details behind path triggers or skill invocation. | **Official mechanism/community practice.** Claude documents that root instructions, skill descriptions, and tool names consume startup context. | Over-pruning removes constraints and causes retries. Keep security and repository invariants visible. |
| Compress verbose skills | Remove duplicated explanation/examples while preserving triggers, procedures, constraints, and failure handling. | **Research:** SkillReducer reports 48% description and 39% body compression across its study, with 2.8% higher functional quality. | This is a skills benchmark, not a Claude Code billing study. Re-test every compressed skill. [Paper](https://arxiv.org/abs/2603.29919). |

## Model routing and alternate agents

- **Route bounded subtasks:** use a cheaper adequate model for extraction, classification, or straightforward searches; reserve stronger reasoning for ambiguous debugging, architecture, and final verification. This reduces cost only when the cheaper route does not create retries. [Method note](docs/methods/model-routing/README.md).
- **Use subagents for isolation, not assumed savings:** a subagent can keep huge logs out of the parent, but it duplicates system/tool context. Agent teams generally multiply tokens further.
- **Caveman Code:** an alternate terminal agent, not a Claude Code plugin. Its project reports 1.93× fewer tokens than Codex on a 25-task MicroBench. Cross-agent harnesses are not equivalent, so treat this as a project benchmark, not a Claude Code saving. [Research note](docs/methods/caveman-code/README.md).

## Research methods not yet turnkey Claude Code defaults

- **SWEzze:** code-aware context distillation for issue resolution. The paper reports about 6× compression, 51.8–71.3% lower token budgets, and higher resolution rates in its evaluated setup. This is benchmark-specific research, not a drop-in Claude Code guarantee. [Paper and note](docs/methods/swezze/README.md).
- **ContextSniper:** has a Claude Code pilot, but remains recent research rather than a mature default.
- **Hierarchical summaries, RAG, result caching, and structured state:** useful architecture patterns for custom agent systems; their indexing, invalidation, and retrieval costs belong in the total.

## What current evidence says

The strongest warning comes from the paired study [Token Reduction Is Not Cost Reduction](https://arxiv.org/abs/2607.12161): across 2,848 analyzed provider-billed Claude Code runs, removing estimated tool-output tokens did not reliably lower task cost. One intervention removed 38% of estimated raw output yet increased paired cost by 6.8%; a separate compressed-code experiment damaged literal edit anchors and reduced patch application.

That does not mean compression never works. It means every tool above should be evaluated on complete successful tasks, not on bytes removed from one payload.

Minimum comparison:

1. Same repository revision, task, model, effort, permissions, and acceptance tests.
2. Baseline versus one intervention; repeat and randomize runs.
3. Record uncached input, cache writes/reads, output, turns, tool calls, latency, retries, and provider-billed cost.
4. Count failures. Compare **cost per successful task**, not the tool's “tokens saved” counter.

[ccusage](https://github.com/ryoppippi/ccusage) can summarize Claude Code usage logs, but it is a measurement tool rather than a reducer; provider billing or plan usage remains authoritative. See the [measurement note](docs/methods/measurement/README.md).

## Security rule

Do not install a proxy, hook, plugin, or MCP server merely because it advertises a large percentage. Review its source, install scripts, license, network destinations, credential handling, command interception, stored data, update path, and uninstall procedure. Pin versions, back up Claude configuration, and retain an unmodified/raw-output path.
