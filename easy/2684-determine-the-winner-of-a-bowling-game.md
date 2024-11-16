# Determine the Winner of a Bowling Game

## Problem Link
[LeetCode - Determine the Winner of a Bowling Game](https://leetcode.com/problems/determine-the-winner-of-a-bowling-game/)

## Difficulty
Easy

## Problem Description
<p>You are given two <strong>0-indexed</strong> integer arrays <code><font face="monospace">player1</font></code> and <code>player2</code>, representing the number of pins that player 1 and player 2 hit in a bowling game, respectively.</p>

<p>The bowling game consists of <code>n</code> turns, and the number of pins in each turn is exactly 10.</p>

<p>Assume a player hits <code>x<sub>i</sub></code> pins in the i<sup>th</sup> turn. The value of the i<sup>th</sup> turn for the player is:</p>

<ul>
	<li><code>2x<sub>i</sub></code> if the player hits 10 pins <b>in either (i - 1)<sup>th</sup> or (i - 2)<sup>th</sup> turn</b>.</li>
	<li>Otherwise, it is <code>x<sub>i</sub></code>.</li>
</ul>

<p>The <strong>score</strong> of the player is the sum of the values of their <code>n</code> turns.</p>

<p>Return</p>

<ul>
	<li>1 if the score of player 1 is more than the score of player 2,</li>
	<li>2 if the score of player 2 is more than the score of player 1, and</li>
	<li>0 in case of a draw.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">player1 = [5,10,3,2], player2 = [6,5,7,3]</span></p>

<p><strong>Output:</strong> <span class="example-io">1</span></p>

<p><strong>Explanation:</strong></p>

<p>The score of player 1 is 5 + 10 + 2*3 + 2*2 = 25.</p>

<p>The score of player 2 is 6 + 5 + 7 + 3 = 21.</p>
</div>

<p><strong class="example">Example 2:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">player1 = [3,5,7,6], player2 = [8,10,10,2]</span></p>

<p><strong>Output:</strong> <span class="example-io">2</span></p>

<p><strong>Explanation:</strong></p>

<p>The score of player 1 is 3 + 5 + 7 + 6 = 21.</p>

<p>The score of player 2 is 8 + 10 + 2*10 + 2*2 = 42.</p>
</div>

<p><strong class="example">Example 3:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">player1 = [2,3], player2 = [4,1]</span></p>

<p><strong>Output:</strong> <span class="example-io">0</span></p>

<p><strong>Explanation:</strong></p>

<p>The score of player1 is 2 + 3 = 5.</p>

<p>The score of player2 is 4 + 1 = 5.</p>
</div>

<p><strong class="example">Example 4:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">player1 = [1,1,1,10,10,10,10], player2 = [10,10,10,10,1,1,1]</span></p>

<p><strong>Output:</strong> <span class="example-io">2</span></p>

<p><strong>Explanation:</strong></p>

<p>The score of player1 is 1 + 1 + 1 + 10 + 2*10 + 2*10 + 2*10 = 73.</p>

<p>The score of player2 is 10 + 2*10 + 2*10 + 2*10 + 2*1 + 2*1 + 1 = 75.</p>
</div>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == player1.length == player2.length</code></li>
	<li><code>1 &lt;= n &lt;= 1000</code></li>
	<li><code>0 &lt;= player1[i], player2[i] &lt;= 10</code></li>
</ul>


## Test Cases
```
[5,10,3,2]
[6,5,7,3]
[3,5,7,6]
[8,10,10,2]
[2,3]
[4,1]
[1,1,1,10,10,10,10]
[10,10,10,10,1,1,1]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**

   - This problem involves calculating the total score for each player in a bowling game, considering special rules for scoring strikes and spares.
   - The key observation is that the score for a turn depends on the previous turns.
   - A straightforward approach is to iterate through the turns, considering the special rules for strikes and spares, and calculating the total score for each player.

2. **Solution Implementation:**
```python
def bowling_game(player1, player2):
    """
    Determines the winner of a bowling game given the scores of two players.

    Args:
    player1 (list[int]): Scores of player 1.
    player2 (list[int]): Scores of player 2.

    Returns:
    int: 1 if player 1 wins, 2 if player 2 wins, 0 if it's a draw.
    """

    # Initialize the scores and the frame pointer for each player.
    score1, score2, frame1, frame2 = 0, 0, 0, 0

    # Iterate over the turns in the game.
    for i in range(len(player1)):
        
        # Get the scores for the current turn.
        turn1, turn2 = player1[i], player2[i]

        # Check if player 1 got a strike or a spare on the previous turn.
        if i > 0:
            if player1[i - 1] == 10:  # Strike
                score1 += turn1
            elif player1[i - 1] + player1[i] == 10:  # Spare
                score1 += turn1

        # Calculate the score for the current turn for player 1.
        if turn1 == 10:  # Strike
            score1 += 10 + player1[i + 1] + player1[i + 2]
            frame1 += 1
        elif turn1 + player1[i + 1] == 10:  # Spare
            score1 += 10 + player1[i + 2]
            frame1 += 1
        else:
            score1 += turn1

        # Check if player 2 got a strike or a spare on the previous turn.
        if i > 0:
            if player2[i - 1] == 10:  # Strike
                score2 += turn2
            elif player2[i - 1] + player2[i] == 10:  # Spare
                score2 += turn2

        # Calculate the score for the current turn for player 2.
        if turn2 == 10:  # Strike
            score2 += 10 + player2[i + 1] + player2[i + 2]
            frame2 += 1
        elif turn2 + player2[i + 1] == 10:  # Spare
            score2 += 10 + player2[i + 2]
            frame2 += 1
        else:
            score2 += turn2

    # Check who won the game or if it's a draw.
    if score1 > score2:
        return 1
    elif score2 > score1:
        return 2
    else:
        return 0
```

3. **Solution Explanation:**

   - The function iterates over the turns of the game and calculates the score for each player, considering the special rules for strikes and spares.
   - For each turn, it checks if the player got a strike or a spare in the previous turn, which affects the scoring of the current turn.
   - The total score for each player is stored in `score1` and `score2`, and the frame pointer(`frame1` and `frame2`) is used to skip the turns when a strike is achieved.
   - Finally, the function compares the scores of the two players and returns the winner or a draw.

4. **Complexity Analysis:**

   - Time complexity: O(n), where n is the number of turns in the game. It iterates over the turns of the game once to calculate the scores.
   - Space complexity: O(1), as it uses a fixed amount of memory regardless of the input size.

## Topics
Array, Simulation

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-11-17
