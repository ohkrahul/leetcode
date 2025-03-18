# Find Target Indices After Sorting Array

## Problem Link
[LeetCode - Find Target Indices After Sorting Array](https://leetcode.com/problems/find-target-indices-after-sorting-array/)

## Difficulty
Easy

## Problem Description
<p>You are given a <strong>0-indexed</strong> integer array <code>nums</code> and a target element <code>target</code>.</p>

<p>A <strong>target index</strong> is an index <code>i</code> such that <code>nums[i] == target</code>.</p>

<p>Return <em>a list of the target indices of</em> <code>nums</code> after<em> sorting </em><code>nums</code><em> in <strong>non-decreasing</strong> order</em>. If there are no target indices, return <em>an <strong>empty</strong> list</em>. The returned list must be sorted in <strong>increasing</strong> order.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,2,5,2,3], target = 2
<strong>Output:</strong> [1,2]
<strong>Explanation:</strong> After sorting, nums is [1,<u><strong>2</strong></u>,<u><strong>2</strong></u>,3,5].
The indices where nums[i] == 2 are 1 and 2.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,2,5,2,3], target = 3
<strong>Output:</strong> [3]
<strong>Explanation:</strong> After sorting, nums is [1,2,2,<u><strong>3</strong></u>,5].
The index where nums[i] == 3 is 3.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,2,5,2,3], target = 5
<strong>Output:</strong> [4]
<strong>Explanation:</strong> After sorting, nums is [1,2,2,3,<u><strong>5</strong></u>].
The index where nums[i] == 5 is 4.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 100</code></li>
	<li><code>1 &lt;= nums[i], target &lt;= 100</code></li>
</ul>


## Test Cases
```
[1,2,5,2,3]
2
[1,2,5,2,3]
3
[1,2,5,2,3]
5
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks for the indices of a target value after sorting the array.
   - Sorting the array is a key step.  We can use Python's built-in `sort()` which has a time complexity of O(n log n).
   - After sorting, we can iterate through the sorted array and check for elements equal to the target.
   - We need to store and return the indices where the target is found, maintaining the order.

2. Solution Implementation:
```python
def targetIndices(nums, target):
    """
    Finds and returns the indices of the target value in a sorted array.

    Args:
        nums: The input integer array.
        target: The target value to search for.

    Returns:
        A list of indices where the target value is found in the sorted array.
    """
    nums.sort()  # Sort the array in-place (non-decreasing order)
    target_indices = []  # Initialize an empty list to store the target indices
    for i, num in enumerate(nums):  # Iterate through the sorted array with indices
        if num == target:  # Check if the current element is equal to the target
            target_indices.append(i)  # If it is, append the index to the result list
    return target_indices  # Return the list of target indices
```

3. Solution Explanation:
   - The `targetIndices` function takes two arguments: the integer array `nums` and the target value `target`.
   - First, the `nums` array is sorted in non-decreasing order using `nums.sort()`.  This is important to ensure the indices we return are correct after sorting.
   - An empty list `target_indices` is initialized to store the indices where the target is found.
   - The code then iterates through the sorted array using `enumerate`, which provides both the index (`i`) and the value (`num`) of each element.
   - Inside the loop, it checks if the current element `num` is equal to the `target`.
   - If a match is found, the current index `i` is appended to the `target_indices` list.
   - Finally, the function returns the `target_indices` list, which contains the indices of the target value in the sorted array.

4. Complexity Analysis:
   - Time complexity: O(n log n) - Dominated by the sorting step (`nums.sort()`).  The iteration through the sorted array adds a linear O(n) component, but O(n log n) is the overall complexity.
   - Space complexity: O(1) or O(n) - If `nums.sort()` is implemented as in-place sorting (which is usually the case in Python), the space complexity is O(1). However, If the sorting algorithm uses extra space (not typical in Python’s built-in sort but possible in general), it could become O(n) in the worst case due to the sorted array. Also, in the worst-case scenario where all elements are equal to the target, the `target_indices` list could grow to size n, making it O(n) space.  In the average case, it will be less than n.  Technically, without specifying how the sort is implemented internally, we have to consider the worst-case space of sorting itself, which could be O(n).


## Topics
Array, Binary Search, Sorting

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-18
