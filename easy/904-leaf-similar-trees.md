# Leaf-Similar Trees

## Problem Link
[LeetCode - Leaf-Similar Trees](https://leetcode.com/problems/leaf-similar-trees/)

## Difficulty
Easy

## Problem Description
<p>Consider all the leaves of a binary tree, from&nbsp;left to right order, the values of those&nbsp;leaves form a <strong>leaf value sequence</strong><em>.</em></p>

<p><img alt="" src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/16/tree.png" style="width: 400px; height: 336px;" /></p>

<p>For example, in the given tree above, the leaf value sequence is <code>(6, 7, 4, 9, 8)</code>.</p>

<p>Two binary trees are considered <em>leaf-similar</em>&nbsp;if their leaf value sequence is the same.</p>

<p>Return <code>true</code> if and only if the two given trees with head nodes <code>root1</code> and <code>root2</code> are leaf-similar.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/09/03/leaf-similar-1.jpg" style="width: 600px; height: 237px;" />
<pre>
<strong>Input:</strong> root1 = [3,5,1,6,2,9,8,null,null,7,4], root2 = [3,5,1,6,7,4,2,null,null,null,null,null,null,9,8]
<strong>Output:</strong> true
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/09/03/leaf-similar-2.jpg" style="width: 300px; height: 110px;" />
<pre>
<strong>Input:</strong> root1 = [1,2,3], root2 = [1,3,2]
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in each tree will be in the range <code>[1, 200]</code>.</li>
	<li>Both of the given trees will have values in the range <code>[0, 200]</code>.</li>
</ul>


## Test Cases
```
[3,5,1,6,2,9,8,null,null,7,4]
[3,5,1,6,7,4,2,null,null,null,null,null,null,9,8]
[1,2,3]
[1,3,2]
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts:
### Problem analysis
- The problem is to determine if two binary trees are leaf-similar.
- Leaf-similar means that the values of the leaves of the two trees, from left to right, are the same.

### Key Observations:

- The leaf values can be obtained by performing a depth-first search on each tree.
- The leaf values can be stored in a list or an array.
- The two lists of leaf values can then be compared to determine if the trees are leaf-similar.

### Possible Approaches:

- One possible approach is to perform a depth-first search on each tree and store the leaf values in two separate lists. The lists can then be compared to determine if the trees are leaf-similar.
- Another possible approach is to perform a depth-first search on both trees at the same time. When a leaf is encountered on one tree, the leaf value is compared to the leaf value on the other tree. If the leaf values are not the same, the trees are not leaf-similar. If all the leaf values are the same, the trees are leaf-similar.

## 2. Solution Implementation
```python
def leafSimilar(root1, root2):
  """
  :type root1: TreeNode
  :type root2: TreeNode
  :rtype: bool
  """
  # Initialize two empty lists to store the leaf values.
  leaves1 = []
  leaves2 = []

  # Perform a depth-first search on the first tree and store the leaf values in the first list.
  def dfs1(node):
    if not node:
      return
    
    if not node.left and not node.right:
      leaves1.append(node.val)
    else:
      dfs1(node.left)
      dfs1(node.right)
  
  # Perform a depth-first search on the second tree and store the leaf values in the second list.
  def dfs2(node):
    if not node:
      return
    
    if not node.left and not node.right:
      leaves2.append(node.val)
    else:
      dfs2(node.left)
      dfs2(node.right)

  # Perform the depth-first searches.
  dfs1(root1)
  dfs2(root2)
  
  # Check if the two lists are equal.
  return leaves1 == leaves2
```

## 3. Solution Explanation:

The solution performs a depth-first search on each tree and stores the leaf values in two separate lists. The lists are then compared to determine if the trees are leaf-similar.

The `dfs1` function performs a depth-first search on the first tree and stores the leaf values in the `leaves1` list. The `dfs2` function performs a depth-first search on the second tree and stores the leaf values in the `leaves2` list.

After the depth-first searches have been performed, the `leaves1` and `leaves2` lists are compared to determine if the trees are leaf-similar. If the lists are equal, the trees are leaf-similar. Otherwise, the trees are not leaf-similar.

## 4. Complexity Analysis:
### Time complexity: O(N)

The solution performs a depth-first search on both trees. The time complexity of a depth-first search is O(N), where N is the number of nodes in the tree. Therefore, the time complexity of the solution is O(N).

### Space complexity: O(N)

The solution stores the leaf values in two lists. The space complexity of storing a list is O(N), where N is the number of elements in the list. Therefore, the space complexity of the solution is O(N).

## Topics
Tree, Depth-First Search, Binary Tree

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-10
