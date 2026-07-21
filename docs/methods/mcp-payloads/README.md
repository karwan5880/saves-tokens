# MCP and tool payload discipline

## Method

Design tools to return IDs, compact summaries, and paginated/filtered records first; fetch full detail only for selected items. Expose only tools relevant to a task.

## Caution

Tool schemas/descriptions themselves are prompt tokens. Overly broad tools produce huge results, but opaque minimal schemas create wrong calls. Favor small, clearly named tools with server-side path/date/field/limit filters.
