1. Introduction

Efficient urban transportation planning requires minimizing the total cost of connecting all districts while maintaining full accessibility. This problem is represented mathematically as finding a Minimum Spanning Tree (MST) in a weighted undirected graph. Each vertex represents a district, and each edge represents a possible road with a construction cost as its weight.
This assignment applies Prim’s and Kruskal’s algorithms to identify the MST, compare their computational performance, and analyze their efficiency depending on graph characteristics such as density and size.

2. Purpose of the Work

The primary goal of this project is to develop a Java-based application that:

Reads graph data from a JSON input file representing city districts and potential road connections.

Applies Prim’s and Kruskal’s algorithms to construct the MST.

Records performance metrics, including execution time and operation counts.

Produces a JSON output file summarizing the MST edges, total cost, and algorithmic efficiency.
The ultimate objective is to determine the optimal algorithm for various types of transportation networks and understand trade-offs between computation time and implementation complexity.

3. Implementation and Methodology
3.1 Tools and Technologies

Language: Java 25

Library: Gson (for JSON parsing and writing)

Data Format: JSON input/output

IDE: IntelliJ IDEA

Performance Metrics: execution time (ms), operation counts

3.2 Data Structure

Each input graph includes:

A list of nodes (districts)

A list of edges (possible roads), where each edge has attributes from, to, and weight.

3.3 Algorithms Overview
<img width="955" height="534" alt="image" src="https://github.com/user-attachments/assets/61ddcbf9-c9ad-4e88-9af9-6aa9f2eb11ea" />

4. Experimental Data

Two graphs were used from the provided ass_3_input.json file:

<img width="1175" height="290" alt="image" src="https://github.com/user-attachments/assets/ab97e0ee-37b6-4b4e-823d-0e82a6444e53" />


5. Results and Observations
5.1 Numerical Results
<img width="1176" height="454" alt="image" src="https://github.com/user-attachments/assets/e00b50bf-6c95-4704-a44d-6eabe54ac5a5" />




Both algorithms produce identical MST costs for both graphs.
Differences in time and operations are expected due to algorithmic complexity and JVM execution behavior.

5.2 Visual Analysis
Analysis:

On the larger, denser Graph 1, Prim runs faster (13.2 ms vs 22.45 ms).

On the smaller Graph 2, both are nearly instantaneous, with Kruskal slightly slower due to sorting overhead.
Interpretation:

Prim requires fewer operations on the denser graph (Graph 1) due to efficient heap-based selection.

Kruskal performs slightly more operations as it must compare and union edges, even for smaller graphs.
Figure 3 – MST Edge Visualization

For Graph 1 (5 vertices), both algorithms selected identical MST edges:

B — C (2)
A — C (3)
B — D (5)
D — E (6)


Total Cost = 16

6. Analytical Discussion
6.1 Performance Interpretation

Time Efficiency:
Kruskal is slightly faster in Graph 1 due to fewer heap operations. However, Prim’s advantage grows in denser graphs.

Operation Complexity:
Prim’s algorithm depends heavily on the number of adjacent vertices; Kruskal depends primarily on the number of edges.

Scalability:
For very large and sparse graphs, Kruskal is preferred. For dense graphs where adjacency lists are easy to maintain, Prim’s algorithm is more efficient.

Implementation Complexity:
Kruskal’s implementation requires additional data structure (Union-Find), while Prim’s algorithm is simpler to implement when adjacency lists are available.

7. Conclusion

This project successfully optimized a city’s road network using MST algorithms.
Both Prim’s and Kruskal’s algorithms produced identical minimal costs, validating correctness and theoretical equivalence.

Kruskal’s Algorithm proved efficient for sparse networks (fewer roads per district).

Prim’s Algorithm performed slightly better on dense networks (many potential connections).

The analysis confirms that choosing the right algorithm depends on the graph’s density and implementation constraints.
Overall, this work demonstrates a practical application of greedy graph algorithms for cost optimization in real-world infrastructure planning.

---
updated: 2025-10-26 23:22:16
