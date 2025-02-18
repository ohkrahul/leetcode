# Course Schedule

## Problem Link
[LeetCode - Course Schedule](https://leetcode.com/problems/course-schedule/)

## Difficulty
Medium

## Problem Description
<p>There are a total of <code>numCourses</code> courses you have to take, labeled from <code>0</code> to <code>numCourses - 1</code>. You are given an array <code>prerequisites</code> where <code>prerequisites[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> indicates that you <strong>must</strong> take course <code>b<sub>i</sub></code> first if you want to take course <code>a<sub>i</sub></code>.</p>

<ul>
	<li>For example, the pair <code>[0, 1]</code>, indicates that to take course <code>0</code> you have to first take course <code>1</code>.</li>
</ul>

<p>Return <code>true</code> if you can finish all courses. Otherwise, return <code>false</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> numCourses = 2, prerequisites = [[1,0]]
<strong>Output:</strong> true
<strong>Explanation:</strong> There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> numCourses = 2, prerequisites = [[1,0],[0,1]]
<strong>Output:</strong> false
<strong>Explanation:</strong> There are a total of 2 courses to take. 
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= numCourses &lt;= 2000</code></li>
	<li><code>0 &lt;= prerequisites.length &lt;= 5000</code></li>
	<li><code>prerequisites[i].length == 2</code></li>
	<li><code>0 &lt;= a<sub>i</sub>, b<sub>i</sub> &lt; numCourses</code></li>
	<li>All the pairs prerequisites[i] are <strong>unique</strong>.</li>
</ul>


## Test Cases
```
2
[[1,0]]
2
[[1,0],[0,1]]
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts:
### Problem analysis:
- The problem asks if it is possible to complete all courses given a list of prerequisites.
- We need a way to track the dependencies between courses and determine if there are any circular dependencies.
### Key observations:
- We can represent the courses and their dependencies as a directed graph.
- If there are no circular dependencies, then it is possible to complete all courses.
### Possible approaches:    
1. **Depth First Search**: We can use a DFS to traverse the graph and detect if there is a cycle.
2. **Topological Sort**: We can use a topological sort to order the courses based on their dependencies. If the sort is successful, then it is possible to complete all courses.

## 2. Solution Implementation:
```python
from collections import defaultdict
from typing import List, Tuple

def canFinish(numCourses: int, prerequisites: List[List[int]]) -> bool:
    # Create an adjacency list to represent the courses and their dependencies
    adj_list = defaultdict(list)
    for course, pre in prerequisites:
        adj_list[pre].append(course)

    # Create a set to keep track of visited courses
    visited = set()

    # Create a set to keep track of courses that are currently being visited
    visiting = set()

    def has_cycle(node):
        # If the node is already being visited, then there is a cycle
        if node in visiting:
            return True

        # If the node has already been visited, then it cannot be part of a cycle
        if node in visited:
            return False

        # Mark the node as being visited
        visiting.add(node)

        # Recursively check for cycles in the neighbors of the node
        for neighbor in adj_list[node]:
            if has_cycle(neighbor):
                return True

        # If no cycles were found in the neighbors, then mark the node as visited
        visited.add(node)

        # Remove the node from the set of nodes being visited
        visiting.remove(node)

        return False

    # Check for cycles in each node in the graph
    for node in range(numCourses):
        if has_cycle(node):
            return False

    # If no cycles were found, then it is possible to complete all courses
    return True
```

## 3. Solution Explanation:
This solution uses a depth-first search to detect cycles in the graph. The `has_cycle` function is called for each node in the graph to check if there is a cycle. If a cycle is detected, the function returns True, indicating that it is not possible to complete all courses. If no cycles are detected, the function returns False, indicating that it is possible to complete all courses.

## 4. Complexity Analysis:
### Time complexity: O(V + E)
- `V` is the number of nodes in the graph (courses) 
- `E` is the number of edges in the graph (prerequisites)
The time complexity is dominated by the depth-first search, which visits each node and edge in the graph once.

### Space complexity: O(V + E)
- The adjacency list uses space proportional to the number of nodes and edges in the graph.
- The visited and visiting sets use space proportional to the number of nodes in the graph.

## Topics
Depth-First Search, Breadth-First Search, Graph, Topological Sort

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-02-18
