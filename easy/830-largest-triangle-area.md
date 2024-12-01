# Largest Triangle Area

## Problem Link
[LeetCode - Largest Triangle Area](https://leetcode.com/problems/largest-triangle-area/)

## Difficulty
Easy

## Problem Description
<p>Given an array of points on the <strong>X-Y</strong> plane <code>points</code> where <code>points[i] = [x<sub>i</sub>, y<sub>i</sub>]</code>, return <em>the area of the largest triangle that can be formed by any three different points</em>. Answers within <code>10<sup>-5</sup></code> of the actual answer will be accepted.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/04/1027.png" style="height: 369px; width: 450px;" />
<pre>
<strong>Input:</strong> points = [[0,0],[0,1],[1,0],[0,2],[2,0]]
<strong>Output:</strong> 2.00000
<strong>Explanation:</strong> The five points are shown in the above figure. The red triangle is the largest.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> points = [[1,0],[0,0],[0,1]]
<strong>Output:</strong> 0.50000
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>3 &lt;= points.length &lt;= 50</code></li>
	<li><code>-50 &lt;= x<sub>i</sub>, y<sub>i</sub> &lt;= 50</code></li>
	<li>All the given points are <strong>unique</strong>.</li>
</ul>


## Test Cases
```
[[0,0],[0,1],[1,0],[0,2],[2,0]]
[[1,0],[0,0],[0,1]]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**

   - The problem is about finding the area of the largest triangle that can be formed by any three points in a given array of points.
   - We can use the Shoelace formula to calculate the area of a triangle given its three vertices.
   - We can iterate over all possible combinations of three points and calculate the area of the triangle formed by them.
   - The time complexity of this approach is O(n^3), where n is the number of points.

2. **Solution Implementation:**

```python
from typing import List

def largestTriangleArea(points: List[List[int]]) -> float:
    """
    Calculate the area of the largest triangle that can be formed by any three different points in the given array of points.
    """
    max_area = 0.0

    for i in range(len(points)):
        for j in range(i + 1, len(points)):
            for k in range(j + 1, len(points)):
                area = abs((points[i][0] * (points[j][1] - points[k][1]) +
                            points[j][0] * (points[k][1] - points[i][1]) +
                            points[k][0] * (points[i][1] - points[j][1])) / 2.0)
                max_area = max(max_area, area)

    return max_area
```

3. **Solution Explanation:**

   - We iterate over all possible combinations of three points and calculate the area of the triangle formed by them using the Shoelace formula.
   - We keep track of the maximum area and return it at the end.

4. **Complexity Analysis:**

   - Time complexity: O(n^3), where n is the number of points. We iterate over all possible combinations of three points, which takes O(n^3) time.
   - Space complexity: O(1), as we only store a few variables.

## Topics
Array, Math, Geometry

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-12-01
