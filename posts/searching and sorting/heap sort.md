*[GeeksforGeeks](https://www.geeksforgeeks.org/heap-sort/)*
# Heap Sort
- based on [binary heap](https://github.com/json9512/json9512/blob/main/posts/data_structure/BinaryTree%2C%20BST%2C%20heap%2C%20hash.md#binary-heap)

Algorithm:
1. build max heap from input data
2. replace the root (largest item) with the last item of the heap. 
3. reduce the size of the heap by 1.
4. Heapify the root of the tree
5. repeat while heap size is greater than 1

```python
def heapify(arr, length, root):
    # initialize largest as root
    largest = root
    print(arr)
    # children nodes
    left = 2 * root + 1 
    right = 2 * root + 2

    # see if left child of root exists and is greater than root
    if left < length and arr[left] > arr[largest]:
        largest = left

    # see if right child of root exists and is greater than root
    if right < length and arr[right] > arr[largest]:
        largest = right

    # change root if needed
    if largest != root:
        # swap
        arr[root], arr[largest] = arr[largest], arr[root] 

        # heapify (check again for largest value to head to the root)
        heapify(arr ,length, largest)
    
# sort
def heapSort(arr):
    length = len(arr)
    # build max heap
    for i in range(length//2 -1, -1, -1):
        heapify(arr, length, i)

    # extract elements
    for i in range(length-1, 0, -1):
        # swap
        arr[i], arr[0] = arr[0], arr[i]
        heapify(arr, i, 0)
    

arr = [12, 15, 13, 5, 6, 7]
heapSort(arr)

'''
[12, 15, 13, 5, 6, 7] # initial
[12, 15, 13, 5, 6, 7]
[12, 15, 13, 5, 6, 7]
[15, 12, 13, 5, 6, 7]
[7, 12, 13, 5, 6, 15]
[13, 12, 7, 5, 6, 15]
[6, 12, 7, 5, 13, 15]
[12, 6, 7, 5, 13, 15]
[5, 6, 7, 12, 13, 15]
[7, 6, 5, 12, 13, 15]
[5, 6, 7, 12, 13, 15]
[6, 5, 7, 12, 13, 15]
[5, 6, 7, 12, 13, 15] # final
'''
```

#### Iterative version
```python
def buildMaxHeap(arr, length):
    for i in range(length):
        # if child is greater than parent
        if arr[i] > arr[(i-1)//2]:
            j = i

            # swap parent and child until parent is smaller
            while arr[j] > arr[int((j-1)/2)]:
                arr[j], arr[int((j-1)/2)] = arr[int((j-1)/2)], arr[j]
                j = int((j-1)/2)
              
def heapsort(arr, length):
    buildMaxHeap(arr, length)

    for i in range(length-1, 0, -1):
        print(arr)
        # Swap value of first indexed value with the last indexed value
        arr[0], arr[i] = arr[i], arr[0]

        # maintaining heap property after swapping
        root_idx = 0
        index = 0

        while True:
            # initially 'index' is the left child index in the max heap array
            #        15      root
            #    10     13   left = 10, right = 13
            #  4   8  11  12
            #
            # as array= [15, 10, 13, 4, 8, 11, 12]
            # root idx = 0
            # left idx (index) = 1
            # right idx (index+1) = 2
            index = 2 * root_idx + 1

            # if left is smaller than right, 
            # point index to right
            if index < i-1 and arr[index] < arr[index +1]:
                index += 1
            
            # if parent is smaller than child, 
            # swap
            if index < i and arr[root_idx] < arr[index]:
                arr[root_idx], arr[index] = arr[index], arr[root_idx]
            
            root_idx = index
            if index >= i:
                break


arr = [ 10, 20, 15, 17, 9, 21]
heapsort(arr, len(arr))
print(arr)
'''
[21, 17, 20, 10, 9, 15] # after max heap
[20, 17, 15, 10, 9, 21]
[17, 10, 15, 9, 20, 21]
[15, 10, 9, 17, 20, 21]
[10, 9, 15, 17, 20, 21]
[9, 10, 15, 17, 20, 21] # final
'''
```

- Time complexity: O(n log n)[heapify is O(log n), creating and building a heap is O(n)] 
- Inplace: True
- Stable: False
