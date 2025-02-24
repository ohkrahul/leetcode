# Smallest String With Swaps

## Problem Link
[LeetCode - Smallest String With Swaps](https://leetcode.com/problems/smallest-string-with-swaps/)

## Difficulty
Medium

## Problem Description
<p>You are given a string <code>s</code>, and an array of pairs of indices in the string&nbsp;<code>pairs</code>&nbsp;where&nbsp;<code>pairs[i] =&nbsp;[a, b]</code>&nbsp;indicates 2 indices(0-indexed) of the string.</p>

<p>You can&nbsp;swap the characters at any pair of indices in the given&nbsp;<code>pairs</code>&nbsp;<strong>any number of times</strong>.</p>

<p>Return the&nbsp;lexicographically smallest string that <code>s</code>&nbsp;can be changed to after using the swaps.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;dcab&quot;, pairs = [[0,3],[1,2]]
<strong>Output:</strong> &quot;bacd&quot;
<strong>Explaination:</strong> 
Swap s[0] and s[3], s = &quot;bcad&quot;
Swap s[1] and s[2], s = &quot;bacd&quot;
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;dcab&quot;, pairs = [[0,3],[1,2],[0,2]]
<strong>Output:</strong> &quot;abcd&quot;
<strong>Explaination: </strong>
Swap s[0] and s[3], s = &quot;bcad&quot;
Swap s[0] and s[2], s = &quot;acbd&quot;
Swap s[1] and s[2], s = &quot;abcd&quot;</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;cba&quot;, pairs = [[0,1],[1,2]]
<strong>Output:</strong> &quot;abc&quot;
<strong>Explaination: </strong>
Swap s[0] and s[1], s = &quot;bca&quot;
Swap s[1] and s[2], s = &quot;bac&quot;
Swap s[0] and s[1], s = &quot;abc&quot;
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10^5</code></li>
	<li><code>0 &lt;= pairs.length &lt;= 10^5</code></li>
	<li><code>0 &lt;= pairs[i][0], pairs[i][1] &lt;&nbsp;s.length</code></li>
	<li><code>s</code>&nbsp;only contains lower case English letters.</li>
</ul>


## Test Cases
```
"dcab"
[[0,3],[1,2]]
"dcab"
[[0,3],[1,2],[0,2]]
"cba"
[[0,1],[1,2]]
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts

### Problem Analysis
The goal of the problem is to find the smallest string that can be formed by swapping characters in pairs within a given list of pairs.

### Key Observations
- The problem can be solved by grouping characters that can be swapped together.
- The smallest string can be formed by sorting the characters within each group.

### Possible Approaches
- **Union Find**: Use a union-find data structure to group characters that can be swapped together.
- **DFS**: Perform a depth-first search starting from each character to find all the characters that can be swapped with it.

## 2. Solution Implementation
```python
from collections import defaultdict
from functools import reduce

def smallestStringWithSwaps(s, pairs):
    """
    :type s: str
    :type pairs: List[List[int]]
    :rtype: str
    """
    # Create a union-find data structure to group characters that can be swapped together.
    parent = [i for i in range(len(s))]
    rank = [1 for i in range(len(s))]

    def find(x):
        if parent[x] != x:
            parent[x] = find(parent[x])
        return parent[x]

    def union(x, y):
        x_root = find(x)
        y_root = find(y)
        if x_root != y_root:
            if rank[x_root] > rank[y_root]:
                parent[y_root] = x_root
                rank[x_root] += rank[y_root]
            else:
                parent[x_root] = y_root
                rank[y_root] += rank[x_root]

    # Create a map from the parent of each character to the characters in its group.
    groups = defaultdict(list)
    for i, c in enumerate(s):
        groups[find(i)].append(i)

    # Sort the characters within each group.
    for group in groups.values():
        group.sort(key=lambda x: s[x])

    # Build the smallest string by concatenating the sorted characters within each group.
    t = []
    for group in groups.values():
        t.extend([s[i] for i in group])
    return reduce(lambda x, y: x + y, t, "")
```

## 3. Solution Explanation
The solution uses a union-find data structure to group characters that can be swapped together. The `find` function is used to find the parent of a character, which represents the root of the group to which it belongs. The `union` function is used to merge two groups together.

Once the groups have been formed, the characters within each group are sorted. This ensures that the smallest string is formed when the characters are concatenated together.

## 4. Complexity Analysis
### Time Complexity: O(n^2)
- The `find` and `union` operations take O(α(n)) time, where α(n) is the inverse Ackermann function.
- There are at most n union operations, and each union operation takes O(α(n)) time.
- There are n characters, and each character needs to be sorted, which takes O(n log n) time.
- Therefore, the total time complexity is O(n^2).

### Space Complexity: O(n)
- The `parent` and `rank` arrays take O(n) space.
- The `groups` dictionary takes O(n) space.
- Therefore, the total space complexity is O(n).

## Topics
Array, Hash Table, String, Depth-First Search, Breadth-First Search, Union Find, Sorting

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-02-24
