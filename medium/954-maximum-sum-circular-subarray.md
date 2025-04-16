# Maximum Sum Circular Subarray

## Problem Link
[LeetCode - Maximum Sum Circular Subarray](https://leetcode.com/problems/maximum-sum-circular-subarray/)

## Difficulty
Medium

## Problem Description
<p>Given a <strong>circular integer array</strong> <code>nums</code> of length <code>n</code>, return <em>the maximum possible sum of a non-empty <strong>subarray</strong> of </em><code>nums</code>.</p>

<p>A <strong>circular array</strong> means the end of the array connects to the beginning of the array. Formally, the next element of <code>nums[i]</code> is <code>nums[(i + 1) % n]</code> and the previous element of <code>nums[i]</code> is <code>nums[(i - 1 + n) % n]</code>.</p>

<p>A <strong>subarray</strong> may only include each element of the fixed buffer <code>nums</code> at most once. Formally, for a subarray <code>nums[i], nums[i + 1], ..., nums[j]</code>, there does not exist <code>i &lt;= k1</code>, <code>k2 &lt;= j</code> with <code>k1 % n == k2 % n</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,-2,3,-2]
<strong>Output:</strong> 3
<strong>Explanation:</strong> Subarray [3] has maximum sum 3.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [5,-3,5]
<strong>Output:</strong> 10
<strong>Explanation:</strong> Subarray [5,5] has maximum sum 5 + 5 = 10.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums = [-3,-2,-3]
<strong>Output:</strong> -2
<strong>Explanation:</strong> Subarray [-2] has maximum sum -2.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == nums.length</code></li>
	<li><code>1 &lt;= n &lt;= 3 * 10<sup>4</sup></code></li>
	<li><code>-3 * 10<sup>4</sup> &lt;= nums[i] &lt;= 3 * 10<sup>4</sup></code></li>
</ul>


## Test Cases
```
[1,-2,3,-2]
[5,-3,5]
[-3,-2,-3]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks for the maximum subarray sum in a circular array. This means we need to consider subarrays that "wrap around" the end of the array back to the beginning.
   - A key observation is that the maximum circular subarray sum can either come from a regular subarray (like in Kadane's algorithm) or from a subarray that wraps around.
   - If the maximum subarray wraps around, it means the remaining elements (those not included in the max subarray) form the minimum subarray sum.  So, we can calculate the total sum, subtract the minimum subarray sum, and this will give the wrapped around maximum sum.
   - We can use Kadane's algorithm to find both the maximum and minimum subarray sums.
   - We need to handle the edge case where all elements are negative – in this case, the maximum sum is simply the largest negative number.

2. Solution Implementation:
```python
def maxSubarraySumCircular(nums):
    """
    Finds the maximum sum of a circular subarray.

    Args:
        nums: A list of integers.

    Returns:
        The maximum circular subarray sum.
    """
    n = len(nums)

    # Kadane's Algorithm for max subarray sum
    max_so_far = nums[0]
    curr_max = nums[0]
    for i in range(1, n):
        curr_max = max(nums[i], curr_max + nums[i])
        max_so_far = max(max_so_far, curr_max)

    # Kadane's Algorithm for min subarray sum (with some tweaks)
    min_so_far = nums[0]
    curr_min = nums[0]
    for i in range(1, n):
        curr_min = min(nums[i], curr_min + nums[i])
        min_so_far = min(min_so_far, curr_min)

    total_sum = sum(nums)

    # Handle the case where all numbers are negative
    if total_sum == min_so_far:  # If all elements are negative, regular Kadane result is correct
        return max_so_far
    else: # Otherwise compare Kadane with wrapped around sum (total - min_so_far)
        return max(max_so_far, total_sum - min_so_far)

```

3. Solution Explanation:
   - We first calculate the maximum subarray sum using Kadane's algorithm.
   - Then, we modify Kadane's algorithm to find the minimum subarray sum.
   - We compute the total sum of the array.
   - If the total sum equals the minimum subarray sum, it means all numbers are negative.  In this case, the maximum subarray sum we calculated using the standard Kadane's algorithm is the correct answer.
   - Otherwise, the maximum circular subarray sum is either the result of the standard Kadane's algorithm or the wrapped-around sum, which is the total sum minus the minimum subarray sum. We take the maximum of these two to get the final result.

4. Complexity Analysis:
   - Time complexity: O(N) - We iterate through the array twice using Kadane's algorithm and once to calculate the total sum.
   - Space complexity: O(1) - We only use a few variables to store intermediate results, so the space used is constant regardless of the input size. 


## Topics
Array, Divide and Conquer, Dynamic Programming, Queue, Monotonic Queue

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-04-16
