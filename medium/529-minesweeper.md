# Minesweeper

## Problem Link
[LeetCode - Minesweeper](https://leetcode.com/problems/minesweeper/)

## Difficulty
Medium

## Problem Description
<p>Let&#39;s play the minesweeper game (<a href="https://en.wikipedia.org/wiki/Minesweeper_(video_game)" target="_blank">Wikipedia</a>, <a href="http://minesweeperonline.com" target="_blank">online game</a>)!</p>

<p>You are given an <code>m x n</code> char matrix <code>board</code> representing the game board where:</p>

<ul>
	<li><code>&#39;M&#39;</code> represents an unrevealed mine,</li>
	<li><code>&#39;E&#39;</code> represents an unrevealed empty square,</li>
	<li><code>&#39;B&#39;</code> represents a revealed blank square that has no adjacent mines (i.e., above, below, left, right, and all 4 diagonals),</li>
	<li>digit (<code>&#39;1&#39;</code> to <code>&#39;8&#39;</code>) represents how many mines are adjacent to this revealed square, and</li>
	<li><code>&#39;X&#39;</code> represents a revealed mine.</li>
</ul>

<p>You are also given an integer array <code>click</code> where <code>click = [click<sub>r</sub>, click<sub>c</sub>]</code> represents the next click position among all the unrevealed squares (<code>&#39;M&#39;</code> or <code>&#39;E&#39;</code>).</p>

<p>Return <em>the board after revealing this position according to the following rules</em>:</p>

<ol>
	<li>If a mine <code>&#39;M&#39;</code> is revealed, then the game is over. You should change it to <code>&#39;X&#39;</code>.</li>
	<li>If an empty square <code>&#39;E&#39;</code> with no adjacent mines is revealed, then change it to a revealed blank <code>&#39;B&#39;</code> and all of its adjacent unrevealed squares should be revealed recursively.</li>
	<li>If an empty square <code>&#39;E&#39;</code> with at least one adjacent mine is revealed, then change it to a digit (<code>&#39;1&#39;</code> to <code>&#39;8&#39;</code>) representing the number of adjacent mines.</li>
	<li>Return the board when no more squares will be revealed.</li>
</ol>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img src="https://assets.leetcode.com/uploads/2023/08/09/untitled.jpeg" style="width: 500px; max-width: 400px; height: 269px;" />
<pre>
<strong>Input:</strong> board = [[&quot;E&quot;,&quot;E&quot;,&quot;E&quot;,&quot;E&quot;,&quot;E&quot;],[&quot;E&quot;,&quot;E&quot;,&quot;M&quot;,&quot;E&quot;,&quot;E&quot;],[&quot;E&quot;,&quot;E&quot;,&quot;E&quot;,&quot;E&quot;,&quot;E&quot;],[&quot;E&quot;,&quot;E&quot;,&quot;E&quot;,&quot;E&quot;,&quot;E&quot;]], click = [3,0]
<strong>Output:</strong> [[&quot;B&quot;,&quot;1&quot;,&quot;E&quot;,&quot;1&quot;,&quot;B&quot;],[&quot;B&quot;,&quot;1&quot;,&quot;M&quot;,&quot;1&quot;,&quot;B&quot;],[&quot;B&quot;,&quot;1&quot;,&quot;1&quot;,&quot;1&quot;,&quot;B&quot;],[&quot;B&quot;,&quot;B&quot;,&quot;B&quot;,&quot;B&quot;,&quot;B&quot;]]
</pre>

<p><strong class="example">Example 2:</strong></p>
<img src="https://assets.leetcode.com/uploads/2023/08/09/untitled-2.jpeg" style="width: 489px; max-width: 400px; height: 269px;" />
<pre>
<strong>Input:</strong> board = [[&quot;B&quot;,&quot;1&quot;,&quot;E&quot;,&quot;1&quot;,&quot;B&quot;],[&quot;B&quot;,&quot;1&quot;,&quot;M&quot;,&quot;1&quot;,&quot;B&quot;],[&quot;B&quot;,&quot;1&quot;,&quot;1&quot;,&quot;1&quot;,&quot;B&quot;],[&quot;B&quot;,&quot;B&quot;,&quot;B&quot;,&quot;B&quot;,&quot;B&quot;]], click = [1,2]
<strong>Output:</strong> [[&quot;B&quot;,&quot;1&quot;,&quot;E&quot;,&quot;1&quot;,&quot;B&quot;],[&quot;B&quot;,&quot;1&quot;,&quot;X&quot;,&quot;1&quot;,&quot;B&quot;],[&quot;B&quot;,&quot;1&quot;,&quot;1&quot;,&quot;1&quot;,&quot;B&quot;],[&quot;B&quot;,&quot;B&quot;,&quot;B&quot;,&quot;B&quot;,&quot;B&quot;]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == board.length</code></li>
	<li><code>n == board[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 50</code></li>
	<li><code>board[i][j]</code> is either <code>&#39;M&#39;</code>, <code>&#39;E&#39;</code>, <code>&#39;B&#39;</code>, or a digit from <code>&#39;1&#39;</code> to <code>&#39;8&#39;</code>.</li>
	<li><code>click.length == 2</code></li>
	<li><code>0 &lt;= click<sub>r</sub> &lt; m</code></li>
	<li><code>0 &lt;= click<sub>c</sub> &lt; n</code></li>
	<li><code>board[click<sub>r</sub>][click<sub>c</sub>]</code> is either <code>&#39;M&#39;</code> or <code>&#39;E&#39;</code>.</li>
</ul>


## Test Cases
```
[["E","E","E","E","E"],["E","E","M","E","E"],["E","E","E","E","E"],["E","E","E","E","E"]]
[3,0]
[["B","1","E","1","B"],["B","1","M","1","B"],["B","1","1","1","B"],["B","B","B","B","B"]]
[1,2]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**

   - **Problem analysis:** The minesweeper game is a classic puzzle where the player has to uncover mines hidden on a grid while avoiding getting blown up.
   - **Key observations:**
     - The game board is represented as a matrix, where each cell can be either a mine ('M'), an empty square ('E'), or a revealed square with a number indicating the number of adjacent mines ('1' to '8').
     - The game is played by clicking on cells to uncover them.
     - If a mine is clicked, the game is over and the mine is revealed with an 'X'.
     - If an empty square is clicked, it is revealed with a 'B' and all adjacent unrevealed squares are recursively uncovered if they are also empty.
   - **Possible approaches:**
     - Depth-first search (DFS): Start from the clicked cell and recursively explore all adjacent cells, updating the board as needed.
     - Breadth-first search (BFS): Start from the clicked cell and explore all adjacent cells at the same level, updating the board as needed.

2. **Solution Implementation:**

```python
class Solution:
    def updateBoard(self, board: List[List[str]], click: List[int]) -> List[List[str]]:
        r, c = click
        
        # If we clicked on a mine, game over
        if board[r][c] == 'M':
            board[r][c] = 'X'
            return board
        
        # If we clicked on an empty square
        elif board[r][c] == 'E':
            self.dfs(board, r, c)
        
        # If we clicked on a number, nothing to do
        return board
    
    def dfs(self, board: List[List[str]], r: int, c: int):
        # Check if out of bounds or already visited
        if not (0 <= r < len(board) and 0 <= c < len(board[0])) or board[r][c] != 'E':
            return
        
        # Count number of adjacent mines
        num_mines = 0
        for i in range(max(0, r-1), min(len(board), r+2)):
            for j in range(max(0, c-1), min(len(board[0]), c+2)):
                if board[i][j] == 'M':
                    num_mines += 1
        
        # Update board
        if num_mines == 0:
            board[r][c] = 'B'
            # Recursively explore adjacent cells
            for i in range(max(0, r-1), min(len(board), r+2)):
                for j in range(max(0, c-1), min(len(board[0]), c+2)):
                    self.dfs(board, i, j)
        else:
            board[r][c] = str(num_mines)
```

3. **Solution Explanation:**

   - Our solution uses a depth-first search (DFS) approach to explore the board recursively.
   - We start by checking if the clicked cell is a mine. If it is, we update the board to 'X' and return.
   - If the clicked cell is an empty square, we call the `dfs` function to explore all adjacent cells.
   - In the `dfs` function, we check if the current cell is out of bounds or has already been visited. If not, we count the number of adjacent mines.
   - If there are no adjacent mines, we update the cell to 'B' and recursively explore all adjacent cells.
   - If there are adjacent mines, we update the cell to the number of adjacent mines.

4. **Complexity Analysis:**

   - Time complexity: O(R * C), where R and C are the number of rows and columns in the board. We visit each cell at most once.
   - Space complexity: O(R * C), for the recursion stack.

## Topics
Array, Depth-First Search, Breadth-First Search, Matrix

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-02-04
