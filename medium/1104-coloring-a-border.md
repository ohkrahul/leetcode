# Coloring A Border

## Problem Link
[LeetCode - Coloring A Border](https://leetcode.com/problems/coloring-a-border/)

## Difficulty
Medium

## Problem Description
<p>You are given an <code>m x n</code> integer matrix <code>grid</code>, and three integers <code>row</code>, <code>col</code>, and <code>color</code>. Each value in the grid represents the color of the grid square at that location.</p>

<p>Two squares are called <strong>adjacent</strong> if they are next to each other in any of the 4 directions.</p>

<p>Two squares belong to the same <strong>connected component</strong> if they have the same color and they are adjacent.</p>

<p>The <strong>border of a connected component</strong> is all the squares in the connected component that are either adjacent to (at least) a square not in the component, or on the boundary of the grid (the first or last row or column).</p>

<p>You should color the <strong>border</strong> of the <strong>connected component</strong> that contains the square <code>grid[row][col]</code> with <code>color</code>.</p>

<p>Return <em>the final grid</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> grid = [[1,1],[1,2]], row = 0, col = 0, color = 3
<strong>Output:</strong> [[3,3],[3,2]]
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> grid = [[1,2,2],[2,3,2]], row = 0, col = 1, color = 3
<strong>Output:</strong> [[1,3,3],[2,3,3]]
</pre><p><strong class="example">Example 3:</strong></p>
<pre><strong>Input:</strong> grid = [[1,1,1],[1,1,1],[1,1,1]], row = 1, col = 1, color = 2
<strong>Output:</strong> [[2,2,2],[2,1,2],[2,2,2]]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == grid.length</code></li>
	<li><code>n == grid[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 50</code></li>
	<li><code>1 &lt;= grid[i][j], color &lt;= 1000</code></li>
	<li><code>0 &lt;= row &lt; m</code></li>
	<li><code>0 &lt;= col &lt; n</code></li>
</ul>


## Test Cases
```
[[1,1],[1,2]]
0
0
3
[[1,2,2],[2,3,2]]
0
1
3
[[1,1,1],[1,1,1],[1,1,1]]
1
1
2
```

## Initial Template
```python
# Code template not available
```

## Solution
## Initial Thoughts:
- The problem asks us to recolor the border of a connected component in a grid.
- A connected component is a group of squares that have the same color and are adjacent to each other.
- The border of a connected component is the set of squares in the component that are adjacent to squares that are not in the component or are on the boundary of the grid.
- We can use depth-first search (DFS) to find the connected component that contains the given square.
- Once we have found the connected component, we can find its border by checking the squares around each square in the component.

## Solution Implementation:
```python
def colorBorder(grid: list[list[int]], row: int, col: int, color: int) -> list[list[int]]:
    """
    Colors the border of the connected component that contains the square grid[row][col] with color.

    Args:
    grid (list[list[int]]): The grid to recolor.
    row (int): The row of the square to recolor.
    col (int): The column of the square to recolor.
    color (int): The color to recolor the border with.

    Returns:
    list[list[int]]: The final grid.
    """
    # Create a set to store the squares that have been visited.
    visited = set()

    # Perform DFS to find the connected component that contains the given square.
    dfs(grid, row, col, grid[row][col], visited)

    # Find the border of the connected component.
    border = set()
    for square in visited:
        if is_on_border(grid, square[0], square[1]):
            border.add(square)
        else:
            for neighbor in get_neighbors(grid, square[0], square[1]):
                if neighbor not in visited:
                    border.add(square)
                    break

    # Recolor the border of the connected component.
    for square in border:
        grid[square[0]][square[1]] = color

    return grid


def dfs(grid: list[list[int]], row: int, col: int, target: int, visited: set):
    """
    Performs DFS to find the connected component that contains the given square.

    Args:
    grid (list[list[int]]): The grid to search.
    row (int): The row of the square to search.
    col (int): The column of the square to search.
    target (int): The target color of the connected component.
    visited (set): The set of squares that have been visited.
    """
    # Check if the square is valid and has not been visited.
    if 0 <= row < len(grid) and 0 <= col < len(grid[0]) and (row, col) not in visited:
        # Add the square to the set of visited squares.
        visited.add((row, col))

        # Check if the square has the target color.
        if grid[row][col] == target:
            # Recursively search the neighbors of the square.
            dfs(grid, row - 1, col, target, visited)
            dfs(grid, row + 1, col, target, visited)
            dfs(grid, row, col - 1, target, visited)
            dfs(grid, row, col + 1, target, visited)


def is_on_border(grid: list[list[int]], row: int, col: int) -> bool:
    """
    Checks if the square is on the border of the grid.

    Args:
    grid (list[list[int]]): The grid to check.
    row (int): The row of the square to check.
    col (int): The column of the square to check.

    Returns:
    bool: True if the square is on the border, False otherwise.
    """
    return row == 0 or row == len(grid) - 1 or col == 0 or col == len(grid[0]) - 1


def get_neighbors(grid: list[list[int]], row: int, col: int) -> list[tuple]:
    """
    Gets the neighbors of the given square.

    Args:
    grid (list[list[int]]): The grid to get the neighbors from.
    row (int): The row of the square to get the neighbors of.
    col (int): The column of the square to get the neighbors of.

    Returns:
    list[tuple]: The list of neighbors of the given square.
    """
    neighbors = []
    if row > 0:
        neighbors.append((row - 1, col))
    if row < len(grid) - 1:
        neighbors.append((row + 1, col))
    if col > 0:
        neighbors.append((row, col - 1))
    if col < len(grid[0]) - 1:
        neighbors.append((row, col + 1))

    return neighbors
```

## Solution Explanation:
- The `colorBorder` function first performs DFS to find the connected component that contains the given square.
- It does this by starting at the given square and recursively searching its neighbors.
- If a neighbor has the same color and has not been visited, it is added to the set of visited squares.
- The `is_on_border` function checks if a square is on the border of the grid.
- It does this by checking if the square is on the first or last row or column of the grid.
- The `get_neighbors` function gets the neighbors of a given square.
- It does this by checking the squares above, below, to the left, and to the right of the given square.
- Once the connected component has been found, the `colorBorder` function finds the border of the component by checking the squares around each square in the component.
- It does this by checking if a square is on the border of the grid or if it is adjacent to a square that is not in the visited set.
- If a square is on the border, it is added to the set of border squares.
- Finally, the `colorBorder` function recocolors the border of the connected component by setting the color of each square in the border set to the given color.

## Complexity Analysis:
- Time complexity: O(mn), where m is the number of rows in the grid and n is the number of columns in the grid.
- Space complexity: O(mn), where m is the number of rows in the grid and n is the number of columns in the grid.

## Topics
Array, Depth-First Search, Breadth-First Search, Matrix

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-06
