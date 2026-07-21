# SWEzze

**Type:** code-aware context-compression research. **Paper:** [Compressing Code Context for LLM-based Issue Resolution](https://arxiv.org/abs/2603.28119).

## Method

SWEzze aims to compress issue-resolution context while retaining code structure and task-relevant patch information, rather than applying generic text compression.

## Evidence and cautions

The paper reports about 6× context compression and 51.8–71.3% lower token budget in its evaluated setup. Treat this as research-specific evidence; implementation, benchmark, model, and task distribution all affect transferability. Exact edit anchors must survive any compression.
