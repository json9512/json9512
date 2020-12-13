*[GeeksforGeeks](https://www.geeksforgeeks.org/insertion-sort/)*
# Insertion Sort
- has two sub arrays: 1. sorted, 2. unsorted
- values from unsorted are placed at the correct position on the sorted array

Algorithm
1. iterate from arr[1] to arr[n] over the array
2. compare the current element to its predecessor
3. if the key element is smaller than its predecessor, compare it to the elements before. Move the greater elements one position up to make space for the swapped element

![visual](https://media.geeksforgeeks.org/wp-content/uploads/insertionsort.png)

```python
def insertionSort(arr):
  for i in range(1, len(arr)):
    print("outer", array)
    key = arr[i]
    
    # move elements of arr[0 ... i-1], that are
    # greater than key, to one position ahead of their current position
    j = i-1
    while j >= 0 and key < arr[j]:
      arr[j+1] = arr[j]
      j -= 1
      print("inner", array)
      
    arr[j+1] = key

array = [43, 32, 3, 21, 15, 4, 2]
insertionSort(array)
print(array) # [[2, 3, 4, 15, 21, 32, 43]]
```

- Time complexity: O(n^2)
- Auxiliary Space: O(1)
- Inplace: True
- Stable: True
