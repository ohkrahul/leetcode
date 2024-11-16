# Game of Life

## Problem Link
[LeetCode - Game of Life](https://leetcode.com/problems/game-of-life/)

## Difficulty
Medium

## Problem Description
<p>According to&nbsp;<a href="https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life" target="_blank">Wikipedia&#39;s article</a>: &quot;The <b>Game of Life</b>, also known simply as <b>Life</b>, is a cellular automaton devised by the British mathematician John Horton Conway in 1970.&quot;</p>

<p>The board is made up of an <code>m x n</code> grid of cells, where each cell has an initial state: <b>live</b> (represented by a <code>1</code>) or <b>dead</b> (represented by a <code>0</code>). Each cell interacts with its <a href="https://en.wikipedia.org/wiki/Moore_neighborhood" target="_blank">eight neighbors</a> (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):</p>

<ol>
	<li>Any live cell with fewer than two live neighbors dies as if caused by under-population.</li>
	<li>Any live cell with two or three live neighbors lives on to the next generation.</li>
	<li>Any live cell with more than three live neighbors dies, as if by over-population.</li>
	<li>Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.</li>
</ol>

<p><span>The next state is created by applying the above rules simultaneously to every cell in the current state, where births and deaths occur simultaneously. Given the current state of the <code>m x n</code> grid <code>board</code>, return <em>the next state</em>.</span></p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/12/26/grid1.jpg" style="width: 562px; height: 322px;" />
<pre>
<strong>Input:</strong> board = [[0,1,0],[0,0,1],[1,1,1],[0,0,0]]
<strong>Output:</strong> [[0,0,0],[1,0,1],[0,1,1],[0,1,0]]
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/12/26/grid2.jpg" style="width: 402px; height: 162px;" />
<pre>
<strong>Input:</strong> board = [[1,1],[1,0]]
<strong>Output:</strong> [[1,1],[1,1]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == board.length</code></li>
	<li><code>n == board[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 25</code></li>
	<li><code>board[i][j]</code> is <code>0</code> or <code>1</code>.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong></p>

<ul>
	<li>Could you solve it in-place? Remember that the board needs to be updated simultaneously: You cannot update some cells first and then use their updated values to update other cells.</li>
	<li>In this question, we represent the board using a 2D array. In principle, the board is infinite, which would cause problems when the active area encroaches upon the border of the array (i.e., live cells reach the border). How would you address these problems?</li>
</ul>


## Test Cases
```
[[0,1,0],[0,0,1],[1,1,1],[0,0,0]]
[[1,1],[1,0]]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**
   - **Problem analysis:** The task is to simulate the Game of Life based on the given rules and update the grid accordingly.
   - **Key observations:**
     - The grid is finite, so we don't need to consider edge cases or infinite boundaries.
     - We can modify the existing grid in-place without creating a copy.
   - **Possible approaches:**
     - **Brute force:** Iterate over each cell and apply the rules.
     - **Efficient:** Use a "lookahead" strategy to avoid redundant computations.

2. **Solution Implementation:**
```python
class Solution:
    def gameOfLife(self, board: List[List[int]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        # Initialize a copy of the board to store the next state
        next_board = [[0] * len(board[0]) for _ in range(len(board))]
        
        # Iterate over each cell
        for i in range(len(board)):
            for j in range(len(board[0])):
                # Count the number of live neighbors
                neighbors = self.count_neighbors(board, i, j)
                
                # Apply the rules of the Game of Life
                if board[i][j] == 1:
                    # Live cell
                    if neighbors < 2 or neighbors > 3:
                        next_board[i][j] = 0  # Dies
                    else:
                        next_board[i][j] = 1  # Lives
                else:
                    # Dead cell
                    if neighbors == 3:
                        next_board[i][j] = 1  # Becomes alive
        
        # Update the original board with the next state
        for i in range(len(board)):
            for j in range(len(board[0])):
                board[i][j] = next_board[i][j]
                
    def count_neighbors(self, board, i, j):
        # Initialize the neighbor count to 0
        neighbors = 0
        
        # Iterate over the 8 neighboring cells
        for x in range(max(0, i-1), min(len(board), i+2)):
            for y in range(max(0, j-1), min(len(board[0]), j+2)):
                # Skip the current cell
                if x == i and y == j:
                    continue
                
                # Count the live neighbors
                if board[x][y] == 1:
                    neighbors += 1
        
        # Return the neighbor count
        return neighbors
```

3. **Solution Explanation:**
   - The solution follows an "efficient" approach using a lookahead strategy.
   - It creates a copy of the original board, `next_board`, which stores the next state of the grid.
   - For each cell in the board, it counts the number of live neighbors using the `count_neighbors` function.
   - Based on the Game of Life rules, it updates the next state of the cell accordingly:
     - If a live cell has fewer than two or more than three live neighbors, it dies (next state is 0).
     - If a live cell has exactly two or three neighbors, it lives (next state is 1).
     - If a dead cell has exactly three neighbors, it becomes alive (next state is 1).
   - Finally, the `next_board` is copied back to the original `board` to update the grid.

4. **Complexity Analysis:**
   - **Time complexity:** O(mn), where m and n are the number of rows and columns in the grid. We iterate through each cell and its neighbors, resulting in O(mn) time complexity.
   - **Space complexity:** O(mn). We create a copy of the grid, which takes additional memory proportional to the grid size.

## Topics
Array, Matrix, Simulation

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-11-16
