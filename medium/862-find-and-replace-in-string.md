# Find And Replace in String

## Problem Link
[LeetCode - Find And Replace in String](https://leetcode.com/problems/find-and-replace-in-string/)

## Difficulty
Medium

## Problem Description
<p>You are given a <strong>0-indexed</strong> string <code>s</code> that you must perform <code>k</code> replacement operations on. The replacement operations are given as three <strong>0-indexed</strong> parallel arrays, <code>indices</code>, <code>sources</code>, and <code>targets</code>, all of length <code>k</code>.</p>

<p>To complete the <code>i<sup>th</sup></code> replacement operation:</p>

<ol>
	<li>Check if the <strong>substring</strong> <code>sources[i]</code> occurs at index <code>indices[i]</code> in the <strong>original string</strong> <code>s</code>.</li>
	<li>If it does not occur, <strong>do nothing</strong>.</li>
	<li>Otherwise if it does occur, <strong>replace</strong> that substring with <code>targets[i]</code>.</li>
</ol>

<p>For example, if <code>s = &quot;<u>ab</u>cd&quot;</code>, <code>indices[i] = 0</code>, <code>sources[i] = &quot;ab&quot;</code>, and <code>targets[i] = &quot;eee&quot;</code>, then the result of this replacement will be <code>&quot;<u>eee</u>cd&quot;</code>.</p>

<p>All replacement operations must occur <strong>simultaneously</strong>, meaning the replacement operations should not affect the indexing of each other. The testcases will be generated such that the replacements will <strong>not overlap</strong>.</p>

<ul>
	<li>For example, a testcase with <code>s = &quot;abc&quot;</code>, <code>indices = [0, 1]</code>, and <code>sources = [&quot;ab&quot;,&quot;bc&quot;]</code> will not be generated because the <code>&quot;ab&quot;</code> and <code>&quot;bc&quot;</code> replacements overlap.</li>
</ul>

<p>Return <em>the <strong>resulting string</strong> after performing all replacement operations on </em><code>s</code>.</p>

<p>A <strong>substring</strong> is a contiguous sequence of characters in a string.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/06/12/833-ex1.png" style="width: 411px; height: 251px;" />
<pre>
<strong>Input:</strong> s = &quot;abcd&quot;, indices = [0, 2], sources = [&quot;a&quot;, &quot;cd&quot;], targets = [&quot;eee&quot;, &quot;ffff&quot;]
<strong>Output:</strong> &quot;eeebffff&quot;
<strong>Explanation:</strong>
&quot;a&quot; occurs at index 0 in s, so we replace it with &quot;eee&quot;.
&quot;cd&quot; occurs at index 2 in s, so we replace it with &quot;ffff&quot;.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/06/12/833-ex2-1.png" style="width: 411px; height: 251px;" />
<pre>
<strong>Input:</strong> s = &quot;abcd&quot;, indices = [0, 2], sources = [&quot;ab&quot;,&quot;ec&quot;], targets = [&quot;eee&quot;,&quot;ffff&quot;]
<strong>Output:</strong> &quot;eeecd&quot;
<strong>Explanation:</strong>
&quot;ab&quot; occurs at index 0 in s, so we replace it with &quot;eee&quot;.
&quot;ec&quot; does not occur at index 2 in s, so we do nothing.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 1000</code></li>
	<li><code>k == indices.length == sources.length == targets.length</code></li>
	<li><code>1 &lt;= k &lt;= 100</code></li>
	<li><code>0 &lt;= indexes[i] &lt; s.length</code></li>
	<li><code>1 &lt;= sources[i].length, targets[i].length &lt;= 50</code></li>
	<li><code>s</code> consists of only lowercase English letters.</li>
	<li><code>sources[i]</code> and <code>targets[i]</code> consist of only lowercase English letters.</li>
</ul>


## Test Cases
```
"abcd"
[0, 2]
["a", "cd"]
["eee", "ffff"]
"abcd"
[0, 2]
["ab","ec"]
["eee","ffff"]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks us to perform string replacements based on given indices, sources, and targets.
   - The replacements should happen simultaneously, meaning the changes made by one replacement shouldn't affect the others.
   - The problem guarantees that the replacements won't overlap.
   - A naive approach would be to iterate through the indices and replace directly in the string, but that would mess up the indices for later replacements.
   - A better approach would be to build the result string piece by piece, either by iterating through the original string and checking for replacements at each index, or by sorting the replacements by index and applying them in order.  Sorting might be cleaner.  Actually, let's keep it simple and sort.

2. Solution Implementation:
```python
def findReplaceString(s, indices, sources, targets):
    """
    Replaces substrings in a string based on given indices, sources, and targets.

    Args:
        s: The original string.
        indices: A list of indices where replacements might occur.
        sources: A list of substrings to be replaced.
        targets: A list of replacement strings.

    Returns:
        The resulting string after performing the replacements.
    """
    replacements = sorted(zip(indices, sources, targets))  # Sort replacements by index
    result = []
    s_idx = 0

    for idx, source, target in replacements:
        # Add the portion of the original string before the current replacement
        result.append(s[s_idx:idx]) 

        # Check if the source string matches the substring at the current index
        if s[idx:idx + len(source)] == source:  
            result.append(target)  # Replace if it matches
            s_idx = idx + len(source)  # Update the current index in the original string
        else:
            s_idx = idx # Source doesn't match, continue from this index

    # Add the remaining part of the original string after all replacements
    result.append(s[s_idx:])

    return "".join(result) # Join the pieces to form the result string
```

3. Solution Explanation:
   - The solution first creates a list of tuples `replacements`, where each tuple contains the index, source, and target for a replacement. This list is then sorted by index.
   - We then iterate through the sorted `replacements`. In each iteration, we append the part of the original string `s` from the previous replacement's end (or the beginning of the string) up to the current replacement index to the `result` list.
   - We then check if the current `source` matches the substring in `s` starting at the current `index`. If it matches, we append the `target` string to the `result` list. Otherwise, we do nothing.  
   - After processing all replacements, we append the remaining part of the original string `s` to the `result` list.
   - Finally, we join the strings in `result` list to form the final result string.

4. Complexity Analysis:
   - Time complexity: O(n log k + n + k*m) -  Sorting the replacements takes O(k log k) time where k is the length of indices array.  Iterating through the original string `s` takes O(n) time, where n is the length of `s`. Checking substrings in the worst case can add O(k*m) where m is the average length of sources. Since n is generally larger, this simplifies to O(n log k), assuming m is relatively small compared to n.
   - Space complexity: O(n) -  The `result` list stores the modified string, which can have a maximum length of `n` in the worst case (if all replacements are made with longer strings) plus the space used for sorted replacements O(k).  So effectively it's O(n) assuming k is much smaller than n.


## Topics
Array, Hash Table, String, Sorting

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-05-05
