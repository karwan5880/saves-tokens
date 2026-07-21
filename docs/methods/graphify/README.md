# Graphify

**Type:** repository knowledge-graph skill/tool. **Repository:** [safishamsi/graphify](https://github.com/safishamsi/graphify).

## Method

Graphify extracts code, schemas, documents, and other repository artifacts into a queryable knowledge graph. The intended saving is to answer architecture and dependency questions from graph facts before loading raw files.

## Best fit

Large, relatively stable repositories and cross-cutting questions. Keep the graph fresh after meaningful changes; use it to locate evidence, then read exact source ranges before edits.

## Evidence and cautions

The project and community material advertise very large reductions, including a 71× example. These are **project/community claims**, not a universal benchmark. Initial extraction has its own token/API/runtime cost; stale or lossy graph facts can create costly rework. Evaluate total billed tokens and task pass rate against targeted `rg`/symbol-search baselines.

## Sources

- [Project README](https://github.com/safishamsi/graphify)
- [Graphify token-saving example](https://gist.github.com/charan-s108/3bf637fbfc5d6ccfb066397ad837ce2c)
