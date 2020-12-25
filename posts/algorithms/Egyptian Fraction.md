*[GeeksforGeeks](https://www.geeksforgeeks.org/greedy-algorithm-egyptian-fraction/)*
# Egypitian Fraction
- Every positive fraction can be represented as a sum of unique unit fractions.
- unit fraction has numerator of 1 and denomiator as a positive integer.
```
  Egyptian fraction of 2/3 is 1/2 + 1/6
```

Algorithm
- For a given number of the form nr/dr where dr > nr,
- find the greatest possible unit fraction
- recur for the remaining part

```python
import math 

def egyptianFraction(nr, dr):
    print("The egyptian fraction representation of {}/{} is".format(nr, dr), end='\n')

    denomitators = []

    # until fraction becomes 0
    while nr != 0:
        # take ceiling
        denomitator = math.ceil(dr/nr)

        denomitators.append(denomitator)

        # update new nr and dr
        nr = denomitator * nr - dr
        dr = dr * denomitator
    
    # print 
    for i in range(len(denomitators)):
        if i != len(denomitators)-1:
            print("1/{} +".format(denomitators[i]), end=' ')
        else:
            print("1/{}".format(denomitators[i]))

egyptianFraction(6, 14)
```
