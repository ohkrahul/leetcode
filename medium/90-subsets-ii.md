# Subsets II

## Problem Link
[LeetCode - Subsets II](https://leetcode.com/problems/subsets-ii/)

## Difficulty
Medium

## Problem Description
<p>Given an integer array <code>nums</code> that may contain duplicates, return <em>all possible</em> <span data-keyword="subset"><em>subsets</em></span><em> (the power set)</em>.</p>

<p>The solution set <strong>must not</strong> contain duplicate subsets. Return the solution in <strong>any order</strong>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [1,2,2]
<strong>Output:</strong> [[],[1],[1,2],[1,2,2],[2],[2,2]]
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [0]
<strong>Output:</strong> [[],[0]]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10</code></li>
	<li><code>-10 &lt;= nums[i] &lt;= 10</code></li>
</ul>


## Test Cases
```
[1,2,2]
[0]
```

## Initial Template
```python
# Code template not available
```

## Solution
## Initial Thoughts:
### Problem Analysis
* The problem asks us to find all subsets (the power set) of an integer array containing duplicates.
* The solution set should not contain duplicate subsets.

### Key Observations
* Each element in the array can be either included or excluded in a subset.
* If we take this approach recursively, we can generate all possible subsets.

### Possible Approaches
* **Recursive approach**: Try all possible combinations of including or excluding each element.

## Solution Implementation:
```python
def subsetsWithDup(nums):
    """
    :type nums: List[int]
    :rtype: List[List[int]]
    """
    # Sort the array to group duplicates together
    nums.sort()
    
    result = []
    # Start with an empty subset
    result.append([])
    
    start = 0
    end = 0
    
    for i in range(len(nums)):
        # If the current element is the same as the previous one, skip it to avoid duplicates
        if i > 0 and nums[i] == nums[i-1]:
            start = end
        end = len(result)
        
        # Add the current element to each existing subset
        for j in range(start, end):
            result.append(result[j] + [nums[i]])
    
    return result
```

## Solution Explanation:
### How the solution works
The solution uses a recursive approach to generate all possible subsets. It starts with an empty subset and iterates through the array, trying all possible combinations of including or excluding each element.

To avoid generating duplicate subsets, the array is first sorted to group duplicates together. Then, when adding each element to the existing subsets, we skip any duplicates by comparing it to the previous element.

### Key steps and logic explained
1. Sort the array to group duplicates together.
2. Initialize the result list with an empty subset.
3. Iterate through the array, keeping track of the start and end indices of the subsets to be updated.
4. For each element in the array, add it to each existing subset.
5. Skip duplicate elements by comparing the current element to the previous one.

### Why this approach is effective
This approach is effective because it systematically tries all possible combinations of elements, while avoiding duplicates by grouping them together using sorting.

## Complexity Analysis:
### Time Complexity: O(n * 2^n)
* The outer loop iterates over n elements.
* For each element, we create 2^n subsets.

### Space Complexity: O(n * 2^n)
* The result list can contain up to 2^n subsets.
* Each subset is of size at most n.

## Topics
Array, Backtracking, Bit Manipulation

Solved on: 2024-11-09
