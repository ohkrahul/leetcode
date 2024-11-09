# Find All Lonely Numbers in the Array

## Problem Link
[LeetCode - Find All Lonely Numbers in the Array](https://leetcode.com/problems/find-all-lonely-numbers-in-the-array/)

## Difficulty
Medium

## Problem Description
<p>You are given an integer array <code>nums</code>. A number <code>x</code> is <strong>lonely</strong> when it appears only <strong>once</strong>, and no <strong>adjacent</strong> numbers (i.e. <code>x + 1</code> and <code>x - 1)</code> appear in the array.</p>

<p>Return <em><strong>all</strong> lonely numbers in </em><code>nums</code>. You may return the answer in <strong>any order</strong>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [10,6,5,8]
<strong>Output:</strong> [10,8]
<strong>Explanation:</strong> 
- 10 is a lonely number since it appears exactly once and 9 and 11 does not appear in nums.
- 8 is a lonely number since it appears exactly once and 7 and 9 does not appear in nums.
- 5 is not a lonely number since 6 appears in nums and vice versa.
Hence, the lonely numbers in nums are [10, 8].
Note that [8, 10] may also be returned.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,3,5,3]
<strong>Output:</strong> [1,5]
<strong>Explanation:</strong> 
- 1 is a lonely number since it appears exactly once and 0 and 2 does not appear in nums.
- 5 is a lonely number since it appears exactly once and 4 and 6 does not appear in nums.
- 3 is not a lonely number since it appears twice.
Hence, the lonely numbers in nums are [1, 5].
Note that [5, 1] may also be returned.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= nums[i] &lt;= 10<sup>6</sup></code></li>
</ul>


## Test Cases
```
[10,6,5,8]
[1,3,5,3]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**

   - The problem asks us to find all lonely numbers in an array, where a lonely number appears only once and no adjacent numbers appear in the array.
   - We can first create a dictionary to store the count of each number in the array.
   - Then, we can iterate over the dictionary and check if the count of a number is 1 and if its adjacent numbers do not exist in the dictionary. If so, we add the number to the list of lonely numbers.

2. **Solution Implementation:**
```python
def findLonelyNumbers(nums):
    """
    :type nums: List[int]
    :rtype: List[int]
    """
    # Create a dictionary to store the count of each number
    num_count = {}
    for num in nums:
        if num not in num_count:
            num_count[num] = 0
        num_count[num] += 1

    # Initialize a list to store the lonely numbers
    lonely_nums = []
    
    # Iterate over the dictionary
    for num, count in num_count.items():
        # Check if the count is 1 and the adjacent numbers do not exist in the dictionary
        if count == 1 and (num + 1 not in num_count) and (num - 1 not in num_count):
            lonely_nums.append(num)
    
    # Return the list of lonely numbers
    return lonely_nums
```

3. **Solution Explanation:**

   - The solution first creates a dictionary to store the count of each number in the array.
   - Then, it iterates over the dictionary and checks if the count of a number is 1 and if its adjacent numbers do not exist in the dictionary. If so, it adds the number to the list of lonely numbers.
   - Finally, the solution returns the list of lonely numbers.

4. **Complexity Analysis:**

   - Time complexity: O(n), where n is the length of the array. We iterate over the array once to create the dictionary and once to find the lonely numbers.
   - Space complexity: O(n), since we store the count of each number in the dictionary.

## Topics
Array, Hash Table, Counting

Solved on: 2024-11-09
