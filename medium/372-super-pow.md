# Super Pow

## Problem Link
[LeetCode - Super Pow](https://leetcode.com/problems/super-pow/)

## Difficulty
Medium

## Problem Description
<p>Your task is to calculate <code>a<sup>b</sup></code> mod <code>1337</code> where <code>a</code> is a positive integer and <code>b</code> is an extremely large positive integer given in the form of an array.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> a = 2, b = [3]
<strong>Output:</strong> 8
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> a = 2, b = [1,0]
<strong>Output:</strong> 1024
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> a = 1, b = [4,3,3,8,5,2]
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= a &lt;= 2<sup>31</sup> - 1</code></li>
	<li><code>1 &lt;= b.length &lt;= 2000</code></li>
	<li><code>0 &lt;= b[i] &lt;= 9</code></li>
	<li><code>b</code> does not contain leading zeros.</li>
</ul>


## Test Cases
```
2
[3]
2
[1,0]
1
[4,3,3,8,5,2]
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**

   - This problem is essentially asking us to find the remainder when `a^b` is divided by 1337, where `a` is a positive integer and `b` is a very large positive integer.
   - Key observations are that:
     - We can use modular exponentiation to compute `a^b` efficiently.
     - We can work with `b` in reverse order, applying modular exponentiation at each digit to reduce the problem to smaller subproblems.

   - A possible approach is to use the following steps:
     - Convert the list `b` into an integer.
     - Use modular exponentiation to compute `a^b` modulo 1337.

2. **Solution Implementation:**
```python
def superPow(a: int, b: List[int]) -> int:
    MOD = 1337  # Given modulo value
    
    # Convert the list 'b' into an integer
    num = 0
    for digit in b:
        num = num * 10 + digit
    
    # Use modular exponentiation to compute 'a^b' modulo 1337
    result = pow(a, num, MOD)
    
    return result
```

3. **Solution Explanation:**

   - We first convert the input list `b` into an integer `num`. This is necessary because the modular exponentiation function expects the exponent to be an integer.
   - We then use the `pow` function to calculate `a^num` modulo 1337. The `pow` function takes three arguments: the base, the exponent, and the modulus.
   - The `pow` function computes `a^num` using the binary exponentiation algorithm, which is an efficient way to compute exponentiation.
   - The result of the `pow` function is the remainder when `a^num` is divided by 1337. We return this result as the answer.

4. **Complexity Analysis:**

   - **Time complexity:** O(n), where n is the number of digits in the input list `b`. The time complexity is dominated by the conversion of `b` into an integer and the modular exponentiation operation.
   - **Space complexity:** O(1). The algorithm does not require any additional space beyond the input list `b` and the result variable.

## Topics
Math, Divide and Conquer

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-02-20
