# Saving tokens with coding agents — research map

Researched: 2026-07-21. This is a practical, source-linked map of the techniques people use to reduce **provider-billed tokens, subscription quota consumption, context-window pressure, latency, or all four** in Claude Code, Codex, Cursor, Kimi Code, GLM-compatible agents, and similar tools.

There is no universal percentage saving. A tool can shrink a shell command by 90% while that command represents under 1% of an entire task. Conversely, a short output can be re-read every later turn and compound its saving. Treat vendor and repository percentages as hypotheses to measure in your own workload.

Start with [the playbook](playbook.md), then use [the catalog](catalog.md) to evaluate every major approach and named project found during this research.

For individual, focused notes—one folder and README per project or method—see the [methods library](methods/README.md).

## The useful mental model

An agent repeatedly sends some combination of:

`system + project instructions + conversation history + tool schemas + files + tool results + reasoning + output`

The durable ways to save are therefore to:

1. avoid an unnecessary turn or tool call;
2. send less, more relevant context;
3. make retained context shorter without losing facts needed for the task;
4. emit less prose/code/tool output; or
5. use a cheaper/smaller model only where it is adequate.

Prompt caching can reduce **price/latency** for repeated prefixes but normally does not mean fewer tokens were processed or less subscription quota was consumed. Keep those measurements distinct.

## Quick recommendations

- Measure first: native `/usage` / `/cost` where available, plus a local ledger such as `ccusage` for Claude Code.
- Keep a task narrow. Name the target files, intended behavior, acceptance test, and non-goals. Do not paste or `@` a whole repository/folder when a symbol or two files will do.
- End unrelated tasks with a fresh session (`/clear`) and carry forward a compact, checked handoff note rather than stale chat.
- Make noisy commands quiet and structured: focused test filters, `git diff --stat` before full diff, `rg` before broad scans, JSON/line limits, and no progress bars/ANSI output.
- Use repository maps / code search / targeted retrieval before whole-file reads. Keep maps concise and regenerate them as code changes.
- Add output caps and a terse response convention only after retaining enough explanation for review and safety.
- Benchmark one intervention at a time on representative tasks. Record total billed input, output, cached input, reasoning (if reported), wall time, failures, and cost-per-success.

## Source quality legend

- **Official** — product documentation; reliable for feature behavior, not universal savings.
- **Project claim** — a tool author’s README or site; useful for mechanism and setup, but not independent proof.
- **Independent test / research** — reproducible benchmark or paper; inspect task set, versions, model, and denominator.
- **Community practice** — useful leads, not evidence of a percentage.

See the catalog’s caveats before installing any hook, proxy, or credential-bearing middleware.
