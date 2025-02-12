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
1. **Initial Thoughts:**
   - The key observation is that we can traverse both trees at the same time, and check if the values of the leaves are the same.
   - If the values of the leaves are different, then the trees are not leaf-similar.
   - If the values of the leaves are the same, then we check if the left and right subtrees are leaf-similar.

2. **Solution Implementation:**
```python
def leafSimilar(root1, root2):
    # Check if the trees are empty
    if not root1 and not root2:
        return True
    if not root1 or not root2:
        return False

    # Check if the values of the leaves are the same
    if root1.val != root2.val:
        return False

    # Check if the left and right subtrees are leaf-similar
    return leafSimilar(root1.left, root2.left) and leafSimilar(root1.right, root2.right)
```

3. **Solution Explanation:**
   - The function `leafSimilar` takes two binary trees as input, and returns `True` if the trees are leaf-similar, and `False` otherwise.
   - The function first checks if the trees are empty. If both trees are empty, then they are leaf-similar. If one of the trees is empty and the other is not, then they are not leaf-similar.
   - If the trees are not empty, the function checks if the values of the leaves are the same. If the values of the leaves are different, then the trees are not leaf-similar.
   - If the values of the leaves are the same, then the function checks if the left and right subtrees are leaf-similar. If the left and right subtrees are leaf-similar, then the trees are leaf-similar.

4. **Complexity Analysis:**
   - Time complexity: O(n), where n is the number of nodes in the trees.
   - Space complexity: O(n), where n is the number of nodes in the trees.

## Topics
Tree, Depth-First Search, Binary Tree

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-02-12
