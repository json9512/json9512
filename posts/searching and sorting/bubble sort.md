*[GeeksforGeeks](https://www.geeksforgeeks.org/fundamentals-of-algorithms/)*
# Bubble sort
- simplest sorting algorithm
- pairwise comparison, switches places if left is less than right
- algorithm requires the last iteration to be done on the sorted array to confirm that it has been sorted

```python
def bubbleSort(arr):
  n = len(arr)
 
  # loop through the entire array
  for i in range(n):
    print(arr)
    # inner loop
    # n-i-1: elements found above here are already sorted
    for j in range(0, n-i-1):
      # Swap if the element found is greater than the next element
      if arr[j] > arr[j+1]:
        arr[j], arr[j+1] = arr[j+1], arr[j]

array = [51, 23, 41, 22, 1, 5]
bubbleSort(array)
'''
[51, 23, 41, 22, 1, 5] initial
[23, 41, 22, 1, 5, 51]
[23, 22, 1, 5, 41, 51]
[22, 1, 5, 23, 41, 51]
[1, 5, 22, 23, 41, 51]
[1, 5, 22, 23, 41, 51] sorted

inner loop operation for first outer loop iteration
outer loop: [51, 23, 41, 22, 1, 5] initial

inner loop: [51, 23, 41, 22, 1, 5] initial
inner loop: [23, 51, 41, 22, 1, 5]
inner loop: [23, 41, 51, 22, 1, 5]
inner loop: [23, 41, 22, 51, 1, 5]
inner loop: [23, 41, 22, 1, 51, 5]
inner loop: [23, 41, 22, 1, 5, 51] after j loop finished
'''
```

Time complexity for above array is always O(n^2) - even if the array is sorted.

Can be optimized to stop algorithm when inner loop does not cause a swap

Time complexity:

- Worst and Average: O(n*m) [if optimized with 'swapped' boolean;Worst case when array is reverse sorted]
- Best case: O(n) [Best case when array is sorted]
- Auxiliary Space: O(1)
- Inplace: True
- Stable: True
