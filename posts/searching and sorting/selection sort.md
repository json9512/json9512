*[GeeksforGeeks](https://www.geeksforgeeks.org/fundamentals-of-algorithms/)*
# Selection Sort

- sorts an array by repeatedly finding the smallest element from the unsorted sub array and placing it at the beginning
- maintains two sub arrays: 1. sorted 2. unsorted (to-sort array)
- inplace sorting algorithm

```python
def selectionSort(arr):
  # loop through the entire array
  for i in range(len(arr)):
    # idx position to store minimum value
    min_idx = i
    
    # loop through the to-sort array (i+1, end)
    for j in range(i+1, len(arr)):
      
      # Update idx with the minimum value
      if arr[j] < arr[min_idx]:
        min_idx = j
    
    # swap positions after j loop is finished
    arr[i], arr[min_idx] = arr[min_idx], arr[i]

array = [64 ,32, 52, 1, 31, 36, 31]
selectionSort(array)
print(array) # [1, 31, 31, 32, 36, 52, 64]
```

Time complexity: O(n^2)

Auxiliary Space: O(1) [Will never make more than O(n) swaps, useful when memory write is a restriction]

#### Stable Selection Sort

In case of the normal selection sort, it is said to be not stable. 

Which means that the sort does not guarantee the order of the elements when there are duplicates. 

For example,

```python
# if we have an array with a duplicate
arr = [51, 1, 41, 32, 61, 51]

# for explaining purposes, add a letter to indicate order of appearance
arr = [51a, 1, 41, 32, 61, 51b]

# after we perform a regular selection sort
# the order of items "51" is not maintained after the sort
arr = [1, 32, 41, 51b, 51a, 61]

# but with a stable selection sort, the order is maintained
arr = [1, 32, 41, 51a, 51b, 61]
```

Method: 
- instead of swapping the `arr[min_val]` and `arr[i]`, 
- insert the `arr[min_val]` to its location and shift all the elements

```python
def selectionSort(arr):
  # loop through the entire array
  for i in range(len(arr)):
    # print for demonstration purposes
    print(arr)
  
    # idx position to store minimum value
    min_idx = i
    
    # loop through the to-sort array (i+1, end)
    for j in range(i+1, len(arr)):
      
      # Update idx with the minimum value
      if arr[j] < arr[min_idx]:
        min_idx = j
    
    # instead of swapping positions
    key = arr[min_idx]
    
    # move elements
    while min_idx > i:
      arr[min_idx] = arr[min_idx -1]
      min_idx -= 1
    arr[i] = key

array = [64 ,32, 52, 1, 31, 36, 31]
selectionSort(array)
'''
  Stable selection sort
  [64, 32, 52, 1, 31, 36, 31] initial       
  [1, 64, 32, 52, 31, 36, 31] 1st iteration
  [1, 31, 64, 32, 52, 36, 31] .
  [1, 31, 31, 64, 32, 52, 36] .
  [1, 31, 31, 32, 64, 52, 36] .
  [1, 31, 31, 32, 36, 64, 52] .
  [1, 31, 31, 32, 36, 52, 64] nth iteration
  
  unstable selection sort
  [64, 32, 52, 1, 31, 36, 31] initial
  [1, 32, 52, 64, 31, 36, 31] 1st iteration
  [1, 31, 52, 64, 32, 36, 31] .
  [1, 31, 31, 64, 32, 36, 52] .
  [1, 31, 31, 32, 64, 36, 52] .
  [1, 31, 31, 32, 36, 64, 52] .
  [1, 31, 31, 32, 36, 52, 64] nth iteration
'''
```
