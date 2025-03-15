# K-diff Pairs in an Array

## Problem Link
[LeetCode - K-diff Pairs in an Array](https://leetcode.com/problems/k-diff-pairs-in-an-array/)

## Difficulty
Medium

## Problem Description
<p>Given an array of integers <code>nums</code> and an integer <code>k</code>, return <em>the number of <b>unique</b> k-diff pairs in the array</em>.</p>

<p>A <strong>k-diff</strong> pair is an integer pair <code>(nums[i], nums[j])</code>, where the following are true:</p>

<ul>
	<li><code>0 &lt;= i, j &lt; nums.length</code></li>
	<li><code>i != j</code></li>
	<li><code>|nums[i] - nums[j]| == k</code></li>
</ul>

<p><strong>Notice</strong> that <code>|val|</code> denotes the absolute value of <code>val</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [3,1,4,1,5], k = 2
<strong>Output:</strong> 2
<strong>Explanation:</strong> There are two 2-diff pairs in the array, (1, 3) and (3, 5).
Although we have two 1s in the input, we should only return the number of <strong>unique</strong> pairs.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,2,3,4,5], k = 1
<strong>Output:</strong> 4
<strong>Explanation:</strong> There are four 1-diff pairs in the array, (1, 2), (2, 3), (3, 4) and (4, 5).
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,3,1,5,4], k = 0
<strong>Output:</strong> 1
<strong>Explanation:</strong> There is one 0-diff pair in the array, (1, 1).
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>4</sup></code></li>
	<li><code>-10<sup>7</sup> &lt;= nums[i] &lt;= 10<sup>7</sup></code></li>
	<li><code>0 &lt;= k &lt;= 10<sup>7</sup></code></li>
</ul>


## Test Cases
```
[3,1,4,1,5]
2
[1,2,3,4,5]
1
[1,3,1,5,4]
0
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks for the number of unique k-diff pairs. This means we need to consider the absolute difference between two numbers in the array and check if it's equal to k.
   - We also need to avoid duplicates. So, if (1, 3) is a valid pair, we don't count (3, 1) as a separate pair.
   - We can consider using a set to store the seen pairs to avoid duplicates.
   - A brute-force approach would be to iterate through all possible pairs using nested loops, but that would have O(n^2) time complexity. We might be able to optimize it using a hash map or a two-pointer approach.
   - If k is 0, we just need to count the duplicates in the array.


2. Solution Implementation:
```python
from collections import Counter

def findPairs(nums, k):
    """
    Finds the number of unique k-diff pairs in an array.

    Args:
        nums: The input array of integers.
        k: The target difference.

    Returns:
        The number of unique k-diff pairs.
    """

    count = Counter(nums)  # Store element frequencies
    res = 0

    if k == 0:  # Handle k = 0 case separately
        for val in count:
            if count[val] > 1:
                res += 1
    else:
        for val in count:
            complement = val + k  # Calculate the complement needed for a k-diff pair
            if complement in count:  # Check if the complement exists in the array
                res += 1

    return res
```

3. Solution Explanation:
   - The solution uses a `Counter` to store the frequency of each number in the array. This helps in quickly checking if a complement exists for a given number.
   - If `k` is 0, we iterate through the `Counter` and increment the result for each number that appears more than once.
   - If `k` is not 0, we iterate through the `Counter`, calculate the complement (`val + k`), and check if the complement exists in the `Counter`. If it does, we increment the result.  We don't need to worry about duplicates like (1,3) and (3,1) because the `Counter` and the way we iterate only counts each unique pair once.
   - This approach avoids the O(n^2) complexity of nested loops and efficiently handles the k=0 case.

4. Complexity Analysis:
   - Time complexity: O(n) - We iterate through the array once to build the `Counter` and then iterate through the `Counter` (which has at most n elements) once more.
   - Space complexity: O(n) - The `Counter` can store up to n elements in the worst case (when all elements in the input array are unique). 


## Topics
Array, Hash Table, Two Pointers, Binary Search, Sorting

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-15
