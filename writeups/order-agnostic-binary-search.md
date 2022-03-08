# Order-agnostic Binary Search

## Problem Statement
Given a sorted array of numbers, find if a given number ‘key’ is present in the array. Though we know that the array is sorted, we don’t know if it’s sorted in ascending or descending order. You should assume that the array can have duplicates.

Write a function to return the index of the ‘key’ if it is present in the array, otherwise return -1.

Example 1:

```text
Input: [1, 2, 3, 4, 5, 6, 7], key = 5
Output: 4
```

Example 2:

```text
Input: [10, 6, 4], key = 4
Output: 2
```
## Solution

This problem is requires a bit modification on the original binary search algorithm. You need to first check the sort direction of the array, and with that information you can properly update the pointers.

```python
def binary_search(arr, key):
  left, right = 0, len(arr) - 1
  is_asc = arr[left] < arr[right]

  while left <= right:
    middle = (left + right) // 2
    if arr[middle] == key:
      return middle

    if is_asc:
      if arr[middle] < key:
        left = middle + 1
      elif arr[middle] > key:
        right = middle - 1
    else:
      if arr[middle] < key:
        right = middle - 1
      elif arr[middle] > key:
        left = middle + 1

  return -1
```

## Source
Educative

## Tags
#binary-search
