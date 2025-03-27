# Jewels and Stones

## Problem Link
[LeetCode - Jewels and Stones](https://leetcode.com/problems/jewels-and-stones/)

## Difficulty
Easy

## Problem Description
<p>You&#39;re given strings <code>jewels</code> representing the types of stones that are jewels, and <code>stones</code> representing the stones you have. Each character in <code>stones</code> is a type of stone you have. You want to know how many of the stones you have are also jewels.</p>

<p>Letters are case sensitive, so <code>&quot;a&quot;</code> is considered a different type of stone from <code>&quot;A&quot;</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> jewels = "aA", stones = "aAAbbbb"
<strong>Output:</strong> 3
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> jewels = "z", stones = "ZZ"
<strong>Output:</strong> 0
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;=&nbsp;jewels.length, stones.length &lt;= 50</code></li>
	<li><code>jewels</code> and <code>stones</code> consist of only English letters.</li>
	<li>All the characters of&nbsp;<code>jewels</code> are <strong>unique</strong>.</li>
</ul>


## Test Cases
```
"aA"
"aAAbbbb"
"z"
"ZZ"
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - Problem analysis: We are given two strings, `jewels` and `stones`. Each character in `jewels` represents a type of jewel, and each character in `stones` represents a type of stone we have. We need to count how many stones we have that are also jewels.
   - Key observations:  Case sensitivity matters.  The `jewels` string contains unique characters.  The strings are relatively short (max length 50).
   - Possible approaches: 
     - We could iterate through each stone in `stones` and check if it exists in `jewels`. We can use a `set` for `jewels` to make the lookup faster (O(1) on average).  This seems like the most straightforward and efficient approach.
     - We could also use a counter (dictionary) to count the occurrences of each stone type and then iterate through the `jewels` to sum up the counts of the jewel types.  However, this seems less efficient than the set approach, especially because we don't need to know the individual counts of each jewel type, just the total.


2. Solution Implementation:
```python
def numJewelsInStones(jewels: str, stones: str) -> int:
    """
    Counts the number of stones that are also jewels.

    Args:
        jewels: A string representing the types of stones that are jewels.
        stones: A string representing the stones we have.

    Returns:
        The number of stones that are also jewels.
    """

    jewels_set = set(jewels)  # Convert jewels to a set for O(1) lookup
    count = 0

    for stone in stones:
        if stone in jewels_set:
            count += 1

    return count


```

3. Solution Explanation:
   - How the solution works: The code first converts the `jewels` string into a set called `jewels_set`. Sets provide efficient (O(1) on average) membership checking. Then, the code iterates through each character (stone) in the `stones` string. For each stone, it checks if the stone is present in the `jewels_set`. If it is, the `count` is incremented. Finally, the function returns the total `count` of jewels found in the stones.
   - Key steps and logic explained: The key to efficiency is using the `set` data structure for fast lookups of whether a given stone is a jewel. The rest is a simple linear scan of the `stones` string.
   - Why this approach is effective: This approach is effective because it leverages the fast membership checking of sets, minimizing the time complexity. It also avoids unnecessary computations like counting the occurrences of individual jewel types, focusing solely on determining the total number of jewels.

4. Complexity Analysis:
   - Time complexity: O(m + n) - where m is the length of `jewels` and n is the length of `stones`. Converting `jewels` to a set takes O(m) time, and iterating through `stones` takes O(n) time. 
   - Space complexity: O(m) - The space complexity is dominated by the space used to store the `jewels_set`, which is proportional to the length of `jewels` (m).


## Topics
Hash Table, String

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-27
