# Find Closest Node to Given Two Nodes

## Problem Link
[LeetCode - Find Closest Node to Given Two Nodes](https://leetcode.com/problems/find-closest-node-to-given-two-nodes/)

## Difficulty
Medium

## Problem Description
<p>You are given a <strong>directed</strong> graph of <code>n</code> nodes numbered from <code>0</code> to <code>n - 1</code>, where each node has <strong>at most one</strong> outgoing edge.</p>

<p>The graph is represented with a given <strong>0-indexed</strong> array <code>edges</code> of size <code>n</code>, indicating that there is a directed edge from node <code>i</code> to node <code>edges[i]</code>. If there is no outgoing edge from <code>i</code>, then <code>edges[i] == -1</code>.</p>

<p>You are also given two integers <code>node1</code> and <code>node2</code>.</p>

<p>Return <em>the <strong>index</strong> of the node that can be reached from both </em><code>node1</code><em> and </em><code>node2</code><em>, such that the <strong>maximum</strong> between the distance from </em><code>node1</code><em> to that node, and from </em><code>node2</code><em> to that node is <strong>minimized</strong></em>. If there are multiple answers, return the node with the <strong>smallest</strong> index, and if no possible answer exists, return <code>-1</code>.</p>

<p>Note that <code>edges</code> may contain cycles.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2022/06/07/graph4drawio-2.png" style="width: 321px; height: 161px;" />
<pre>
<strong>Input:</strong> edges = [2,2,3,-1], node1 = 0, node2 = 1
<strong>Output:</strong> 2
<strong>Explanation:</strong> The distance from node 0 to node 2 is 1, and the distance from node 1 to node 2 is 1.
The maximum of those two distances is 1. It can be proven that we cannot get a node with a smaller maximum distance than 1, so we return node 2.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2022/06/07/graph4drawio-4.png" style="width: 195px; height: 161px;" />
<pre>
<strong>Input:</strong> edges = [1,2,-1], node1 = 0, node2 = 2
<strong>Output:</strong> 2
<strong>Explanation:</strong> The distance from node 0 to node 2 is 2, and the distance from node 2 to itself is 0.
The maximum of those two distances is 2. It can be proven that we cannot get a node with a smaller maximum distance than 2, so we return node 2.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == edges.length</code></li>
	<li><code>2 &lt;= n &lt;= 10<sup>5</sup></code></li>
	<li><code>-1 &lt;= edges[i] &lt; n</code></li>
	<li><code>edges[i] != i</code></li>
	<li><code>0 &lt;= node1, node2 &lt; n</code></li>
</ul>


## Test Cases
```
[2,2,3,-1]
0
1
[1,2,-1]
0
2
```

## Initial Template
```python
# Code template not available
```

## Solution
### 1. Initial Thoughts:

- This problem can be solved using Depth First Search (DFS).
- We start with the two nodes, `node1` and `node2`, and perform DFS in opposite directions.
- We keep track of the maximum distance from `node1` to any node and the maximum distance from `node2` to any node.
- If we encounter a node that has already been visited by both DFS searches, then that node is the closest node that can be reached from both `node1` and `node2`.
- If we reach the end of the graph without finding a common node, then there is no node that can be reached from both `node1` and `node2`.

### 2. Solution Implementation:
```python
def closestNode(edges, node1, node2):
    # Keep track of visited nodes
    visited = set()

    # Maximum distance from node1 and node2 to any node
    max_dist1, max_dist2 = 0, 0

    # Initialize two DFS stacks
    stack1 = [node1]
    stack2 = [node2]

    while stack1 or stack2:
        # DFS from node1
        if stack1:
            node = stack1.pop()
            if node not in visited:
                visited.add(node)
                if node == node2:
                    return node
                if edges[node] != -1:
                    stack1.append(edges[node])
                    max_dist1 = max(max_dist1, len(stack1))

        # DFS from node2
        if stack2:
            node = stack2.pop()
            if node not in visited:
                visited.add(node)
                if node == node1:
                    return node
                if edges[node] != -1:
                    stack2.append(edges[node])
                    max_dist2 = max(max_dist2, len(stack2))

    # If no common node is found, return -1
    return -1
```

### 3. Solution Explanation:

- We keep track of visited nodes to avoid cycles in the graph.
- For each node we visit, we update the maximum distance from `node1` and `node2` to that node.
- If we encounter a node that has already been visited by both DFS searches, then that node is the closest node that can be reached from both `node1` and `node2`.
- If we reach the end of the graph without finding a common node, then there is no node that can be reached from both `node1` and `node2`.

### 4. Complexity Analysis:

- **Time complexity**: O(n), where n is the number of nodes in the graph. We visit each node at most once.
- **Space complexity**: O(n), as we store the visited nodes in a set.

## Topics
Depth-First Search, Graph

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-02-25
