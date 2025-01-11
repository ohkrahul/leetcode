# Maximum Subarray Sum With Length Divisible by K

## Problem Link
[LeetCode - Maximum Subarray Sum With Length Divisible by K](https://leetcode.com/problems/maximum-subarray-sum-with-length-divisible-by-k/)

## Difficulty
Medium

## Problem Description
<p>You are given an array of integers <code>nums</code> and an integer <code>k</code>.</p>

<p>Return the <strong>maximum</strong> sum of a <span data-keyword="subarray-nonempty">subarray</span> of <code>nums</code>, such that the size of the subarray is <strong>divisible</strong> by <code>k</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">nums = [1,2], k = 1</span></p>

<p><strong>Output:</strong> <span class="example-io">3</span></p>

<p><strong>Explanation:</strong></p>

<p>The subarray <code>[1, 2]</code> with sum 3 has length equal to 2 which is divisible by 1.</p>
</div>

<p><strong class="example">Example 2:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">nums = [-1,-2,-3,-4,-5], k = 4</span></p>

<p><strong>Output:</strong> <span class="example-io">-10</span></p>

<p><strong>Explanation:</strong></p>

<p>The maximum sum subarray is <code>[-1, -2, -3, -4]</code> which has length equal to 4 which is divisible by 4.</p>
</div>

<p><strong class="example">Example 3:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">nums = [-5,1,2,-3,4], k = 2</span></p>

<p><strong>Output:</strong> <span class="example-io">4</span></p>

<p><strong>Explanation:</strong></p>

<p>The maximum sum subarray is <code>[1, 2, -3, 4]</code> which has length equal to 4 which is divisible by 2.</p>
</div>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= k &lt;= nums.length &lt;= 2 * 10<sup>5</sup></code></li>
	<li><code>-10<sup>9</sup> &lt;= nums[i] &lt;= 10<sup>9</sup></code></li>
</ul>


## Test Cases
```
[1,2]
1
[-1,-2,-3,-4,-5]
4
[-5,1,2,-3,4]
2
```

## Initial Template
```python
# Code template not available
```

## Solution
## Initial Thoughts:

This is a dynamic programming problem. We can break down the problem into subproblems:

- Let `dp[i][r]` denote the maximum subarray sum of elements from `nums[0]` to `nums[i]` where the length of the subarray is divisible by `k` and `r` is the remainder of the length of the subarray when divided by `k`.
- We can compute `dp[i][r]` for all `i` and `r` in `O(n*k)` time.
- The answer is `max(dp[n-1][r])` for all `r`.

## Solution Implementation:

```python
def max_subarray_sum_divisible_by_k(nums, k):
  # Initialize the dp table.
  dp = [[0 for _ in range(k)] for _ in range(len(nums))]

  # Base case: the subarray of length 0 is divisible by any k.
  for i in range(k):
    dp[0][i] = nums[0]

  # Compute the dp table.
  for i in range(1, len(nums)):
    for r in range(k):
      # If the current element is divisible by k, then the maximum
      # subarray sum of length divisible by k is the current element.
      if nums[i] % k == r:
        dp[i][r] = nums[i]
      # Otherwise, the maximum subarray sum of length divisible by k is
      # the maximum of the current element and the maximum subarray sum
      # of length divisible by k ending at the previous index.
      else:
        dp[i][r] = max(nums[i], dp[i-1][r])

      # If the current element is not divisible by k, then the maximum
      # subarray sum of length divisible by k is the maximum of the
      # maximum subarray sum of length divisible by k ending at the
      # previous index and the maximum subarray sum of length divisible
      # by k starting at the current index.
      if r > 0:
        dp[i][r] = max(dp[i][r], dp[i-1][(r-nums[i]%k)%k])

  # Return the maximum subarray sum of length divisible by k.
  return max(dp[len(nums)-1][r] for r in range(k))
```

## Solution Explanation:

The solution works by computing the maximum subarray sum of length divisible by `k` for all indices `i` and remainders `r`. The base case is when `i` is 0, in which case the maximum subarray sum of length divisible by `k` is the first element of the array. For all other indices `i`, the maximum subarray sum of length divisible by `k` is the maximum of the following two values:

- The maximum subarray sum of length divisible by `k` ending at the previous index `i-1`.
- The maximum subarray sum of length divisible by `k` starting at the current index `i`.

If the current element `nums[i]` is divisible by `k`, then the maximum subarray sum of length divisible by `k` is the current element. Otherwise, the maximum subarray sum of length divisible by `k` is the maximum of the current element and the maximum subarray sum of length divisible by `k` ending at the previous index.

The time complexity of the solution is `O(n*k)`, where `n` is the length of the array and `k` is the given number. The space complexity of the solution is `O(n)`, since we are using a dp table of size `n*k`.

## Complexity Analysis:

- Time complexity: `O(n*k)` - We iterate over the array of size `n` and for each element, we compute the maximum subarray sum of length divisible by `k`. This takes `O(k)` time.
- Space complexity: `O(n)` - We use a dp table of size `n*k` to store the maximum subarray sum of length divisible by `k` for all indices `i` and remainders `r`.

## Topics
Array, Hash Table, Prefix Sum

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-11
