# Permutation

## Problem statement

Given a set of distinct numbers, find all of its permutations.

## Solution summary

* You can use BFS approach to get permutations given a set of elements.
* The time complexity for permutation is huge. The input size should not be more than 10 or 11.

## Solution

This problem can be solved by following a BFS approach.

```python
def  get_permutations(nums):
    result = []

    # A queue that hold temporary permutations
    permutations = deque()
    permutations.append([])
    for num in nums:
        n = len(permutations)
        for _ in range(n):
            # Pop each item in the permutations 
            old = permutations.popleft()

            # For each item copy and insert current number
            # from position 0 to the len(old) + 1
            for j in range(len(old) + 1):
                new = old[:]
                new.insert(j, num)
                if len(new) == len(nums):
                    # If the len of permutation is already
                    # equal to len of number, add to result.
                    result.append(new)
                else:
                    # Store the permutations to a temporary
                    # queue.
                    permutations.append(new)
    return result
```

### Time complexity

We iterate through all permutations with the help of two 'for' loops. In each iteration, we go through all the current permutations to insert a new number. To insert a number into a permutation of size N will take $O(N)$, which makes the overall time complexity of this algorithm to $O(N * N!)$

### Space complexity

All the additional space used by this algorithm is for the result list and the queue to store the intermediate permutations. We don’t have more than $N!$ permutations between the result list and the queue. Therefore the overall space complexity to store $N!$ permutations each containing $N$ elements will be $O(N*N!)$

### Using Python library

Python has built-in library to generate permutations.

```python
from itertools import permutations

def find_permutations(nums):
  return list(permutations(nums))
```

## Source
Educative

## Tags
#subsets #bfs #queue
