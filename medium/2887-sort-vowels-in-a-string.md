# Sort Vowels in a String

## Problem Link
[LeetCode - Sort Vowels in a String](https://leetcode.com/problems/sort-vowels-in-a-string/)

## Difficulty
Medium

## Problem Description
<p>Given a <strong>0-indexed</strong> string <code>s</code>, <strong>permute</strong> <code>s</code> to get a new string <code>t</code> such that:</p>

<ul>
	<li>All consonants remain in their original places. More formally, if there is an index <code>i</code> with <code>0 &lt;= i &lt; s.length</code> such that <code>s[i]</code> is a consonant, then <code>t[i] = s[i]</code>.</li>
	<li>The vowels must be sorted in the <strong>nondecreasing</strong> order of their <strong>ASCII</strong> values. More formally, for pairs of indices <code>i</code>, <code>j</code> with <code>0 &lt;= i &lt; j &lt; s.length</code> such that <code>s[i]</code> and <code>s[j]</code> are vowels, then <code>t[i]</code> must not have a higher ASCII value than <code>t[j]</code>.</li>
</ul>

<p>Return <em>the resulting string</em>.</p>

<p>The vowels are <code>&#39;a&#39;</code>, <code>&#39;e&#39;</code>, <code>&#39;i&#39;</code>, <code>&#39;o&#39;</code>, and <code>&#39;u&#39;</code>, and they can appear in lowercase or uppercase. Consonants comprise all letters that are not vowels.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;lEetcOde&quot;
<strong>Output:</strong> &quot;lEOtcede&quot;
<strong>Explanation:</strong> &#39;E&#39;, &#39;O&#39;, and &#39;e&#39; are the vowels in s; &#39;l&#39;, &#39;t&#39;, &#39;c&#39;, and &#39;d&#39; are all consonants. The vowels are sorted according to their ASCII values, and the consonants remain in the same places.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;lYmpH&quot;
<strong>Output:</strong> &quot;lYmpH&quot;
<strong>Explanation:</strong> There are no vowels in s (all characters in s are consonants), so we return &quot;lYmpH&quot;.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>5</sup></code></li>
	<li><code>s</code> consists only of letters of the&nbsp;English alphabet&nbsp;in <strong>uppercase and lowercase</strong>.</li>
</ul>


## Test Cases
```
"lEetcOde"
"lYmpH"
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts**
   - The problem asks us to sort the vowels in a string while keeping the consonants in their original places.
   - We can solve it by traversing the string, identifying the vowels, and sorting them using the ASCII values.
   - We need to be careful when updating the string because the vowels may be in uppercase or lowercase.

2. **Solution Implementation**
```python
class Solution:
    def sortVowels(self, s: str) -> str:
        vowels = []
        for char in s:
            if char.lower() in {'a', 'e', 'i', 'o', 'u'}:
                vowels.append(char)

        # Sort the vowels in ascending order
        vowels.sort()

        # Replace the vowels in the original string with the sorted vowels
        idx = 0
        for i in range(len(s)):
            if s[i].lower() in {'a', 'e', 'i', 'o', 'u'}:
                s = s[:i] + vowels[idx] + s[i+1:]
                idx += 1

        return s
```

3. **Solution Explanation**
   - The first loop collects all the vowels from the string, regardless of their case.
   - The vowels are sorted in ascending order.
   - Then, we loop over the string again. If the current character is a vowel, we replace it with the sorted vowel at the same index.
   - This ensures that the consonants remain in their original places and the vowels are sorted.

4. **Complexity Analysis**
   - **Time Complexity:** O(n), where n is the length of the string. We iterate over the string twice. Sorting takes O(n log n) time, but it is dominated by the O(n) iteration.
   - **Space Complexity:** O(n), where n is the length of the string. We use a list to store the vowels.

## Topics
String, Sorting

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-02
