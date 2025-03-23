# Reverse Words in a String III

## Problem Link
[LeetCode - Reverse Words in a String III](https://leetcode.com/problems/reverse-words-in-a-string-iii/)

## Difficulty
Easy

## Problem Description
<p>Given a string <code>s</code>, reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;Let&#39;s take LeetCode contest&quot;
<strong>Output:</strong> &quot;s&#39;teL ekat edoCteeL tsetnoc&quot;
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;Mr Ding&quot;
<strong>Output:</strong> &quot;rM gniD&quot;
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 5 * 10<sup>4</sup></code></li>
	<li><code>s</code> contains printable <strong>ASCII</strong> characters.</li>
	<li><code>s</code> does not contain any leading or trailing spaces.</li>
	<li>There is <strong>at least one</strong> word in <code>s</code>.</li>
	<li>All the words in <code>s</code> are separated by a single space.</li>
</ul>


## Test Cases
```
"Let's take LeetCode contest"
"Mr Ding"
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - Problem analysis:  The problem asks us to reverse the characters within each word of a string, but keep the word order and spacing the same.
   - Key observations: We can split the string into words using spaces as delimiters. Then, reverse each word individually and join them back with spaces.
   - Possible approaches:
     - Splitting the string into a list of words, reversing each word, and joining them back.  This seems like the most straightforward approach.
     - Iterating through the string character by character, building words, and reversing them when a space is encountered or the end of the string is reached. This might be slightly more memory efficient but potentially more complex to implement.
     - Using Python's slicing capabilities within a loop to reverse words in-place. This could be tricky with the spaces though.

2. Solution Implementation:
```python
def reverseWords(s: str) -> str:
    """Reverses the characters in each word of a string while preserving word order and spacing.

    Args:
        s: The input string.

    Returns:
        The string with reversed words.
    """
    words = s.split() # Split the string into a list of words
    reversed_words = [word[::-1] for word in words]  # Reverse each word using slicing
    return " ".join(reversed_words)  # Join the reversed words back into a string with spaces
```

3. Solution Explanation:
   - How the solution works:
     - The `split()` method splits the input string `s` into a list of words, using spaces as the delimiter.
     - A list comprehension `[word[::-1] for word in words]` is used to iterate through the list of words.  Inside the comprehension, `word[::-1]` efficiently reverses each word using slicing. This creates a new list `reversed_words` containing the reversed words.
     - Finally, `" ".join(reversed_words)` joins the reversed words back into a single string, using a single space as the separator.

   - Key steps and logic explained:  The key steps are splitting, reversing, and joining. Splitting separates the words, reversing flips the characters in each word, and joining reconstructs the string with the reversed words.
   - Why this approach is effective:  This approach is effective because it's concise, readable, and leverages Python's built-in string manipulation functions for efficiency.

4. Complexity Analysis:
   - Time complexity: O(N) - where N is the length of the string.  We iterate through the string once during the split operation and once during the join operation.  Reversing each word also takes time proportional to the word's length, but summing these lengths over all words is still O(N).
   - Space complexity: O(N) - We store the reversed words in a new list `reversed_words`, which in the worst case (all single-character words) could have the same size as the original string. The `split()` operation itself also creates a list of words which can contribute to the space complexity.  Therefore the overall space complexity is O(N). 


## Topics
Two Pointers, String

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-23
