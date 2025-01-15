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
## 1. Initial Thoughts:
- This problem asks for the area of the largest triangle formed by any three points in a given array of points.
- The first step is to notice that the area of a triangle can be computed using the cross product of two vectors formed by the three points.
- Since we have an array of points, we can compute the cross product for all possible combinations of three points and take the maximum.

## 2. Solution Implementation:
```python
from typing import List

def largestTriangleArea(points: List[List[int]]) -> float:
    """
    :param points: A list of points in the X-Y plane.
    :return: The area of the largest triangle that can be formed by any three different points.
    """
    n = len(points)
    max_area = 0.0

    for i in range(n):
        for j in range(i+1, n):
            for k in range(j+1, n):
                x1, y1 = points[i]
                x2, y2 = points[j]
                x3, y3 = points[k]
                area = 0.5 * abs((x1 * (y2 - y3) + x2 * (y3 - y1) + x3 * (y1 - y2)))
                max_area = max(max_area, area)

    return max_area
```

## 3. Solution Explanation:
- The function `largestTriangleArea` takes a list of points as input and returns the area of the largest triangle formed by any three different points.
- The function computes the cross product for all possible combinations of three points and takes the maximum.
- The cross product is computed using the formula:
```
area = 0.5 * abs((x1 * (y2 - y3) + x2 * (y3 - y1) + x3 * (y1 - y2)))
```
where `(x1, y1)`, `(x2, y2)`, and `(x3, y3)` are the coordinates of the three points.
- The absolute value of the cross product is used to ensure that the area is positive.
- The maximum area is then returned as the result.

## 4. Complexity Analysis:
- Time complexity: O(n^3) - The function computes the cross product for all possible combinations of three points, so the time complexity is O(n^3), where n is the number of points in the input list.
- Space complexity: O(1) - The function does not use any additional data structures, so the space complexity is O(1).

## Topics
Array, Math, Geometry

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-15
