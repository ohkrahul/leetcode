# Remove K Digits

## Problem Link
[LeetCode - Remove K Digits](https://leetcode.com/problems/remove-k-digits/)

## Difficulty
Medium

## Problem Description
<p>Given string num representing a non-negative integer <code>num</code>, and an integer <code>k</code>, return <em>the smallest possible integer after removing</em> <code>k</code> <em>digits from</em> <code>num</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> num = &quot;1432219&quot;, k = 3
<strong>Output:</strong> &quot;1219&quot;
<strong>Explanation:</strong> Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> num = &quot;10200&quot;, k = 1
<strong>Output:</strong> &quot;200&quot;
<strong>Explanation:</strong> Remove the leading 1 and the number is 200. Note that the output must not contain leading zeroes.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> num = &quot;10&quot;, k = 2
<strong>Output:</strong> &quot;0&quot;
<strong>Explanation:</strong> Remove all the digits from the number and it is left with nothing which is 0.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= k &lt;= num.length &lt;= 10<sup>5</sup></code></li>
	<li><code>num</code> consists of only digits.</li>
	<li><code>num</code> does not have any leading zeros except for the zero itself.</li>
</ul>


## Test Cases
```
"1432219"
3
"10200"
1
"10"
2
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - This problem can be solved by identifying the smallest digits to remove.
   - The digits are removed from left to right, so the smallest digits should be removed first.
   - We can use a stack to keep track of the digits that we have seen so far.
   - Whenever we encounter a digit that is smaller than the digit at the top of the stack, we can pop the digit from the stack and add the new digit to the stack.
   - We can repeat this process until we have removed the desired number of digits.

2. Solution Implementation:
```python
def remove_k_digits(num, k):
    """
    :type num: str
    :type k: int
    :rtype: str
    """
    stack = []
    for digit in num:
        # Remove any larger digits from the stack
        while stack and stack[-1] > digit and k:
            stack.pop()
            k -= 1
        stack.append(digit)
    
    # If there are still digits left to remove, remove them from the end
    while k > 0:
        stack.pop()
        k -= 1
    
    # If the stack is empty, return "0"
    if not stack:
        return "0"
    
    # Remove leading zeros
    while stack and stack[0] == '0':
        stack.pop(0)
    
    return ''.join(stack)
```

3. Solution Explanation:
   - The solution works by iterating over the digits in the string and adding them to a stack.
   - Whenever we encounter a digit that is smaller than the digit at the top of the stack, we can pop the digit from the stack and add the new digit to the stack.
   - This ensures that the stack always contains the smallest digits in the string.
   - We can repeat this process until we have removed the desired number of digits.
   - If there are still digits left to remove, we can remove them from the end of the string.
   - If the stack is empty at any point, we can return "0" to indicate that the smallest possible integer is 0.
   - Finally, we can remove any leading zeros from the stack and return the resulting string.

4. Complexity Analysis:
   - Time complexity: O(n), where n is the length of the string. We iterate over the string once to build the stack and once to remove the remaining digits.
   - Space complexity: O(n), where n is the length of the string. We store the digits in a stack, which can hold up to n digits.

## Topics
String, Stack, Greedy, Monotonic Stack

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-18
