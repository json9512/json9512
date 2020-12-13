*[GeeksforGeeks](https://www.geeksforgeeks.org/merge-sort/)*
# Merge Sort
- Divide and Conquer algorithm
- divide input into two halves
- sorts each half
- merge sorted halves

![process](https://media.geeksforgeeks.org/wp-content/cdn-uploads/Merge-Sort-Tutorial.png)

```python
def mergeSort(arr):
    if len(arr) > 1:
        
    
        # find the mid point
        mid = len(arr) // 2

        # divide into two sub arrays
        left = arr[:mid]
        right = arr[mid:]

        # Sort the left half
        mergeSort(left)
        
        # Sort the right half
        mergeSort(right)

        i = j = k = 0

        while i < len(left) and j < len(right):
            if left[i] < right[j]:
                arr[k] = left[i]
                i+=1
            else:
                arr[k] = right[j]
                j+= 1
            k += 1
        
        while i < len(left):
            arr[k] = left[i]
            i += 1
            k += 1

        while j < len(right):
            arr[k] = right[j]
            j += 1
            k += 1

array = [1, 5, 32, 2, 42, 3, 55]
mergeSort(array)
print(array) # [1, 2, 3, 5, 32 42, 55]
```

- Time complexity: θ(n log n) (because merger sort will always divide the array in half and take linear time to merge the sub array)
- Auxiliary Space: O(n)
- Inplace: False
- Stable: Yes
- Good for external sorting

