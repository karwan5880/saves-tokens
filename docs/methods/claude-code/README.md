# Claude Code controls

## Relevant built-ins

Use `/usage` or `/cost` to observe consumption; `/clear` for unrelated work; `/compact` with explicit retention instructions; model selection and output discipline where appropriate. Claude Code automatically applies prompt caching and auto-compaction.

## Practical policy

Keep `CLAUDE.md` short and scoped, avoid `@` file injection unless the whole file is necessary, persist a handoff note before clearing, and use hooks only after measuring their whole-task effect.

## Sources

- [Official cost management guide](https://code.claude.com/docs/en/costs)
- [Official context-window guide](https://code.claude.com/docs/en/context-window)
- [Anthropic help: `@` can inject a file and CLAUDE.md tree](https://support.claude.com/en/articles/14552983-models-usage-and-limits-in-claude-code)
