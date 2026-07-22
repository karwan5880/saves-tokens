# Session handoff and compaction

## Method

Before clearing or compacting, save a small durable note: goal, confirmed facts, changed files, decisions, open question, and exact next action. Start a fresh session for unrelated work.

## Why

Raw conversational/tool history is repeatedly carried; a verified handoff lets the agent drop noise without rediscovering facts. Compaction is lossy, so source-of-truth plans and ADRs belong in files.

## Sources

- [Claude Code cost guide](https://code.claude.com/docs/en/costs)
- [Claude API compaction](https://platform.claude.com/docs/en/build-with-claude/compaction)
