# Two Sum

## Problem Link
[LeetCode - Two Sum](https://leetcode.com/problems/two-sum/)

## Difficulty
Easy

## Problem Description
<p>Given an array of integers <code>nums</code>&nbsp;and an integer <code>target</code>, return <em>indices of the two numbers such that they add up to <code>target</code></em>.</p>

<p>You may assume that each input would have <strong><em>exactly</em> one solution</strong>, and you may not use the <em>same</em> element twice.</p>

<p>You can return the answer in any order.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [2,7,11,15], target = 9
<strong>Output:</strong> [0,1]
<strong>Explanation:</strong> Because nums[0] + nums[1] == 9, we return [0, 1].
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [3,2,4], target = 6
<strong>Output:</strong> [1,2]
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums = [3,3], target = 6
<strong>Output:</strong> [0,1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 &lt;= nums.length &lt;= 10<sup>4</sup></code></li>
	<li><code>-10<sup>9</sup> &lt;= nums[i] &lt;= 10<sup>9</sup></code></li>
	<li><code>-10<sup>9</sup> &lt;= target &lt;= 10<sup>9</sup></code></li>
	<li><strong>Only one valid answer exists.</strong></li>
</ul>

<p>&nbsp;</p>
<strong>Follow-up:&nbsp;</strong>Can you come up with an algorithm that is less than <code>O(n<sup>2</sup>)</code><font face="monospace">&nbsp;</font>time complexity?

## Test Cases
```
[2,7,11,15]
9
[3,2,4]
6
[3,3]
6
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts:
- This is a classic problem that can be solved using a brute-force approach or a more efficient approach.
- A brute-force approach would be to check all possible pairs of elements in the array to see if they add up to the target.
- However, this approach would have a time complexity of O(n^2), which is not ideal for large arrays.
- Instead, we can use a more efficient approach that has a time complexity of O(n) using a hash table.

## 2. Solution Implementation:
```python
def two_sum(nums, target):
  """
  Finds the indices of the two numbers in the array that add up to the target.

  Parameters:
    nums: The array of integers to search.
    target: The target sum.

  Returns:
    The indices of the two numbers that add up to the target.
  """

  # Create a hash table to store the indices of the numbers in the array.
  num_to_index = {}
  for i, num in enumerate(nums):
    num_to_index[num] = i

  # Iterate over the array and check if the target - the current number is in the hash table.
  for i, num in enumerate(nums):
    complement = target - num
    if complement in num_to_index and num_to_index[complement] != i:
      return [i, num_to_index[complement]]

  # If no solution is found, return an empty list.
  return []
```

## 3. Solution Explanation:
- The solution works by first creating a hash table that stores the indices of the numbers in the array.
- Then, it iterates over the array and checks if the target - the current number is in the hash table.
- If it is, and the index of the complement is not the same as the current index, then the solution has been found and the indices of the two numbers are returned.
- If no solution is found, an empty list is returned.

## 4. Complexity Analysis:
- **Time complexity:** O(n)
- **Space complexity:** O(n)

## Topics
Array, Hash Table

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-12-31
