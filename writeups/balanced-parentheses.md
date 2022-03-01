# Balanced Parentheses

## Problem statement

For a given number ‘N’, write a function to generate all combination of ‘N’ pairs of balanced parentheses.

Example 1:

```text
Input: N=2
Output: (()), ()()
```

Example 2:

```text
Input: N=3
Output: ((())), (()()), (())(), ()(()), ()()()
```
## Solution

This problem follows the [Subsets](subsets.md) pattern and can be mapped to [Permutations](permutations.md). We can follow a similar BFS approach.

Following a BFS approach, we will keep adding an open parentheses `(` or a close parentheses `)`. At each step we need to keep two things in mind:

1. We can’t add more than ‘N’ open parenthesis.
2. To keep the parentheses balanced, we can add a close parenthesis `)` only when we have already added enough open parenthesis `(`. For this, we can keep a count of open and close parenthesis with every combination.

```python
from collections import deque, namedtuple

ParenthessString = namedtuple("ParenthessString", ["the_str", "open", "close"])

def generate_valid_parentheses(n):
    result = []
    queue = deque()
    queue.append(ParenthessString("", 0, 0))
    while queue:
        p = queue.popleft()
        if p.open == p.close == n:
            result.append(p.the_str)
        if p.open < n:
            queue.append(ParenthessString(p.the_str + "(", p.open + 1, p.close))
        if p.close < p.open:
            queue.append(ParenthessString(p.the_str + ")", p.open, p.close + 1))
    return result
```

## Time complexity

The overall time complexity of our algorithm will be $O(N*2^N)$. This is not completely accurate but reasonable enough to be presented in the interview.

The actual time complexity $O(4^n/\sqrt{n})$ is bounded by the Catalan number and is beyond the scope of a coding interview. 

## Space complexity

All the additional space used by our algorithm is for the output list. Since we can’t have more than $O(2^N)$ combinations, the space complexity of our algorithm is $O(N*2^N)$.

## Source
Educative

## Tags
#subsets #bfs
