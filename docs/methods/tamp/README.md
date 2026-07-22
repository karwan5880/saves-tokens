# Tamp

**Type:** local HTTP-proxy payload compressor. **Repository:** [sliday/tamp](https://github.com/sliday/tamp).

## Method

Tamp sits between an agent and model endpoint and transforms accumulated payloads. Its lower levels use minification, whitespace/line cleanup, command filtering, deduplication, and diffs; higher levels add lossy pruning, semantic compression, retrieval, and offloaded storage. It documents Claude Code plugin/proxy support.

## Evidence and cautions

The project reports 45% fewer tokens with no quality regression in 216 author-run A/B tasks at its tested setting, plus larger savings for more aggressive modes. These are **project claims** based on its scenarios and judging procedure, not independent proof across repositories or Claude Code plans.

A proxy can access prompts, code, tool results, and credentials and can change prompt caching, tool protocols, or debugging behavior. Lossy stages may remove identifiers, stack frames, or edit anchors. Audit the source and declared license, start with lossless transforms if evaluating, retain a bypass, and compare provider-billed cost per successful task.

## Sources

- [Project site, mechanism, benchmark summary, and installation paths](https://tamp.dev/)
- [Repository](https://github.com/sliday/tamp)
- [Project whitepaper](https://tamp.dev/whitepaper.pdf)
