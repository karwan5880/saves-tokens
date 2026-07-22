# Repowise

**Type:** codebase-intelligence index and MCP server. **Repository:** [repowise-dev/repowise](https://github.com/repowise-dev/repowise). **License:** AGPL-3.0 for the open-source edition.

## Method

Repowise indexes dependency structure, git history, generated documentation, architectural decisions, and code-health signals. Its task-shaped MCP tools aim to answer repository questions with fewer searches and file reads than raw exploration. It also offers command-output distillation.

## Evidence and cautions

The project reports early paired SWE-QA results of up to 70% fewer tool calls, 89% fewer file reads, and 36% lower cost per query at comparable answer quality. These are **project claims**; the README says a more rigorous benchmark is still being prepared.

Index generation, synchronization, generated documentation, MCP schemas, and retrieval calls have costs. Verify exact source before edits, test stale-index behavior, and include indexing/maintenance in end-to-end evaluation. Review AGPL obligations and any hosted-service data flow.

## Sources

- [Repository and early benchmark description](https://github.com/repowise-dev/repowise)
- [MCP context guide and paired example](https://www.repowise.dev/guides/ai-context-mcp)
- [Licensing](https://docs.repowise.dev/docs/licensing)
