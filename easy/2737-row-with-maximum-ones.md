# Row With Maximum Ones

## Problem Link
[LeetCode - Row With Maximum Ones](https://leetcode.com/problems/row-with-maximum-ones/)

## Difficulty
Easy

## Problem Description
<p>Given a <code>m x n</code> binary matrix <code>mat</code>, find the <strong>0-indexed</strong> position of the row that contains the <strong>maximum</strong> count of <strong>ones,</strong> and the number of ones in that row.</p>

<p>In case there are multiple rows that have the maximum count of ones, the row with the <strong>smallest row number</strong> should be selected.</p>

<p>Return<em> an array containing the index of the row, and the number of ones in it.</em></p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> mat = [[0,1],[1,0]]
<strong>Output:</strong> [0,1]
<strong>Explanation:</strong> Both rows have the same number of 1&#39;s. So we return the index of the smaller row, 0, and the maximum count of ones (1<code>)</code>. So, the answer is [0,1]. 
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> mat = [[0,0,0],[0,1,1]]
<strong>Output:</strong> [1,2]
<strong>Explanation:</strong> The row indexed 1 has the maximum count of ones <code>(2)</code>. So we return its index, <code>1</code>, and the count. So, the answer is [1,2].
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> mat = [[0,0],[1,1],[0,0]]
<strong>Output:</strong> [1,2]
<strong>Explanation:</strong> The row indexed 1 has the maximum count of ones (2). So the answer is [1,2].
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == mat.length</code>&nbsp;</li>
	<li><code>n == mat[i].length</code>&nbsp;</li>
	<li><code>1 &lt;= m, n &lt;= 100</code>&nbsp;</li>
	<li><code>mat[i][j]</code> is either <code>0</code> or <code>1</code>.</li>
</ul>


## Test Cases
```
[[0,1],[1,0]]
[[0,0,0],[0,1,1]]
[[0,0],[1,1],[0,0]]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:

- This problem requires us to find the row in a binary matrix with the maximum number of ones.
- We need to return both the row index and the count of ones in that row.
- A straightforward approach is to iterate through each row and count the number of ones.

2. Solution Implementation:
```python
def find_row_with_max_ones(mat):
  """
  :type mat: List[List[int]]
  :rtype: List[int]
  """
  # Initialize the result with the first row as default
  res = [0, mat[0].count(1)]

  # Iterate through each row starting from the second row
  for i in range(1, len(mat)):
    # Count the number of ones in the current row
    count = mat[i].count(1)

    # Update the result if the current row has more ones
    if count > res[1]:
      res = [i, count]

  # Return the result
  return res
```

3. Solution Explanation:

- The solution initializes the result with the first row as default, assuming it has the maximum number of ones initially.
- It then iterates through each row starting from the second row and counts the number of ones in each row.
- If the current row has more ones than the previous maximum, the result is updated to contain the current row index and the count of ones.
- Finally, the result is returned, containing the row index and the count of ones in the row with the maximum number of ones.

4. Complexity Analysis:

- Time complexity: O(m * n), where m is the number of rows and n is the number of columns in the matrix. This is because we need to iterate through each row and count the number of ones in each row.
- Space complexity: O(1), as we only need to store the result, which is a constant size.

## Topics
Array, Matrix

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-11-14
