*[GeeksforGeeks](https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-algorithm-greedy-algo-2/)*
# Kruskal's minimum spanning tree
- is a greedy algorithm
- **Minimum spanning tree** 
    - a subgraph of a connected undirected graph, that is a tree and connects all vertices together.
    - A single graph can have multiple spanning trees. *Minimum spanning tree* is a spanning tree with weight less than or equal to the weight of every other spanning tree.
    - Minimum spanning tree has (V-1) edges where V is the number of vertices in the given graph

**Algorithm**
1. Sort all the edges in non-decreasing order of their weight
2. Pick the smallest edge. Check if it forms a cycle ([Union-Find algorithm](https://github.com/json9512/json9512/blob/main/posts/algorithms/Union-find.md)) with the spanning tree formed so far. If cycle is not formed include the edge. Else, discard it
3. Repeat step 2 until there are (V-1) edges in the spanning tree

