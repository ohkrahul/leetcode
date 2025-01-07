# Longest Mountain in Array

## Problem Link
[LeetCode - Longest Mountain in Array](https://leetcode.com/problems/longest-mountain-in-array/)

## Difficulty
Medium

## Problem Description
<p>You may recall that an array <code>arr</code> is a <strong>mountain array</strong> if and only if:</p>

<ul>
	<li><code>arr.length &gt;= 3</code></li>
	<li>There exists some index <code>i</code> (<strong>0-indexed</strong>) with <code>0 &lt; i &lt; arr.length - 1</code> such that:
	<ul>
		<li><code>arr[0] &lt; arr[1] &lt; ... &lt; arr[i - 1] &lt; arr[i]</code></li>
		<li><code>arr[i] &gt; arr[i + 1] &gt; ... &gt; arr[arr.length - 1]</code></li>
	</ul>
	</li>
</ul>

<p>Given an integer array <code>arr</code>, return <em>the length of the longest subarray, which is a mountain</em>. Return <code>0</code> if there is no mountain subarray.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> arr = [2,1,4,7,3,2,5]
<strong>Output:</strong> 5
<strong>Explanation:</strong> The largest mountain is [1,4,7,3,2] which has length 5.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> arr = [2,2,2]
<strong>Output:</strong> 0
<strong>Explanation:</strong> There is no mountain.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= arr.length &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= arr[i] &lt;= 10<sup>4</sup></code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong></p>

<ul>
	<li>Can you solve it using only one pass?</li>
	<li>Can you solve it in <code>O(1)</code> space?</li>
</ul>


## Test Cases
```
[2,1,4,7,3,2,5]
[2,2,2]
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts

### Problem analysis

The problem asks for the length of the longest mountain in an integer array. A mountain is defined as a subarray where the first part is strictly increasing and the second part is strictly decreasing.

### Key observations

* The length of a mountain is always odd.
* The peak of a mountain is always the middle element of the mountain.

### Possible approaches

**Brute force approach**: Check every possible subarray of the array and find the longest mountain.

This approach is not efficient as it takes O(n^3) time, where n is the length of the array.

**Dynamic programming approach**: For each element in the array, find the length of the longest increasing subarray ending at that element and the length of the longest decreasing subarray starting at that element. The longest mountain is then the sum of the two longest subarrays.

This approach takes O(n) time and O(n) space.

## 2. Solution Implementation

```python
def longest_mountain(arr):
    """
    :type arr: List[int]
    :rtype: int
    """
    n = len(arr)
    if n < 3:
        return 0

    # dp[i][0] stores the length of the longest increasing subarray ending at arr[i]
    # dp[i][1] stores the length of the longest decreasing subarray starting at arr[i]
    dp = [[0] * 2 for _ in range(n)]

    for i in range(1, n):
        if arr[i] > arr[i - 1]:
            dp[i][0] = dp[i - 1][0] + 1
    for i in range(n - 2, -1, -1):
        if arr[i] > arr[i + 1]:
            dp[i][1] = dp[i + 1][1] + 1

    max_length = 0
    for i in range(n):
        if dp[i][0] > 0 and dp[i][1] > 0:
            max_length = max(max_length, dp[i][0] + dp[i][1] + 1)

    return max_length
```

## 3. Solution Explanation

The solution uses dynamic programming to solve the problem. It first calculates the length of the longest increasing subarray ending at each element in the array. It then calculates the length of the longest decreasing subarray starting at each element in the array. The longest mountain is then the sum of the two longest subarrays.

The time complexity of the solution is O(n), where n is the length of the array. The space complexity is also O(n).

## 4. Complexity Analysis

### Time complexity

The time complexity of the solution is O(n), where n is the length of the array. This is because the solution iterates over the array twice, once to calculate the length of the longest increasing subarray ending at each element and once to calculate the length of the longest decreasing subarray starting at each element.

### Space complexity

The space complexity of the solution is also O(n), where n is the length of the array. This is because the solution stores the length of the longest increasing subarray ending at each element and the length of the longest decreasing subarray starting at each element in a 2D array.

## Topics
Array, Two Pointers, Dynamic Programming, Enumeration

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-07
