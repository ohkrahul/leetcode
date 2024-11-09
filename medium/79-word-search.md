# Word Search

## Problem Link
[LeetCode - Word Search](https://leetcode.com/problems/word-search/)

## Difficulty
Medium

## Problem Description
<p>Given an <code>m x n</code> grid of characters <code>board</code> and a string <code>word</code>, return <code>true</code> <em>if</em> <code>word</code> <em>exists in the grid</em>.</p>

<p>The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/04/word2.jpg" style="width: 322px; height: 242px;" />
<pre>
<strong>Input:</strong> board = [[&quot;A&quot;,&quot;B&quot;,&quot;C&quot;,&quot;E&quot;],[&quot;S&quot;,&quot;F&quot;,&quot;C&quot;,&quot;S&quot;],[&quot;A&quot;,&quot;D&quot;,&quot;E&quot;,&quot;E&quot;]], word = &quot;ABCCED&quot;
<strong>Output:</strong> true
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg" style="width: 322px; height: 242px;" />
<pre>
<strong>Input:</strong> board = [[&quot;A&quot;,&quot;B&quot;,&quot;C&quot;,&quot;E&quot;],[&quot;S&quot;,&quot;F&quot;,&quot;C&quot;,&quot;S&quot;],[&quot;A&quot;,&quot;D&quot;,&quot;E&quot;,&quot;E&quot;]], word = &quot;SEE&quot;
<strong>Output:</strong> true
</pre>

<p><strong class="example">Example 3:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/15/word3.jpg" style="width: 322px; height: 242px;" />
<pre>
<strong>Input:</strong> board = [[&quot;A&quot;,&quot;B&quot;,&quot;C&quot;,&quot;E&quot;],[&quot;S&quot;,&quot;F&quot;,&quot;C&quot;,&quot;S&quot;],[&quot;A&quot;,&quot;D&quot;,&quot;E&quot;,&quot;E&quot;]], word = &quot;ABCB&quot;
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == board.length</code></li>
	<li><code>n = board[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 6</code></li>
	<li><code>1 &lt;= word.length &lt;= 15</code></li>
	<li><code>board</code> and <code>word</code> consists of only lowercase and uppercase English letters.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Could you use search pruning to make your solution faster with a larger <code>board</code>?</p>


## Test Cases
```
[["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]]
"ABCCED"
[["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]]
"SEE"
[["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]]
"ABCB"
```

## Initial Template
```python
# Code template not available
```

## Solution
### 1. Initial Thoughts:
- The problem is to find a given word in a grid of letters. The word can be made of letters from adjacent cells, where adjacent means horizontally or vertically neighbouring.
- Since we are allowed to visit the same cell multiple times, a naive solution is to start at each cell in the grid and check if there is a path to the end of the word.
- For each cell we visit, we would perform a Depth First Search (DFS) to check if there is a path to the end of the word. This would result in a DFS of $m \times n \times k$, where $m$ and $n$ are the size of the grid and $k$ is the length of the word.
- We can prune the DFS by keeping track of the cells that we have visited and checking if we have visited the same cell twice. If we have visited the same cell twice, then the DFS is bound to fail and we can stop exploring that path.

### 2. Solution Implementation:
```python
def exist(board, word):
    """
    :type board: List[List[str]]
    :type word: str
    :rtype: bool
    """
    
    # Function to check if there is a path from the given cell to the end of the word.
    def dfs(row, col, word_index):
        # If we have reached the end of the word, then we have found a valid path.
        if word_index == len(word):
            return True

        # If we have gone out of bounds or we have visited this cell before, then we cannot proceed further.
        if row < 0 or row >= len(board) or col < 0 or col >= len(board[0]) or board[row][col] != word[word_index]:
            return False

        # Mark the current cell as visited.
        temp, board[row][col] = board[row][col], '/'
        
        # Check if there is a path from the current cell to the end of the word. If there is, return True. Otherwise, backtrack and mark the current cell as unvisited.
        found = dfs(row + 1, col, word_index + 1) or dfs(row - 1, col, word_index + 1) or dfs(row, col + 1, word_index + 1) or dfs(row, col - 1, word_index + 1)
        board[row][col] = temp
        return found

    # Iterate over each cell in the grid.
    for row in range(len(board)):
        for col in range(len(board[0])):
            # If the current cell matches the first letter of the word, then perform a DFS to check if there is a path to the end of the word. If there is, return True.
            if board[row][col] == word[0] and dfs(row, col, 0):
                return True

    # If we have not found a path to the end of the word, then return False.
    return False

```

### 3. Solution Explanation:
- The solution is a Depth First Search (DFS) with pruning.
- We iterate over each cell in the grid. For each cell, we check if it matches the first letter of the word. If it does, we perform a DFS to check if there is a path to the end of the word.
- The DFS function takes three parameters: the row and column of the current cell, and the index of the letter in the word that we are currently trying to match.
- The DFS function checks if we have reached the end of the word. If we have, then we have found a valid path and we return True.
- The DFS function also checks if we have gone out of bounds or we have visited the current cell before. If we have, then we cannot proceed further and we return False.
- If we have not reached the end of the word and we have not gone out of bounds or visited the current cell before, then we mark the current cell as visited and check if there is a path from the current cell to the end of the word. If there is, we return True. Otherwise, we backtrack and mark the current cell as unvisited.
- If we have iterated over all the cells in the grid and we have not found a path to the end of the word, then we return False.

### 4. Complexity Analysis:
- Time complexity: $m \times n \times k$, where $m$ and $n$ are the size of the grid and $k$ is the length of the word. We can consider each cell as the root of a DFS tree, and since we can visit each cell at most once, we can prune the search tree by keeping track of the visited cells.
- Space complexity: $k$, as we need to store the path from the start to the current cell.

## Topics
Array, String, Backtracking, Matrix

Solved on: 2024-11-09
