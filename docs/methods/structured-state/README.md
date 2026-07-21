# Structured durable state

## Method

Store the task plan, decisions, changed paths, test status, open questions, and next action in compact Markdown or JSON rather than replaying a transcript. Reinject only the fields needed for the next phase.

## Caution

Do not serialize every message, tool result, or hidden reasoning. JSON keys and tool schemas cost tokens too. Link to authoritative source files for exact code and decisions.
