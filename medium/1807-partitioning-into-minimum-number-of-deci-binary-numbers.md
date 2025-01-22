# Partitioning Into Minimum Number Of Deci-Binary Numbers

## Problem Link
[LeetCode - Partitioning Into Minimum Number Of Deci-Binary Numbers](https://leetcode.com/problems/partitioning-into-minimum-number-of-deci-binary-numbers/)

## Difficulty
Medium

## Problem Description
<p>A decimal number is called <strong>deci-binary</strong> if each of its digits is either <code>0</code> or <code>1</code> without any leading zeros. For example, <code>101</code> and <code>1100</code> are <strong>deci-binary</strong>, while <code>112</code> and <code>3001</code> are not.</p>

<p>Given a string <code>n</code> that represents a positive decimal integer, return <em>the <strong>minimum</strong> number of positive <strong>deci-binary</strong> numbers needed so that they sum up to </em><code>n</code><em>.</em></p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> n = &quot;32&quot;
<strong>Output:</strong> 3
<strong>Explanation:</strong> 10 + 11 + 11 = 32
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> n = &quot;82734&quot;
<strong>Output:</strong> 8
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> n = &quot;27346209830709182346&quot;
<strong>Output:</strong> 9
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n.length &lt;= 10<sup>5</sup></code></li>
	<li><code>n</code> consists of only digits.</li>
	<li><code>n</code> does not contain any leading zeros and represents a positive integer.</li>
</ul>


## Test Cases
```
"32"
"82734"
"27346209830709182346"
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**
   - This problem is about finding the minimum number of deci-binary numbers that sum up to a given decimal number.
   - A deci-binary number is a number that consists of only 0s and 1s.
   - We can use a greedy approach to solve this problem. We can repeatedly take the largest possible deci-binary number from the given number until the given number becomes 0.

2. **Solution Implementation:**
```python
def minPartitions(n):
    """
    :type n: str
    :rtype: int
    """
    ans = 0
    
    for digit in n:
        ans = max(ans, int(digit))
        
    return ans
```

3. **Solution Explanation:**
   - The solution is based on the greedy approach described above.
   - We iterate over the digits of the given number and find the largest digit.
   - We then update the answer to be the maximum of the current answer and the largest digit.
   - We repeat this process until all the digits of the given number have been processed.
   - Finally, we return the answer.

4. **Complexity Analysis:**
   - Time complexity: O(n), where n is the length of the given number.
   - Space complexity: O(1).


## Topics
String, Greedy

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-22
