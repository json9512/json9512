*[GeekforGeeks](https://www.geeksforgeeks.org/data-structures/)*
# Graph
consists of two components:
- A finite set of vertices also called as nodes
- A finite set of ordered pair of the form (u, v) called as edge. 
    - The pair is ordered because (u, v) is not same as (v, u) in case of a directed graph. 
    - The pair of form (u, v) indicates that there is an edge from vertex u to vertex v. 
    - The edges may contain weight, value, cost.

V = Number of vertices<br>
E = Number of edges

Graph can be classified based on basis of many things, the two most common are:
1. Direction: 
    - Undirected Graph: a graph which all edges are bidirectional.
    - Directed Graph: a graph which all edges are unidirectional.
2. Weight:
    - Weighted Graph: a graph which weight is associated with edges
    - Unweighted Graph: a graph which there is no weight assosicated with edges
    
Graph can be represented in many ways:

#### Sample graph
![graph](https://media.geeksforgeeks.org/wp-content/cdn-uploads/Tree_overview_of_data_structures_1.jpg)

#### As Adjacency Matrix
![adjmat](https://media.geeksforgeeks.org/wp-content/cdn-uploads/Tree_overview_of_data_structures_2.png)

#### As Adjacency List
![adjlist](https://media.geeksforgeeks.org/wp-content/cdn-uploads/Tree_overview_of_data_structures_3.jpg)

Time Complexity:
1. In case of adjacency matrix:
    - Traversal (BFS or DFS): O(V^2)
    - Space: O(V^2)
2. In case of adjacency list:
    - Traversal (BFS or DFS): O(V+E)
    - Space: O(V+E)
    
Used to solve many real world problems. Eg. finding the shortest path from PC-A to PC-B through the network.

# Trie

[Use this to visualize](https://www.cs.usfca.edu/~galles/visualization/Trie.html)

- Efficient for searching words in a dictionary
- No collisions unlike hashing
- Prefix search can be done
- Search complexity is linear in terms of word length to be searched. (Faster than words stored in BST)
- Requires more space
- Also known as radix tree, prefix tree

Time complexity: 
- Insertion Time: O(M) where M is the length of the string
- Deletion Time: O(M)
- Search Time: O(M)
- Space: O(Alphabet Size * M * N) where N is the number of keys in trie, Alphabet size is 26 if considering only uppercase Latin letters.

# Segment Tree
- used when there are lot of queries (min, max, sum, etc) on a set of values.
- queries also include update of values in given set.  
- implemented using array

![image](https://media.geeksforgeeks.org/wp-content/cdn-uploads/Tree_overview_of_data_structures_4.jpg)

Time complexity:
- Construction of tree(N): O(N)
- Query: O(log N)
- Update: O(log N)
- Space: O(N) [Exact Space= 2*N-1]

Used to find Max/Min/Sum/Prod of a range of values

# Suffix Tree
- Mainly used to search a pattern in text
- Preprocess text to make search operation be done in linear time in terms of patter length
- Pattern searching algorithm like KMP, Z take time proportional to the length of pattern
- Not good when text continuously changes. eg. text editors
- Suffix tree is a compressed Trie of all suffixes, abstract steps to build the suffix tree:
    - Generate all suffixes of given text
    - Consider all suffixes as individual words and build a compressed trie

![suffix](https://media.geeksforgeeks.org/wp-content/cdn-uploads/Tree_overview_of_data_structures_5.jpg)



