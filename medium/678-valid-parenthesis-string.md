# Valid Parenthesis String

## Problem Link
[LeetCode - Valid Parenthesis String](https://leetcode.com/problems/valid-parenthesis-string/)

## Difficulty
Medium

## Problem Description
<p>Given a string <code>s</code> containing only three types of characters: <code>&#39;(&#39;</code>, <code>&#39;)&#39;</code> and <code>&#39;*&#39;</code>, return <code>true</code> <em>if</em> <code>s</code> <em>is <strong>valid</strong></em>.</p>

<p>The following rules define a <strong>valid</strong> string:</p>

<ul>
	<li>Any left parenthesis <code>&#39;(&#39;</code> must have a corresponding right parenthesis <code>&#39;)&#39;</code>.</li>
	<li>Any right parenthesis <code>&#39;)&#39;</code> must have a corresponding left parenthesis <code>&#39;(&#39;</code>.</li>
	<li>Left parenthesis <code>&#39;(&#39;</code> must go before the corresponding right parenthesis <code>&#39;)&#39;</code>.</li>
	<li><code>&#39;*&#39;</code> could be treated as a single right parenthesis <code>&#39;)&#39;</code> or a single left parenthesis <code>&#39;(&#39;</code> or an empty string <code>&quot;&quot;</code>.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> s = "()"
<strong>Output:</strong> true
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> s = "(*)"
<strong>Output:</strong> true
</pre><p><strong class="example">Example 3:</strong></p>
<pre><strong>Input:</strong> s = "(*))"
<strong>Output:</strong> true
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 100</code></li>
	<li><code>s[i]</code> is <code>&#39;(&#39;</code>, <code>&#39;)&#39;</code> or <code>&#39;*&#39;</code>.</li>
</ul>


## Test Cases
```
"()"
"(*)"
"(*))"
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - **Problem Analysis**
     - The problem asks whether the string of parentheses is valid.
   - **Key Observations**
     - An open parenthesis must be closed.
     - A closed parenthesis must be opened.
     - An asterisk can be an open or closed parenthesis or nothing.
   - **Possible Approaches**
     - A greedy approach can be used to solve this problem. The key idea is to iterate over the string and maintain a count of the open parentheses and the asterisks. When an open parenthesis is encountered, we increment the count of open parentheses, and we decrement the count of open parentheses when a closed parenthesis is encountered. The count of open parentheses should always be greater than or equal to 0. When an asterisk is encountered, we decrement the count of asterisks. The count of asterisks should always be greater than or equal to 0.
     - A stack can also be used to solve this problem. The key idea is to push open parentheses and asterisks onto the stack and pop them when closed parentheses are encountered.
     - A regular expression can be used to solve this problem. The key idea is to match the string against the regular expression pattern.

2. Solution Implementation:
```python
def checkValidString(s: str) -> bool:
    # Initialize the count of open parentheses and asterisks.
    open_parentheses = 0
    asterisks = 0

    # Iterate over the string.
    for char in s:
        if char == "(":
            open_parentheses += 1
        elif char == ")":
            if open_parentheses > 0:
                open_parentheses -= 1
            elif asterisks > 0:
                asterisks -= 1
            else:
                return False
        else:
            asterisks += 1

    # Check if the count of open parentheses is equal to 0.
    return open_parentheses == 0
```

3. Solution Explanation:
   - The solution uses the greedy approach to solve this problem.
   - It iterates over the string and maintains a count of the open parentheses and the asterisks.
   - When an open parenthesis is encountered, we increment the count of open parentheses. When a closed parenthesis is encountered, we decrement the count of open parentheses. The count of open parentheses should always be greater than or equal to 0. When an asterisk is encountered, we decrement the count of asterisks. The count of asterisks should always be greater than or equal to 0.
   - If the count of open parentheses or the count of asterisks becomes negative at any point, the string is not valid.
   - If the count of open parentheses is equal to 0 at the end of the string, the string is valid.

4. Complexity Analysis:
   - **Time complexity:** O(n), where n is the length of the string.
   - **Space complexity:** O(1), as we only use a constant amount of memory to store the count of open parentheses and the count of asterisks.

## Topics
String, Dynamic Programming, Stack, Greedy

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-12-10
