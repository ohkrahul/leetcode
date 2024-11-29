# Maximum Number of Removable Characters

## Problem Link
[LeetCode - Maximum Number of Removable Characters](https://leetcode.com/problems/maximum-number-of-removable-characters/)

## Difficulty
Medium

## Problem Description
<p>You are given two strings <code>s</code> and <code>p</code> where <code>p</code> is a <strong>subsequence </strong>of <code>s</code>. You are also given a <strong>distinct 0-indexed </strong>integer array <code>removable</code> containing a subset of indices of <code>s</code> (<code>s</code> is also <strong>0-indexed</strong>).</p>

<p>You want to choose an integer <code>k</code> (<code>0 &lt;= k &lt;= removable.length</code>) such that, after removing <code>k</code> characters from <code>s</code> using the <strong>first</strong> <code>k</code> indices in <code>removable</code>, <code>p</code> is still a <strong>subsequence</strong> of <code>s</code>. More formally, you will mark the character at <code>s[removable[i]]</code> for each <code>0 &lt;= i &lt; k</code>, then remove all marked characters and check if <code>p</code> is still a subsequence.</p>

<p>Return <em>the <strong>maximum</strong> </em><code>k</code><em> you can choose such that </em><code>p</code><em> is still a <strong>subsequence</strong> of </em><code>s</code><em> after the removals</em>.</p>

<p>A <strong>subsequence</strong> of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;abcacb&quot;, p = &quot;ab&quot;, removable = [3,1,0]
<strong>Output:</strong> 2
<strong>Explanation</strong>: After removing the characters at indices 3 and 1, &quot;a<s><strong>b</strong></s>c<s><strong>a</strong></s>cb&quot; becomes &quot;accb&quot;.
&quot;ab&quot; is a subsequence of &quot;<strong><u>a</u></strong>cc<strong><u>b</u></strong>&quot;.
If we remove the characters at indices 3, 1, and 0, &quot;<s><strong>ab</strong></s>c<s><strong>a</strong></s>cb&quot; becomes &quot;ccb&quot;, and &quot;ab&quot; is no longer a subsequence.
Hence, the maximum k is 2.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;abcbddddd&quot;, p = &quot;abcd&quot;, removable = [3,2,1,4,5,6]
<strong>Output:</strong> 1
<strong>Explanation</strong>: After removing the character at index 3, &quot;abc<s><strong>b</strong></s>ddddd&quot; becomes &quot;abcddddd&quot;.
&quot;abcd&quot; is a subsequence of &quot;<u><strong>abcd</strong></u>dddd&quot;.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;abcab&quot;, p = &quot;abc&quot;, removable = [0,1,2,3,4]
<strong>Output:</strong> 0
<strong>Explanation</strong>: If you remove the first index in the array removable, &quot;abc&quot; is no longer a subsequence.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= p.length &lt;= s.length &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= removable.length &lt; s.length</code></li>
	<li><code>0 &lt;= removable[i] &lt; s.length</code></li>
	<li><code>p</code> is a <strong>subsequence</strong> of <code>s</code>.</li>
	<li><code>s</code> and <code>p</code> both consist of lowercase English letters.</li>
	<li>The elements in <code>removable</code> are <strong>distinct</strong>.</li>
</ul>


## Test Cases
```
"abcacb"
"ab"
[3,1,0]
"abcbddddd"
"abcd"
[3,2,1,4,5,6]
"abcab"
"abc"
[0,1,2,3,4]
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts

### Problem analysis

We are given two strings: `s` and `p`. `p` is a subsequence of `s`. The subsequence of `s` is a new string formed from `s` by deleting some characters (possibly none) without changing the relative order of the remaining characters. Also, we are given an array `removable` that represents the indices of the characters that are removable from `s`. We need to find the maximum number of characters that can be removed from `s` using the first `k` indices in `removable` such that `p` is still a subsequence of `s`.

### Key observations

- If `p` is longer than `s`, it's impossible to form `p` by removing some characters from `s`.
- If `p` is equal to `s`, we can remove any character from `s` without affecting `p`.
- If any character in `p` is at an index in `removable`, then it's impossible to form `p` by removing some characters from `s`.
- If all the characters in `p` are at indices not in `removable`, then we can remove any number of characters from `s` without affecting `p`.
- Otherwise, we need to find the maximum number of characters that can be removed from `s` such that no character in `p` is at an index that is removable.

### Possible approaches

One approach is to try all possible values of `k` from 0 to `removable.length` and check if `p` is still a subsequence of `s` after removing the first `k` characters from `s`. If `p` is still a subsequence of `s`, then we can increase `k` by 1. Otherwise, we can stop and return `k - 1` as the maximum number of characters that can be removed.

Another approach is to find the indices of the characters in `p` in `s`. Then, for each index, we can check if it is in `removable` or not. If it is not in `removable`, then we can increase `k` by 1. Otherwise, we can stop and return `k` as the maximum number of characters that can be removed.

## 2. Solution Implementation
```python
def maximumRemovals(s, p, removable):
    p_idx = 0
    p_len = len(p)
    for r in removable:
        if p_idx < p_len and r >= s.find(p[p_idx]):
            p_idx += 1
        if p_idx == p_len:
            return len(removable)
    return p_idx
```

## 3. Solution Explanation

The provided solution implements the second approach described in the Initial Thoughts section. First, we calculate the length of `p` and `removable`. Then, we use a for loop to iterate over each element in `removable`. Inside the loop, we check if the current character in `p` is equal to the character at the current index in `s`. If it is, we increment the `p_idx` variable. We also check if `p_idx` is equal to `p_len`. If it is, it means that we have found all the characters in `p` in `s`, and we can return the length of `removable`. Otherwise, we continue to the next iteration of the loop.

## 4. Complexity Analysis

### Time complexity

The time complexity of the code is O(s + p), where s is the length of `s` and p is the length of `p`. We iterate over the array `removable` which has a length of s to check if the current character in `p` is equal to the character at the current index in `s`. We also iterate over the string `p` to find the next character in `p`.

### Space complexity

The space complexity of the code is O(1). We only use a few variables to store the current index in `p` and the length of `p`.

## Topics
Array, Two Pointers, String, Binary Search

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-11-29
