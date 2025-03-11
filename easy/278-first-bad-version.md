# First Bad Version

## Problem Link
[LeetCode - First Bad Version](https://leetcode.com/problems/first-bad-version/)

## Difficulty
Easy

## Problem Description
<p>You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.</p>

<p>Suppose you have <code>n</code> versions <code>[1, 2, ..., n]</code> and you want to find out the first bad one, which causes all the following ones to be bad.</p>

<p>You are given an API <code>bool isBadVersion(version)</code> which returns whether <code>version</code> is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> n = 5, bad = 4
<strong>Output:</strong> 4
<strong>Explanation:</strong>
call isBadVersion(3) -&gt; false
call isBadVersion(5)&nbsp;-&gt; true
call isBadVersion(4)&nbsp;-&gt; true
Then 4 is the first bad version.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> n = 1, bad = 1
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= bad &lt;= n &lt;= 2<sup>31</sup> - 1</code></li>
</ul>


## Test Cases
```
5
4
1
1
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks us to find the first bad version in a sorted array of versions. Since the versions are sorted and we know that all versions after a bad version are also bad, we can use binary search to efficiently locate the first bad one.
   - The key is to minimize calls to the `isBadVersion` API.
   - Binary search seems the most natural approach due to the sorted nature of the problem.

2. Solution Implementation:
```python
# The isBadVersion API is already defined for you.
# def isBadVersion(version: int) -> bool:

class Solution:
    def firstBadVersion(self, n: int) -> int:
        left, right = 1, n  # Initialize search space

        while left < right:
            mid = left + (right - left) // 2  # Calculate midpoint to prevent overflow

            if isBadVersion(mid):  # If mid is a bad version
                right = mid  # Search in the left half (including mid)
            else:
                left = mid + 1  # Search in the right half (excluding mid)

        return left  # Left will eventually hold the first bad version
```

3. Solution Explanation:
   - The code implements binary search to find the first bad version.
   - We initialize `left` to 1 and `right` to `n`.
   - Inside the `while` loop, we calculate the midpoint `mid`.
   - If `isBadVersion(mid)` is true, it means the bad version is at `mid` or to its left, so we update `right` to `mid`.
   - If `isBadVersion(mid)` is false, it means the bad version is to the right of `mid`, so we update `left` to `mid + 1`.
   - The loop continues until `left` and `right` converge, at which point `left` (and also `right`) will hold the first bad version. 
   -  We use  `mid = left + (right - left) // 2` to prevent potential integer overflow if `left + right` exceeds the maximum integer value.


4. Complexity Analysis:
   - Time complexity: O(log n) - Binary search divides the search space in half with each iteration, resulting in logarithmic time complexity.
   - Space complexity: O(1) - We only use a few constant extra variables, resulting in constant space complexity. 


## Topics
Binary Search, Interactive

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-11
