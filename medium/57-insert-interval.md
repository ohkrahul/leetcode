# Insert Interval

## Problem Link
[LeetCode - Insert Interval](https://leetcode.com/problems/insert-interval/)

## Difficulty
Medium

## Problem Description
<p>You are given an array of non-overlapping intervals <code>intervals</code> where <code>intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]</code> represent the start and the end of the <code>i<sup>th</sup></code> interval and <code>intervals</code> is sorted in ascending order by <code>start<sub>i</sub></code>. You are also given an interval <code>newInterval = [start, end]</code> that represents the start and end of another interval.</p>

<p>Insert <code>newInterval</code> into <code>intervals</code> such that <code>intervals</code> is still sorted in ascending order by <code>start<sub>i</sub></code> and <code>intervals</code> still does not have any overlapping intervals (merge overlapping intervals if necessary).</p>

<p>Return <code>intervals</code><em> after the insertion</em>.</p>

<p><strong>Note</strong> that you don&#39;t need to modify <code>intervals</code> in-place. You can make a new array and return it.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> intervals = [[1,3],[6,9]], newInterval = [2,5]
<strong>Output:</strong> [[1,5],[6,9]]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
<strong>Output:</strong> [[1,2],[3,10],[12,16]]
<strong>Explanation:</strong> Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= intervals.length &lt;= 10<sup>4</sup></code></li>
	<li><code>intervals[i].length == 2</code></li>
	<li><code>0 &lt;= start<sub>i</sub> &lt;= end<sub>i</sub> &lt;= 10<sup>5</sup></code></li>
	<li><code>intervals</code> is sorted by <code>start<sub>i</sub></code> in <strong>ascending</strong> order.</li>
	<li><code>newInterval.length == 2</code></li>
	<li><code>0 &lt;= start &lt;= end &lt;= 10<sup>5</sup></code></li>
</ul>


## Test Cases
```
[[1,3],[6,9]]
[2,5]
[[1,2],[3,5],[6,7],[8,10],[12,16]]
[4,8]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks us to insert a new interval into a sorted list of non-overlapping intervals and merge any overlapping intervals.
   - The key observation is that we can iterate through the existing intervals and determine three cases:
     1. The new interval comes before the current interval.
     2. The new interval overlaps with the current interval.
     3. The new interval comes after the current interval.
   - We can use a list to store the resulting intervals. We add intervals to this list based on the three cases mentioned above.  If there's an overlap, we merge the intervals by updating the `end` of the new interval to the maximum of the current interval's end and the new interval's end.

2. Solution Implementation:
```python
def insert(intervals, newInterval):
    """
    Inserts a new interval into a sorted list of non-overlapping intervals and merges overlapping intervals.

    Args:
        intervals: A list of intervals, where each interval is a list of two integers [start, end].
        newInterval: The new interval to insert.

    Returns:
        A list of intervals after the insertion and merging.
    """

    result = []
    i = 0
    n = len(intervals)

    # Add all intervals ending before newInterval starts
    while i < n and intervals[i][1] < newInterval[0]:
        result.append(intervals[i])
        i += 1

    # Merge overlapping intervals
    while i < n and intervals[i][0] <= newInterval[1]:
        newInterval[0] = min(newInterval[0], intervals[i][0])
        newInterval[1] = max(newInterval[1], intervals[i][1])
        i += 1
    result.append(newInterval)

    # Add the remaining intervals
    while i < n:
        result.append(intervals[i])
        i += 1

    return result

```

3. Solution Explanation:
   - We iterate through the input `intervals` list.
   - First, we add all intervals that end before the `newInterval` starts to the `result` list.
   - Then, we handle overlapping intervals. While the start of the current interval is less than or equal to the end of the `newInterval`, we merge the intervals.  Merging is done by updating the `newInterval`'s start to the minimum of both starts and its end to the maximum of both ends. This efficiently combines overlapping intervals.
   - Finally, we add the remaining intervals (those that start after the merged `newInterval` ends) to the `result` list.

4. Complexity Analysis:
   - Time complexity: O(N) - We iterate through the `intervals` list once in the worst case.
   - Space complexity: O(N) -  The `result` list can potentially store all the original intervals plus the new one in the worst-case scenario (no overlaps).


## Topics
Array

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-04-22
