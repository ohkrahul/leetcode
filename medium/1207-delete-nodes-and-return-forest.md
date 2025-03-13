# Delete Nodes And Return Forest

## Problem Link
[LeetCode - Delete Nodes And Return Forest](https://leetcode.com/problems/delete-nodes-and-return-forest/)

## Difficulty
Medium

## Problem Description
<p>Given the <code>root</code> of a binary tree, each node in the tree has a distinct value.</p>

<p>After deleting all nodes with a value in <code>to_delete</code>, we are left with a forest (a disjoint union of trees).</p>

<p>Return the roots of the trees in the remaining forest. You may return the result in any order.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2019/07/01/screen-shot-2019-07-01-at-53836-pm.png" style="width: 237px; height: 150px;" />
<pre>
<strong>Input:</strong> root = [1,2,3,4,5,6,7], to_delete = [3,5]
<strong>Output:</strong> [[1,2,null,4],[6],[7]]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> root = [1,2,4,null,3], to_delete = [3]
<strong>Output:</strong> [[1,2,4]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the given tree is at most <code>1000</code>.</li>
	<li>Each node has a distinct value between <code>1</code> and <code>1000</code>.</li>
	<li><code>to_delete.length &lt;= 1000</code></li>
	<li><code>to_delete</code> contains distinct values between <code>1</code> and <code>1000</code>.</li>
</ul>


## Test Cases
```
[1,2,3,4,5,6,7]
[3,5]
[1,2,4,null,3]
[3]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - Problem analysis:  We're given a binary tree and a list of nodes to delete. We need to return a list of the roots of the remaining trees after deletion. The tricky part is handling the disconnection and reconnection properly when a node is deleted.
   - Key observations: If a node is deleted, its children might become roots of new trees. If the root itself is deleted, its children become roots. We need a way to track these new roots.
   - Possible approaches: A recursive approach seems most natural for tree problems. We can traverse the tree, and for each node, check if it should be deleted.  If so, we add its non-null children to our result list and return `None` to disconnect it from its parent. If not deleted, we recursively process its children and return the current node.

2. Solution Implementation:
```python
from typing import List, Optional

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def delNodes(root: Optional[TreeNode], to_delete: List[int]) -> List[TreeNode]:
    """
    Deletes nodes from a binary tree and returns the roots of the remaining forest.
    """
    to_delete_set = set(to_delete) # Convert to set for efficient lookup
    result = []

    def delete_nodes_recursive(node: Optional[TreeNode]) -> Optional[TreeNode]:
        """
        Recursively deletes nodes and updates the result list.
        Returns the node if it's not deleted, otherwise returns None.
        """
        if not node:
            return None
        
        # Check if the current node should be deleted
        if node.val in to_delete_set:
            # If deleted, its children potentially become roots
            if node.left:
                result.append(node.left)
            if node.right:
                result.append(node.right)
            # Return None to disconnect from the parent
            return None
        else:
            # If not deleted, recursively process children
            node.left = delete_nodes_recursive(node.left)  # Reconnect left child
            node.right = delete_nodes_recursive(node.right) # Reconnect right child
            return node

    # Handle the case where the root itself needs to be deleted
    if delete_nodes_recursive(root):
        result.append(root)  # Original root wasn't deleted, so it's part of the forest

    return result

```

3. Solution Explanation:
   - How the solution works: The `delNodes` function uses a helper function `delete_nodes_recursive` to traverse the tree. The `to_delete` list is converted to a set for faster checking.  The recursive function checks if the current node needs to be deleted.  If so, its children are potentially added to the `result` list, and `None` is returned to disconnect the deleted node.  If the node is not deleted, we recursively process its left and right children and reconnect them to the current node before returning the node itself.
   - Key steps and logic explained: The key is the `delete_nodes_recursive` function. It modifies the tree in place by setting `node.left` and `node.right` to the results of the recursive calls.  This handles the disconnection and reconnection of nodes effectively. The initial call to `delete_nodes_recursive(root)`  modifies the tree according to the `to_delete` set.
   - Why this approach is effective: Recursion is well-suited for tree traversal.  The in-place modification of the tree structure simplifies the logic, and the use of a set for `to_delete` makes the deletion check efficient.

4. Complexity Analysis:
   - Time complexity: O(N) - We visit each node in the tree exactly once.
   - Space complexity: O(N) - In the worst case, where the tree is skewed and all nodes except the leaf nodes are deleted, the recursion depth can be O(N), leading to O(N) space on the call stack.  The `to_delete_set` also takes O(D) space where D is the length of `to_delete`, but D <= N. The result list can also store up to N nodes in the worst-case (a tree where all nodes are in `to_delete`). So overall, space complexity is dominated by the potential recursion depth.


## Topics
Array, Hash Table, Tree, Depth-First Search, Binary Tree

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-13
