# OpenWolf

**Type:** lifecycle-hook middleware and project memory. **Repository:** [cytostack/openwolf](https://github.com/cytostack/openwolf). **License:** AGPL-3.0.

## Method

It builds a project anatomy/map, remembers preferences and fixes, tracks repeated reads, and injects lifecycle guidance. The aim is to prevent rereading files and rediscovering already-known facts.

## Best fit

Long-lived projects with repeated sessions and a willingness to review hook behavior. Its current documentation describes support for Claude Code, Codex, and OpenCode.

## Evidence and cautions

The repository claims 65.8% average reduction across its own sessions; its token ledger is estimation-based, not provider billing. Hooks and generated instructions add context and have access to repository activity. Audit scripts/configuration, pin versions, and retain a no-hook comparison.

## Sources

- [Repository and implementation notes](https://github.com/cytostack/openwolf)
- [Current getting-started docs](https://openwolf.com/getting-started.html)
