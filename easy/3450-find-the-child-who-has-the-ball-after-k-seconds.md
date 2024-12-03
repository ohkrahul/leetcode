# Find the Child Who Has the Ball After K Seconds

## Problem Link
[LeetCode - Find the Child Who Has the Ball After K Seconds](https://leetcode.com/problems/find-the-child-who-has-the-ball-after-k-seconds/)

## Difficulty
Easy

## Problem Description
<p>You are given two <strong>positive</strong> integers <code>n</code> and <code>k</code>. There are <code>n</code> children numbered from <code>0</code> to <code>n - 1</code> standing in a queue <em>in order</em> from left to right.</p>

<p>Initially, child 0 holds a ball and the direction of passing the ball is towards the right direction. After each second, the child holding the ball passes it to the child next to them. Once the ball reaches <strong>either</strong> end of the line, i.e. child 0 or child <code>n - 1</code>, the direction of passing is <strong>reversed</strong>.</p>

<p>Return the number of the child who receives the ball after <code>k</code> seconds.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">n = 3, k = 5</span></p>

<p><strong>Output:</strong> <span class="example-io">1</span></p>

<p><strong>Explanation:</strong></p>

<table>
	<tbody>
		<tr>
			<th>Time elapsed</th>
			<th>Children</th>
		</tr>
		<tr>
			<td><code>0</code></td>
			<td><code>[<u>0</u>, 1, 2]</code></td>
		</tr>
		<tr>
			<td><code>1</code></td>
			<td><code>[0, <u>1</u>, 2]</code></td>
		</tr>
		<tr>
			<td><code>2</code></td>
			<td><code>[0, 1, <u>2</u>]</code></td>
		</tr>
		<tr>
			<td><code>3</code></td>
			<td><code>[0, <u>1</u>, 2]</code></td>
		</tr>
		<tr>
			<td><code>4</code></td>
			<td><code>[<u>0</u>, 1, 2]</code></td>
		</tr>
		<tr>
			<td><code>5</code></td>
			<td><code>[0, <u>1</u>, 2]</code></td>
		</tr>
	</tbody>
</table>
</div>

<p><strong class="example">Example 2:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">n = 5, k = 6</span></p>

<p><strong>Output:</strong> <span class="example-io">2</span></p>

<p><strong>Explanation:</strong></p>

<table>
	<tbody>
		<tr>
			<th>Time elapsed</th>
			<th>Children</th>
		</tr>
		<tr>
			<td><code>0</code></td>
			<td><code>[<u>0</u>, 1, 2, 3, 4]</code></td>
		</tr>
		<tr>
			<td><code>1</code></td>
			<td><code>[0, <u>1</u>, 2, 3, 4]</code></td>
		</tr>
		<tr>
			<td><code>2</code></td>
			<td><code>[0, 1, <u>2</u>, 3, 4]</code></td>
		</tr>
		<tr>
			<td><code>3</code></td>
			<td><code>[0, 1, 2, <u>3</u>, 4]</code></td>
		</tr>
		<tr>
			<td><code>4</code></td>
			<td><code>[0, 1, 2, 3, <u>4</u>]</code></td>
		</tr>
		<tr>
			<td><code>5</code></td>
			<td><code>[0, 1, 2, <u>3</u>, 4]</code></td>
		</tr>
		<tr>
			<td><code>6</code></td>
			<td><code>[0, 1, <u>2</u>, 3, 4]</code></td>
		</tr>
	</tbody>
</table>
</div>

<p><strong class="example">Example 3:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">n = 4, k = 2</span></p>

<p><strong>Output:</strong> <span class="example-io">2</span></p>

<p><strong>Explanation:</strong></p>

<table>
	<tbody>
		<tr>
			<th>Time elapsed</th>
			<th>Children</th>
		</tr>
		<tr>
			<td><code>0</code></td>
			<td><code>[<u>0</u>, 1, 2, 3]</code></td>
		</tr>
		<tr>
			<td><code>1</code></td>
			<td><code>[0, <u>1</u>, 2, 3]</code></td>
		</tr>
		<tr>
			<td><code>2</code></td>
			<td><code>[0, 1, <u>2</u>, 3]</code></td>
		</tr>
	</tbody>
</table>
</div>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 &lt;= n &lt;= 50</code></li>
	<li><code>1 &lt;= k &lt;= 50</code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Note:</strong> This question is the same as <a href="https://leetcode.com/problems/pass-the-pillow/description/" target="_blank"> 2582: Pass the Pillow.</a></p>


## Test Cases
```
3
5
5
6
4
2
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts
- **Problem Analysis**:
   - The problem asks us to find the position of the child who holds the ball after K seconds.
   - This problem can be simulated by the movement of the ball.
- **Key Observations**:
   - The ball always moves from left to right or right to left.
   - When the ball reaches the beginning or the end of the line, the direction is reversed.
- **Possible Approaches**:
   - We can simulate the movement of the ball until `K` seconds.
   - We can use the remainder approach (K % (2 * (n - 1))) to determine the direction and the position.

## 2. Solution Implementation
```python
def findTheChildWhoHasTheBallAfterKSeconds(n, k):
    """
    :type n: int
    :type k: int
    :rtype: int
    """
    # If there is only one child, return 0
    if n == 1:
        return 0

    # Calculate the number of full cycles
    cycles = k // (2 * (n - 1))

    # Calculate the remaining steps after the full cycles
    remaining_steps = k % (2 * (n - 1))

    # If the remaining steps are less than n-1, the ball is moving from left to right
    if remaining_steps < n - 1:
        return remaining_steps

    # Otherwise, the ball is moving from right to left
    else:
        return n - 1 - remaining_steps
```

## 3. Solution Explanation
- The main idea is to simulate the movement of the ball.
- We can calculate the number of full cycles by dividing `k` by `2 * (n - 1)`.
- The remainder after the full cycles represents the remaining steps.
- If the remaining steps are less than `n-1`, the ball is moving from left to right.
- Otherwise, the ball is moving from right to left.
- We can then calculate the position of the child who holds the ball after `k` seconds based on the remaining steps and the direction.

## 4. Complexity Analysis
- **Time Complexity**: O(1).
- **Space Complexity**: O(1).

## Topics
Math, Simulation

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-12-03
