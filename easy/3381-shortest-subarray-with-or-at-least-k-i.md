# Shortest Subarray With OR at Least K I

## Problem Link
[LeetCode - Shortest Subarray With OR at Least K I](https://leetcode.com/problems/shortest-subarray-with-or-at-least-k-i/)

## Difficulty
Easy

## Problem Description
<p>You are given an array <code>nums</code> of <strong>non-negative</strong> integers and an integer <code>k</code>.</p>

<p>An array is called <strong>special</strong> if the bitwise <code>OR</code> of all of its elements is <strong>at least</strong> <code>k</code>.</p>

<p>Return <em>the length of the <strong>shortest</strong> <strong>special</strong> <strong>non-empty</strong> <span data-keyword="subarray-nonempty">subarray</span> of</em> <code>nums</code>, <em>or return</em> <code>-1</code> <em>if no special subarray exists</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">nums = [1,2,3], k = 2</span></p>

<p><strong>Output:</strong> <span class="example-io">1</span></p>

<p><strong>Explanation:</strong></p>

<p>The subarray <code>[3]</code> has <code>OR</code> value of <code>3</code>. Hence, we return <code>1</code>.</p>

<p>Note that <code>[2]</code> is also a special subarray.</p>
</div>

<p><strong class="example">Example 2:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">nums = [2,1,8], k = 10</span></p>

<p><strong>Output:</strong> <span class="example-io">3</span></p>

<p><strong>Explanation:</strong></p>

<p>The subarray <code>[2,1,8]</code> has <code>OR</code> value of <code>11</code>. Hence, we return <code>3</code>.</p>
</div>

<p><strong class="example">Example 3:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">nums = [1,2], k = 0</span></p>

<p><strong>Output:</strong> <span class="example-io">1</span></p>

<p><strong>Explanation:</strong></p>

<p>The subarray <code>[1]</code> has <code>OR</code> value of <code>1</code>. Hence, we return <code>1</code>.</p>
</div>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 50</code></li>
	<li><code>0 &lt;= nums[i] &lt;= 50</code></li>
	<li><code>0 &lt;= k &lt; 64</code></li>
</ul>


## Test Cases
```
[1,2,3]
2
[2,1,8]
10
[1,2]
0
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**

   - **Problem analysis:** We need to find the shortest subarray whose bitwise OR is at least k.
   - **Key observations:**
     - The bitwise OR of a subarray is the OR of its elements.
     - We can use a sliding window to iterate through the array and update the current OR value.
     - We need to keep track of the minimum length of a special subarray.
   - **Possible approaches:**
     - **Brute force:** Check every possible subarray and find the shortest one that is special. Time complexity: O(n^2).
     - **Sliding window:** Use a sliding window to iterate through the array and update the current OR value. Time complexity: O(n).

2. **Solution Implementation:**

```python
def shortestSubarray(nums, k):
    """
    :type nums: List[int]
    :type k: int
    :rtype: int
    """
    # Initialize the minimum length to infinity
    min_length = float('inf')
    # Initialize the start and end pointers of the sliding window
    start = 0
    end = 0
    # Initialize the current OR value to 0
    current_or = 0
    # Iterate through the array
    while end < len(nums):
        # Add the current element to the current OR value
        current_or |= nums[end]
        # If the current OR value is at least k, update the minimum length
        if current_or >= k:
            min_length = min(min_length, end - start + 1)
            # Remove elements from the start of the sliding window until the current OR value is less than k
            while current_or >= k:
                current_or ^= nums[start]
                start += 1
        # Move the end pointer of the sliding window to the next element
        end += 1
    # Return the minimum length if it is not infinity, otherwise return -1
    return min_length if min_length != float('inf') else -1
```

3. **Solution Explanation:**

   - We use a sliding window to iterate through the array and update the current OR value.
   - We keep track of the minimum length of a special subarray.
   - If the current OR value is at least k, we update the minimum length and remove elements from the start of the sliding window until the current OR value is less than k.
   - We move the end pointer of the sliding window to the next element and repeat the process.
   - If the minimum length is still infinity after iterating through the entire array, then no special subarray exists and we return -1.

4. **Complexity Analysis:**

   - **Time complexity:** O(n), where n is the length of the array. We iterate through the array once using a sliding window.
   - **Space complexity:** O(1). The space complexity is constant because we only use a fixed number of variables.

## Topics
Array, Bit Manipulation, Sliding Window

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-11-11
