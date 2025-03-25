# Maximum Binary Tree

## Problem Link
[LeetCode - Maximum Binary Tree](https://leetcode.com/problems/maximum-binary-tree/)

## Difficulty
Medium

## Problem Description
<p>You are given an integer array <code>nums</code> with no duplicates. A <strong>maximum binary tree</strong> can be built recursively from <code>nums</code> using the following algorithm:</p>

<ol>
	<li>Create a root node whose value is the maximum value in <code>nums</code>.</li>
	<li>Recursively build the left subtree on the <strong>subarray prefix</strong> to the <strong>left</strong> of the maximum value.</li>
	<li>Recursively build the right subtree on the <strong>subarray suffix</strong> to the <strong>right</strong> of the maximum value.</li>
</ol>

<p>Return <em>the <strong>maximum binary tree</strong> built from </em><code>nums</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/12/24/tree1.jpg" style="width: 302px; height: 421px;" />
<pre>
<strong>Input:</strong> nums = [3,2,1,6,0,5]
<strong>Output:</strong> [6,3,5,null,2,0,null,null,1]
<strong>Explanation:</strong> The recursive calls are as follow:
- The largest value in [3,2,1,6,0,5] is 6. Left prefix is [3,2,1] and right suffix is [0,5].
    - The largest value in [3,2,1] is 3. Left prefix is [] and right suffix is [2,1].
        - Empty array, so no child.
        - The largest value in [2,1] is 2. Left prefix is [] and right suffix is [1].
            - Empty array, so no child.
            - Only one element, so child is a node with value 1.
    - The largest value in [0,5] is 5. Left prefix is [0] and right suffix is [].
        - Only one element, so child is a node with value 0.
        - Empty array, so no child.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/12/24/tree2.jpg" style="width: 182px; height: 301px;" />
<pre>
<strong>Input:</strong> nums = [3,2,1]
<strong>Output:</strong> [3,null,2,null,1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 1000</code></li>
	<li><code>0 &lt;= nums[i] &lt;= 1000</code></li>
	<li>All integers in <code>nums</code> are <strong>unique</strong>.</li>
</ul>


## Test Cases
```
[3,2,1,6,0,5]
[3,2,1]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks us to build a maximum binary tree recursively.  The root is always the maximum element in the current subarray, and we recursively build the left and right subtrees using the elements to the left and right of the maximum, respectively.
   - The base case for the recursion is an empty array, which results in no node (None).
   - A simple approach would be to find the maximum element in the array, create a node with that value, and recursively call the function on the left and right subarrays.

2. Solution Implementation:
```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def constructMaximumBinaryTree(nums: list[int]) -> TreeNode | None:
    """
    Constructs a maximum binary tree from a given integer array.

    Args:
        nums: The input integer array.

    Returns:
        The root of the constructed maximum binary tree.
    """

    if not nums:  # Base case: empty array
        return None

    max_val = max(nums)  # Find the maximum value
    max_index = nums.index(max_val)  # Find its index

    root = TreeNode(max_val)  # Create the root node

    # Recursively build left and right subtrees
    root.left = constructMaximumBinaryTree(nums[:max_index])  
    root.right = constructMaximumBinaryTree(nums[max_index + 1:])

    return root
```

3. Solution Explanation:
   - The `constructMaximumBinaryTree` function takes a list of integers `nums` as input and returns the root of the constructed maximum binary tree.
   - The base case is when `nums` is empty. In this case, we return `None` to signify no node.
   - Otherwise, we find the maximum value (`max_val`) and its index (`max_index`) in the `nums` array.
   - We create a new `TreeNode` with the `max_val` as the root.
   - We recursively call the `constructMaximumBinaryTree` function on the left subarray (`nums[:max_index]`) to build the left subtree and assign it to `root.left`.
   - We recursively call the `constructMaximumBinaryTree` function on the right subarray (`nums[max_index + 1:]`) to build the right subtree and assign it to `root.right`.
   - Finally, we return the `root` node.


4. Complexity Analysis:
   - Time complexity: O(N^2) in the worst case. In the worst-case scenario (e.g., a sorted array), each recursive call processes a subarray of size n, n-1, n-2, ..., 1.  Finding the max element using `max()` within each call takes O(n) in the worst case if the input is sorted or nearly sorted . This leads to a total time complexity close to O(n^2). The average case is closer to O(NlogN) if the tree remains relatively balanced.
   - Space complexity: O(N) in the worst case due to the recursion depth, which can be equal to the number of nodes in a skewed tree (when the input array is sorted).  In the average case, the space complexity is closer to O(logN) due to a more balanced tree structure and therefore a lower recursion depth. The space is used by the recursion stack and for creating the tree nodes.


## Topics
Array, Divide and Conquer, Stack, Tree, Monotonic Stack, Binary Tree

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-25
