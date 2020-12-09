*[GeeksforGeeks](https://www.geeksforgeeks.org/data-structures/)*
# Array

- linear data structure
- a collection of items stored **contiguous** memory locations.
- ideally, store multiple data of the same type
- calculate the position of each element by adding an offset to the base value

Time complexity:
- Accessing time O(1) [Possible when elements are stored next to each other]
- Search time O(n) for sequential search, O(log n) for binary search [when array is sorted]
- Insertion time O(n) [Worst case: inserting at the beginning, causing the entire array to shift]
- Deletion time O(n) [Worst case: same as above]

# Linked List
- each element(node) is a separate object (not necessarily have to be stored continguously in memory)
- each element(node) has two items: 
    1. the data
    2. reference to next node

Three types of linked list:
1. Singly linked list - each node reference the next node, and the last node reference either null or next address in memory
2. Doubly linked list - each node reference the next node and the prior node
    - advantage: can traverse in both direction, don't need previous node for deletion
3. Circular linked list - the list forms a circle (eg. the last node points to the start node). can be implemented either singly or doubly.
    - advantage: any node can be a starting node
    
Time complexity:
- Accessing time O(n)
- Search time O(n)
- Insertion time O(1) [if we are at the position where we have to insert]
- Deletion time O(1) [if we know the address of previous node connected with the deletion node]

Advantage:
- Effective memory usage
- Insertion, Deletion more efficient compared to arrays

Disadvantage:
- random access is not allowed

# Stack

- abstract data type: can be implemented with arrays or linked lists
- Last in first out: imagine a pile of books in a box.
- Two main functions: push() - adds item, pop() - removes the top item
- Insertion/Deletion are only allowed on one end

Time complexity:
- Accessing time O(n) [Worst case]
- Insertion O(1)
- Deletion O(1)

# Queue

- abstract data type: can be implemented with arrays or linked lists
- First in first out: imagine a queue at KFC.
- two main functions: enqueue(), dequeue()

Time complexity:
- Accessing time: O(n) [Worst case]
- Insertion O(1)
- Deletion O(1)
