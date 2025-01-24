# Find the Number of Distinct Colors Among the Balls

## Problem Link
[LeetCode - Find the Number of Distinct Colors Among the Balls](https://leetcode.com/problems/find-the-number-of-distinct-colors-among-the-balls/)

## Difficulty
Medium

## Problem Description
<p>You are given an integer <code>limit</code> and a 2D array <code>queries</code> of size <code>n x 2</code>.</p>

<p>There are <code>limit + 1</code> balls with <strong>distinct</strong> labels in the range <code>[0, limit]</code>. Initially, all balls are uncolored. For every query in <code>queries</code> that is of the form <code>[x, y]</code>, you mark ball <code>x</code> with the color <code>y</code>. After each query, you need to find the number of <strong>distinct</strong> colors among the balls.</p>

<p>Return an array <code>result</code> of length <code>n</code>, where <code>result[i]</code> denotes the number of distinct colors <em>after</em> <code>i<sup>th</sup></code> query.</p>

<p><strong>Note</strong> that when answering a query, lack of a color <em>will not</em> be considered as a color.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">limit = 4, queries = [[1,4],[2,5],[1,3],[3,4]]</span></p>

<p><strong>Output:</strong> <span class="example-io">[1,2,2,3]</span></p>

<p><strong>Explanation:</strong></p>

<p><img alt="" src="https://assets.leetcode.com/uploads/2024/04/17/ezgifcom-crop.gif" style="width: 455px; height: 145px;" /></p>

<ul>
	<li>After query 0, ball 1 has color 4.</li>
	<li>After query 1, ball 1 has color 4, and ball 2 has color 5.</li>
	<li>After query 2, ball 1 has color 3, and ball 2 has color 5.</li>
	<li>After query 3, ball 1 has color 3, ball 2 has color 5, and ball 3 has color 4.</li>
</ul>
</div>

<p><strong class="example">Example 2:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">limit = 4, queries = [[0,1],[1,2],[2,2],[3,4],[4,5]]</span></p>

<p><strong>Output:</strong> <span class="example-io">[1,2,2,3,4]</span></p>

<p><strong>Explanation:</strong></p>

<p><strong><img alt="" src="https://assets.leetcode.com/uploads/2024/04/17/ezgifcom-crop2.gif" style="width: 457px; height: 144px;" /></strong></p>

<ul>
	<li>After query 0, ball 0 has color 1.</li>
	<li>After query 1, ball 0 has color 1, and ball 1 has color 2.</li>
	<li>After query 2, ball 0 has color 1, and balls 1 and 2 have color 2.</li>
	<li>After query 3, ball 0 has color 1, balls 1 and 2 have color 2, and ball 3 has color 4.</li>
	<li>After query 4, ball 0 has color 1, balls 1 and 2 have color 2, ball 3 has color 4, and ball 4 has color 5.</li>
</ul>
</div>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= limit &lt;= 10<sup>9</sup></code></li>
	<li><code>1 &lt;= n == queries.length &lt;= 10<sup>5</sup></code></li>
	<li><code>queries[i].length == 2</code></li>
	<li><code>0 &lt;= queries[i][0] &lt;= limit</code></li>
	<li><code>1 &lt;= queries[i][1] &lt;= 10<sup>9</sup></code></li>
</ul>


## Test Cases
```
4
[[1,4],[2,5],[1,3],[3,4]]
4
[[0,1],[1,2],[2,2],[3,4],[4,5]]
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts

### Overview
The problem asks us to find the number of distinct colors among balls after each query. We are given an array of queries where each query is of the form [x, y], which means we need to mark ball x with color y. After each query, we need to determine the number of distinct colors among the marked balls.

### Observations
* The number of balls is equal to limit + 1.
* The initial color of all balls is uncolored, which is not considered a color when counting distinct colors.
* Each query marks a ball with a specific color.
* We only need to keep track of the colors that have been used to mark balls.

### Approaches
* **Naive Approach:**
    * For each query, iterate over all balls and check if the ball has been marked with a color. If so, add the color to a set of colors. The number of distinct colors is the size of the set.
    * This approach has a time complexity of O(n * limit), where n is the number of queries and limit is the number of balls.
* **Optimized Approach:**
    * Use a hash map to store the colors that have been used to mark balls.
    * For each query, add the color to the hash map if it does not exist. The number of distinct colors is the size of the hash map.
    * This approach has a time complexity of O(n), where n is the number of queries.

## 2. Solution Implementation
```python
from collections import defaultdict

def count_distinct_colors(limit, queries):
  """
  Finds the number of distinct colors among the balls after each query.

  Args:
    limit: The number of balls.
    queries: A list of queries in the form [x, y], where x is the ball to be marked and y is the color to mark it with.

  Returns:
    A list of integers representing the number of distinct colors after each query.
  """

  # Create a hash map to store the colors that have been used to mark balls.
  color_map = defaultdict(int)

  # Initialize the result array to store the number of distinct colors after each query.
  result = []

  # Iterate over the queries and mark balls with colors.
  for query in queries:
    # Extract the ball and color from the query.
    ball, color = query

    # Add the color to the hash map if it does not exist.
    if color not in color_map:
      color_map[color] = 1

    # Update the result array with the number of distinct colors.
    result.append(len(color_map))

  # Return the result array.
  return result
```

## 3. Solution Explanation
The solution first creates a hash map to store the colors that have been used to mark balls. It then iterates over the queries and marks balls with colors. For each query, it checks if the color does not already exist in the hash map, and if not, it adds the color to the hash map. It then updates the result array with the number of distinct colors. The result array is returned at the end.

## 4. Complexity Analysis
* **Time Complexity:** O(n), where n is the number of queries. The solution iterates over the queries once, and each query takes constant time to process.
* **Space Complexity:** O(limit), where limit is the number of balls. The solution stores the colors that have been used to mark balls in a hash map, and the size of the hash map is at most limit + 1.

## Topics
Array, Hash Table, Simulation

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-24
