# Saving tokens with coding agents

Research map for reducing billed tokens, quota use, context pressure, or latency without reducing task quality.

Start: [playbook](playbook.md). Compare tools: [catalog](catalog.md). Product guides: [Claude Code](../claude-code-saves-tokens.md), [Codex](../codex-best-practice.md). Focused notes: [methods](methods/README.md).

## Model

`system + instructions + history + tools + files + results + reasoning + output`

Save by avoiding turns, sending less relevant context, dropping stale history, reducing output, or routing easy work to an adequate cheaper model.

Prompt caching usually lowers repeated-prefix price/latency, not processed-token or quota use.

## Defaults

- Measure billed cost and task success first.
- Name goal, paths, constraints, and non-goals.
- Search before broad reads; use bounded tool output.
- Clear unrelated sessions; keep a compact handoff.
- Measure one intervention at a time; report cost per successful task.

## Evidence labels

- **Official:** feature behavior, not universal savings.
- **Project claim:** vendor result; verify independently.
- **Research:** inspect tasks, versions, and denominator.
- **Community practice:** useful lead, not proof.

Audit hooks, proxies, and credential-bearing tools before installation.
