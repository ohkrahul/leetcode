# Count Number of Maximum Bitwise-OR Subsets

## Problem Link
[LeetCode - Count Number of Maximum Bitwise-OR Subsets](https://leetcode.com/problems/count-number-of-maximum-bitwise-or-subsets/)

## Difficulty
Medium

## Problem Description
<p>Given an integer array <code>nums</code>, find the <strong>maximum</strong> possible <strong>bitwise OR</strong> of a subset of <code>nums</code> and return <em>the <strong>number of different non-empty subsets</strong> with the maximum bitwise OR</em>.</p>

<p>An array <code>a</code> is a <strong>subset</strong> of an array <code>b</code> if <code>a</code> can be obtained from <code>b</code> by deleting some (possibly zero) elements of <code>b</code>. Two subsets are considered <strong>different</strong> if the indices of the elements chosen are different.</p>

<p>The bitwise OR of an array <code>a</code> is equal to <code>a[0] <strong>OR</strong> a[1] <strong>OR</strong> ... <strong>OR</strong> a[a.length - 1]</code> (<strong>0-indexed</strong>).</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [3,1]
<strong>Output:</strong> 2
<strong>Explanation:</strong> The maximum possible bitwise OR of a subset is 3. There are 2 subsets with a bitwise OR of 3:
- [3]
- [3,1]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [2,2,2]
<strong>Output:</strong> 7
<strong>Explanation:</strong> All non-empty subsets of [2,2,2] have a bitwise OR of 2. There are 2<sup>3</sup> - 1 = 7 total subsets.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums = [3,2,1,5]
<strong>Output:</strong> 6
<strong>Explanation:</strong> The maximum possible bitwise OR of a subset is 7. There are 6 subsets with a bitwise OR of 7:
- [3,5]
- [3,1,5]
- [3,2,5]
- [3,2,1,5]
- [2,5]
- [2,1,5]</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 16</code></li>
	<li><code>1 &lt;= nums[i] &lt;= 10<sup>5</sup></code></li>
</ul>


## Test Cases
```
[3,1]
[2,2,2]
[3,2,1,5]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**

- **Problem analysis:** The problem asks to find how many non-empty subsets of `nums` share the same maximum possible bitwise OR value.
- **Key observations:**
   - The maximum possible bitwise OR value of a subset of integers is the maximum value in that subset.
   - The number of subsets with the maximum bitwise OR value is equivalent to the number of subsets that contain the maximum value.
- **Possible approaches:**
   - **Brute force:** Try all possible subsets and compute the bitwise OR of each subset. Count the number of subsets with the maximum bitwise OR value.
   - **Dynamic programming:** Use a bottom-up approach to compute the maximum bitwise OR value and the number of subsets with that value for each subset of `nums`.

2. **Solution Implementation:**

```python
def countMaxOrSubsets(nums):
    """
    :type nums: List[int]
    :rtype: int
    """
    # Initialize the maximum bitwise OR value and the count of subsets with that value
    max_or = 0
    max_or_count = 0

    # Iterate over all possible subsets of nums
    for mask in range(1 << len(nums)):
        # Compute the bitwise OR of the current subset
        subset_or = 0
        for i in range(len(nums)):
            if mask & (1 << i):
                subset_or |= nums[i]
        
        # Update the maximum bitwise OR value and the count of subsets with that value
        if subset_or > max_or:
            max_or = subset_or
            max_or_count = 1
        elif subset_or == max_or:
            max_or_count += 1
    
    # Return the count of subsets with the maximum bitwise OR value
    return max_or_count
```

3. **Solution Explanation:**

- The solution uses a dynamic programming approach to compute the maximum bitwise OR value and the number of subsets with that value for each subset of `nums`.
- It iterates over all possible subsets of `nums` using a bitmask, which represents the indices of the elements in the subset.
- For each subset, it computes the bitwise OR of the elements in the subset and updates the maximum bitwise OR value and the count of subsets with that value if necessary.
- Finally, it returns the count of subsets with the maximum bitwise OR value.

4. **Complexity Analysis:**

- **Time complexity:** O(2^n), where n is the length of `nums`. The solution iterates over all possible subsets of `nums`, which takes exponential time.
- **Space complexity:** O(1). The solution uses a constant amount of space.

## Topics
Array, Backtracking, Bit Manipulation, Enumeration

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-17
