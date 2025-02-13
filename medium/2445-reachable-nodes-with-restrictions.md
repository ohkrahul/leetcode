# Reachable Nodes With Restrictions

## Problem Link
[LeetCode - Reachable Nodes With Restrictions](https://leetcode.com/problems/reachable-nodes-with-restrictions/)

## Difficulty
Medium

## Problem Description
<p>There is an undirected tree with <code>n</code> nodes labeled from <code>0</code> to <code>n - 1</code> and <code>n - 1</code> edges.</p>

<p>You are given a 2D integer array <code>edges</code> of length <code>n - 1</code> where <code>edges[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> indicates that there is an edge between nodes <code>a<sub>i</sub></code> and <code>b<sub>i</sub></code> in the tree. You are also given an integer array <code>restricted</code> which represents <strong>restricted</strong> nodes.</p>

<p>Return <em>the <strong>maximum</strong> number of nodes you can reach from node </em><code>0</code><em> without visiting a restricted node.</em></p>

<p>Note that node <code>0</code> will <strong>not</strong> be a restricted node.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2022/06/15/ex1drawio.png" style="width: 402px; height: 322px;" />
<pre>
<strong>Input:</strong> n = 7, edges = [[0,1],[1,2],[3,1],[4,0],[0,5],[5,6]], restricted = [4,5]
<strong>Output:</strong> 4
<strong>Explanation:</strong> The diagram above shows the tree.
We have that [0,1,2,3] are the only nodes that can be reached from node 0 without visiting a restricted node.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2022/06/15/ex2drawio.png" style="width: 412px; height: 312px;" />
<pre>
<strong>Input:</strong> n = 7, edges = [[0,1],[0,2],[0,5],[0,4],[3,2],[6,5]], restricted = [4,2,1]
<strong>Output:</strong> 3
<strong>Explanation:</strong> The diagram above shows the tree.
We have that [0,5,6] are the only nodes that can be reached from node 0 without visiting a restricted node.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 &lt;= n &lt;= 10<sup>5</sup></code></li>
	<li><code>edges.length == n - 1</code></li>
	<li><code>edges[i].length == 2</code></li>
	<li><code>0 &lt;= a<sub>i</sub>, b<sub>i</sub> &lt; n</code></li>
	<li><code>a<sub>i</sub> != b<sub>i</sub></code></li>
	<li><code>edges</code> represents a valid tree.</li>
	<li><code>1 &lt;= restricted.length &lt; n</code></li>
	<li><code>1 &lt;= restricted[i] &lt; n</code></li>
	<li>All the values of <code>restricted</code> are <strong>unique</strong>.</li>
</ul>


## Test Cases
```
7
[[0,1],[1,2],[3,1],[4,0],[0,5],[5,6]]
[4,5]
7
[[0,1],[0,2],[0,5],[0,4],[3,2],[6,5]]
[4,2,1]
```

## Initial Template
```python
# Code template not available
```

## Solution
### 1. Initial Thoughts

---
- This problem asks us to find the maximum number of nodes reachable from node 0 without visiting any of the restricted nodes. We are given the number of nodes in the tree, the edges that define the tree, and the list of restricted nodes.
- One way to approach this problem is to use Depth First Search (DFS) to traverse the tree, starting from node 0. While traversing, we can keep track of the visited nodes and avoid visiting any of the restricted nodes.
- We can also use a set to store the restricted nodes for quick lookup. This will help us avoid unnecessary checks while traversing the tree.

### 2. Solution Implementation

```python
def max_reachable_nodes(n: int, edges: List[List[int]], restricted: List[int]) -> int:
    """
    Finds the maximum number of nodes reachable from node 0 without visiting any of the restricted nodes.

    Args:
    n: The number of nodes in the tree.
    edges: The edges that define the tree.
    restricted: The list of restricted nodes.

    Returns:
    The maximum number of nodes reachable from node 0 without visiting any of the restricted nodes.
    """
    # Create a set to store the restricted nodes for quick lookup.
    restricted_set = set(restricted)
    
    # Create an adjacency list to represent the tree.
    adj_list = [[] for _ in range(n)]
    for edge in edges:
        a, b = edge
        adj_list[a].append(b)
        adj_list[b].append(a)
    
    # Perform DFS to traverse the tree.
    visited = set()
    stack = [0]
    max_nodes = 0
    while stack:
        node = stack.pop()
        if node in restricted_set:
            continue
        
        visited.add(node)
        max_nodes += 1
        
        # Add the neighbors of the current node to the stack.
        for neighbor in adj_list[node]:
            if neighbor not in visited:
                stack.append(neighbor)
    
    return max_nodes
```

### 3. Solution Explanation

---
- The first step is to create a set of the restricted nodes for quick lookup.
- Next, we create an adjacency list to represent the tree.
- We then perform DFS starting from node 0. We keep track of the visited nodes in the `visited` set.
- We also keep track of the maximum number of nodes reached in the `max_nodes` variable.
- While traversing the tree, we check if the current node is in the `restricted_set`. If it is, we skip it.
- Otherwise, we add the current node to the `visited` set and increment the `max_nodes` counter.
- We then add the neighbors of the current node to the stack.
- We repeat this process until the stack is empty.
- Finally, we return the `max_nodes` counter.

### 4. Complexity Analysis

---
- Time complexity: O(N + E), where N is the number of nodes and E is the number of edges in the tree. This is because we traverse the entire tree once using DFS.
- Space complexity: O(N), as we store the visited nodes in a set and the adjacency list in a list of lists.

## Topics
Array, Hash Table, Tree, Depth-First Search, Breadth-First Search, Union Find, Graph

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-02-13
