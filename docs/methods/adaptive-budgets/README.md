# Adaptive budgets

## Method

Set output, tool-call, time, and context budgets by phase: small for routing/discovery, larger for implementation and verification. Have the agent return a resumable partial state when a cap is reached.

## Caution

Hard caps can truncate patches or omit a failure. Never hide an error merely to meet budget.
