# Ones and Zeroes

## Problem Link
[LeetCode - Ones and Zeroes](https://leetcode.com/problems/ones-and-zeroes/)

## Difficulty
Medium

## Problem Description
<p>You are given an array of binary strings <code>strs</code> and two integers <code>m</code> and <code>n</code>.</p>

<p>Return <em>the size of the largest subset of <code>strs</code> such that there are <strong>at most</strong> </em><code>m</code><em> </em><code>0</code><em>&#39;s and </em><code>n</code><em> </em><code>1</code><em>&#39;s in the subset</em>.</p>

<p>A set <code>x</code> is a <strong>subset</strong> of a set <code>y</code> if all elements of <code>x</code> are also elements of <code>y</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> strs = [&quot;10&quot;,&quot;0001&quot;,&quot;111001&quot;,&quot;1&quot;,&quot;0&quot;], m = 5, n = 3
<strong>Output:</strong> 4
<strong>Explanation:</strong> The largest subset with at most 5 0&#39;s and 3 1&#39;s is {&quot;10&quot;, &quot;0001&quot;, &quot;1&quot;, &quot;0&quot;}, so the answer is 4.
Other valid but smaller subsets include {&quot;0001&quot;, &quot;1&quot;} and {&quot;10&quot;, &quot;1&quot;, &quot;0&quot;}.
{&quot;111001&quot;} is an invalid subset because it contains 4 1&#39;s, greater than the maximum of 3.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> strs = [&quot;10&quot;,&quot;0&quot;,&quot;1&quot;], m = 1, n = 1
<strong>Output:</strong> 2
<b>Explanation:</b> The largest subset is {&quot;0&quot;, &quot;1&quot;}, so the answer is 2.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= strs.length &lt;= 600</code></li>
	<li><code>1 &lt;= strs[i].length &lt;= 100</code></li>
	<li><code>strs[i]</code> consists only of digits <code>&#39;0&#39;</code> and <code>&#39;1&#39;</code>.</li>
	<li><code>1 &lt;= m, n &lt;= 100</code></li>
</ul>


## Test Cases
```
["10","0001","111001","1","0"]
5
3
["10","0","1"]
1
1
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - This problem is asking for the maximum size of a subset of strings that satisfies a constraint on the total number of '0's and '1's.  This smells like a dynamic programming problem. Specifically, it resembles the knapsack problem where we have a limited capacity (m and n) and we want to maximize the number of items (strings) we can "fit".
   - The key observation is that the order of the strings doesn't matter, only the counts of '0's and '1's.
   - We can approach this using a 2D DP table where dp[i][j] represents the maximum number of strings we can include with at most i '0's and j '1's.


2. Solution Implementation:
```python
def findMaxForm(strs, m, n):
    """
    Finds the maximum size of a subset of strings with at most m 0's and n 1's.

    Args:
        strs: A list of binary strings.
        m: The maximum number of 0's allowed.
        n: The maximum number of 1's allowed.

    Returns:
        The size of the largest subset.
    """
    num_strs = len(strs)
    dp = [[0] * (n + 1) for _ in range(m + 1)]  # Initialize DP table

    for s in strs:
        zeros = s.count('0')
        ones = len(s) - zeros  # Count 1's efficiently

        for i in range(m, zeros - 1, -1):  # Iterate backwards to avoid overwriting
            for j in range(n, ones - 1, -1):
                dp[i][j] = max(dp[i][j], 1 + dp[i - zeros][j - ones])  # Update DP table

    return dp[m][n]


```

3. Solution Explanation:
   - The code initializes a 2D DP table `dp` where `dp[i][j]` stores the maximum number of strings that can be included with at most `i` zeros and `j` ones.
   - It iterates through each string `s` in `strs`.
   - For each string, it counts the number of zeros and ones.
   - Then, it iterates through the DP table from the maximum allowed zeros and ones down to the number of zeros and ones in the current string.  Crucially, the iteration is backwards to avoid using the same string multiple times within the same subproblem calculation (which is why the knapsack problem often has this backwards iteration).
   - The core logic is in `dp[i][j] = max(dp[i][j], 1 + dp[i - zeros][j - ones])`.  This means the maximum number of strings we can form with `i` zeros and `j` ones is either the current value (without including `s`), OR it's one more (including `s`) than what we could form with `i - zeros` and `j - ones` (i.e., the remaining capacity after using `s`).
   - Finally, it returns `dp[m][n]`, which represents the maximum number of strings with at most `m` zeros and `n` ones.


4. Complexity Analysis:
   - Time complexity: O(l * m * n) - where l is the length of `strs`, m is the maximum number of zeros, and n is the maximum number of ones. This is due to the nested loops.
   - Space complexity: O(m * n) - The space is dominated by the 2D DP table.


## Topics
Array, String, Dynamic Programming

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-07
