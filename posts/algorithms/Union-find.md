*[GeeksforGeeks](https://www.geeksforgeeks.org/union-find/)*
# Union Find algorithm
- Check if undirected graph has a cycle or not
- Uses `find()` and `union()` to determine a cycle
- `find()` is used to check which subset a particular element is in. Used for determining if two elements are in the same subset
- `union()` is used to join two subsets into a single subset
- *Union by rank* and *path compression* is used to optimize the algorithm from O(n) to O(log n) or even less.

```python
from collections import defaultdict

# Graph class
class Graph:
    def __init__(self, total_v: int) -> None:
        self.total_v = total_v
        self.edges = defaultdict(list)

    def addEdge(self, u: int, v: int) -> None:
        self.edges[u].append(v)

# Subset holds each node's parent and its rank
class Subset:
    def __init__(self, parent: int, rank: int) -> None:
        self.parent = parent
        self.rank = rank

# finds the set of an element node (uses path compression)
def find(subsets: list, node: int) -> int:
    
    if subsets[node].parent != node:
        subsets[node].parent = find(subsets, subsets[node].parent)
    
    return subsets[node].parent

# union of two sets using union by rank
def union(subsets: list, u: int, v: int) -> None:

    # attach smaller rank tree under root of high rank tree (union by rank)
    if subsets[u].rank > subsets[v].rank:
        subsets[v].parent = u
    elif subsets[v].rank > subsets[u].rank:
        subsets[u].parent = v
    else:
        # if the rank is the same, make one as parent and increment its rank
        subsets[v].parent = u
        subsets[u].rank += 1

def isCycle(graph: object) -> bool:
    subsets = []


    for u in range(graph.total_v):
        subsets.append(Subset(u, 0))

    # iterate through all edges of the graph
    # find set of both vertices of every edge
    # if sets are the same, there is a cycle
    for u in graph.edges:
        u_rep = find(subsets, u)
        for v in graph.edges[u]:
            v_rep = find(subsets, v)
            if u_rep == v_rep:
                return True
            else:
                union(subsets, u_rep, v_rep)

# Driver Code
g = Graph(4)
 
# add edge 0-1
g.addEdge(0, 1)
 
# add edge 1-2
g.addEdge(1, 2)
 
# add edge 0-2
g.addEdge(0, 2)

print(isCycle(g)) # True
```
