# Reorder Data in Log Files

## Problem Link
[LeetCode - Reorder Data in Log Files](https://leetcode.com/problems/reorder-data-in-log-files/)

## Difficulty
Medium

## Problem Description
<p>You are given an array of <code>logs</code>. Each log is a space-delimited string of words, where the first word is the <strong>identifier</strong>.</p>

<p>There are two types of logs:</p>

<ul>
	<li><b>Letter-logs</b>: All words (except the identifier) consist of lowercase English letters.</li>
	<li><strong>Digit-logs</strong>: All words (except the identifier) consist of digits.</li>
</ul>

<p>Reorder these logs so that:</p>

<ol>
	<li>The <strong>letter-logs</strong> come before all <strong>digit-logs</strong>.</li>
	<li>The <strong>letter-logs</strong> are sorted lexicographically by their contents. If their contents are the same, then sort them lexicographically by their identifiers.</li>
	<li>The <strong>digit-logs</strong> maintain their relative ordering.</li>
</ol>

<p>Return <em>the final order of the logs</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> logs = [&quot;dig1 8 1 5 1&quot;,&quot;let1 art can&quot;,&quot;dig2 3 6&quot;,&quot;let2 own kit dig&quot;,&quot;let3 art zero&quot;]
<strong>Output:</strong> [&quot;let1 art can&quot;,&quot;let3 art zero&quot;,&quot;let2 own kit dig&quot;,&quot;dig1 8 1 5 1&quot;,&quot;dig2 3 6&quot;]
<strong>Explanation:</strong>
The letter-log contents are all different, so their ordering is &quot;art can&quot;, &quot;art zero&quot;, &quot;own kit dig&quot;.
The digit-logs have a relative order of &quot;dig1 8 1 5 1&quot;, &quot;dig2 3 6&quot;.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> logs = [&quot;a1 9 2 3 1&quot;,&quot;g1 act car&quot;,&quot;zo4 4 7&quot;,&quot;ab1 off key dog&quot;,&quot;a8 act zoo&quot;]
<strong>Output:</strong> [&quot;g1 act car&quot;,&quot;a8 act zoo&quot;,&quot;ab1 off key dog&quot;,&quot;a1 9 2 3 1&quot;,&quot;zo4 4 7&quot;]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= logs.length &lt;= 100</code></li>
	<li><code>3 &lt;= logs[i].length &lt;= 100</code></li>
	<li>All the tokens of <code>logs[i]</code> are separated by a <strong>single</strong> space.</li>
	<li><code>logs[i]</code> is guaranteed to have an identifier and at least one word after the identifier.</li>
</ul>


## Test Cases
```
["dig1 8 1 5 1","let1 art can","dig2 3 6","let2 own kit dig","let3 art zero"]
["a1 9 2 3 1","g1 act car","zo4 4 7","ab1 off key dog","a8 act zoo"]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:

- The problem asks us to reorder logs based on two types - letter-logs and digit-logs.
- Letter-logs come before digit-logs.
- Letter-logs should be sorted lexicographically by their contents, and if they have the same contents, then sort them lexicographically by their identifiers.
- Digit-logs maintain their relative ordering.

2. Solution Implementation:
```python
def reorderLogFiles(logs):
  """
  Reorders the given logs based on the specified rules.

  Parameters:
    logs: A list of strings representing logs.

  Returns:
    A list of strings representing the reordered logs.
  """
  
  # Initialize two lists to store the two types of logs.
  letter_logs = []
  digit_logs = []

  # Iterate over the given logs.
  for log in logs:
    # Split the log into its identifier and the rest of the content.
    identifier, content = log.split(' ', 1)

    # Check if the log is a letter-log or a digit-log.
    if content.isalpha():
      letter_logs.append((content, identifier))
    else:
      digit_logs.append(log)

  # Sort the letter-logs lexicographically by their contents and identifiers.
  letter_logs.sort(key=lambda log: (log[0], log[1]))

  # Combine the sorted letter-logs and the digit-logs.
  reordered_logs = letter_logs + digit_logs

  # Return the reordered logs.
  return reordered_logs
```

3. Solution Explanation:

- The solution first initializes two lists, `letter_logs` and `digit_logs`, to store the two types of logs.
- It then iterates over the given logs and splits each log into its identifier and the rest of the content.
- It then checks if the log is a letter-log or a digit-log based on the content.
- If the log is a letter-log, it is appended to the `letter_logs` list as a tuple of its content and identifier.
- If the log is a digit-log, it is appended to the `digit_logs` list as a string.
- After iterating over all the logs, the `letter_logs` list is sorted lexicographically by its contents and identifiers using the `sort()` function with a custom key function.
- Finally, the sorted `letter_logs` list and the `digit_logs` list are combined and returned as the reordered logs.

4. Complexity Analysis:

- Time complexity: The time complexity of this solution is O(n log n), where n is the number of logs. This is because we need to sort the letter-logs, which takes O(n log n) time.
- Space complexity: The space complexity of this solution is O(n), as we need to store all the logs in memory.

## Topics
Array, String, Sorting

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-12-09
