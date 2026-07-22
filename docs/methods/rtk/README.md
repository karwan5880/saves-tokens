# RTK (Rust Token Killer)

**Type:** terminal-output compressor. **Repository:** [rtk-ai/rtk](https://github.com/rtk-ai/rtk).

## Method

RTK intercepts selected shell commands and returns a compact representation to the agent, targeting progress noise, routine status output, and repetitive logs. Preserve an easy path to run/view the unmodified command.

## Evidence and cautions

The project advertises 60–90% compression for supported output, not necessarily full-task savings. A paired SkillsBench evaluation found real payload compression but +7.6% modeled cost at low reasoning and roughly neutral results at high reasoning. Full raw output remains essential for failures, migrations, security scans, and exact patch diagnostics.

## Sources

- [Project README](https://github.com/rtk-ai/rtk)
- [Independent JetBrains trial](https://blog.jetbrains.com/ai/2026/07/rtk-claude-code-token-savings/)
