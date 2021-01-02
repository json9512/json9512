*[GeeksforGeeks](https://www.geeksforgeeks.org/external-sorting/#:~:text=External%20sorting%20is%20required%20when,(usually%20a%20hard%20drive).&text=Then%20sort%20each%20run%20in%20main%20memory%20using%20merge%20sort%20sorting%20algorithm.)*
# External Sorting

External sorting is a technique used when massive amount of data that do not fit in main memory have to be sorted.

For example, if the main memory only supports 8 KBs of data and the external memory to sort is 64 KBs, an external sorting algorithm must be used to sort the entire 64 KBs.

The algorithm will sort the 64 KBs in pieces of 8 KBs and the pieces of 8 KBs would later be merged. 

There are three well known methods for external sorting:
1. External merge sort
2. External distribution sort
3. External buffer-tree sort

# External Merge Sort

Idea:
- data is divided into chunks
- chunks are sorted using merge sort
- sorted chunk is dumped to file
- sort the whole array using merge k sorted array algorithm

**Algorithm**

Chunk is referred as 'run'

1. Read input file elements at most the 'run size'
2. sort the run using merge sort
3. store the sorted array in a file (store the order of runs as well)
4. merge the sorted files using the merge k sorted arrays algorithm

**Implement python version here**

# External Distribution Sort

Look into this *[J. Erickson, Lecture from University of Illinois at Urbana Campaign](https://jeffe.cs.illinois.edu/teaching/473/01-search+sort.pdf)*
