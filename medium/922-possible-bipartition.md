# Possible Bipartition

## Problem Link
[LeetCode - Possible Bipartition](https://leetcode.com/problems/possible-bipartition/)

## Difficulty
Medium

## Problem Description
<p>We want to split a group of <code>n</code> people (labeled from <code>1</code> to <code>n</code>) into two groups of <strong>any size</strong>. Each person may dislike some other people, and they should not go into the same group.</p>

<p>Given the integer <code>n</code> and the array <code>dislikes</code> where <code>dislikes[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> indicates that the person labeled <code>a<sub>i</sub></code> does not like the person labeled <code>b<sub>i</sub></code>, return <code>true</code> <em>if it is possible to split everyone into two groups in this way</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> n = 4, dislikes = [[1,2],[1,3],[2,4]]
<strong>Output:</strong> true
<strong>Explanation:</strong> The first group has [1,4], and the second group has [2,3].
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> n = 3, dislikes = [[1,2],[1,3],[2,3]]
<strong>Output:</strong> false
<strong>Explanation:</strong> We need at least 3 groups to divide them. We cannot put them in two groups.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 2000</code></li>
	<li><code>0 &lt;= dislikes.length &lt;= 10<sup>4</sup></code></li>
	<li><code>dislikes[i].length == 2</code></li>
	<li><code>1 &lt;= a<sub>i</sub> &lt; b<sub>i</sub> &lt;= n</code></li>
	<li>All the pairs of <code>dislikes</code> are <strong>unique</strong>.</li>
</ul>


## Test Cases
```
4
[[1,2],[1,3],[2,4]]
3
[[1,2],[1,3],[2,3]]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - Problem analysis: This problem is essentially asking if we can divide the people into two groups such that no two people who dislike each other are in the same group. This sounds like a graph coloring problem with two colors (groups).
   - Key observations: We can represent the dislikes as an undirected graph where each person is a node, and an edge connects two people who dislike each other. If the graph is bipartite (can be colored with two colors), then we can split the people into two groups.
   - Possible approaches: We can use either Depth-First Search (DFS) or Breadth-First Search (BFS) to color the graph and check for bipartiteness. DFS seems slightly easier to implement in this case.

2. Solution Implementation:
```python
def possibleBipartition(n, dislikes):
    """
    Checks if it's possible to bipartition n people given their dislikes.

    Args:
        n: The number of people.
        dislikes: A list of dislike pairs.

    Returns:
        True if bipartition is possible, False otherwise.
    """
    adj = [[] for _ in range(n + 1)]  # Adjacency list to represent the graph
    for u, v in dislikes:
        adj[u].append(v)
        adj[v].append(u)

    colors = [0] * (n + 1)  # 0: uncolored, 1: color 1, -1: color 2

    def dfs(node, color):
        colors[node] = color
        for neighbor in adj[node]:
            if colors[neighbor] == color:
                return False  # Conflict found, not bipartite
            if colors[neighbor] == 0 and not dfs(neighbor, -color):
                return False  # Recursively color neighbors
        return True

    # Iterate through all nodes (people) in case the graph is disconnected
    for i in range(1, n + 1):
        if colors[i] == 0 and not dfs(i, 1):
            return False
    return True

```

3. Solution Explanation:
   - How the solution works: We first build an adjacency list representing the dislike relationships. Then, we use DFS to color the graph with two colors (1 and -1). We start coloring a node with color 1, then its neighbors with -1, and so on. If we encounter a neighbor that has already been colored with the same color, it means a conflict, and the graph is not bipartite. We iterate through all nodes to handle disconnected graphs.
   - Key steps and logic explained: Building the adjacency list allows us to efficiently access the neighbors of a node. DFS is used for traversing and coloring the graph. The use of two colors (1 and -1) simplifies the conflict check.
   - Why this approach is effective: This approach directly translates the problem into a graph coloring problem, which can be efficiently solved using DFS.  Handling disconnected components ensures correctness.


4. Complexity Analysis:
   - Time complexity: O(V + E) - We visit each node and edge at most once. V is the number of nodes (n), and E is the number of edges (dislikes.length).
   - Space complexity: O(V + E) - The adjacency list takes O(V + E) space, and the recursion stack in DFS can reach a depth of V in the worst case (though unlikely in this sparse graph representation).  The `colors` array also contributes O(V).


## Topics
Depth-First Search, Breadth-First Search, Union Find, Graph

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-04-25
