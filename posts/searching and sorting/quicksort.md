*[GeeksforGeeks](https://www.geeksforgeeks.org/quick-sort/)*
# Quick sort
- Divide and Conquer 
- use pivot and partitions given array around the pivot

```python
def partition(arr, low, high):
    # partition the array
    # place the pivot on the right position 
    # start i (all the numbers less than pivot) from low -1
    i = low-1

    # pivot will be the rightmost element
    pivot = arr[high]

    # iterate through the array
    for j in range(low, high):
        
        # if the current element is less than the pivot
        if arr[j] < pivot:
            # print for visuals
            print(arr)

            # increment the lower bound index
            i+=1

            # swap the current element with the element right after the lower bound index
            arr[i], arr[j] = arr[j], arr[i]
        

    # swap the pivot with the element at lower bound index + 1
    arr[i+1], arr[high] = arr[high], arr[i+1]

    # return the position of the pivot
    return i + 1

def quickSort(arr, low, high):
    # only partition when lower bound is lower than higher bound
    if low < high:
        partitioned = partition(arr, low, high)

        # quick sort the left sub array of pivot
        quickSort(arr, low, partitioned-1)

        # quick sort the right sub array of pivot
        quickSort(arr, partitioned+1, high)

arr = [0, 10, 7, 3, 8, 9, 1, 5] 
n = len(arr) 
quickSort(arr,0,n-1) 
print(arr)

'''
[0, 10, 7, 3, 8, 9, 1, 5] # j = 0
[0, 10, 7, 3, 8, 9, 1, 5] # swap j, i = 0, 0
[0, 3, 7, 10, 8, 9, 1, 5] # swap j = 3, i = 1 + 1 = 2; arr[j] <-> arr[i]
[0, 3, 1, 5, 8, 9, 7, 10]
[0, 1, 3, 5, 8, 9, 7, 10]
[0, 1, 3, 5, 8, 9, 7, 10]
[0, 1, 3, 5, 8, 9, 7, 10]
[0, 1, 3, 5, 7, 8, 9, 10] # final
'''
```

#### Iterative
```python
def partition(arr, low, high):
    # partition the array
    # place the pivot on the right position 
    # start i (all the numbers less than pivot) from low -1
    i = low-1

    # pivot will be the rightmost element
    pivot = arr[high]

    # iterate through the array
    for j in range(low, high):
        
        # if the current element is less than the pivot
        if arr[j] < pivot:
            # print for visuals
            print(arr)

            # increment the lower bound index
            i+=1

            # swap the current element with the element right after the lower bound index
            arr[i], arr[j] = arr[j], arr[i]
        

    # swap the pivot with the element at lower bound index + 1
    arr[i+1], arr[high] = arr[high], arr[i+1]

    # return the position of the pivot
    return i + 1


def quickSort(arr, low, high):
    # create supplementary stack
    size = high - low + 1
    stack = [0] * size

    # push initial values to stack
    top = 0
    stack[top] = low
    top += 1
    stack[top] = high

    # keep popping while stack is not empty
    while top >= 0:
        # pop low, high
        high = stack[top]
        top -= 1
        low = stack[top]
        top -=1

        # set pivot in its correct position
        pivot = partition(arr, low, high)

        # if there are elements on left side of pivot,
        # push it to stack
        if pivot-1 > low:
            top += 1
            stack[top] = low
            top += 1
            stack[top] = pivot - 1
        
        # if there are elements on right side of pivot,
        # push it to the stack
        if pivot+1 < high:
            top += 1
            stack[top] = pivot + 1
            top += 1
            stack[top] = high

arr = [4, 3, 5, 2, 1, 3, 2, 3] 
n = len(arr) 
quickSort(arr, 0, n-1) 
print(arr)
'''
[4, 3, 5, 2, 1, 3, 2, 3]
[2, 3, 5, 4, 1, 3, 2, 3]
[2, 1, 5, 4, 3, 3, 2, 3]
[2, 1, 2, 3, 3, 3, 5, 4]
[2, 1, 2, 3, 3, 3, 5, 4]
[2, 1, 2, 3, 3, 3, 4, 5]
[1, 2, 2, 3, 3, 3, 4, 5]
'''
```

- To reduce stack size, first push the indexes of smaller half
- Use insertion sort when the size reduces below a experimentally calculated threshold

***


- Time taken depends on input array and partition strategy
- Worst Case: O(n^2) [When pivot is always the last element, and when array is already sorted]
- Best Case: O(n log n) [When pivot is always the middle]
- Average Case: O(n log n)
- Inplace: True
- Stable: False

***
#### Why quick sort is preferred over merge sort for sorting arrays?
- inplace sort (merge sort requires O(n) extra storage)
- cache friendly algorithm because it has good locality of reference when used for arrays
- tail recursive

#### Why merge sort over quick sort on linked lists?
- merge operation of merge sort can be executed without extra space since it takes O(1) space and time for insertion in linked list
- cannot do random access on linked lists, finding the i-th element takes traversing in linked list. [Quick sort uses a lot these, while merge sort does not]

## Three way quick sort
- when elements are redundant
- array is divided into 3 parts
- arr[left . . . i] : elements less than the pivot
- arr[i . . . j]: elements equal to the pivot
- arr[j . . . end]: elements greater than the pivot
