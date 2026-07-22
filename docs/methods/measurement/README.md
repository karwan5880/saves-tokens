# Measurement and A/B evaluation

## Method

Run matched tasks on the same repository revision, prompt, model, reasoning setting, permissions, and environment. Repeat/randomize runs. Record billed input, cached input, output, reasoning where available, latency, tool calls, task outcome, and cost per successful task.

## Why

Agent runs are stochastic and reported compression percentages often cover only one payload category. Research reports high usage variance and warns that token reduction can worsen solution rate or cost per solve.

## Sources

- [How Do AI Agents Spend Your Money?](https://arxiv.org/abs/2604.22750)
- [Token Reduction Is Not Cost Reduction](https://arxiv.org/abs/2607.12161)
