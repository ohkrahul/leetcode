# Maximum Product Subarray

## Problem Link
[LeetCode - Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)

## Difficulty
Medium

## Problem Description
<p>Given an integer array <code>nums</code>, find a <span data-keyword="subarray-nonempty">subarray</span> that has the largest product, and return <em>the product</em>.</p>

<p>The test cases are generated so that the answer will fit in a <strong>32-bit</strong> integer.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [2,3,-2,4]
<strong>Output:</strong> 6
<strong>Explanation:</strong> [2,3] has the largest product 6.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [-2,0,-1]
<strong>Output:</strong> 0
<strong>Explanation:</strong> The result cannot be 2, because [-2,-1] is not a subarray.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 2 * 10<sup>4</sup></code></li>
	<li><code>-10 &lt;= nums[i] &lt;= 10</code></li>
	<li>The product of any subarray of <code>nums</code> is <strong>guaranteed</strong> to fit in a <strong>32-bit</strong> integer.</li>
</ul>


## Test Cases
```
[2,3,-2,4]
[-2,0,-1]
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts

### Problem analysis
The problem asks for the maximum product of a subarray. A subarray is a contiguous part of the original array. The product of an array can be positive or negative depending on whether there are even or odd number of negative integers in the array.
The product of an array can be very large so we need to make sure the result is within the range of 32-bits integer.

### Key observations
- The product of an array can be positive or negative.
- The maximum product of a subarray can be positive or negative.
- The product of an array can be very large.

### Possible approaches
- Brute force: Generate all possible subarrays and calculate their products.
- Dynamic programming: Create a table to store the maximum product of subarrays ending at each index.
- Divide and conquer: Divide the array into smaller subarrays and solve the problem recursively.

## 2. Solution Implementation

```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        if not nums:
            return 0

        max_product = nums[0]
        min_product = nums[0]
        result = max_product

        for i in range(1, len(nums)):
            # If the current number is negative, swap the max and min products
            if nums[i] < 0:
                max_product, min_product = min_product, max_product

            # Update the max and min products
            max_product = max(nums[i], nums[i] * max_product)
            min_product = min(nums[i], nums[i] * min_product)

            # Update the result
            result = max(result, max_product)

        return result
```

## 3. Solution Explanation

The solution uses a dynamic programming approach to solve the problem. It creates two tables, `max_product` and `min_product`, to store the maximum and minimum product of subarrays ending at each index. The solution also keeps track of the overall maximum product.

For each element in the array, the solution updates the `max_product` and `min_product` tables as follows:

- If the current element is negative, the solution swaps the `max_product` and `min_product` tables.
- The solution updates the `max_product` table to be the maximum of the current element and the product of the current element and the previous `max_product`.
- The solution updates the `min_product` table to be the minimum of the current element and the product of the current element and the previous `min_product`.

The solution also keeps track of the overall maximum product. At the end of the loop, the solution returns the overall maximum product.

## 4. Complexity Analysis

### Time complexity: O(n)
The solution iterates over the array once, so the time complexity is O(n).

### Space complexity: O(1)
The solution uses a constant amount of space, so the space complexity is O(1).

## Topics
Array, Dynamic Programming

Solved on: 2024-11-10
