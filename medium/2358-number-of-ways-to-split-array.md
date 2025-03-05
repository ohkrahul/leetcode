# Number of Ways to Split Array

## Problem Link
[LeetCode - Number of Ways to Split Array](https://leetcode.com/problems/number-of-ways-to-split-array/)

## Difficulty
Medium

## Problem Description
<p>You are given a <strong>0-indexed</strong> integer array <code>nums</code> of length <code>n</code>.</p>

<p><code>nums</code> contains a <strong>valid split</strong> at index <code>i</code> if the following are true:</p>

<ul>
	<li>The sum of the first <code>i + 1</code> elements is <strong>greater than or equal to</strong> the sum of the last <code>n - i - 1</code> elements.</li>
	<li>There is <strong>at least one</strong> element to the right of <code>i</code>. That is, <code>0 &lt;= i &lt; n - 1</code>.</li>
</ul>

<p>Return <em>the number of <strong>valid splits</strong> in</em> <code>nums</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [10,4,-8,7]
<strong>Output:</strong> 2
<strong>Explanation:</strong> 
There are three ways of splitting nums into two non-empty parts:
- Split nums at index 0. Then, the first part is [10], and its sum is 10. The second part is [4,-8,7], and its sum is 3. Since 10 &gt;= 3, i = 0 is a valid split.
- Split nums at index 1. Then, the first part is [10,4], and its sum is 14. The second part is [-8,7], and its sum is -1. Since 14 &gt;= -1, i = 1 is a valid split.
- Split nums at index 2. Then, the first part is [10,4,-8], and its sum is 6. The second part is [7], and its sum is 7. Since 6 &lt; 7, i = 2 is not a valid split.
Thus, the number of valid splits in nums is 2.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [2,3,1,0]
<strong>Output:</strong> 2
<strong>Explanation:</strong> 
There are two valid splits in nums:
- Split nums at index 1. Then, the first part is [2,3], and its sum is 5. The second part is [1,0], and its sum is 1. Since 5 &gt;= 1, i = 1 is a valid split. 
- Split nums at index 2. Then, the first part is [2,3,1], and its sum is 6. The second part is [0], and its sum is 0. Since 6 &gt;= 0, i = 2 is a valid split.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>-10<sup>5</sup> &lt;= nums[i] &lt;= 10<sup>5</sup></code></li>
</ul>


## Test Cases
```
[10,4,-8,7]
[2,3,1,0]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - Problem analysis: We're given an array and we need to find the number of "valid splits". A valid split is defined by the sum of the left side being greater than or equal to the sum of the right side, and there must be at least one element on the right side.
   - Key observations: We don't need to recalculate the entire left and right sums for every split point.  If we know the total sum and the current left sum, we can calculate the right sum by subtraction.  This hints at a prefix sum approach.
   - Possible approaches:  Iterate through the array, maintaining a prefix sum.  At each index, calculate the right sum and check the condition.  Count the valid splits.

2. Solution Implementation:
```python
def waysToSplitArray(nums: list[int]) -> int:
    """
    Counts the number of valid splits in the given array.
    A split is valid if the sum of the left part is greater than or equal to the sum of the right part.
    """

    n = len(nums)
    total_sum = sum(nums)
    left_sum = 0
    count = 0

    # Iterate through possible split points (0 to n-2 inclusive)
    for i in range(n - 1):  # Stop at n-2 because we need at least one element on the right
        left_sum += nums[i]
        right_sum = total_sum - left_sum

        if left_sum >= right_sum:
            count += 1

    return count
```

3. Solution Explanation:
   - How the solution works: The code first calculates the total sum of the array. Then, it iterates through the possible split points from index 0 up to n-2 (exclusive).  In each iteration, it adds the current element to the `left_sum`.  The `right_sum` is calculated by subtracting the `left_sum` from the `total_sum`.  If the `left_sum` is greater than or equal to the `right_sum`, the split is valid, and the `count` is incremented.
   - Key steps and logic explained: The core logic is the efficient calculation of the right sum using `total_sum - left_sum`, avoiding redundant calculations.  The loop condition ensures we always have at least one element on the right side.
   - Why this approach is effective:  Using the prefix sum approach allows us to achieve a linear time complexity because we avoid recalculating sums repeatedly.

4. Complexity Analysis:
   - Time complexity: O(n) - We iterate through the array once.  Calculating the total sum is also an O(n) operation, but it's done only once.
   - Space complexity: O(1) - We use a few variables to store sums and the count, which take constant space regardless of the input array size.  We do not create any new arrays or data structures that scale with the input size.


## Topics
Array, Prefix Sum

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-05
