# Prefix/prompt caching

## Method

Keep stable system instructions, tool schemas, policy, and project baseline at the prompt prefix; append volatile task data later. Cache hits can reduce repeated-prefix API price and latency.

## Caution

Caching is not synonymous with fewer processed tokens, context pressure, or subscription quota. Small changes to a cached prefix can destroy reuse. Measure cached input separately from billed/non-cached input.

## Source

- [Claude Code cost guide](https://code.claude.com/docs/en/costs)
