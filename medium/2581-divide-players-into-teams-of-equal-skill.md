# Divide Players Into Teams of Equal Skill

## Problem Link
[LeetCode - Divide Players Into Teams of Equal Skill](https://leetcode.com/problems/divide-players-into-teams-of-equal-skill/)

## Difficulty
Medium

## Problem Description
<p>You are given a positive integer array <code>skill</code> of <strong>even</strong> length <code>n</code> where <code>skill[i]</code> denotes the skill of the <code>i<sup>th</sup></code> player. Divide the players into <code>n / 2</code> teams of size <code>2</code> such that the total skill of each team is <strong>equal</strong>.</p>

<p>The <strong>chemistry</strong> of a team is equal to the <strong>product</strong> of the skills of the players on that team.</p>

<p>Return <em>the sum of the <strong>chemistry</strong> of all the teams, or return </em><code>-1</code><em> if there is no way to divide the players into teams such that the total skill of each team is equal.</em></p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> skill = [3,2,5,1,3,4]
<strong>Output:</strong> 22
<strong>Explanation:</strong> 
Divide the players into the following teams: (1, 5), (2, 4), (3, 3), where each team has a total skill of 6.
The sum of the chemistry of all the teams is: 1 * 5 + 2 * 4 + 3 * 3 = 5 + 8 + 9 = 22.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> skill = [3,4]
<strong>Output:</strong> 12
<strong>Explanation:</strong> 
The two players form a team with a total skill of 7.
The chemistry of the team is 3 * 4 = 12.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> skill = [1,1,2,3]
<strong>Output:</strong> -1
<strong>Explanation:</strong> 
There is no way to divide the players into teams such that the total skill of each team is equal.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 &lt;= skill.length &lt;= 10<sup>5</sup></code></li>
	<li><code>skill.length</code> is even.</li>
	<li><code>1 &lt;= skill[i] &lt;= 1000</code></li>
</ul>


## Test Cases
```
[3,2,5,1,3,4]
[3,4]
[1,1,2,3]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem requires pairing up players such that each team has the same total skill.
   - The chemistry is the product of the skills in each pair. We need to maximize the total chemistry.
   - A key observation is that if a solution exists, sorting the array and pairing the lowest with the highest, second lowest with the second highest, and so on will always work and give a valid solution (if one exists).
   - If a valid solution doesn't exist, it means we cannot find a common team skill sum.
   - The approach will be to sort the `skill` array, calculate the target team skill (sum of first and last element), and then iterate inwards, checking if each pair sums up to the target. If not, return -1.  If it does, calculate the chemistry and sum it up.


2. Solution Implementation:
```python
def dividePlayers(skill):
    """
    Divides players into teams of equal skill and calculates the total chemistry.

    Args:
        skill: A list of player skills.

    Returns:
        The total chemistry of all teams, or -1 if no valid division exists.
    """
    n = len(skill)
    skill.sort()
    target_skill = skill[0] + skill[n - 1]
    total_chemistry = 0

    for i in range(n // 2):
        if skill[i] + skill[n - 1 - i] != target_skill:
            return -1
        total_chemistry += skill[i] * skill[n - 1 - i]

    return total_chemistry
```

3. Solution Explanation:
   - The code first sorts the `skill` array.  This is crucial because it allows us to easily find pairs that sum to the same value by iterating from both ends.
   - It then calculates the `target_skill` using the first and last elements of the sorted array.  This will be the sum we'll aim for with every pair.
   - We then iterate through half the array (since we're creating pairs), checking if the sum of elements at `i` and `n-1-i` equals `target_skill`.
   - If any pair doesn't sum to `target_skill`, we know there's no valid solution, so we return -1.
   - If all pairs satisfy the condition, we calculate the chemistry (product of skills in the pair) and add it to `total_chemistry`.
   - Finally, we return `total_chemistry`.

4. Complexity Analysis:
   - Time complexity: O(n log n) - The dominant operation is sorting the `skill` array.  The rest of the code runs in linear time, O(n).
   - Space complexity: O(log n) - This is due to the space used by the sorting algorithm (depending on the implementation. Could be O(n) in worst case for some implementations).  Other than that, we only use constant extra space.


## Topics
Array, Hash Table, Two Pointers, Sorting

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-04-15
