# Task scoping

## Method

State goal, likely target paths, acceptance tests, constraints, and non-goals in the first request. This prevents broad exploration and correction loops.

```text
Goal: fix timeout handling in src/api/client.ts.
Done when: direct tests pass.
Do not: change public API or refactor unrelated modules.
Report: changed files, tests, remaining risk.
```

## Caution

Do not name paths so narrowly that the agent cannot make a required adjacent change. Update scope when evidence disproves the initial hypothesis.
