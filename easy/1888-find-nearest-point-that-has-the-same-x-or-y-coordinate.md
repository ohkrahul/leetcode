# Find Nearest Point That Has the Same X or Y Coordinate

## Problem Link
[LeetCode - Find Nearest Point That Has the Same X or Y Coordinate](https://leetcode.com/problems/find-nearest-point-that-has-the-same-x-or-y-coordinate/)

## Difficulty
Easy

## Problem Description
<p>You are given two integers, <code>x</code> and <code>y</code>, which represent your current location on a Cartesian grid: <code>(x, y)</code>. You are also given an array <code>points</code> where each <code>points[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> represents that a point exists at <code>(a<sub>i</sub>, b<sub>i</sub>)</code>. A point is <strong>valid</strong> if it shares the same x-coordinate or the same y-coordinate as your location.</p>

<p>Return <em>the index <strong>(0-indexed)</strong> of the <strong>valid</strong> point with the smallest <strong>Manhattan distance</strong> from your current location</em>. If there are multiple, return <em>the valid point with the <strong>smallest</strong> index</em>. If there are no valid points, return <code>-1</code>.</p>

<p>The <strong>Manhattan distance</strong> between two points <code>(x<sub>1</sub>, y<sub>1</sub>)</code> and <code>(x<sub>2</sub>, y<sub>2</sub>)</code> is <code>abs(x<sub>1</sub> - x<sub>2</sub>) + abs(y<sub>1</sub> - y<sub>2</sub>)</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> x = 3, y = 4, points = [[1,2],[3,1],[2,4],[2,3],[4,4]]
<strong>Output:</strong> 2
<strong>Explanation:</strong> Of all the points, only [3,1], [2,4] and [4,4] are valid. Of the valid points, [2,4] and [4,4] have the smallest Manhattan distance from your current location, with a distance of 1. [2,4] has the smallest index, so return 2.</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> x = 3, y = 4, points = [[3,4]]
<strong>Output:</strong> 0
<strong>Explanation:</strong> The answer is allowed to be on the same location as your current location.</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> x = 3, y = 4, points = [[2,3]]
<strong>Output:</strong> -1
<strong>Explanation:</strong> There are no valid points.</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= points.length &lt;= 10<sup>4</sup></code></li>
	<li><code>points[i].length == 2</code></li>
	<li><code>1 &lt;= x, y, a<sub>i</sub>, b<sub>i</sub> &lt;= 10<sup>4</sup></code></li>
</ul>


## Test Cases
```
3
4
[[1,2],[3,1],[2,4],[2,3],[4,4]]
3
4
[[3,4]]
3
4
[[2,3]]
```

## Initial Template
```python
# Code template not available
```

## Solution
## Initial Thoughts:

- This problem requires us to find the nearest point to our current location that shares the same x or y coordinate.
- A simple approach is to iterate through all points and compute the Manhattan distance for each point. Then return the index of the point with the smallest distance.
- We can optimize this approach by leveraging the fact that the points share either x or y coordinates.
- We can first check if any point shares the same x coordinate and compute the Manhattan distance. If there is no such point, then we check for points with the same y coordinate.
- This optimization reduces the number of points we need to check, resulting in better time efficiency.

## Solution Implementation:

```python
def nearestValidPoint(x: int, y: int, points: List[List[int]]) -> int:
    min_dist = float('inf')
    min_idx = -1

    for i, point in enumerate(points):
        if point[0] == x or point[1] == y:
            dist = abs(point[0] - x) + abs(point[1] - y)
            if dist < min_dist:
                min_dist = dist
                min_idx = i

    return min_idx
```

## Solution Explanation:

The solution iterates over each point in the `points` array. For each point, it checks if it shares the same x coordinate or y coordinate as our current location. If it does, it computes the Manhattan distance and stores it in the `dist` variable.

The `min_dist` variable keeps track of the minimum distance found so far. If the current `dist` is less than `min_dist`, then we update `min_dist` and `min_idx`.

Finally, we return the `min_idx`, which represents the index of the nearest valid point to our current location.

## Complexity Analysis:

- Time complexity: O(n), where n is the number of points in the `points` array. We iterate through each point once, so the time complexity is linear.
- Space complexity: O(1), since we only store a few variables in memory regardless of the input size.

## Topics
Array

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-02-07
