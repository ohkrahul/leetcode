# Check if Word Can Be Placed In Crossword

## Problem Link
[LeetCode - Check if Word Can Be Placed In Crossword](https://leetcode.com/problems/check-if-word-can-be-placed-in-crossword/)

## Difficulty
Medium

## Problem Description
<p>You are given an <code>m x n</code> matrix <code>board</code>, representing the<strong> current </strong>state of a crossword puzzle. The crossword contains lowercase English letters (from solved words), <code>&#39; &#39;</code> to represent any <strong>empty </strong>cells, and <code>&#39;#&#39;</code> to represent any <strong>blocked</strong> cells.</p>

<p>A word can be placed<strong> horizontally</strong> (left to right <strong>or</strong> right to left) or <strong>vertically</strong> (top to bottom <strong>or</strong> bottom to top) in the board if:</p>

<ul>
	<li>It does not occupy a cell containing the character <code>&#39;#&#39;</code>.</li>
	<li>The cell each letter is placed in must either be <code>&#39; &#39;</code> (empty) or <strong>match</strong> the letter already on the <code>board</code>.</li>
	<li>There must not be any empty cells <code>&#39; &#39;</code> or other lowercase letters <strong>directly left or right</strong><strong> </strong>of the word if the word was placed <strong>horizontally</strong>.</li>
	<li>There must not be any empty cells <code>&#39; &#39;</code> or other lowercase letters <strong>directly above or below</strong> the word if the word was placed <strong>vertically</strong>.</li>
</ul>

<p>Given a string <code>word</code>, return <code>true</code><em> if </em><code>word</code><em> can be placed in </em><code>board</code><em>, or </em><code>false</code><em> <strong>otherwise</strong></em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/10/04/crossword-ex1-1.png" style="width: 478px; height: 180px;" />
<pre>
<strong>Input:</strong> board = [[&quot;#&quot;, &quot; &quot;, &quot;#&quot;], [&quot; &quot;, &quot; &quot;, &quot;#&quot;], [&quot;#&quot;, &quot;c&quot;, &quot; &quot;]], word = &quot;abc&quot;
<strong>Output:</strong> true
<strong>Explanation:</strong> The word &quot;abc&quot; can be placed as shown above (top to bottom).
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/10/04/crossword-ex2-1.png" style="width: 180px; height: 180px;" />
<pre>
<strong>Input:</strong> board = [[&quot; &quot;, &quot;#&quot;, &quot;a&quot;], [&quot; &quot;, &quot;#&quot;, &quot;c&quot;], [&quot; &quot;, &quot;#&quot;, &quot;a&quot;]], word = &quot;ac&quot;
<strong>Output:</strong> false
<strong>Explanation:</strong> It is impossible to place the word because there will always be a space/letter above or below it.</pre>

<p><strong class="example">Example 3:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/10/04/crossword-ex3-1.png" style="width: 478px; height: 180px;" />
<pre>
<strong>Input:</strong> board = [[&quot;#&quot;, &quot; &quot;, &quot;#&quot;], [&quot; &quot;, &quot; &quot;, &quot;#&quot;], [&quot;#&quot;, &quot; &quot;, &quot;c&quot;]], word = &quot;ca&quot;
<strong>Output:</strong> true
<strong>Explanation:</strong> The word &quot;ca&quot; can be placed as shown above (right to left). 
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == board.length</code></li>
	<li><code>n == board[i].length</code></li>
	<li><code>1 &lt;= m * n &lt;= 2 * 10<sup>5</sup></code></li>
	<li><code>board[i][j]</code> will be <code>&#39; &#39;</code>, <code>&#39;#&#39;</code>, or a lowercase English letter.</li>
	<li><code>1 &lt;= word.length &lt;= max(m, n)</code></li>
	<li><code>word</code> will contain only lowercase English letters.</li>
</ul>


## Test Cases
```
[["#"," ","#"],[" "," ","#"],["#","c"," "]]
"abc"
[[" ","#","a"],[" ","#", "c"],[" ","#","a"]]
"ac"
[["#"," ","#"],[" "," ","#"],["#"," ","c"]]
"ca"
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts:

This problem can be solved using a depth-first search (DFS) approach. We can start at each empty cell and try to place the word in all possible directions (horizontally and vertically). If we can place the word without violating any of the constraints (empty cells or blocked cells), we return `True`. Otherwise, we continue the DFS until we have explored all possible placements.
```
# Initial Thoughts:
# This problem can be solved using a depth-first search (DFS) approach.
# We can start at each empty cell and try to place the word in all possible directions (horizontally and vertically).
# If we can place the word without violating any of the constraints (empty cells or blocked cells), we return True.
# Otherwise, we continue the DFS until we have explored all possible placements.
```

## 2. Solution Implementation:
```python
def placeWordInCrossword(board, word):
  # DFS function to check if the word can be placed in the board
  def dfs(r, c, i):
    if i == len(word):
      return True

    # Check if the current cell is within the bounds of the board and is empty or matches the letter in the word
    if 0 <= r < m and 0 <= c < n and (board[r][c] == ' ' or board[r][c] == word[i]):
      # Mark the current cell as visited
      original = board[r][c]
      board[r][c] = word[i]

      # Check if the word can be placed in the horizontal direction
      if dfs(r, c+1, i+1):
        return True

      # Check if the word can be placed in the vertical direction
      if dfs(r+1, c, i+1):
        return True

      # If the word cannot be placed in any direction, reset the current cell to its original value
      board[r][c] = original

    return False

  # Convert the board to a 2D list of characters
  board = [list(row) for row in board]

  # Get the dimensions of the board
  m, n = len(board), len(board[0])

  # Iterate over all the cells in the board
  for r in range(m):
    for c in range(n):
      # If the current cell is empty, try to place the word starting from this cell
      if board[r][c] == ' ':
        if dfs(r, c, 0):
          return True

  return False
```

## 3. Solution Explanation:

The `placeWordInCrossword` function takes a 2D board and a word as input. It converts the board to a 2D list of characters and gets the dimensions of the board. It then iterates over all the cells in the board and checks if the current cell is empty. If it is, it calls the `dfs` function to try to place the word starting from this cell.

The `dfs` function takes three parameters: the current row index, the current column index, and the index of the current letter in the word. It returns `True` if the word can be placed in the board starting from the current cell, and `False` otherwise.

The `dfs` function first checks if the current cell is within the bounds of the board and is empty or matches the letter in the word. If it is, it marks the current cell as visited and calls the `dfs` function again with the next row index, column index, and letter index. It checks if the word can be placed in the horizontal direction by calling the `dfs` function with the next column index and letter index. It also checks if the word can be placed in the vertical direction by calling the `dfs` function with the next row index and letter index. If the word can be placed in either direction, it returns `True`. Otherwise, it resets the current cell to its original value and returns `False`.

Finally, the `placeWordInCrossword` function returns `True` if the `dfs` function returns `True` for any of the empty cells in the board. Otherwise, it returns `False`.

## 4. Complexity Analysis:

- Time complexity: O(mn * w) - where m and n are the dimensions of the board and w is the length of the word. The `dfs` function is called at most once for each cell in the board, and each call takes O(w) time to check if the word can be placed starting from that cell.

- Space complexity: O(w) - The `dfs` function uses a stack to keep track of the cells that have been visited, and the stack can contain at most w cells.

## Topics
Array, Matrix, Enumeration

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-11-15
