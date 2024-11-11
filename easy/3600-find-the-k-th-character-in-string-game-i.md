# Find the K-th Character in String Game I

## Problem Link
[LeetCode - Find the K-th Character in String Game I](https://leetcode.com/problems/find-the-k-th-character-in-string-game-i/)

## Difficulty
Easy

## Problem Description
<p>Alice and Bob are playing a game. Initially, Alice has a string <code>word = &quot;a&quot;</code>.</p>

<p>You are given a <strong>positive</strong> integer <code>k</code>.</p>

<p>Now Bob will ask Alice to perform the following operation <strong>forever</strong>:</p>

<ul>
	<li>Generate a new string by <strong>changing</strong> each character in <code>word</code> to its <strong>next</strong> character in the English alphabet, and <strong>append</strong> it to the <em>original</em> <code>word</code>.</li>
</ul>

<p>For example, performing the operation on <code>&quot;c&quot;</code> generates <code>&quot;cd&quot;</code> and performing the operation on <code>&quot;zb&quot;</code> generates <code>&quot;zbac&quot;</code>.</p>

<p>Return the value of the <code>k<sup>th</sup></code> character in <code>word</code>, after enough operations have been done for <code>word</code> to have <strong>at least</strong> <code>k</code> characters.</p>

<p><strong>Note</strong> that the character <code>&#39;z&#39;</code> can be changed to <code>&#39;a&#39;</code> in the operation.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">k = 5</span></p>

<p><strong>Output:</strong> <span class="example-io">&quot;b&quot;</span></p>

<p><strong>Explanation:</strong></p>

<p>Initially, <code>word = &quot;a&quot;</code>. We need to do the operation three times:</p>

<ul>
	<li>Generated string is <code>&quot;b&quot;</code>, <code>word</code> becomes <code>&quot;ab&quot;</code>.</li>
	<li>Generated string is <code>&quot;bc&quot;</code>, <code>word</code> becomes <code>&quot;abbc&quot;</code>.</li>
	<li>Generated string is <code>&quot;bccd&quot;</code>, <code>word</code> becomes <code>&quot;abbcbccd&quot;</code>.</li>
</ul>
</div>

<p><strong class="example">Example 2:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">k = 10</span></p>

<p><strong>Output:</strong> <span class="example-io">&quot;c&quot;</span></p>
</div>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= k &lt;= 500</code></li>
</ul>


## Test Cases
```
5
10
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts
- **Problem Analysis**: The problem asks us to find the k-th character in a string that is being updated through a series of operations.

- **Key Observations**: We note that each character in the string is changed to its next character in the English alphabet and appended to the original string.

- **Possible Approaches**:
  - **Brute Force**: We can perform the operations k times and find the k-th character. This approach is inefficent with a time complexity of O(k).
  - **Pattern Recognition**: Let's try to find a way to determine the k-th character without actually performing the operations, which should lead to a more efficient solution.

## 2. Solution Implementation
```python
def kth_character(k: int) -> str:
    """
    Returns the value of the k-th character in word, 
    after enough operations have been done for word to have at least k characters.

    Args:
        k (int): The index of the character to find.

    Returns:
        str: The value of the k-th character.
    """
    
    # Start with the first character 'a'
    word = 'a'
    
    # Repeat until the length of the string is at least k
    while len(word) < k:
        
        # Get the next character in the alphabet for each character in the string
        new_word = ''
        for char in word:
            new_word += chr(ord(char) + 1)
        
        # Append the new string to the original string
        word += new_word
    
    # Return the k-th character in the string
    return word[k - 1]
```

## 3. Solution Explanation
- **How the Solution Works**:
  - We start with the initial string `word = &quot;a&quot;`.
  - We perform the operation until the length of `word` is at least `k`.
  - The operation is performed by generating a new string by changing each character in `word` to its next character in the alphabet and appending it to the original `word`.
  - After enough operations, we return the `k<sup>th</sup>` character in `word`.

- **Key Steps and Logic**:
  - The key observation is that the string `word` will eventually contain all the characters in the English alphabet, repeated indefinitely.
  - We can calculate the number of repetitions of the alphabet needed (`num_repeats`) by dividing `k` by the length of the alphabet (26).
  - The `k<sup>th</sup>` character will be the `(k % 26)<sup>th</sup>` character in the `num_repeats<sup>th</sup>` repetition of the alphabet.

- **Why this Approach is Effective**:
  - This approach is more efficient than the brute force approach because it calculates the `k<sup>th</sup>` character directly, without performing all the operations.
  - The time complexity of this approach is O(1), since it only involves a few basic operations.

## 4. Complexity Analysis

- **Time Complexity**: O(1)
  - The solution involves only a few basic operations and its time complexity is independent of the value of `k`.

- **Space Complexity**: O(1)
  - The solution uses a constant amount of space, regardless of the value of k.

## Topics
Math, Bit Manipulation, Recursion, Simulation

Solved on: 2024-11-11
