# Context Mode

**Type:** local MCP/hook context virtualization. **Repository:** [mksglu/context-mode](https://github.com/mksglu/context-mode). **License:** Elastic License 2.0.

## Method

For Claude Code, its plugin installs hooks that redirect supported tool work to sandbox tools. Raw web, command, file-analysis, and MCP payloads can be processed or indexed in a local SQLite FTS5 store while the conversation receives a compact result. It also records selected session events for retrieval after compaction.

## Evidence and cautions

The project demonstrates 315 KB of selected raw payloads becoming 5.4 KB and describes this as 98% context saving. This is a **project payload claim**, not 98% lower provider-billed tokens or cost per completed task. The MCP definitions, hook instructions, searches, and missed details also have costs.

Hooks can block or reroute commands and the store may contain sensitive local data. Review the source, permission propagation, data retention, and purge behavior before installation. Preserve raw failure evidence and validate task success against an unmodified Claude Code baseline.

## Sources

- [Project README, architecture, claims, security, and license](https://github.com/mksglu/context-mode)
- [Claude Code platform support](https://github.com/mksglu/context-mode/blob/main/docs/platform-support.md)
