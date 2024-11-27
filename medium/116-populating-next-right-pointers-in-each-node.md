# Populating Next Right Pointers in Each Node

## Problem Link
[LeetCode - Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/)

## Difficulty
Medium

## Problem Description
<p>You are given a <strong>perfect binary tree</strong> where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:</p>

<pre>
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
</pre>

<p>Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to <code>NULL</code>.</p>

<p>Initially, all next pointers are set to <code>NULL</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2019/02/14/116_sample.png" style="width: 500px; height: 171px;" />
<pre>
<strong>Input:</strong> root = [1,2,3,4,5,6,7]
<strong>Output:</strong> [1,#,2,3,#,4,5,6,7,#]
<strong>Explanation: </strong>Given the above perfect binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with &#39;#&#39; signifying the end of each level.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> root = []
<strong>Output:</strong> []
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[0, 2<sup>12</sup> - 1]</code>.</li>
	<li><code>-1000 &lt;= Node.val &lt;= 1000</code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow-up:</strong></p>

<ul>
	<li>You may only use constant extra space.</li>
	<li>The recursive approach is fine. You may assume implicit stack space does not count as extra space for this problem.</li>
</ul>


## Test Cases
```
[1,2,3,4,5,6,7]
[]
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts:

**Problem analysis:**
The problem presents a perfect binary tree where each node has two children. Our task is to populate the `next` pointers of the nodes such that each node points to its adjacent right node. If there is no adjacent right node, the `next` pointer should be set to `NULL`.

**Key observations:**
- We have to traverse the binary tree in a level-order fashion to populate the `next` pointers.
- We can use a queue to keep track of the nodes at each level.

**Possible approaches:**
- **Breadth-First Search (BFS):** We can use BFS to traverse the tree level by level and populate the `next` pointers as we visit each node.
- **Recursion:** We can use a recursive approach to traverse the tree. As we visit each node, we populate the `next` pointers for its children.

## 2. Solution Implementation:
```python
def connect(root):
    """
    :type root: Node
    :rtype: Node
    """
    if not root:
        return root

    level_start = root
    while level_start:
        current = level_start
        while current:
            if current.left:
                current.left.next = current.right
            if current.right and current.next:
                current.right.next = current.next.left
            current = current.next
        level_start = level_start.left

    return root
```

## 3. Solution Explanation:
We use a BFS approach to traverse the tree level by level. We maintain a `level_start` pointer that points to the first node in each level. We then iterate through each node in the current level using the `current` pointer.

For each node in the current level:
1. If the node has a left child, we set the `next` pointer of the left child to point to the right child of the current node.
2. If the node has a right child and the current node has a `next` pointer, we set the `next` pointer of the right child to point to the left child of the node pointed to by the `next` pointer.

After updating the `next` pointers for all nodes in the current level, we move the `level_start` pointer to the left child of the first node in the current level. This effectively moves us to the next level in the tree.

We continue this process until we reach the last level of the tree.

## 4. Complexity Analysis:
**Time complexity:** O(N), where N is the number of nodes in the tree. We visit each node in the tree once.

**Space complexity:** O(1), as we do not use any additional data structures besides the tree itself.

## Topics
Linked List, Tree, Depth-First Search, Breadth-First Search, Binary Tree

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-11-27
