# Longest Univalue Path

## Problem Link
[LeetCode - Longest Univalue Path](https://leetcode.com/problems/longest-univalue-path/)

## Difficulty
Medium

## Problem Description
<p>Given the <code>root</code> of a binary tree, return <em>the length of the longest path, where each node in the path has the same value</em>. This path may or may not pass through the root.</p>

<p><strong>The length of the path</strong> between two nodes is represented by the number of edges between them.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/13/ex1.jpg" style="width: 450px; height: 238px;" />
<pre>
<strong>Input:</strong> root = [5,4,5,1,1,null,5]
<strong>Output:</strong> 2
<strong>Explanation:</strong> The shown image shows that the longest path of the same value (i.e. 5).
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/13/ex2.jpg" style="width: 450px; height: 238px;" />
<pre>
<strong>Input:</strong> root = [1,4,5,4,4,null,5]
<strong>Output:</strong> 2
<strong>Explanation:</strong> The shown image shows that the longest path of the same value (i.e. 4).
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[0, 10<sup>4</sup>]</code>.</li>
	<li><code>-1000 &lt;= Node.val &lt;= 1000</code></li>
	<li>The depth of the tree will not exceed <code>1000</code>.</li>
</ul>


## Test Cases
```
[5,4,5,1,1,null,5]
[1,4,5,4,4,null,5]
```

## Initial Template
```python
# Code template not available
```

## Solution
### Initial Thoughts

**Problem analysis:**

The problem asks us to find the length of the longest path in a binary tree where all the nodes in the path have the same value. The path can start from any node and end at any node.

**Key observations:**

- The length of the path is the number of edges between two nodes.
- The longest path may or may not pass through the root.

**Possible approaches:**

One possible approach is to use a recursive function to traverse the tree and find the longest path in each subtree. 

Another possible approach is to use a post-order traversal to calculate the longest path from each node to its leaf nodes.

### Solution Implementation

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def longestUnivaluePath(self, root: TreeNode) -> int:
        self.max_length = 0

        def dfs(node):
            if not node:
                return 0

            left_length = dfs(node.left)
            right_length = dfs(node.right)

            # If the left and right subtrees have the same value as the current node
            if node.left and node.left.val == node.val:
                left_length += 1
            else:
                left_length = 0

            # If the left and right subtrees have the same value as the current node
            if node.right and node.right.val == node.val:
                right_length += 1
            else:
                right_length = 0

            # Update the maximum length
            self.max_length = max(self.max_length, left_length + right_length)

            # Return the longest path from the current node to its leaf nodes
            return max(left_length, right_length)

        dfs(root)
        return self.max_length
```

### Solution Explanation

The solution uses a post-order traversal to calculate the longest path from each node to its leaf nodes. The function `dfs` takes a node as input and returns the length of the longest path from that node to its leaf nodes.

The function first checks if the node is None. If it is, then the longest path from that node to its leaf nodes is 0.

Next, the function checks if the left and right subtrees have the same value as the current node. If they do, then the longest path from the current node to its leaf nodes is the maximum of the longest path from the left subtree to its leaf nodes and the longest path from the right subtree to its leaf nodes, plus 1.

If the left and right subtrees do not have the same value as the current node, then the longest path from the current node to its leaf nodes is 0.

Finally, the function updates the maximum length and returns the longest path from the current node to its leaf nodes.

The overall time complexity of the solution is O(N), where N is the number of nodes in the tree. The space complexity is O(H), where H is the height of the tree.

### Complexity Analysis

- **Time complexity:** O(N), where N is the number of nodes in the tree. The solution performs a post-order traversal of the tree, which takes O(N) time.
- **Space complexity:** O(H), where H is the height of the tree. The solution uses a recursive function, which requires O(H) space for the call stack.

## Topics
Tree, Depth-First Search, Binary Tree

Solved on: 2024-11-09
