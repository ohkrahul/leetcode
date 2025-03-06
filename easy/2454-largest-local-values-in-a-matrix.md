# Largest Local Values in a Matrix

## Problem Link
[LeetCode - Largest Local Values in a Matrix](https://leetcode.com/problems/largest-local-values-in-a-matrix/)

## Difficulty
Easy

## Problem Description
<p>You are given an <code>n x n</code> integer matrix <code>grid</code>.</p>

<p>Generate an integer matrix <code>maxLocal</code> of size <code>(n - 2) x (n - 2)</code> such that:</p>

<ul>
	<li><code>maxLocal[i][j]</code> is equal to the <strong>largest</strong> value of the <code>3 x 3</code> matrix in <code>grid</code> centered around row <code>i + 1</code> and column <code>j + 1</code>.</li>
</ul>

<p>In other words, we want to find the largest value in every contiguous <code>3 x 3</code> matrix in <code>grid</code>.</p>

<p>Return <em>the generated matrix</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2022/06/21/ex1.png" style="width: 371px; height: 210px;" />
<pre>
<strong>Input:</strong> grid = [[9,9,8,1],[5,6,2,6],[8,2,6,4],[6,2,2,2]]
<strong>Output:</strong> [[9,9],[8,6]]
<strong>Explanation:</strong> The diagram above shows the original matrix and the generated matrix.
Notice that each value in the generated matrix corresponds to the largest value of a contiguous 3 x 3 matrix in grid.</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2022/07/02/ex2new2.png" style="width: 436px; height: 240px;" />
<pre>
<strong>Input:</strong> grid = [[1,1,1,1,1],[1,1,1,1,1],[1,1,2,1,1],[1,1,1,1,1],[1,1,1,1,1]]
<strong>Output:</strong> [[2,2,2],[2,2,2],[2,2,2]]
<strong>Explanation:</strong> Notice that the 2 is contained within every contiguous 3 x 3 matrix in grid.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == grid.length == grid[i].length</code></li>
	<li><code>3 &lt;= n &lt;= 100</code></li>
	<li><code>1 &lt;= grid[i][j] &lt;= 100</code></li>
</ul>


## Test Cases
```
[[9,9,8,1],[5,6,2,6],[8,2,6,4],[6,2,2,2]]
[[1,1,1,1,1],[1,1,1,1,1],[1,1,2,1,1],[1,1,1,1,1],[1,1,1,1,1]]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks us to find the maximum value within each 3x3 subgrid of a given square matrix.
   - The output matrix will be (n-2)x(n-2) because we are looking at 3x3 subgrids within an nxn grid.
   - A straightforward approach is to iterate through each possible top-left corner of a 3x3 subgrid (from (0,0) to (n-3, n-3)) and find the maximum value within that 3x3 region.

2. Solution Implementation:
```python
def largestLocal(grid):
    n = len(grid)
    max_local = [[0] * (n - 2) for _ in range(n - 2)]  # Initialize the result matrix

    for i in range(n - 2):
        for j in range(n - 2):
            max_val = 0
            for row in range(i, i + 3):  # Iterate through the 3x3 subgrid
                for col in range(j, j + 3):
                    max_val = max(max_val, grid[row][col])  # Update max_val
            max_local[i][j] = max_val # Store the maximum value in the result matrix
    
    return max_local
```

3. Solution Explanation:
   - We initialize a result matrix `max_local` of size (n-2) x (n-2) filled with zeros.
   - We iterate through each possible top-left corner (i, j) of a 3x3 subgrid. The outer loops iterate from 0 to n-3 (inclusive) for both rows and columns.
   - The inner loops iterate through the rows and columns of the current 3x3 subgrid (from i to i+2 and j to j+2).
   - Inside the inner loops, we keep track of the maximum value `max_val` encountered so far within the current 3x3 subgrid.
   - After iterating through the entire 3x3 subgrid, we store `max_val` in `max_local[i][j]`.
   - Finally, we return the `max_local` matrix.

4. Complexity Analysis:
   - Time complexity: O(n^2 * 9) = O(n^2). We have nested loops. The outer two loops iterate (n-2) times each, and the inner two loops iterate 3 times each. Since the inner loop iterations are constant (9), the dominant factor is n^2.
   - Space complexity: O((n-2)^2). We create a new matrix `max_local` of size (n-2) x (n-2) to store the results. The space used is proportional to n^2.  Ignoring the constant factor, it becomes O(n^2).


## Topics
Array, Matrix

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-06
