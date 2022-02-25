# Subsets

## Problem statement

Given a set with distinct elements, find all of its distinct subsets.

Example:
```text
Input: [1, 3]
Output: [], [1], [3], [1,3]
```

## Solution 

To solve this problem we start with an empty set, iterate through all numbers one-by-one, and add them to existing sets to create new subsets. For example:

Given set: [1, 5, 3]

1. Start with an empty set: [[]]
2. Add the first number (1) to all the existing subsets to create new subsets: [[], [1]];
3. Add the second number (5) to all the existing subsets: [[], [1], [5], [1,5]];
4. Add the third number (3) to all the existing subsets: [[], [1], [5], [1,5], [3], [1,3], [5,3], [1,5,3]].

```python
def get_subset(nums):
  result = []
  result.append([])
  for num in nums:
    n = len(result)
    for i in range(n):
      # For each element we copy and add
      # the new number.
      subset = list(result[i])
      subset.append(num)
      result.append(subset)
  return result
```

## Time complexity

In each step, the number of subsets doubles as we add each element to all the existing subsets, therefore, we will have a total of $O(2^N)$ subsets, where ‘N’ is the total number of elements in the input set. And because we construct a new subset from an existing set, the time complexity of the above algorithm will be $O(N * 2^N)$.

## Space complexity

We will have a total of $O(2^N)$ subsets, and each subset can take up to $O(N)$ space, therefore, the space complexity of our algorithm will be $O(N * 2^N)$.

## Tags
#subsets #bfs
