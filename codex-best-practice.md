# Codex: save tokens, keep quality

Optimize cost per successful task, not smallest prompt.

## Task prompt

```text
Goal: validate empty display names in src/profile.ts.
Constraints: no schema or API error-format change.
Done when: empty names are rejected.
```

Add relevant paths, errors, docs, and non-goals only. Use direct implementation for small fixes. Use Plan mode for ambiguous, risky, or multi-step work. Require minimal patch and diff review.

## Context and session

- Search symbols/maps before broad reads; use targeted file ranges.
- Use bounded, structured tool output; retain exact failure evidence.
- Start a new task for unrelated work.
- Handoff: goal, files, decisions, exact failure, next action.
- More reasoning cannot fix missing requirements.

## `AGENTS.md`

Keep checked-in guidance short: layout, commands, project-only conventions, safety boundaries, review rules, done definition. Use nested files only for subtree rules. Remove generic advice, tutorials, stale details, and references Codex can discover. Put one-off constraints in the prompt.

## Skills, plugins, MCP, hooks, config

| Need | Use | Rule |
|---|---|---|
| One task | Prompt | Task-only context. |
| Shared rules | `AGENTS.md` | Short, versioned, verifiable. |
| Personal defaults | Global configuration | Do not impose on repos. |
| Trusted repo settings | `.codex/config.toml` | Scope model, sandbox, MCP, hooks. |
| Occasional workflow | Skill | Precise trigger; load on demand. |
| Extension bundle | Plugin | Audit manifest, skills, tools, hooks, MCP, scripts, license. |
| Live external data/action | MCP/connector | Filter, paginate, check authorization. |
| Required lifecycle action | Hook | Fast, narrow, inspectable. |
| Scheduled stable task | Automation | Bound side effects, preserve logs. |

Do not install proxies, hooks, or middleware with source/credential/traffic access without explicit approval and security review.

## Safety and parallelism

Keep sandbox and approvals tight. Separate filesystem, network, shell, credential, and destructive access decisions. Review before deploys, publishing, or production data changes.

Use agents/worktrees only for isolated work. Require concise evidence reports. Parallelism can reduce time but duplicates context and creates conflicts.

## Measure

Compare one change at a time: billed input/output/cached input, turns, tool calls, latency, rework, cost per successful task. Treat plugin/vendor savings as hypotheses.

Sources: [Codex best practices](https://learn.chatgpt.com/guides/best-practices), [Codex manual](https://developers.openai.com/codex/codex-manual.md), [`AGENTS.md`](https://developers.openai.com/codex/concepts/customization#agents-guidance), [plugins](https://developers.openai.com/codex/plugins/build#plugin-structure).
