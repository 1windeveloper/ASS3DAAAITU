# Introduction
Designing a cheap-but-connected road network can be modeled as the **Minimum Spanning Tree (MST)** problem on a weighted, undirected graph: districts are vertices and candidate roads are edges whose weights are construction costs. This report compares two greedy methods — **Prim’s** and **Kruskal’s** — focusing on correctness and speed on graphs with different densities.

## Aim & Scope
**Goal.** Build a small Java tool that:
- reads a city graph from **JSON**;
- computes an MST with **Prim** and with **Kruskal**;
- records **performance metrics** (runtime in ms and counts of key operations);
- writes a compact **JSON summary** (MST edges, total cost, short comparison).

We want to see which algorithm fits different types of transport networks and what trade-offs appear between speed and implementation effort.

## Methodology
**Tools.** Java 25; Gson for JSON; IntelliJ IDEA; metrics: runtime (ms) and operation counters.  
**Data format.** Input contains a list of vertices (districts) and a list of edges objects `{from, to, weight}`.

## Algorithm Overview
- **Prim.** Grows the tree vertex-by-vertex by always picking the cheapest edge to any unvisited vertex.  
  *Key data structure:* priority queue (min-heap).  *Time:* `O(E log V)`.
- **Kruskal.** Sorts all edges by weight and connects components with Union-Find, avoiding cycles.  
  *Key data structure:* Disjoint Set Union (Union-Find).  *Time:* `O(E log E)` ≈ `O(E log V)`.

![Algorithm overview](docs/img/alg_overview_table.png)

## Experimental Data
Two graphs from `ass_3_input.json`:
- **Graph 1:** 5 vertices, 7 edges — medium-density, moderately connected city area.  
- **Graph 2:** 4 vertices, 5 edges — low-density, smaller and simpler network.

![Experimental data](docs/img/experimental_data_table.png)

## Results
Both algorithms return the same MST total cost on both graphs, which validates the implementations.

- **Graph 1:** Prim → cost 16, time ~13.20 ms, ops 29; Kruskal → cost 16, time ~22.45 ms, ops 32  
- **Graph 2:** Prim → cost 6, time ~0.04 ms, ops 19; Kruskal → cost 6, time ~0.09 ms, ops 22

![Numerical results](docs/img/results_table.png)

### MST snapshot (Graph 1)
Selected edges: **B—C (2), A—C (3), B—D (5), D—E (6)**.  
Total cost: **16**.

![MST of Graph 1](docs/img/mst_graph1.png)

## Discussion
- **Time efficiency.** Prim often benefits on medium/denser graphs because only the local frontier in the heap is touched; Kruskal pays a fixed sorting cost on all edges. On very large **sparse** graphs (E ≈ V) the gap shrinks and the choice can depend on coding convenience.
- **Work profile.** Prim’s cost scales with vertex degrees (how many incident edges are relaxed); Kruskal’s cost is dominated by sorting and `find/union` calls.
- **Implementation effort.** Kruskal needs a careful Union-Find (path compression + union by rank/size). Prim is straightforward with adjacency lists and a min-heap.

## Conclusions
1) Both methods give the same minimal total cost — experiment agrees with theory.  
2) On medium-density data **Prim** was faster; on a small sparse graph the difference is tiny, with Kruskal slightly behind because of sorting.  
3) Rule of thumb: dense/medium graphs → **Prim**; very sparse or very large graphs → **Kruskal** is competitive and convenient when edges arrive as one flat list.
