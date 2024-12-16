# Diagonal Traverse

## Problem Link
[LeetCode - Diagonal Traverse](https://leetcode.com/problems/diagonal-traverse/)

## Difficulty
Medium

## Problem Description
<p>Given an <code>m x n</code> matrix <code>mat</code>, return <em>an array of all the elements of the array in a diagonal order</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/04/10/diag1-grid.jpg" style="width: 334px; height: 334px;" />
<pre>
<strong>Input:</strong> mat = [[1,2,3],[4,5,6],[7,8,9]]
<strong>Output:</strong> [1,2,4,7,5,3,6,8,9]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> mat = [[1,2],[3,4]]
<strong>Output:</strong> [1,2,3,4]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == mat.length</code></li>
	<li><code>n == mat[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 10<sup>4</sup></code></li>
	<li><code>1 &lt;= m * n &lt;= 10<sup>4</sup></code></li>
	<li><code>-10<sup>5</sup> &lt;= mat[i][j] &lt;= 10<sup>5</sup></code></li>
</ul>


## Test Cases
```
[[1,2,3],[4,5,6],[7,8,9]]
[[1,2],[3,4]]
```

## Initial Template
```python
# Code template not available
```

## Solution
## Initial Thoughts:
- The problem requires us to traverse the matrix diagonally.
- We can start from the top-left corner and move towards the bottom-right corner while collecting elements from the diagonal.
- We need to handle the cases where we reach the end of a row or column.

## Solution Implementation:
```python
def findDiagonalOrder(mat):
  """
  :type mat: List[List[int]]
  :rtype: List[int]
  """
  # Initialize the result list
  result = []

  # Initialize the row and column indices
  row, col = 0, 0

  # Initialize the direction (up or down)
  direction = 1

  # Continue until we reach the end of the matrix
  while row < len(mat) and col < len(mat[0]):
    # Add the current element to the result
    result.append(mat[row][col])

    # Update the row and column indices based on the direction
    if direction == 1:
      row -= 1
      col += 1
    else:
      row += 1
      col -= 1

    # Handle the cases where we reach the end of a row or column
    if row < 0 or row >= len(mat) or col < 0 or col >= len(mat[0]):
      # Change the direction
      direction *= -1

      # Update the row and column indices
      if direction == 1:
        row += 1
      else:
        col += 1

  # Return the result
  return result
```

## Solution Explanation:
- We start from the top-left corner of the matrix.
- We move towards the bottom-right corner while collecting elements from the diagonal.
- We handle the cases where we reach the end of a row or column by changing the direction and updating the row and column indices.
- We repeat this process until we reach the end of the matrix.
- Finally, we return the result list containing the elements from the diagonal.

## Complexity Analysis:
- Time complexity: O(m * n), where m and n are the number of rows and columns in the matrix.
- Space complexity: O(1), as we only use a constant amount of extra space.

## Topics
Array, Matrix, Simulation

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-12-16
