*[GeeksforGeeks](https://www.geeksforgeeks.org/prims-minimum-spanning-tree-mst-greedy-algo-5/)*

# Prim's Minimum Spanning Tree

- Greedy algorithm

Idea: 
- Spanning tree means all vertices must be connected
- so keeping two disjoint subsets of vertices must be connected to make the spanning tre
- choosing the minimum weighted edge will produce minimum spanning tree
- Starts with empty spanning tree
- Maintain two sets of vertices
    1. First contains vertices already included in MST
    2. Second contains vertices that are not included
- On each iteration, 
    1. consider all edges that connect the two set and pick the least weighted edge
    2. moves the other endpoint of the edge to the set containing MST (first set)
    
**Algorithm**
1. create a set that keeps track of vertices included in MST
2. assign key values to all vertices in the input graph. 
    - initialize key values as INF
    - assign key values as 0 for the first vertex so that it is picked first
3. While set(tracking vertices in MST) doesn't include all vertices:
    1. pick a vertex `u` which is not in the set(tracking vertices in MST) and has the minimum weight
    2. include `u` to set
    3. update key value of all adjacent vertices of `u`
        - To update key values, iterate through all adjacent vertices.
        - For every adjacent vertext `v`, if weight of `u`-`v` is less than the previous key value of `v`,
        - Update the key value as weight of `u`-`v`

**Implementation**

[source](https://cppsecrets.com/users/1032115979910410511011497115116111103105505149484957575564103109971051084699111109/Python-Implementation-of-Prims-Minimum-Spanning-Tree.php)
```python
def createAdjMatrix(V, G):
    # Create empty adjacent matrix
    adjMatrix = [[0 for row in range(V)] for col in range(V)]

    # populate adjacency matrix with correct weights
    for i in range(0, len(G)):
        # G[i][0] is index of one vertex (node)
        # G[i][1] is index of the other vertex
        adjMatrix[G[i][0]][G[i][1]] = G[i][2]
        adjMatrix[G[i][1]][G[i][0]] = G[i][2]
    
    return adjMatrix

def primsMST(V, G):
    # create adjacency matrix from graph
    adjMatrix = createAdjMatrix(V, G)

    # choose initial vertex from graph
    vertex = 0

    # initialize empty edges array and empty MST
    MST = []
    edges = []
    visited = []
    # keep track of min Edge
    # [from, to, weight]
    minEdge = [None, None, float('inf')]

    # run prim's algorithm until the MST
    # has all the vertices
    while len(MST) != V - 1:
        

        # mark the vertex as visited
        visited.append(vertex)

        # add each edge to the list of potential edges
        for i in range(0, V):
            if adjMatrix[vertex][i] != 0:
                edges.append([vertex, i, adjMatrix[vertex][i]])
        
        # find the edge with the smallest weight to a vertex
        # that has not yet visited
        for edge in range(0, len(edges)):
            if edges[edge][2] < minEdge[2] and edges[edge][1] not in visited:
                minEdge = edges[edge]
        
        # remove min weighted edge from the list of edges
        edges.remove(minEdge)

        # push min edge to MST
        MST.append(minEdge)

        # update vertex and rest minEdge
        vertex = minEdge[1]
        minEdge = [None, None, float('inf')]
    
    return MST

if __name__ == "__main__":
    # create graph nodes (vertices)
    a, b, c, d, e, f = 0, 1, 2, 3, 4, 5

    # create graph edges with weights
    graph = [[a, b, 2],
        [a, c, 3],
        [b, d, 3],
        [b, c, 5],
        [b, e, 4],
        [c, e, 4],
        [d, e, 2],
        [d, f, 3],
        [e, f, 5]]

    print(primsMST(6, graph))

    # prints [[0, 1, 2], [0, 2, 3], [1, 3, 3], [3, 4, 2], [3, 5, 3]]
    # Which is a graph
    #     1(b) - 3(d) - 4(e)
    #     |      |
    #     0(a)   5(f)
    #     |
    #     2(c)
```


