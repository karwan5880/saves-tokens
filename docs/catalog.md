# Catalog: techniques, tools, and caveats

This catalog is intentionally broad, not an endorsement. “Claim” means the source’s stated mechanism or result, not a verified promise.

## A. Built-in product controls

| Method | Products | What it saves | Evidence / notes |
|---|---|---|---|
| Fresh sessions, manual/automatic compaction, prompt caching, usage tracking, model choice, preprocessing hooks | Claude Code | stale context; cache can lower repeated-prefix cost | **Official.** [Manage costs](https://code.claude.com/docs/en/costs); [compaction](https://platform.claude.com/docs/en/build-with-claude/compaction). Cache savings are not necessarily token-count or quota savings. |
| Surgical `@file` / `@code`; avoid broad `@folder` | Cursor | accidental full-folder injection | **Official.** [Working with context](https://docs.cursor.com/en/guides/working-with-context), [folder behavior](https://docs.cursor.com/context/%40-symbols/%40-folders). |
| `/clear`, `/compact`, `/usage`, output cap, choice to retain prior reasoning | Kimi Code / compatible providers | history and output; retained thinking tradeoff | **Official.** [overview](https://www.kimi.com/resources/kimi-code-introduction), [config](https://www.kimi.com/code/docs/en/kimi-code-cli/configuration/config-files). |
| compact task prompt, scoped files, project instructions, optional diff summaries | Codex | input context and exploratory turns | **Official support documentation** says Codex sends prompt, high-level context and optional diff summaries; exact controls differ between CLI, app, and cloud ([Codex CLI getting started](https://help.openai.com/en/articles/11096431)). |

## B. Human workflow and prompt patterns

| Pattern | Mechanism | Common failure mode |
|---|---|---|
| Precise goal + target paths + acceptance tests + non-goals | less exploration and fewer correction turns | overconstraining blocks a necessary adjacent fix |
| Explore → plan → implement → verify, with persisted handoff | avoids rediscovery after new/compacted sessions | using an elaborate plan for a trivial change |
| Batched, decision-oriented request | fewer conversational turns | batching unrelated work creates huge context |
| Minimal patch / “lazy senior developer” | less generated code and prose | cutting necessary checks or maintainability |
| Terse response convention / no preamble | reduces assistant text retained in history | unreadable handoffs; missing risks |
| Scoped, concise agent instructions | avoids loading irrelevant rules/examples | deleting important project constraints |
| Targeted search / AST symbols before file reading | replaces raw code with location metadata | summary becomes stale or misses dynamic behavior |
| Quiet focused commands and structured tool results | reduces tool-result payload | removes the one diagnostic detail needed |
| Ignore generated/noisy artifacts | fewer wasteful searches/reads | ignores source generated at build time that must be edited |
| Intentional model/reasoning routing | lower cost per easy subtask | weak model causes retries or bad code |
| Minimize subagents | avoids duplicated independent context windows | loses useful parallelism on genuinely separable work |

## C. Context maps, retrieval, and memory

| Project | Core method | Scope / claim | Caveats |
|---|---|---|---|
| [Graphify](https://github.com/safishamsi/graphify) | compiles folders/code/docs/schemas into a queryable knowledge graph; agent queries it rather than reading raw content | Multi-agent skill; project documentation and community material advertise very large reductions (including a 71× example). | **Project claim.** Extraction itself costs time/tokens/API money; graph quality/freshness and query retrieval determine results. Best for large, stable, cross-cutting codebases. |
| [OpenWolf](https://github.com/cytostack/openwolf) | project anatomy, learned preferences, bug log, read tracking, lifecycle hooks | Works with Claude Code, Codex and OpenCode; repository claims 65.8% average reduction over its own sessions. | **Project claim; AGPL-3.0.** Its ledger is estimation-based (project says ~15% accuracy); hooks/instructions add their own context and may fail. Audit generated files and hooks. |
| [ContextSniper](https://github.com/Calluking/ContextSniper) / AntTrail | hybrid retrieval, ranking and intention-aware compact evidence packets | Paper reports lower tokens/cost in pilot settings. | **Research/preprint.** Evaluate on your repository; avoid losing exact code/edit anchors. |
| Code maps, ctags/LSP/AST search, repository `ARCHITECTURE.md`, ADRs | user-maintained or generated semantic index | universally applicable | Keep summary entries short and verified; a giant map can cost more than targeted reads. |
| Session memory / compact handoff notes | externalizes durable facts so old chat can be dropped | all agents | Store decisions, contracts, test results and next action—not every transcript line. |

## D. Compressing terminal, tool, web, and MCP payloads

| Project / method | Core method | Scope / claim | Caveats |
|---|---|---|---|
| [RTK (Rust Token Killer)](https://github.com/rtk-ai/rtk) | intercepts/rewrite eligible shell commands and returns compact command output | Project reports 60–90% compression for supported output. | **Project claim.** An independent SkillsBench trial found +7.6% modeled cost at low reasoning and about neutral at high reasoning, despite real compression ([JetBrains test](https://blog.jetbrains.com/ai/2026/07/rtk-claude-code-token-savings/)). Keep an escape hatch for full output. |
| [Headroom](https://github.com/chopratejas/headroom) | API/proxy context compression | Claude Code-oriented; reduces payloads before provider | **Third-party proxy.** It may receive prompts/code/credentials and can disrupt caching, tool protocols, or debugging. Measure billed totals, not its local count. |
| Command design (`rg`, line ranges, test filters, no ANSI/progress, capped logs) | manual loss-aware compression | all terminal agents | safest first step; retain failure payloads and exact diffs when patching. |
| MCP/tool output schemas, pagination and server-side filtering | return IDs/summaries first, fetch detail on demand | all MCP-enabled agents | schema descriptions themselves consume context; do not expose dozens of broad tools in every session. |
| Images/screenshots: resize, crop, JPEG when sufficient | lower multimodal payload/context | visual agents | do not over-compress text, error output, or pixel-critical UI details. |

## E. API/application-level architecture

These patterns matter when building an agent with Claude, OpenAI/Codex-family, GLM/Z.ai, Kimi, or an OpenAI-/Anthropic-compatible gateway. They are not usually configurable inside a hosted IDE alone.

| Method | Mechanism | Watch-outs |
|---|---|---|
| Prefix/prompt caching | keep stable system prompt, tools, policy and project baseline byte-for-byte at the beginning; append volatile task data | typically lowers input price/latency, not necessarily usage quota; changing the prefix destroys cache hits. Claude Code documents prompt caching as an automatic cost optimization ([official guide](https://code.claude.com/docs/en/costs)). |
| Server-side conversation state / compaction | retain a compact summary and durable state rather than replay every raw turn | summaries need versioning and an exact source-of-truth reference for code/decisions. |
| Retrieval-augmented generation (RAG) | index chunks/symbols; retrieve a small, task-specific evidence set | naive chunking loses call relationships and gives stale/irrelevant passages; code-aware retrieval/maps are preferable. |
| Semantic + lexical + structural retrieval | combine embeddings with filename/symbol/text search, import/call graph and recency | more infrastructure and index-maintenance cost; measure end-to-end, including retrieval model calls. |
| Hierarchical summaries | file → package → repository summaries, expanding only selected branches | summary drift and duplicated facts can outweigh benefit. |
| Contextual compression / LLMLingua-style summarization | replace retrieved text/tool outputs with a shorter representation | can remove literal anchors, identifiers and exact error details required for an edit. |
| Structured state instead of prose | store decisions, plan, changed paths, test status and open questions in compact JSON/Markdown fields | tool schemas and JSON keys have tokens too; do not serialize full transcripts. |
| Tool schema minimization | expose only tools relevant to the session and keep names/descriptions/examples compact | avoid opaque names; a failed tool choice costs more than a few schema tokens. |
| Server-side filtering/pagination | query with path, date, status, limit and fields; return IDs/snippets before full records | requires a follow-up fetch and sensible defaults. |
| Result caching and deduplication | cache deterministic searches, docs, file maps and repeated tool calls | invalidate on repository revision and configuration changes. |
| Batching independent retrievals | fetch several known-needed small facts in one request | do not batch unrelated large content; parallel subagents still duplicate model context. |
| Adaptive budgets | set output/token/tool-call/time budgets by phase: discovery, planning, edit, verify | hard caps can truncate a patch or hide a failure; return a resumable partial result. |
| Cascaded model routing | cheap model for routing/extraction/summarization; stronger model for decisions and verification | poor routing introduces retries and latent bugs; evaluate quality by task type. |
| Speculative decoding / provider batch/async modes | infrastructure-level latency/cost optimizations where provider supports them | these may change price/latency but not the logical amount of useful context; consult the current provider pricing/docs. |

## F. Terse-agent and minimal-code skills

| Project | Method | Scope / claim | Caveats |
|---|---|---|---|
| [Caveman](https://github.com/juliusbrussee/caveman) | instruction/skill that replaces filler with telegraphic language; variants from lite to very terse | Claude Code skill claims roughly 65% token reduction. | **Project claim.** Primarily reduces agent output, not tool/file input or hidden reasoning. A recent paired SkillsBench test measured only 8.5% lower modeled cost on real agentic tasks ([JetBrains test](https://blog.jetbrains.com/ai/2026/07/speak-to-ai-agents-like-cavemen-tosave-tokens/)). |
| [Caveman Code](https://github.com/JuliusBrussee/caveman-code) | alternate terminal agent that uses terse interaction plus own architecture/memory | README reports 1.93× fewer tokens in its 25-task MicroBench. | **Project benchmark.** Different harnesses/tool policies make comparisons non-equivalent; validate task success and security. |
| [Ponytail](https://github.com/DietrichGebert/ponytail) | “lazy senior dev” skill: decide what not to build; produce minimal sufficient code | designed to reduce unnecessary code and churn | **Project/community practice.** Saving is indirect and should never override acceptance, safety, accessibility, migration, or testing requirements. |
| “No preamble / concise status only” custom rule | same mechanism without a dependency | all agents | easy and low risk; retain explicit test results and risks. |

## G. Measurement, experiments, and validation

| Tool / method | Use |
|---|---|
| [ccusage](https://github.com/ryoppippi/ccusage) | parses/visualizes Claude Code and other agent usage records; measurement, not a reducer. |
| Native `/usage`, `/cost`, provider API billing | ground truth where a provider exposes it. Compare billed counts with any local estimates. |
| Task harness + tests + raw logs | paired A/B evaluation; use cost-per-success rather than compression ratio alone. |
| [Token Reduction Is Not Cost Reduction](https://arxiv.org/abs/2607.12161) | key cautionary research: compressed contexts can cause worse solutions and higher cost per solve. |
| [SWEzze](https://arxiv.org/abs/2603.28119) | research approach to code-aware compression; paper reports 6× context compression and 51.8–71.3% token-budget reduction in its evaluated issue-resolution setup. |

## Security, licensing, and operational checklist

- Read the source and installation scripts of hooks/proxies before granting them access to repositories, shell commands, API keys, or subscription sessions.
- Prefer local, transparent transforms. A network proxy can see proprietary code and may affect provider terms, prompt caching, and auditability.
- Pin versions; back up `.claude/settings.json`, `AGENTS.md`, `CLAUDE.md`, Cursor rules, and configuration before installers modify them.
- Check licenses before embedding a tool in a company workflow: OpenWolf is AGPL-3.0; individual tools differ.
- Provide a bypass command and automatically preserve raw output on command failure, diagnostics, migrations, security scans, and patch application.
- Never use “token saving” to bypass service limits, account rules, or billing. This guide concerns reducing legitimate work, not evasion.

## Findings in one sentence

The highest-confidence stack is: measure → narrow task/context → targeted search and quiet tools → deliberate compaction with a handoff → only then test retrieval maps, compressors, terse skills, or routing; their advertised percentages are not interchangeable with actual cost-per-correct-task savings.
