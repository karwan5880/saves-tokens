# Caveman

**Type:** terse-response skill. **Repository:** [juliusbrussee/caveman](https://github.com/juliusbrussee/caveman).

## Method

The skill directs Claude Code to use terse, telegraphic answers and remove conversational filler. This can also shrink what later turns must reread.

## Evidence and cautions

The project claims roughly 65% reduction. That is chiefly output text, not file/tool input or hidden reasoning. A paired SkillsBench study measured 8.5% lower modeled cost on real agentic tasks, illustrating why output compression percentages should not be treated as total savings. Preserve concise risks and decisions.

## Sources

- [Project README](https://github.com/juliusbrussee/caveman)
- [Independent JetBrains trial](https://blog.jetbrains.com/ai/2026/07/speak-to-ai-agents-like-cavemen-tosave-tokens/)
