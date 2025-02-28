# Rearrange Array Elements by Sign

## Problem Link
[LeetCode - Rearrange Array Elements by Sign](https://leetcode.com/problems/rearrange-array-elements-by-sign/)

## Difficulty
Medium

## Problem Description
<p>You are given a <strong>0-indexed</strong> integer array <code>nums</code> of <strong>even</strong> length consisting of an <strong>equal</strong> number of positive and negative integers.</p>

<p>You should return the array of nums such that the the array follows the given conditions:</p>

<ol>
	<li>Every <strong>consecutive pair</strong> of integers have <strong>opposite signs</strong>.</li>
	<li>For all integers with the same sign, the <strong>order</strong> in which they were present in <code>nums</code> is <strong>preserved</strong>.</li>
	<li>The rearranged array begins with a positive integer.</li>
</ol>

<p>Return <em>the modified array after rearranging the elements to satisfy the aforementioned conditions</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [3,1,-2,-5,2,-4]
<strong>Output:</strong> [3,-2,1,-5,2,-4]
<strong>Explanation:</strong>
The positive integers in nums are [3,1,2]. The negative integers are [-2,-5,-4].
The only possible way to rearrange them such that they satisfy all conditions is [3,-2,1,-5,2,-4].
Other ways such as [1,-2,2,-5,3,-4], [3,1,2,-2,-5,-4], [-2,3,-5,1,-4,2] are incorrect because they do not satisfy one or more conditions.  
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [-1,1]
<strong>Output:</strong> [1,-1]
<strong>Explanation:</strong>
1 is the only positive integer and -1 the only negative integer in nums.
So nums is rearranged to [1,-1].
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 &lt;= nums.length &lt;= 2 * 10<sup>5</sup></code></li>
	<li><code>nums.length</code> is <strong>even</strong></li>
	<li><code>1 &lt;= |nums[i]| &lt;= 10<sup>5</sup></code></li>
	<li><code>nums</code> consists of <strong>equal</strong> number of positive and negative integers.</li>
</ul>

<p>&nbsp;</p>
It is not required to do the modifications in-place.

## Test Cases
```
[3,1,-2,-5,2,-4]
[-1,1]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks us to rearrange an array with equal positive and negative numbers such that positive and negative numbers alternate and the original order of positive and negative numbers is preserved.
   - Key observation: We need to maintain two separate lists (or queues) to track positive and negative numbers in their original order. 
   - Possible approaches: We can iterate through the input array once, adding positive numbers to a positive list and negative numbers to a negative list. Then, we can build the result array by alternating between taking elements from the positive and negative lists.

2. Solution Implementation:
```python
def rearrange_array(nums):
    """
    Rearranges an array of positive and negative integers such that 
    positive and negative numbers alternate, preserving original order.

    Args:
        nums: The input array.

    Returns:
        The rearranged array.
    """
    n = len(nums)
    pos = []  # Store positive numbers
    neg = []  # Store negative numbers
    result = [0] * n  # Initialize the result array

    for num in nums:
        if num > 0:
            pos.append(num)
        else:
            neg.append(num)

    pos_idx = 0
    neg_idx = 0
    for i in range(n):
        if i % 2 == 0:  # Even indices should be positive
            result[i] = pos[pos_idx]
            pos_idx += 1
        else:  # Odd indices should be negative
            result[i] = neg[neg_idx]
            neg_idx += 1

    return result

```

3. Solution Explanation:
   - The solution first initializes two empty lists `pos` and `neg` to store positive and negative numbers respectively. It also initializes the `result` array with zeros.
   - We iterate through the input `nums` array. If a number is positive, we add it to the `pos` list; otherwise, we add it to the `neg` list.
   - After populating `pos` and `neg`, we iterate through the `result` array using a `for` loop with an index `i`.
   - Inside the loop, we check if `i` is even. If it is, we take the next positive number from `pos` and place it at `result[i]`. If `i` is odd, we take the next negative number from `neg` and place it at `result[i]`.
   - This way, we ensure that positive and negative numbers alternate in the `result` array while maintaining their original order.

4. Complexity Analysis:
   - Time complexity: O(n) - We iterate through the input array `nums` once to create the positive and negative lists and then iterate through the `result` array once to populate it.
   - Space complexity: O(n) - We use two additional lists, `pos` and `neg`, and the `result` array, each of which can have a size up to n/2 in the worst case (all positive or all negative input except for one element of the opposite sign), which still simplifies to O(n).




## Topics
Array, Two Pointers, Simulation

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-02-28
