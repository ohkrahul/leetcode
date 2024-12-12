# Sum Multiples

## Problem Link
[LeetCode - Sum Multiples](https://leetcode.com/problems/sum-multiples/)

## Difficulty
Easy

## Problem Description
<p>Given a positive integer <code>n</code>, find the sum of all integers in the range <code>[1, n]</code> <strong>inclusive</strong> that are divisible by <code>3</code>, <code>5</code>, or <code>7</code>.</p>

<p>Return <em>an integer denoting the sum of all numbers in the given range satisfying&nbsp;the constraint.</em></p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> n = 7
<strong>Output:</strong> 21
<strong>Explanation:</strong> Numbers in the range <code>[1, 7]</code> that are divisible by <code>3</code>, <code>5,</code> or <code>7 </code>are <code>3, 5, 6, 7</code>. The sum of these numbers is <code>21</code>.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> n = 10
<strong>Output:</strong> 40
<strong>Explanation:</strong> Numbers in the range <code>[1, 10] that are</code> divisible by <code>3</code>, <code>5,</code> or <code>7</code> are <code>3, 5, 6, 7, 9, 10</code>. The sum of these numbers is 40.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> n = 9
<strong>Output:</strong> 30
<strong>Explanation:</strong> Numbers in the range <code>[1, 9]</code> that are divisible by <code>3</code>, <code>5</code>, or <code>7</code> are <code>3, 5, 6, 7, 9</code>. The sum of these numbers is <code>30</code>.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 10<sup>3</sup></code></li>
</ul>


## Test Cases
```
7
10
9
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:

- This problem can be solved by iterating over all the numbers from 1 to n and checking if they are divisible by 3, 5, or 7.
- The sum of the divisible numbers can be calculated as they are encountered.

2. Solution Implementation:
```python
def sum_multiples(n):
    """
    :type n: int
    :rtype: int
    """
    sum = 0
    for i in range(1, n + 1):
        if i % 3 == 0 or i % 5 == 0 or i % 7 == 0:
            sum += i
    return sum
```

3. Solution Explanation:

- We iterate over the numbers from 1 to n using a for loop.
- For each number, we check if it is divisible by 3, 5, or 7 using the modulo operator.
- If the number is divisible by any of these numbers, we add it to the sum.
- Finally, we return the sum of all the divisible numbers.

4. Complexity Analysis:

- Time complexity: O(n) - We iterate over the numbers from 1 to n.
- Space complexity: O(1) - We only store a few variables, so the space complexity is constant.

## Topics
Math

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-12-12
