# Catalog: methods, tools, caveats

Claims describe source-reported behavior or results, not verified savings.

## Built-ins

| Method | Product | Save | Note |
|---|---|---|---|
| Clear/compact, caching, usage, model choice | Claude Code | stale history, repeated prefix | [Official costs](https://code.claude.com/docs/en/costs); cache ≠ lower quota. |
| Scoped `@file`/`@code` | Cursor | accidental folder context | [Official context](https://docs.cursor.com/en/guides/working-with-context). |
| `/clear`, `/compact`, `/usage`, output cap | Kimi | history/output | [Official overview](https://www.kimi.com/resources/kimi-code-introduction). |
| Compact task, scoped files, instructions, diff summary | Codex | exploration/context | Surface controls vary; [official guide](https://help.openai.com/en/articles/11096431). |

## Workflow

| Method | Benefit | Failure mode |
|---|---|---|
| Goal + paths + non-goals | fewer turns | scope too tight |
| Explore, plan, edit, verify, handoff | less rediscovery | overplanning |
| Minimal patch, concise status | less code/prose | missing checks/risks |
| Scoped instructions, search before reads | less injected context | stale summary/dynamic code |
| Quiet focused tools | smaller results | missing diagnostics |
| Model routing, limited subagents | lower easy-task cost | retries/duplicated context |

## Maps, retrieval, memory

| Tool/method | Claim or use | Caveat |
|---|---|---|
| [Graphify](https://github.com/safishamsi/graphify) | queryable code/docs graph; reports large reductions | Project claim; indexing and stale graphs cost. |
| [Repowise](https://github.com/repowise-dev/repowise) | graph/git/docs/ADR retrieval; reports up to 36% lower cost/query | Early project benchmark; AGPL-3.0; include indexing and verify source. |
| [OpenWolf](https://github.com/cytostack/openwolf) | anatomy, preferences, read tracking; claims 65.8% | Project claim; AGPL-3.0; estimated ledger; audit hooks. |
| [ContextSniper](https://github.com/Calluking/ContextSniper) | ranked compact evidence | Preprint; retain edit anchors. |
| Maps, LSP, AST, ADRs, handoffs | targeted retrieval, durable facts | Keep short and current. |

## Tool and payload reduction

| Tool/method | Claim or use | Caveat |
|---|---|---|
| [Context Mode](https://github.com/mksglu/context-mode) | local sandbox/index; claims 98% on selected raw payloads | Project payload claim, not whole-task saving; audit hooks/MCP; ELv2. |
| [RTK](https://github.com/rtk-ai/rtk) | claims 60–90% command compression | Project claim; [trial](https://blog.jetbrains.com/ai/2026/07/rtk-claude-code-token-savings/) found no task-cost gain; retain raw-output bypass. |
| [Tamp](https://github.com/sliday/tamp) | proxy compression; claims 45% in author-run A/B tasks | Proxy sees sensitive payloads; lossy modes and caching/tool changes; verify license. |
| [Headroom](https://github.com/chopratejas/headroom) | proxy compression | Third party sees prompts/code/credentials; may break caching/tools. |
| `rg`, ranges, filters, no ANSI, capped logs | safe manual reduction | Preserve failures and exact diffs. |
| Small schemas, pagination, field filters | smaller MCP/web results | Tool schemas also cost; fetch details on demand. |
| Crop/resize images | lower visual context | Do not damage text or pixel-critical UI. |

## Architecture

| Method | Use | Caveat |
|---|---|---|
| Prefix caching | stable prefix; volatile suffix | price/latency, not always quota. |
| Compacted server state | replay facts, not raw turns | version facts/source of truth. |
| RAG + lexical/structural search | retrieve small evidence set | stale chunks and missing relationships. |
| Hierarchical/contextual summaries | expand selected branches | lose identifiers/errors. |
| Structured state | decisions, paths, open questions | do not serialize transcripts. |
| Result cache, batching, adaptive budgets | avoid repeat calls | invalidate; caps can hide failure. |
| Cascades/speculative/batch modes | route easy work or lower latency | quality/retry and provider trade-offs. |

## Skills and measurement

| Tool/method | Claim or use | Caveat |
|---|---|---|
| [Caveman](https://github.com/juliusbrussee/caveman) | terse output; claims ~65% | Project claim; [trial](https://blog.jetbrains.com/ai/2026/07/speak-to-ai-agents-like-cavemen-tosave-tokens/) measured 8.5% modeled cost reduction. |
| [Caveman Code](https://github.com/JuliusBrussee/caveman-code) | claims 1.93× fewer MicroBench tokens | Project benchmark; compare equivalent tasks. |
| [Ponytail](https://github.com/DietrichGebert/ponytail) | avoid needless code | Indirect saving; never skip requirements. |
| [Skillreaper](https://github.com/thousandflowers/skillreaper) | audits unused skills/MCP/agents for reversible pruning | Historical non-use is not future irrelevance; estimates vary; MIT. |
| [ccusage](https://github.com/ryoppippi/ccusage) | usage ledger | Measurement, not reducer. |
| [SWEzze](https://arxiv.org/abs/2603.28119) | code-aware compression research | Evaluate on repository. |
| [Token Reduction Is Not Cost Reduction](https://arxiv.org/abs/2607.12161) | reducer evaluation warning | Measure cost per solve. |

## Safety

- Review source/install scripts; pin versions and back up configuration.
- Check license: OpenWolf is AGPL-3.0; others differ.
- Preserve raw output for failures, migrations, scans, and patching.
- Never use token reduction to evade limits, billing, or policy.

Best default: measure; narrow task/context; search first; use quiet tools; hand off before reset; then evaluate advanced tools.
