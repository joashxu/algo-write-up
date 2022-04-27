# Topological Sort

## Problem Statement

Topological Sort of a directed graph (a graph with unidirectional edges) is a linear ordering of its vertices such that for every directed edge (U, V) from vertex U to vertex V, U comes before V in the ordering.

Given a directed graph, find the topological ordering of its vertices.

Example:

Input: Vertices=7, Edges=[6, 4], [6, 2], [5, 3], [5, 4], [3, 0], [3, 1], [3, 2], [4, 1]
Output: Following are all valid topological sorts for the given graph:
1) 5, 6, 3, 4, 0, 1, 2
2) 6, 5, 3, 4, 0, 1, 2
3) 5, 6, 4, 3, 0, 2, 1
4) 6, 5, 4, 3, 0, 1, 2
5) 5, 6, 3, 4, 0, 2, 1
6) 5, 6, 3, 4, 1, 2, 0

There are other valid topological ordering of the graph too.

## Solution

To solve this problem you can:

1. Use hash for a graph and an in-degree counter.
2. Build the graph and find in-degrees of all vertices.
3. Find all sources (notes with 0 in-degree) and put them in the queue.
4. Sort. you can traverse the graph in a Breadth First Search (BFS) way. For each source:
   * Add it to the sorted list.
   * Get all of its children from the graph.
   * Decrement the in-degree of each child by 1.
   * If a child's in-degree becomes '0', add it to the souurces queue.
   * Repeat until sources queue is empty. 

```python
from collections import deque

def topological_sort(vertices, edges):
  sorted_order = []
  if vertices <= 0:
    return sorted_order

  # Initialize the graph.
  graph = {i: [] for i in range(vertices)}
  # Count of incoming edges
  in_degree = {i: 0 for i in range(vertices)}
  
  # Build the graph.
  for parent, child in edges:
    graph[parent].append(child)
    in_degree[child] += 1

  # Find all the sources (vertex with 0 in-degrees)
  # and add to queue.
  sources = deque()
  for vertex, degree in in_degree.items():
    if degree == 0:
      sources.append(vertex)

  # For each source, add it to sorted_order 
  # and substract in-degree from 
  # all its children.  
  while sources:
    vertex = sources.popleft()
    sorted_order.append(vertex)
    for child in graph[vertex]:
      in_degree[child] -= 1
      # If child's in-degree becomes zero, 
      # add it to the sources queue.
      if in_degree[child] == 0:
        sources.append(child)

  # Topological sort is not possible 
  # as the graph has a cycle.
  if len(sorted_order) != vertices:
    return []

  return sorted_order
```

## Time Complexity
When we are in the sort state, each vertex will become a source only once and each edge will be accessed and removed once. Therefore, the time complexity of the above algorithm will be O(V+E), where ‘V’ is the total number of vertices and ‘E’ is the total number of edges in the graph.

## Space Complexity
The space complexity will be O(V+E), since we are storing all of the edges for each vertex in an adjacency list.

## Source
Educative

## Tags
#topological-sortf #bfs
