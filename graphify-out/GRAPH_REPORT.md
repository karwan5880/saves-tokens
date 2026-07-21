# Graph Report - .  (2026-07-22)

## Corpus Check
- cluster-only mode — file stats not available

## Summary
- 50 nodes · 74 edges · 10 communities (5 shown, 5 thin omitted)
- Extraction: 92% EXTRACTED · 8% INFERRED · 0% AMBIGUOUS · INFERRED: 6 edges (avg confidence: 0.83)
- Token cost: 23,797 input · 1,267 output

## Community Hubs (Navigation)
- Context and Session Management
- Token Optimization Techniques
- Model Selection and Performance
- Context Compression Methods
- Terse Response Design
- Token Capacity Limits
- Adaptive Budget Allocation
- Retrieval Batching
- Hierarchical Summarization
- Data Pagination and Filtering

## God Nodes (most connected - your core abstractions)
1. `Problem: high token usage and provider billing` - 10 edges
2. `Token-saving playbook` - 8 edges
3. `Catalog: techniques, tools, and caveats` - 7 edges
4. `Contextual compression and summarization` - 5 edges
5. `Problem: accumulated context history and stale information` - 5 edges
6. `Pattern: terse response convention` - 5 edges
7. `Built-in product controls` - 5 edges
8. `Context maps, retrieval, and memory` - 5 edges
9. `API and application-level architecture` - 5 edges
10. `Fresh sessions and session lifecycle management` - 4 edges

## Surprising Connections (you probably didn't know these)
- `Task scoping with goal, paths, tests, constraints` --conceptually_related_to--> `Pattern: surgical file and folder context`  [INFERRED]
  docs/playbook.md → docs/catalog.md
- `Result caching and deduplication` --addresses--> `Problem: high token usage and provider billing`  [EXTRACTED]
  docs/catalog.md → docs/README.md
- `ContextSniper: hybrid retrieval and ranking` --implements--> `Contextual compression and summarization`  [INFERRED]
  docs/methods/contextsniper/README.md → docs/catalog.md
- `Saving tokens with coding agents — research map` --references--> `Token-saving playbook`  [EXTRACTED]
  docs/README.md → docs/playbook.md
- `Token-saving playbook` --cites--> `Intentional model and reasoning routing`  [EXTRACTED]
  docs/playbook.md → docs/catalog.md

## Hyperedges (group relationships)
- **Token-saving playbook sequential process** — technique_fresh_sessions, technique_task_scoping, technique_code_maps, technique_compact_tools, technique_session_handoff, technique_output_control, technique_model_routing [EXTRACTED 1.00]
- **High-confidence cost-reduction technique stack** — problem_high_cost, technique_task_scoping, technique_code_maps, technique_compact_tools, technique_session_handoff, technique_output_control [EXTRACTED 0.95]
- **Context retrieval and memory preservation methods** — project_graphify, project_openwolf, project_contextsniper, technique_code_maps, technique_rag, technique_result_caching [INFERRED 0.85]

## Communities (10 total, 5 thin omitted)

### Community 0 - "Context and Session Management"
Cohesion: 0.29
Nodes (12): Context maps, retrieval, and memory, Token-saving playbook, Problem: accumulated context history and stale information, ContextSniper: hybrid retrieval and ranking, Graphify: knowledge graph skill, OpenWolf: lifecycle hooks and project memory, Code maps and structural search, Fresh sessions and session lifecycle management (+4 more)

### Community 1 - "Token Optimization Techniques"
Cohesion: 0.22
Nodes (10): Built-in product controls, Human workflow and prompt patterns, Catalog: techniques, tools, and caveats, Token-saving methods library, Saving tokens with coding agents — research map, Pattern: surgical file and folder context, Codex, Cursor (+2 more)

### Community 2 - "Model Selection and Performance"
Cohesion: 0.28
Nodes (9): API and application-level architecture, Problem: high token usage and provider billing, Problem: latency and round-trip time, Claude Code, ccusage: usage measurement and visualization, How Do AI Agents Spend Your Money?, Model choice and routing, Intentional model and reasoning routing (+1 more)

### Community 3 - "Context Compression Methods"
Cohesion: 0.33
Nodes (7): Compressing payloads: terminal, tool, web, MCP, Headroom: API proxy context compression, RTK: Rust Token Killer terminal compressor, SWEzze: code-aware context compression, Token Reduction Is Not Cost Reduction, Compact tool and command design, Contextual compression and summarization

### Community 4 - "Terse Response Design"
Cohesion: 0.47
Nodes (6): Terse-agent and minimal-code skills, Pattern: minimal correct patch, Pattern: terse response convention, Caveman: terse-response skill, Caveman Code: terse terminal agent, Ponytail: minimal-implementation skill

## Knowledge Gaps
- **13 isolated node(s):** `Token-saving methods library`, `Tool schema minimization`, `Server-side filtering and pagination`, `Hierarchical summaries`, `Batching independent retrievals` (+8 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **5 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Catalog: techniques, tools, and caveats` connect `Token Optimization Techniques` to `Context and Session Management`, `Model Selection and Performance`, `Context Compression Methods`, `Terse Response Design`?**
  _High betweenness centrality (0.211) - this node is a cross-community bridge._
- **Why does `Problem: high token usage and provider billing` connect `Model Selection and Performance` to `Context and Session Management`, `Token Optimization Techniques`, `Context Compression Methods`, `Terse Response Design`?**
  _High betweenness centrality (0.201) - this node is a cross-community bridge._
- **Why does `API and application-level architecture` connect `Model Selection and Performance` to `Context and Session Management`, `Token Optimization Techniques`, `Context Compression Methods`?**
  _High betweenness centrality (0.131) - this node is a cross-community bridge._
- **What connects `Token-saving methods library`, `Tool schema minimization`, `Server-side filtering and pagination` to the rest of the system?**
  _13 weakly-connected nodes found - possible documentation gaps or missing edges._