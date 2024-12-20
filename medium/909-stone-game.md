# Stone Game

## Problem Link
[LeetCode - Stone Game](https://leetcode.com/problems/stone-game/)

## Difficulty
Medium

## Problem Description
<p>Alice and Bob play a game with piles of stones. There are an <strong>even</strong> number of piles arranged in a row, and each pile has a <strong>positive</strong> integer number of stones <code>piles[i]</code>.</p>

<p>The objective of the game is to end with the most stones. The <strong>total</strong> number of stones across all the piles is <strong>odd</strong>, so there are no ties.</p>

<p>Alice and Bob take turns, with <strong>Alice starting first</strong>. Each turn, a player takes the entire pile of stones either from the <strong>beginning</strong> or from the <strong>end</strong> of the row. This continues until there are no more piles left, at which point the person with the <strong>most stones wins</strong>.</p>

<p>Assuming Alice and Bob play optimally, return <code>true</code><em> if Alice wins the game, or </em><code>false</code><em> if Bob wins</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> piles = [5,3,4,5]
<strong>Output:</strong> true
<strong>Explanation:</strong> 
Alice starts first, and can only take the first 5 or the last 5.
Say she takes the first 5, so that the row becomes [3, 4, 5].
If Bob takes 3, then the board is [4, 5], and Alice takes 5 to win with 10 points.
If Bob takes the last 5, then the board is [3, 4], and Alice takes 4 to win with 9 points.
This demonstrated that taking the first 5 was a winning move for Alice, so we return true.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> piles = [3,7,2,3]
<strong>Output:</strong> true
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 &lt;= piles.length &lt;= 500</code></li>
	<li><code>piles.length</code> is <strong>even</strong>.</li>
	<li><code>1 &lt;= piles[i] &lt;= 500</code></li>
	<li><code>sum(piles[i])</code> is <strong>odd</strong>.</li>
</ul>


## Test Cases
```
[5,3,4,5]
[3,7,2,3]
```

## Initial Template
```python
# Code template not available
```

## Solution
## Initial Thoughts
- The problem statement is straightforward. We need to find out if Alice can win the game, given an array of piles with a fixed set of rules.
- One key observation is that the total number of stones is odd. This means that there is no way for both Alice and Bob to end up with the same number of stones.
- Another observation is that Alice starts first. This gives her an advantage, as she can choose to take the pile with the most stones initially.
- Therefore, we can deduce that if Alice plays optimally, she will always win the game.

## Solution Implementation
```python
def stoneGame(piles):
    """
    :type piles: List[int]
    :rtype: bool
    """
    # Initialize the dp table with -1s.
    dp = [[-1] * len(piles) for _ in range(len(piles))]

    # Function to calculate the optimal score for Alice.
    def dfs(i, j):
        # If we have reached the end of the array, return 0.
        if i == j:
            return 0

        # If the value has already been calculated, return it.
        if dp[i][j] != -1:
            return dp[i][j]

        # Calculate the score for taking the first pile.
        take_first = piles[i] - dfs(i + 1, j)

        # Calculate the score for taking the last pile.
        take_last = piles[j] - dfs(i, j - 1)

        # Choose the move that gives Alice the maximum score.
        dp[i][j] = max(take_first, take_last)

        # Return the maximum score.
        return dp[i][j]

    # Return True if Alice can win the game, False otherwise.
    return dfs(0, len(piles) - 1) > 0
```

## Solution Explanation
- The solution uses a dynamic programming approach to solve the problem.
- We define a dp table where `dp[i][j]` represents the optimal score that Alice can get if she starts from pile `i` and ends at pile `j`.
- The function `dfs` calculates the optimal score for Alice given the starting and ending indices.
- If `i` is equal to `j`, it means that there is only one pile left, so Alice's score is 0.
- If `i` is less than `j`, it means that there are multiple piles left. In this case, Alice can either take the first pile and get `piles[i]` points, or she can take the last pile and get `piles[j]` points.
- Alice will choose the move that gives her the maximum score.
- The function `dfs` returns the maximum score that Alice can get.
- The main function calls `dfs(0, len(piles) - 1)` to calculate the optimal score that Alice can get if she starts from the first pile and ends at the last pile. If the score is greater than 0, it means that Alice can win the game, and the function returns `True`. Otherwise, the function returns `False`.

## Complexity Analysis
- Time complexity: O(n^2), where n is the number of piles. The `dfs` function takes O(n) time to compute the optimal score for a given starting and ending index. The main function calls `dfs` O(n^2) times to compute the optimal score for all possible starting and ending indices.
- Space complexity: O(n^2). The dp table takes O(n^2) space.

## Topics
Array, Math, Dynamic Programming, Game Theory

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-12-20
