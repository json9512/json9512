*[GeeksforGeeks](https://www.geeksforgeeks.org/fundamentals-of-algorithms/)*
# Greedy algorithms
- builds up a solution piece by piece
- always chooses the next piece that gives the most profit
- used for optimization problems

Some algorithms that are greedy:
1. [Kruskal's minimum spanning tree](https://github.com/json9512/json9512/blob/main/posts/algorithms/kruskal's%20minimum%20spanning%20tree.md): always picks the smallest weighted edge that does not form a cycle
2. Prim's minimum spanning tree: always picks the smallest weighted edge that connects two sets. (first set stores vertices already stored in MST, other set stores the remaining vertices)
3. Dijkstra's shortest path: similar to prim's algorithm, picks the smallest weighted edge that connects two sets and is on the smallest weight path from source
4. Huffman Coding: lossless compression technique, assigns the least bit length code to the most frequent character

# More
- [Activity Selection](https://github.com/json9512/json9512/blob/main/posts/algorithms/activity%20selection.md)
