# SLE-4: Architecture Decision Record (ADR) Defense

**Course:** 02AML204 – Introduction to Artificial Intelligence  
**Student:** Sanket Patil  
**PRN:** 25UAM050  
**Division:** A  
**System:** Python BFS and DFS Graph Search System

## Aim
Record and justify one important design decision from the earlier SLE work, connect it to the SLE-2 complexity/profiling work and SLE-3 C4 architecture, and prepare to defend it during the viva.

## Selected Architecture Decision
**Use a visited set and mark BFS vertices when they are enqueued.**

The BFS implementation stores discovered vertices in a set and uses `collections.deque` as a FIFO queue. Marking a vertex at enqueue time prevents multiple neighbours from adding the same vertex to the queue. DFS also uses a visited set to avoid revisiting vertices.

## Why this decision?
- Prevents repeated processing and supports termination on cyclic graphs.
- Works with adjacency-list traversal in O(V + E) time and O(V) auxiliary space.
- Keeps traversal state distinct from graph storage, consistent with the SLE-3 C4 containers.
- Makes the queue and visited-state responsibilities straightforward to test and explain.

**Evidence note:** The accessible SLE-2 README records asymptotic complexity but the numeric profiling report was not present among the accessible files. No timing or memory measurements are invented in this ADR. Add the actual SLE-2 profiler measurements if they are available in your original report.

## Earlier SLE journey
- **SLE-1:** Agent/search problem and implementation work.
- **SLE-2:** BFS/DFS graph traversal in Python, graph representation, traversal output, and complexity documentation.
- **SLE-3:** C4 Context, Container, Component, and Code views for the BFS/DFS system.
- **SLE-4:** Document and defend the visited-set / BFS enqueue-time decision.

## Repository files
- [ADR.md](ADR.md) — complete Architecture Decision Record.
- [CONTRIBUTION_LOG.md](CONTRIBUTION_LOG.md) — work and AI contribution log.
- Four-page Word submission: `SLE4_25UAM050.docx` (provided as a separate attachment with this task).

## References
- [SLE-2 repository](https://github.com/sanketpatil-7421/IAI_SLE2)
- [SLE-3 repository](https://github.com/sanketpatil-7421/IAI_SLE3)
