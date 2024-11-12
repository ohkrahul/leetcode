# Check if All the Integers in a Range Are Covered

## Problem Link
[LeetCode - Check if All the Integers in a Range Are Covered](https://leetcode.com/problems/check-if-all-the-integers-in-a-range-are-covered/)

## Difficulty
Easy

## Problem Description
<p>You are given a 2D integer array <code>ranges</code> and two integers <code>left</code> and <code>right</code>. Each <code>ranges[i] = [start<sub>i</sub>, end<sub>i</sub>]</code> represents an <strong>inclusive</strong> interval between <code>start<sub>i</sub></code> and <code>end<sub>i</sub></code>.</p>

<p>Return <code>true</code> <em>if each integer in the inclusive range</em> <code>[left, right]</code> <em>is covered by <strong>at least one</strong> interval in</em> <code>ranges</code>. Return <code>false</code> <em>otherwise</em>.</p>

<p>An integer <code>x</code> is covered by an interval <code>ranges[i] = [start<sub>i</sub>, end<sub>i</sub>]</code> if <code>start<sub>i</sub> &lt;= x &lt;= end<sub>i</sub></code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> ranges = [[1,2],[3,4],[5,6]], left = 2, right = 5
<strong>Output:</strong> true
<strong>Explanation:</strong> Every integer between 2 and 5 is covered:
- 2 is covered by the first range.
- 3 and 4 are covered by the second range.
- 5 is covered by the third range.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> ranges = [[1,10],[10,20]], left = 21, right = 21
<strong>Output:</strong> false
<strong>Explanation:</strong> 21 is not covered by any range.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= ranges.length &lt;= 50</code></li>
	<li><code>1 &lt;= start<sub>i</sub> &lt;= end<sub>i</sub> &lt;= 50</code></li>
	<li><code>1 &lt;= left &lt;= right &lt;= 50</code></li>
</ul>


## Test Cases
```
[[1,2],[3,4],[5,6]]
2
5
[[1,10],[10,20]]
21
21
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**

   - **Problem analysis:** The problem asks if every integer in the range [left, right] is covered by at least one interval in the given list of intervals.
   - **Key observations:**
     - The intervals are non-overlapping and inclusive.
     - The range [left, right] is also inclusive.
   - **Possible approaches:**
     - **Brute force:** Check each integer in the range [left, right] and see if it is covered by any of the intervals.
     - **Sorting:** Sort the intervals and the range, then do a merge-like process to check if each integer in the range is covered.
     - **Interval tree:** Build an interval tree for the given intervals, then for each integer in the range, check if it is covered by any of the intervals in the tree.

2. **Solution Implementation:**

```python
def isCovered(ranges, left, right):
    """
    :type ranges: List[List[int]]
    :type left: int
    :type right: int
    :rtype: bool
    """

    # Sort the intervals and the range
    ranges.sort()
    range_list = [left, right]
    range_list.sort()

    # Check if each integer in the range is covered
    for i in range(range_list[0], range_list[1] + 1):
        covered = False
        for interval in ranges:
            if interval[0] <= i <= interval[1]:
                covered = True
                break
        if not covered:
            return False

    return True
```

3. **Solution Explanation:**

   - The solution uses the **sorting approach**.
   - It sorts the intervals and the range, then iterates over the range to check if each integer is covered by any of the intervals.
   - The sorting step is O(N log N), where N is the number of intervals.
   - The checking step is O(N), because for each integer in the range, we need to check at most N intervals.
   - Therefore, the overall time complexity is O(N log N).

4. **Complexity Analysis:**

   - **Time complexity:** O(N log N)
   - **Space complexity:** O(1) (no extra space is used)

## Topics
Array, Hash Table, Prefix Sum

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-11-12
