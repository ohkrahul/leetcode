# Soup Servings

## Problem Link
[LeetCode - Soup Servings](https://leetcode.com/problems/soup-servings/)

## Difficulty
Medium

## Problem Description
<p>There are two types of soup: <strong>type A</strong> and <strong>type B</strong>. Initially, we have <code>n</code> ml of each type of soup. There are four kinds of operations:</p>

<ol>
	<li>Serve <code>100</code> ml of <strong>soup A</strong> and <code>0</code> ml of <strong>soup B</strong>,</li>
	<li>Serve <code>75</code> ml of <strong>soup A</strong> and <code>25</code> ml of <strong>soup B</strong>,</li>
	<li>Serve <code>50</code> ml of <strong>soup A</strong> and <code>50</code> ml of <strong>soup B</strong>, and</li>
	<li>Serve <code>25</code> ml of <strong>soup A</strong> and <code>75</code> ml of <strong>soup B</strong>.</li>
</ol>

<p>When we serve some soup, we give it to someone, and we no longer have it. Each turn, we will choose from the four operations with an equal probability <code>0.25</code>. If the remaining volume of soup is not enough to complete the operation, we will serve as much as possible. We stop once we no longer have some quantity of both types of soup.</p>

<p><strong>Note</strong> that we do not have an operation where all <code>100</code> ml&#39;s of <strong>soup B</strong> are used first.</p>

<p>Return <em>the probability that <strong>soup A</strong> will be empty first, plus half the probability that <strong>A</strong> and <strong>B</strong> become empty at the same time</em>. Answers within <code>10<sup>-5</sup></code> of the actual answer will be accepted.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> n = 50
<strong>Output:</strong> 0.62500
<strong>Explanation:</strong> If we choose the first two operations, A will become empty first.
For the third operation, A and B will become empty at the same time.
For the fourth operation, B will become empty first.
So the total probability of A becoming empty first plus half the probability that A and B become empty at the same time, is 0.25 * (1 + 1 + 0.5 + 0) = 0.625.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> n = 100
<strong>Output:</strong> 0.71875
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= n &lt;= 10<sup>9</sup></code></li>
</ul>


## Test Cases
```
50
100
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks for the probability that soup A becomes empty first, plus half the probability that both become empty simultaneously.
   - The operations can be seen as transitions in a state space where the state is defined by the remaining amounts of soup A and B.
   - Direct simulation for large values of `n` is infeasible due to exponential complexity.
   - We can use dynamic programming or memoization to avoid redundant calculations.
   - For very large `n`, the probability approaches 1. This is because if both soups are large, then the operations can be approximated as continuous reductions, and since there's no operation that uses only B, A is more likely to become empty first (or they both become empty).
   - We can exploit this observation to optimize the solution for large `n`.

2. Solution Implementation:
```python
from functools import lru_cache

def soupServings(n: int) -> float:
    n = (n + 24) // 25  # Optimization: Reduce the state space

    if n >= 500: # Optimization: For large n, the probability is close to 1
        return 1.0

    @lru_cache(None)  # Memoization to avoid redundant calculations
    def dp(a, b):
        if a <= 0 and b <= 0:
            return 0.5
        if a <= 0:
            return 1.0
        if b <= 0:
            return 0.0
        return 0.25 * (dp(a - 4, b) + dp(a - 3, b - 1) + dp(a - 2, b - 2) + dp(a - 1, b - 3))

    return dp(n, n)
```

3. Solution Explanation:
   - The `dp(a, b)` function calculates the desired probability recursively. `a` and `b` represent the remaining servings (in units of 25ml) of soup A and B, respectively.
   - The base cases are:
      - If both `a` and `b` are non-positive (both soups are empty or negative, meaning emptied at the same time or very close), the probability is 0.5.
      - If `a` is non-positive (soup A is empty), the probability is 1.0.
      - If `b` is non-positive (soup B is empty), the probability is 0.0.
   - The recursive step calculates the probability by considering all four operations with equal probability (0.25) and summing the resulting probabilities from the next states.
   - The `lru_cache` decorator implements memoization, storing the results of `dp(a, b)` calls to avoid redundant calculations for the same input.
   - The initial `n` is divided by 25 and rounded up. This significantly reduces the state space and improves performance. This is because the operations work in units of 25ml.
   - If `n` is greater than or equal to 500 (equivalent to 12500ml original n), the function returns 1.0. This is the key optimization for large `n` discussed in the initial thoughts.

4. Complexity Analysis:
   - Time complexity: O(n^2) after the optimization where n is the transformed input (n // 25). Without the optimization, it would be exponential.  Memoization reduces the time complexity to roughly the number of unique states, which is proportional to the square of the transformed input `n`.
   - Space complexity: O(n^2) due to the memoization cache. The recursion depth can be at most `n`, but with memoization, the number of entries in the cache is proportional to the square of the transformed input `n`.


## Topics
Math, Dynamic Programming, Probability and Statistics

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-04-14
