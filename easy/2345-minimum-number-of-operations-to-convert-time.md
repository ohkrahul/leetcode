# Minimum Number of Operations to Convert Time

## Problem Link
[LeetCode - Minimum Number of Operations to Convert Time](https://leetcode.com/problems/minimum-number-of-operations-to-convert-time/)

## Difficulty
Easy

## Problem Description
<p>You are given two strings <code>current</code> and <code>correct</code> representing two <strong>24-hour times</strong>.</p>

<p>24-hour times are formatted as <code>&quot;HH:MM&quot;</code>, where <code>HH</code> is between <code>00</code> and <code>23</code>, and <code>MM</code> is between <code>00</code> and <code>59</code>. The earliest 24-hour time is <code>00:00</code>, and the latest is <code>23:59</code>.</p>

<p>In one operation you can increase the time <code>current</code> by <code>1</code>, <code>5</code>, <code>15</code>, or <code>60</code> minutes. You can perform this operation <strong>any</strong> number of times.</p>

<p>Return <em>the <strong>minimum number of operations</strong> needed to convert </em><code>current</code><em> to </em><code>correct</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> current = &quot;02:30&quot;, correct = &quot;04:35&quot;
<strong>Output:</strong> 3
<strong>Explanation:
</strong>We can convert current to correct in 3 operations as follows:
- Add 60 minutes to current. current becomes &quot;03:30&quot;.
- Add 60 minutes to current. current becomes &quot;04:30&quot;.
- Add 5 minutes to current. current becomes &quot;04:35&quot;.
It can be proven that it is not possible to convert current to correct in fewer than 3 operations.</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> current = &quot;11:00&quot;, correct = &quot;11:01&quot;
<strong>Output:</strong> 1
<strong>Explanation:</strong> We only have to add one minute to current, so the minimum number of operations needed is 1.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>current</code> and <code>correct</code> are in the format <code>&quot;HH:MM&quot;</code></li>
	<li><code>current &lt;= correct</code></li>
</ul>


## Test Cases
```
"02:30"
"04:35"
"11:00"
"11:01"
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**
   
   - **Problem analysis**: This problem asks us to find the minimum number of operations needed to convert a given time `current` to another time `correct`, where each operation can increase the time by 1, 5, 15, or 60 minutes.
   
   - **Key observations:** 
   - We are only allowed to add time to `current`, not subtract it.
   - The minimum number of operations will be the smallest number that we can achieve by adding 1, 5, 15, or 60 minutes to `current` until it becomes equal to `correct`.
   
   - **Possible approaches:** 
   - **Brute force**: We can list all the possible combinations of operations that can be applied to `current` and then check which one gives us `correct` with the minimum number of operations. However, this approach has a time complexity of O(4^n), where n is the difference in minutes between `current` and `correct`, and it will be too slow for large inputs.
   - **Greedy**: We can apply the largest possible operation that still doesn't make `current` greater than `correct`. This approach has a time complexity of O(log n), where n is the difference in minutes between `current` and `correct`.
   
2. **Solution Implementation:**
```python
def convertTime(current, correct):
    """
    :type current: str
    :type correct: str
    :rtype: int
    """
    # Convert the times to minutes
    current_minutes = int(current[:2]) * 60 + int(current[3:])
    correct_minutes = int(correct[:2]) * 60 + int(correct[3:])

    # Calculate the difference between the times in minutes
    diff = correct_minutes - current_minutes

    # Calculate the minimum number of operations needed
    operations = 0
    while diff > 0:
        if diff >= 60:
            operations += 1
            diff -= 60
        elif diff >= 15:
            operations += 1
            diff -= 15
        elif diff >= 5:
            operations += 1
            diff -= 5
        else:
            operations += 1
            diff -= 1

    # Return the minimum number of operations
    return operations
```
3. **Solution Explanation:**

   - The solution implements a greedy approach to find the minimum number of operations needed to convert `current` to `correct`.

   - First, we convert both `current` and `correct` to minutes, and then we calculate the difference between them.

   - We then iterate over the difference in minutes, adding 1, 5, 15, or 60 minutes to `current` at each iteration, until it becomes equal to `correct`.

   - We count the number of operations needed, and return it.

4. **Complexity Analysis:**
   
   - **Time complexity**: O(log n), where n is the difference in minutes between `current` and `correct`.
   
   - **Space complexity**: O(1), since we only use a few variables, regardless of the input size.

## Topics
String, Greedy

Solved on: 2024-11-09
