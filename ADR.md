# ADR: Use a Visited Set and Mark Vertices When Enqueued in BFS

- **Status:** Accepted
- **Date:** 11 October 2026
- **Student:** Sanket Patil
- **PRN:** 25UAM069
- **Division:** A
- **System:** Python BFS/DFS graph-search system
- **Repository:** https://github.com/sanketpatil-7421/IAI_SLE4

## 1. Context
The SLE project implements Breadth First Search (BFS) and Depth First Search (DFS) on a graph with vertices A–G. Graphs may contain cycles or multiple paths to the same vertex, so traversal needs a reliable way to avoid processing vertices repeatedly. In BFS, a vertex can be discovered from more than one neighbour before it is removed from the queue. The SLE-3 C4 architecture separates graph management, the search engine, traversal-state management, and output.

## 2. Decision
Use a set named `visited` to record discovered vertices in BFS and DFS. In BFS, mark a neighbour visited when it is added to the queue, rather than waiting until it is removed. Keep a `deque` for the FIFO queue and retain recursive DFS.

## 3. Alternatives Considered
- **No visited tracking:** rejected because cycles can cause repeated traversal or non-termination.
- **Mark only when dequeued:** rejected because a vertex can be queued by multiple neighbours.
- **Use a list for membership checks:** possible, but membership checks are generally linear in list length; a set better suits repeated membership tests.

## 4. Rationale / Justification
- Marking at enqueue time ensures each vertex enters the BFS queue at most once.
- The visited set prevents revisiting vertices in cyclic graphs.
- With adjacency lists and set membership, BFS and DFS run in O(V + E) time; auxiliary traversal storage is O(V).
- `collections.deque` supports efficient append and left-pop operations for BFS.
- Both algorithms can share the visited-state idea while retaining distinct traversal strategies.
- This decision matches the SLE-3 C4 design, where graph storage, search, traversal state, and output have separate responsibilities.
- For the seven-vertex sample graph, the expected traversal from A is BFS: A, B, C, D, E, F, G; DFS with the current neighbour order: A, B, D, E, C, F, G.
- **Profiling evidence limitation:** the accessible SLE-2 README documents asymptotic complexity, but a numeric profiling report/table was not available in the accessible files. Therefore, this ADR does not claim runtime or memory numbers that were not measured.

## 5. Consequences

### Positive
- Each reachable vertex is processed once, avoiding duplicate queue entries and unnecessary work.
- The code remains readable and easy to explain during viva.
- Traversal-state responsibilities are explicit and fit the C4 architecture.

### Negative / Trade-offs
- The visited set consumes O(V) additional memory.
- Set membership has overhead for a tiny fixed graph, although it scales better than repeated linear list searches.
- Traversal order depends on neighbour order in the adjacency list, especially for DFS.

## 6. References
- SLE-2: https://github.com/sanketpatil-7421/IAI_SLE2
- SLE-3: https://github.com/sanketpatil-7421/IAI_SLE3
- SLE-4: https://github.com/sanketpatil-7421/IAI_SLE4
