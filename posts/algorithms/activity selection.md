*[GeeksforGeeks](https://www.geeksforgeeks.org/activity-selection-problem-greedy-algo-1/)*
# Activity Selection Problem
- given n activites with their start and finish time
- select the maximum number of activities that can be performed by a single person,
- assuming that a person can only work on a single activity at a time

##### Approach
1. sort the activities by their finish time in ascending order
2. always pick the next activity whose finish time is least among the remaining activites
3. and the start time is more than or equal to the finish time of previously selected activity


##### Example
```python
def getMostActivities(s, f):
    stack = []
    n = len(f)

    # always choose the first activity
    i = 0 
    stack.append(i)
    for j in range(n):
        # if start time is greater than or equal to the finish time of previous activity
        if s[j] >= f[i]:
            stack.append(j)
            
            # update 'previous activity'
            i = j


    return stack
s = [1 , 3 , 0 , 5 , 8 , 5] 
f = [2 , 4 , 6 , 7 , 9 , 9] 
print(getMostActivities(s, f))
'''
[0, 1, 3, 4] # index values of the s,f pair. {(1, 2), (3, 4), (5, 7), (8, 9)}
'''
```
