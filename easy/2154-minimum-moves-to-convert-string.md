# Minimum Moves to Convert String

## Problem Link
[LeetCode - Minimum Moves to Convert String](https://leetcode.com/problems/minimum-moves-to-convert-string/)

## Difficulty
Easy

## Problem Description
<p>You are given a string <code>s</code> consisting of <code>n</code> characters which are either <code>&#39;X&#39;</code> or <code>&#39;O&#39;</code>.</p>

<p>A <strong>move</strong> is defined as selecting <strong>three</strong> <strong>consecutive characters</strong> of <code>s</code> and converting them to <code>&#39;O&#39;</code>. Note that if a move is applied to the character <code>&#39;O&#39;</code>, it will stay the <strong>same</strong>.</p>

<p>Return <em>the <strong>minimum</strong> number of moves required so that all the characters of </em><code>s</code><em> are converted to </em><code>&#39;O&#39;</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;XXX&quot;
<strong>Output:</strong> 1
<strong>Explanation:</strong> <u>XXX</u> -&gt; OOO
We select all the 3 characters and convert them in one move.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;XXOX&quot;
<strong>Output:</strong> 2
<strong>Explanation:</strong> <u>XXO</u>X -&gt; O<u>OOX</u> -&gt; OOOO
We select the first 3 characters in the first move, and convert them to <code>&#39;O&#39;</code>.
Then we select the last 3 characters and convert them so that the final string contains all <code>&#39;O&#39;</code>s.</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;OOOO&quot;
<strong>Output:</strong> 0
<strong>Explanation:</strong> There are no <code>&#39;X&#39;s</code> in <code>s</code> to convert.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>3 &lt;= s.length &lt;= 1000</code></li>
	<li><code>s[i]</code> is either <code>&#39;X&#39;</code> or <code>&#39;O&#39;</code>.</li>
</ul>


## Test Cases
```
"XXX"
"XXOX"
"OOOO"
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**

   - **Problem analysis**: We need to convert all the 'X's in the string to 'O's using a minimum number of moves. Each move converts three consecutive characters to 'O'.
   - **Key observations**: 
     - If there are no 'X's in the string, we don't need to perform any moves.
     - We can convert three consecutive 'X's in a single move.
     - We can start converting 'X's from either end of the string.
   - **Possible approaches**: One possible approach is to iterate through the string and count the number of consecutive 'X's. Then we can convert these consecutive 'X's in a minimum number of moves. Another approach is to start converting 'X's from one end of the string and moving towards the other end.

2. **Solution Implementation**:

```python
def minimumMovesToConvertString(s):
    """
    :type s: str
    :rtype: int
    """
    # Count consecutive 'X's in the string.
    x = 0
    for i in range(len(s)):
        if s[i] == 'X':
            x += 1
    # If there are no consecutive 'X's, return 0.
    if x == 0:
        return 0
    # If the length of the string is not divisible by 3, the minimum number of moves is 1.
    if len(s) % 3 != 0:
        return 1
    # Convert consecutive 'X's in a minimum number of moves.
    moves = x // 3
    return moves
```

3. **Solution Explanation:**

   - The solution works by first counting the number of consecutive 'X's in the string.
   - If there are no consecutive 'X's, we don't need to perform any moves.
   - If the length of the string is not divisible by 3, we need to perform at least one move to convert all the 'X's to 'O's.
   - If the length of the string is divisible by 3, we can convert all the 'X's to 'O's in a minimum number of moves by converting three consecutive 'X's in each move.

4. **Complexity Analysis**:

   - **Time complexity**: O(n), where n is the length of the string. The solution iterates through the string once to count the number of consecutive 'X's.
   - **Space complexity**: O(1). The solution does not require any additional space.

## Topics
String, Greedy

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-12-04
