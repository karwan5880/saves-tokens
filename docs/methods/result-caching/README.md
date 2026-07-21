# Result caching and deduplication

## Method

Cache deterministic searches, documentation fetches, repository maps, and repeated tool calls; give the agent compact references/hashes rather than returning the same payload repeatedly.

## Caution

Invalidate by repository revision, configuration, dependency lock, query parameters, and external-data freshness. A stale cached answer causes more waste than a refetch.
