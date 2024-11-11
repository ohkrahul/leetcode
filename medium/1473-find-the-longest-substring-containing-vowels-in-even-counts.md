# Find the Longest Substring Containing Vowels in Even Counts

## Problem Link
[LeetCode - Find the Longest Substring Containing Vowels in Even Counts](https://leetcode.com/problems/find-the-longest-substring-containing-vowels-in-even-counts/)

## Difficulty
Medium

## Problem Description
<p>Given the string <code>s</code>, return the size of the longest substring containing each vowel an even number of times. That is, &#39;a&#39;, &#39;e&#39;, &#39;i&#39;, &#39;o&#39;, and &#39;u&#39; must appear an even number of times.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;eleetminicoworoep&quot;
<strong>Output:</strong> 13
<strong>Explanation: </strong>The longest substring is &quot;leetminicowor&quot; which contains two each of the vowels: <strong>e</strong>, <strong>i</strong> and <strong>o</strong> and zero of the vowels: <strong>a</strong> and <strong>u</strong>.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;leetcodeisgreat&quot;
<strong>Output:</strong> 5
<strong>Explanation:</strong> The longest substring is &quot;leetc&quot; which contains two e&#39;s.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;bcbcbc&quot;
<strong>Output:</strong> 6
<strong>Explanation:</strong> In this case, the given string &quot;bcbcbc&quot; is the longest because all vowels: <strong>a</strong>, <strong>e</strong>, <strong>i</strong>, <strong>o</strong> and <strong>u</strong> appear zero times.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 5 x 10^5</code></li>
	<li><code>s</code>&nbsp;contains only lowercase English letters.</li>
</ul>


## Test Cases
```
"eleetminicoworoep"
"leetcodeisgreat"
"bcbcbc"
```

## Initial Template
```python
# Code template not available
```

## Solution
## Initial Thoughts

### Problem analysis

The problem asks us to find the size of the longest substring containing each vowel an even number of times. This means that the substring should contain an even number of 'a', 'e', 'i', 'o', and 'u'.

### Key observations

* We can use a sliding window approach to solve this problem.
* The sliding window will contain the current substring.
* We will move the window forward until the substring contains an odd number of vowels.
* When the substring contains an odd number of vowels, we will move the window backward until the substring contains an even number of vowels.
* We will keep track of the longest substring we have seen so far.

### Possible approaches

* Sliding window approach

## Solution Implementation

```python
def findTheLongestSubstring(s):
  # Initialize the sliding window.
  window_start = 0
  window_end = 0

  # Initialize the frequency of each vowel.
  vowel_frequency = {
    'a': 0,
    'e': 0,
    'i': 0,
    'o': 0,
    'u': 0
  }

  # Initialize the longest substring.
  longest_substring = 0

  # Iterate over the string.
  while window_end < len(s):
    # Add the current character to the sliding window.
    vowel_frequency[s[window_end]] += 1
    window_end += 1

    # Check if the substring contains an odd number of vowels.
    if any(value % 2 == 1 for value in vowel_frequency.values()):
      # Move the window backward until the substring contains an even number of vowels.
      while any(value % 2 == 1 for value in vowel_frequency.values()):
        vowel_frequency[s[window_start]] -= 1
        window_start += 1

    # Update the longest substring.
    longest_substring = max(longest_substring, window_end - window_start)

  # Return the longest substring.
  return longest_substring
```

## Solution Explanation

The solution works as follows. We initialize the sliding window to contain the first character of the string. We then iterate over the string, adding each character to the sliding window. We keep track of the frequency of each vowel in the sliding window. If the substring contains an odd number of vowels, we move the window backward until the substring contains an even number of vowels. We keep track of the longest substring we have seen so far.

## Complexity Analysis

### Time complexity

The time complexity of the solution is O(n), where n is the length of the string. This is because we iterate over the string once.

### Space complexity

The space complexity of the solution is O(1). This is because we only store a constant number of variables.

## Topics
Hash Table, String, Bit Manipulation, Prefix Sum

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-11-11
