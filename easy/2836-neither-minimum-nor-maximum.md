# Neither Minimum nor Maximum

## Problem Link
[LeetCode - Neither Minimum nor Maximum](https://leetcode.com/problems/neither-minimum-nor-maximum/)

## Difficulty
Easy

## Problem Description
<p>Given an integer array <code>nums</code> containing <strong>distinct</strong> <strong>positive</strong> integers, find and return <strong>any</strong> number from the array that is neither the <strong>minimum</strong> nor the <strong>maximum</strong> value in the array, or <strong><code>-1</code></strong> if there is no such number.</p>

<p>Return <em>the selected integer.</em></p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [3,2,1,4]
<strong>Output:</strong> 2
<strong>Explanation:</strong> In this example, the minimum value is 1 and the maximum value is 4. Therefore, either 2 or 3 can be valid answers.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,2]
<strong>Output:</strong> -1
<strong>Explanation:</strong> Since there is no number in nums that is neither the maximum nor the minimum, we cannot select a number that satisfies the given condition. Therefore, there is no answer.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums = [2,1,3]
<strong>Output:</strong> 2
<strong>Explanation:</strong> Since 2 is neither the maximum nor the minimum value in nums, it is the only valid answer. 
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 100</code></li>
	<li><code>1 &lt;= nums[i] &lt;= 100</code></li>
	<li>All values in <code>nums</code> are distinct</li>
</ul>


## Test Cases
```
[3,2,1,4]
[1,2]
[2,1,3]
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts

- The problem asks us to find a number in an array that is neither the minimum nor maximum value in the array.
- We can first find the minimum and maximum values in the array.
- Then we can iterate through the array and check if each number is equal to either the minimum or maximum value.
- If a number is not equal to either the minimum or maximum value, we return it.
- If we iterate through the entire array without finding a number that is not equal to the minimum or maximum value, we return -1.

## 2. Solution Implementation
```python
def neither_minimum_nor_maximum(nums):
  """
  Finds a number in an array that is neither the minimum nor maximum value in the array.

  Args:
    nums: A list of distinct positive integers.

  Returns:
    The number that is neither the minimum nor maximum value in the array, or -1 if there is no such number.
  """

  # Find the minimum and maximum values in the array.
  min_value = min(nums)
  max_value = max(nums)

  # Iterate through the array and check if each number is equal to either the minimum or maximum value.
  for num in nums:
    if num != min_value and num != max_value:
      return num

  # If we iterate through the entire array without finding a number that is not equal to the minimum or maximum value, we return -1.
  return -1
```

## 3. Solution Explanation

The solution works by first finding the minimum and maximum values in the array.
Then it iterates through the array and checks if each number is equal to either the minimum or maximum value.
If a number is not equal to either the minimum or maximum value, it is returned.
If the iteration completes without finding a number that is not equal to the minimum or maximum value, -1 is returned.

## 4. Complexity Analysis

- Time complexity: O(n) - The solution iterates through the array once to find the minimum and maximum values, and then iterates through the array again to check if each number is equal to either the minimum or maximum value.
- Space complexity: O(1) - The solution does not use any additional space beyond the space used by the input array.

## Topics
Array, Sorting

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-12-11
