# Largest Merge Of Two Strings

## Problem Link
[LeetCode - Largest Merge Of Two Strings](https://leetcode.com/problems/largest-merge-of-two-strings/)

## Difficulty
Medium

## Problem Description
<p>You are given two strings <code>word1</code> and <code>word2</code>. You want to construct a string <code>merge</code> in the following way: while either <code>word1</code> or <code>word2</code> are non-empty, choose <strong>one</strong> of the following options:</p>

<ul>
	<li>If <code>word1</code> is non-empty, append the <strong>first</strong> character in <code>word1</code> to <code>merge</code> and delete it from <code>word1</code>.

	<ul>
		<li>For example, if <code>word1 = &quot;abc&quot; </code>and <code>merge = &quot;dv&quot;</code>, then after choosing this operation, <code>word1 = &quot;bc&quot;</code> and <code>merge = &quot;dva&quot;</code>.</li>
	</ul>
	</li>
	<li>If <code>word2</code> is non-empty, append the <strong>first</strong> character in <code>word2</code> to <code>merge</code> and delete it from <code>word2</code>.
	<ul>
		<li>For example, if <code>word2 = &quot;abc&quot; </code>and <code>merge = &quot;&quot;</code>, then after choosing this operation, <code>word2 = &quot;bc&quot;</code> and <code>merge = &quot;a&quot;</code>.</li>
	</ul>
	</li>
</ul>

<p>Return <em>the lexicographically <strong>largest</strong> </em><code>merge</code><em> you can construct</em>.</p>

<p>A string <code>a</code> is lexicographically larger than a string <code>b</code> (of the same length) if in the first position where <code>a</code> and <code>b</code> differ, <code>a</code> has a character strictly larger than the corresponding character in <code>b</code>. For example, <code>&quot;abcd&quot;</code> is lexicographically larger than <code>&quot;abcc&quot;</code> because the first position they differ is at the fourth character, and <code>d</code> is greater than <code>c</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> word1 = &quot;cabaa&quot;, word2 = &quot;bcaaa&quot;
<strong>Output:</strong> &quot;cbcabaaaaa&quot;
<strong>Explanation:</strong> One way to get the lexicographically largest merge is:
- Take from word1: merge = &quot;c&quot;, word1 = &quot;abaa&quot;, word2 = &quot;bcaaa&quot;
- Take from word2: merge = &quot;cb&quot;, word1 = &quot;abaa&quot;, word2 = &quot;caaa&quot;
- Take from word2: merge = &quot;cbc&quot;, word1 = &quot;abaa&quot;, word2 = &quot;aaa&quot;
- Take from word1: merge = &quot;cbca&quot;, word1 = &quot;baa&quot;, word2 = &quot;aaa&quot;
- Take from word1: merge = &quot;cbcab&quot;, word1 = &quot;aa&quot;, word2 = &quot;aaa&quot;
- Append the remaining 5 a&#39;s from word1 and word2 at the end of merge.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> word1 = &quot;abcabc&quot;, word2 = &quot;abdcaba&quot;
<strong>Output:</strong> &quot;abdcabcabcaba&quot;
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= word1.length, word2.length &lt;= 3000</code></li>
	<li><code>word1</code> and <code>word2</code> consist only of lowercase English letters.</li>
</ul>


## Test Cases
```
"cabaa"
"bcaaa"
"abcabc"
"abdcaba"
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts

* **Problem Analysis:**
   - The goal is to concatenate the two input strings into a single string in such a way that the resulting string is lexicographically the largest possible.
   - We can only append characters from either of the two strings at each step.

* **Key Observations:**
   - We can greedily choose the character with the largest ASCII value at each step. This is because larger characters will appear later in the sorted order.
   - If the first characters of the two strings are the same, we can choose either of them.

* **Possible Approaches:**
   - **Greedy Approach:** Continuously append the character with the largest ASCII value from either string to the result until both strings are empty.
   - **Dynamic Programming:** Use dynamic programming to find the lexicographically largest merge for all possible substrings of the two strings.

## 2. Solution Implementation
```python
def largestMerge(word1, word2):
    """
    :type word1: str
    :type word2: str
    :rtype: str
    """

    # Initialize the result string.
    result = ""

    # While both strings are not empty, continue merging.
    while word1 and word2:
        # Get the larger character at the current position.
        if word1[0] >= word2[0]:
            result += word1[0]
            word1 = word1[1:]  # Remove the character from word1.
        else:
            result += word2[0]
            word2 = word2[1:]  # Remove the character from word2.

    # Append the remaining characters from the longer string.
    if word1:
        result += word1
    elif word2:
        result += word2

    # Return the lexicographically largest merged string.
    return result
```

## 3. Solution Explanation
* The solution follows a greedy approach to continuously append the larger character from either string to the result.
* We compare the first characters of the two strings and append the larger one to the result.
* This process is repeated until one of the strings becomes empty.
* If both strings become empty, the result is the lexicographically largest merged string.
* If one string has remaining characters, they are appended to the result.

## 4. Complexity Analysis
### Time Complexity: O(max(m, n))
- m is the length of the first string.
- n is the length of the second string.
- The algorithm iterates through the strings one character at a time, so the time complexity is O(max(m, n)).

### Space Complexity: O(1)
- The algorithm uses constant space to store the result string.

## Topics
Two Pointers, String, Greedy

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-09
