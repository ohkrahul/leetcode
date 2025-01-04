# Maximum Size of a Set After Removals

## Problem Link
[LeetCode - Maximum Size of a Set After Removals](https://leetcode.com/problems/maximum-size-of-a-set-after-removals/)

## Difficulty
Medium

## Problem Description
<p>You are given two <strong>0-indexed</strong> integer arrays <code>nums1</code> and <code>nums2</code> of even length <code>n</code>.</p>

<p>You must remove <code>n / 2</code> elements from <code>nums1</code> and <code>n / 2</code> elements from <code>nums2</code>. After the removals, you insert the remaining elements of <code>nums1</code> and <code>nums2</code> into a set <code>s</code>.</p>

<p>Return <em>the <strong>maximum</strong> possible size of the set</em> <code>s</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums1 = [1,2,1,2], nums2 = [1,1,1,1]
<strong>Output:</strong> 2
<strong>Explanation:</strong> We remove two occurences of 1 from nums1 and nums2. After the removals, the arrays become equal to nums1 = [2,2] and nums2 = [1,1]. Therefore, s = {1,2}.
It can be shown that 2 is the maximum possible size of the set s after the removals.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums1 = [1,2,3,4,5,6], nums2 = [2,3,2,3,2,3]
<strong>Output:</strong> 5
<strong>Explanation:</strong> We remove 2, 3, and 6 from nums1, as well as 2 and two occurrences of 3 from nums2. After the removals, the arrays become equal to nums1 = [1,4,5] and nums2 = [2,3,2]. Therefore, s = {1,2,3,4,5}.
It can be shown that 5 is the maximum possible size of the set s after the removals.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums1 = [1,1,2,2,3,3], nums2 = [4,4,5,5,6,6]
<strong>Output:</strong> 6
<strong>Explanation:</strong> We remove 1, 2, and 3 from nums1, as well as 4, 5, and 6 from nums2. After the removals, the arrays become equal to nums1 = [1,2,3] and nums2 = [4,5,6]. Therefore, s = {1,2,3,4,5,6}.
It can be shown that 6 is the maximum possible size of the set s after the removals.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == nums1.length == nums2.length</code></li>
	<li><code>1 &lt;= n &lt;= 2 * 10<sup>4</sup></code></li>
	<li><code>n</code> is even.</li>
	<li><code>1 &lt;= nums1[i], nums2[i] &lt;= 10<sup>9</sup></code></li>
</ul>


## Test Cases
```
[1,2,1,2]
[1,1,1,1]
[1,2,3,4,5,6]
[2,3,2,3,2,3]
[1,1,2,2,3,3]
[4,4,5,5,6,6]
```

## Initial Template
```python
# Code template not available
```

## Solution
---

## 1. Initial Thoughts:
- The problem asks to remove `n/2` elements from each array and insert the remaining elements into a set to maximize the size of the set.
- Key observation: After removing `n/2` elements from each array, the remaining elements are unique.
- Possible approaches:
  - Brute force: Try all possible combinations of removing elements and find the maximum size of the set.
  - Greedy: Remove the smallest `n/2` elements from each array and insert the remaining elements into a set.

## 2. Solution Implementation:

```python
from typing import List

class Solution:
    def maximumSize(self, nums1: List[int], nums2: List[int]) -> int:
        # Sort the arrays in ascending order
        nums1.sort()
        nums2.sort()

        # Initialize the set
        s = set()

        # Remove the smallest n/2 elements from each array
        for i in range(len(nums1) // 2):
            s.add(nums1[i])
            s.add(nums2[i])

        # Return the size of the set
        return len(s)
```

## 3. Solution Explanation:
- We sort both arrays in ascending order. This makes it easier to identify the smallest `n/2` elements in each array.
- We initialize an empty set.
- We iterate through the first `n/2` elements in both sorted arrays and add them to the set.
- Finally, we return the size of the set, which represents the maximum size of the set after removing `n/2` elements from each array.

## 4. Complexity Analysis:
- Time complexity: O(n log n), where n is the length of the input arrays. Sorting the arrays takes O(n log n) time, and the rest of the operations take constant time.
- Space complexity: O(n), since we need to store the remaining elements in the set.

## Topics
Array, Hash Table, Greedy

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-04
