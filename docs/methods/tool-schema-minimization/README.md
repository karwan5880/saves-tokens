# Tool-schema minimization

## Method

Load only the MCP/tools needed for the current task and keep their descriptions/examples compact, clear, and structured. Prefer a few specific operations over one unbounded “search everything” endpoint.

## Trade-off

Too many schemas consume every turn’s context. Too little detail yields wrong tool calls and retries. Measure token use and tool-call success rate.
