# Minimum Positive Sum Subarray 

## Problem Link
[LeetCode - Minimum Positive Sum Subarray ](https://leetcode.com/problems/minimum-positive-sum-subarray/)

## Difficulty
Easy

## Problem Description
<p>You are given an integer array <code>nums</code> and <strong>two</strong> integers <code>l</code> and <code>r</code>. Your task is to find the <strong>minimum</strong> sum of a <strong>subarray</strong> whose size is between <code>l</code> and <code>r</code> (inclusive) and whose sum is greater than 0.</p>

<p>Return the <strong>minimum</strong> sum of such a subarray. If no such subarray exists, return -1.</p>

<p>A <strong>subarray</strong> is a contiguous <b>non-empty</b> sequence of elements within an array.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">nums = [3, -2, 1, 4], l = 2, r = 3</span></p>

<p><strong>Output:</strong> <span class="example-io">1</span></p>

<p><strong>Explanation:</strong></p>

<p>The subarrays of length between <code>l = 2</code> and <code>r = 3</code> where the sum is greater than 0 are:</p>

<ul>
	<li><code>[3, -2]</code> with a sum of 1</li>
	<li><code>[1, 4]</code> with a sum of 5</li>
	<li><code>[3, -2, 1]</code> with a sum of 2</li>
	<li><code>[-2, 1, 4]</code> with a sum of 3</li>
</ul>

<p>Out of these, the subarray <code>[3, -2]</code> has a sum of 1, which is the smallest positive sum. Hence, the answer is 1.</p>
</div>

<p><strong class="example">Example 2:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">nums = [-2, 2, -3, 1], l = 2, r = 3</span></p>

<p><strong>Output:</strong> <span class="example-io">-1</span></p>

<p><strong>Explanation:</strong></p>

<p>There is no subarray of length between <code>l</code> and <code>r</code> that has a sum greater than 0. So, the answer is -1.</p>
</div>

<p><strong class="example">Example 3:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">nums = [1, 2, 3, 4], l = 2, r = 4</span></p>

<p><strong>Output:</strong> <span class="example-io">3</span></p>

<p><strong>Explanation:</strong></p>

<p>The subarray <code>[1, 2]</code> has a length of 2 and the minimum sum greater than 0. So, the answer is 3.</p>
</div>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 100</code></li>
	<li><code>1 &lt;= l &lt;= r &lt;= nums.length</code></li>
	<li><code>-1000 &lt;= nums[i] &lt;= 1000</code></li>
</ul>


## Test Cases
```
[3,-2,1,4]
2
3
[-2,2,-3,1]
2
3
[1,2,3,4]
2
4
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**

   - **Problem analysis:**
     - We need to find a subarray whose length is between l and r (inclusive) and whose sum is greater than 0.
     - If there is no such subarray, we return -1.
   - **Key observations:**
     - The subarray must contain at least one positive number.
     - We can use a sliding window to find the subarray with the minimum sum greater than 0.
   - **Possible approaches:**
     - Brute force: Check all possible subarrays and calculate their sum. This approach has a time complexity of O(n^3).
     - Sliding window: Maintain a sliding window of length l to r and update the minimum sum as we move the window. This approach has a time complexity of O(n).

2. **Solution Implementation:**

```python
from typing import List

def min_positive_sum_subarray(nums: List[int], l: int, r: int) -> int:
    """
    Finds the minimum sum of a subarray whose size is between l and r (inclusive) and whose sum is greater than 0.

    Args:
        nums (List[int]): The input array.
        l (int): The minimum size of the subarray.
        r (int): The maximum size of the subarray.

    Returns:
        int: The minimum sum of a subarray that satisfies the conditions, or -1 if no such subarray exists.
    """

    # Initialize the minimum sum and the window sum
    min_sum = float('inf')
    window_sum = 0

    # Initialize the start and end of the window
    start = 0
    end = 0

    # Slide the window until the end of the array is reached
    while end < len(nums):
        # Add the current element to the window sum
        window_sum += nums[end]

        # Check if the window sum is greater than 0
        if window_sum > 0:
            # Check if the window size is between l and r
            if end - start + 1 >= l and end - start + 1 <= r:
                # Update the minimum sum
                min_sum = min(min_sum, window_sum)

        # Check if the window size is greater than r
        if end - start + 1 > r:
            # Remove the first element from the window sum
            window_sum -= nums[start]
            # Move the start of the window to the right
            start += 1

        # Move the end of the window to the right
        end += 1

    # Return the minimum sum
    return min_sum if min_sum != float('inf') else -1
```

3. **Solution Explanation:**

   - The solution uses a sliding window to find the subarray with the minimum sum greater than 0.
   - The sliding window is initialized to have a length of l.
   - As the window slides, we calculate the sum of the elements in the window.
   - If the window sum is greater than 0 and the window size is between l and r, we update the minimum sum.
   - If the window size is greater than r, we remove the first element from the window sum and move the start of the window to the right.
   - We continue sliding the window until the end of the array is reached.
   - If the minimum sum is still infinity, then there is no subarray that satisfies the conditions and we return -1.

4. **Complexity Analysis:**

   - **Time complexity:** O(n), where n is the length of the input array. The sliding window iterates over the entire array once.
   - **Space complexity:** O(1), as we only store a few variables in memory.

## Topics
Array, Sliding Window, Prefix Sum

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-08
