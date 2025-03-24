# Most Stones Removed with Same Row or Column

## Problem Link
[LeetCode - Most Stones Removed with Same Row or Column](https://leetcode.com/problems/most-stones-removed-with-same-row-or-column/)

## Difficulty
Medium

## Problem Description
<p>On a 2D plane, we place <code>n</code> stones at some integer coordinate points. Each coordinate point may have at most one stone.</p>

<p>A stone can be removed if it shares either <strong>the same row or the same column</strong> as another stone that has not been removed.</p>

<p>Given an array <code>stones</code> of length <code>n</code> where <code>stones[i] = [x<sub>i</sub>, y<sub>i</sub>]</code> represents the location of the <code>i<sup>th</sup></code> stone, return <em>the largest possible number of stones that can be removed</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> stones = [[0,0],[0,1],[1,0],[1,2],[2,1],[2,2]]
<strong>Output:</strong> 5
<strong>Explanation:</strong> One way to remove 5 stones is as follows:
1. Remove stone [2,2] because it shares the same row as [2,1].
2. Remove stone [2,1] because it shares the same column as [0,1].
3. Remove stone [1,2] because it shares the same row as [1,0].
4. Remove stone [1,0] because it shares the same column as [0,0].
5. Remove stone [0,1] because it shares the same row as [0,0].
Stone [0,0] cannot be removed since it does not share a row/column with another stone still on the plane.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> stones = [[0,0],[0,2],[1,1],[2,0],[2,2]]
<strong>Output:</strong> 3
<strong>Explanation:</strong> One way to make 3 moves is as follows:
1. Remove stone [2,2] because it shares the same row as [2,0].
2. Remove stone [2,0] because it shares the same column as [0,0].
3. Remove stone [0,2] because it shares the same row as [0,0].
Stones [0,0] and [1,1] cannot be removed since they do not share a row/column with another stone still on the plane.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> stones = [[0,0]]
<strong>Output:</strong> 0
<strong>Explanation:</strong> [0,0] is the only stone on the plane, so you cannot remove it.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= stones.length &lt;= 1000</code></li>
	<li><code>0 &lt;= x<sub>i</sub>, y<sub>i</sub> &lt;= 10<sup>4</sup></code></li>
	<li>No two stones are at the same coordinate point.</li>
</ul>


## Test Cases
```
[[0,0],[0,1],[1,0],[1,2],[2,1],[2,2]]
[[0,0],[0,2],[1,1],[2,0],[2,2]]
[[0,0]]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks for the maximum number of stones that can be removed.  A stone can be removed if it shares a row or column with another stone. This sounds like a graph problem where stones connected by row or column are in the same component.
   - Key observation: The order of removal doesn't seem to matter. As long as stones are connected in some way (directly or indirectly), they can be removed except one representative stone per connected component.
   - Possible approaches:  Union-Find algorithm seems like a good fit to track connected components. We can connect stones sharing the same row or same column.

2. Solution Implementation:
```python
def removeStones(stones):
    n = len(stones)
    parent = list(range(n)) # Initialize parent array for Union-Find

    def find(i): # Find the root/representative of the set containing i
        if parent[i] == i:
            return i
        parent[i] = find(parent[i]) # Path compression for optimization
        return parent[i]

    def union(i, j): # Union two sets represented by i and j
        root_i = find(i)
        root_j = find(j)
        if root_i != root_j:
            parent[root_i] = root_j  # Attach one root to the other

    # Create connections (Union) based on shared row or column
    for i in range(n):
        for j in range(i + 1, n):
            if stones[i][0] == stones[j][0] or stones[i][1] == stones[j][1]:
                union(i, j)

    # Count the number of distinct connected components
    components = set()
    for i in range(n):
        components.add(find(i))

    # The number of removable stones is total stones - number of components
    return n - len(components)


```

3. Solution Explanation:
   - We use the Union-Find algorithm to group stones that are connected (share row/column).  `find(i)` finds the representative element of the set containing stone `i`. `union(i, j)` connects the sets of `i` and `j`. Path compression in `find` optimizes the time complexity.
   - We iterate through all stone pairs, and if they share a row or column, we perform `union` on their indices.
   - Finally, we count the number of unique representative elements (roots) using a set.  This gives us the number of connected components.
   - The maximum removable stones is the total number of stones minus the number of connected components (because one stone per component needs to remain).

4. Complexity Analysis:
   - Time complexity: O(n^2 * α(n)), where n is the number of stones and α(n) is the inverse Ackermann function, which is practically constant. The n^2 comes from iterating through all pairs of stones.
   - Space complexity: O(n) for the `parent` array used in Union-Find.




## Topics
Hash Table, Depth-First Search, Union Find, Graph

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-24
