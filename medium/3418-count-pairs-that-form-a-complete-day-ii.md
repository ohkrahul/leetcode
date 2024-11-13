# Count Pairs That Form a Complete Day II

## Problem Link
[LeetCode - Count Pairs That Form a Complete Day II](https://leetcode.com/problems/count-pairs-that-form-a-complete-day-ii/)

## Difficulty
Medium

## Problem Description
<p>Given an integer array <code>hours</code> representing times in <strong>hours</strong>, return an integer denoting the number of pairs <code>i</code>, <code>j</code> where <code>i &lt; j</code> and <code>hours[i] + hours[j]</code> forms a <strong>complete day</strong>.</p>

<p>A <strong>complete day</strong> is defined as a time duration that is an <strong>exact</strong> <strong>multiple</strong> of 24 hours.</p>

<p>For example, 1 day is 24 hours, 2 days is 48 hours, 3 days is 72 hours, and so on.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">hours = [12,12,30,24,24]</span></p>

<p><strong>Output:</strong> <span class="example-io">2</span></p>

<p><strong>Explanation:</strong> The pairs of indices that form a complete day are <code>(0, 1)</code> and <code>(3, 4)</code>.</p>
</div>

<p><strong class="example">Example 2:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">hours = [72,48,24,3]</span></p>

<p><strong>Output:</strong> <span class="example-io">3</span></p>

<p><strong>Explanation:</strong> The pairs of indices that form a complete day are <code>(0, 1)</code>, <code>(0, 2)</code>, and <code>(1, 2)</code>.</p>
</div>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= hours.length &lt;= 5 * 10<sup>5</sup></code></li>
	<li><code>1 &lt;= hours[i] &lt;= 10<sup>9</sup></code></li>
</ul>


## Test Cases
```
[12,12,30,24,24]
[72,48,24,3]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks for the number of pairs of indices that form a complete day.
   - A complete day is defined as a time duration that is an exact multiple of 24 hours.
   - We can iterate over all pairs of indices and check if the sum of hours[i] and hours[j] is a multiple of 24.

2. Solution Implementation:
```python
def get_complete_day_pairs(hours):
    """
    :type hours: List[int]
    :rtype: int
    """
    count = 0
    for i in range(len(hours)):
        for j in range(i + 1, len(hours)):
            if (hours[i] + hours[j]) % 24 == 0:
                count += 1
    return count
```

3. Solution Explanation:
   - We iterate over all pairs of indices (i, j) where i < j using two nested loops.
   - For each pair, we check if the sum of hours[i] and hours[j] is a multiple of 24.
   - If so, we increment the count by 1.
   - Finally, we return the count.

4. Complexity Analysis:
   - Time complexity: O(n^2) - We iterate over all pairs of indices, which takes O(n^2) time.
   - Space complexity: O(1) - We only use a constant amount of extra space.

## Topics
Array, Hash Table, Counting

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-11-13
