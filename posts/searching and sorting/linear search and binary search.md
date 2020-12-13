# Linear search

- Sequential search
- Start from left most element, check if element is the search value, move the pointer to the right if not

```python
arr = [1, 2, 42, 31, 55, 34, 521]
target = 55

def search(target, arr):
  for i in range(len(arr)):
    if arr[i] == target:
      return i
  return -1

print("index: %d" % search(target, arr))
    
# prints => "index: 4"
```

Time complexity: O(n)

# Binary search

- Can only be used with a sorted array
- Finds target by checking the mid-point value of the given search array
- Divde the search scope in half on each operation
    - Given the the array is sorted in ascending order:
    - drop left part of the search array if mid-point is less than the target or drop right part of the search array if mid-point is greater than the target
    - move the left pointer to mid + 1, or move the right pointer to mid - 1
    - repeat
 
 ```python
def binarySearch(arr,left, right, target) -> int:
    while left <= right:
      mid = left + (right - left) // 2
      
      if arr[mid] == target:
        return mid
      
      elif arr[mid] < target:
        left = mid + 1
        
      else:
        right = mid - 1
        
    return -1
    
array = [1, 2, 3, 4, 5]
target = 4

print(binarySearch(array, 0, len(array)-1, target)) # prints: 3
 ```
 
 Time complexity: O(log n)
 
 Auxiliary Space (temporary space needed by the algorithm) complexity: O(1) for iterative, O(log n) for recursive
