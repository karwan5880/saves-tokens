# Kimi Code controls

## Relevant controls

Kimi Code offers `/usage`, `/clear`, and `/compact`. Its configuration documents `max_output_size` per request and an option controlling whether prior reasoning is retained.

## Practical policy

Use `/clear` for unrelated work, compact with a factual handoff, and set output caps only for bounded outputs such as classification or summaries. Retaining reasoning can aid continuation but increases carried context; measure it by task type.

## Sources

- [Kimi Code overview](https://www.kimi.com/code/docs/en/)
- [Kimi command reference](https://www.kimi.com/code/docs/en/kimi-code-cli/reference/kimi-command)
- [Configuration reference](https://www.kimi.com/code/docs/en/kimi-code-cli/configuration/config-files)
