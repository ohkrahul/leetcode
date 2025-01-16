# Concatenation of Consecutive Binary Numbers

## Problem Link
[LeetCode - Concatenation of Consecutive Binary Numbers](https://leetcode.com/problems/concatenation-of-consecutive-binary-numbers/)

## Difficulty
Medium

## Problem Description
<p>Given an integer <code>n</code>, return <em>the <strong>decimal value</strong> of the binary string formed by concatenating the binary representations of </em><code>1</code><em> to </em><code>n</code><em> in order, <strong>modulo </strong></em><code>10<sup>9 </sup>+ 7</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> n = 1
<strong>Output:</strong> 1
<strong>Explanation: </strong>&quot;1&quot; in binary corresponds to the decimal value 1. 
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> n = 3
<strong>Output:</strong> 27
<strong>Explanation: </strong>In binary, 1, 2, and 3 corresponds to &quot;1&quot;, &quot;10&quot;, and &quot;11&quot;.
After concatenating them, we have &quot;11011&quot;, which corresponds to the decimal value 27.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> n = 12
<strong>Output:</strong> 505379714
<strong>Explanation</strong>: The concatenation results in &quot;1101110010111011110001001101010111100&quot;.
The decimal value of that is 118505380540.
After modulo 10<sup>9</sup> + 7, the result is 505379714.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 10<sup>5</sup></code></li>
</ul>


## Test Cases
```
1
3
12
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts

- **Problem analysis:** We need to find the decimal value of a binary string formed by concatenating the binary representations of 1 to n. Since the binary string can be very large, we need to modulo the result by 10<sup>9</sup> + 7 to avoid overflow.

- **Key observations:**
  - The binary representation of a number is just the number in base 2.
  - We can concatenate binary strings by simply appending them together.
  - We can convert a binary string to a decimal value by multiplying each digit by 2<sup>i</sup>, where i is the position of the digit in the binary string.

- **Possible approaches:**
  - **Brute force:** Concatenate the binary representations of 1 to n and then convert the resulting binary string to a decimal value. This approach is not efficient for large n.
  - **Dynamic programming:** Store the decimal value of the binary string formed by concatenating the binary representations of 1 to i for each i from 1 to n. This approach is more efficient than the brute force approach but still requires us to iterate through all the numbers from 1 to n.

## 2. Solution Implementation
```python
def concatenatedBinary(n):
  mod = 10 ** 9 + 7

  # Initialize the decimal value of the binary string to 0
  res = 0

  # Iterate through the numbers from 1 to n
  for i in range(1, n + 1):
    # Get the binary representation of the number
    binary = bin(i)[2:]

    # Calculate the length of the binary representation
    length = len(binary)

    # Shift the decimal value of the binary string by the length of the binary representation
    res = (res << length) % mod

    # Add the decimal value of the binary representation to the decimal value of the binary string
    res = (res + int(binary, 2)) % mod

  return res
```

## 3. Solution Explanation
The solution uses a dynamic programming approach to calculate the decimal value of the binary string formed by concatenating the binary representations of 1 to n. It initializes the decimal value of the binary string to 0 and then iterates through the numbers from 1 to n. For each number, it gets the binary representation of the number and calculates the length of the binary representation. It then shifts the decimal value of the binary string by the length of the binary representation and adds the decimal value of the binary representation to the decimal value of the binary string. Finally, it returns the decimal value of the binary string modulo 10<sup>9</sup> + 7.

## 4. Complexity Analysis
- **Time complexity:** O(n log n) - We iterate through the numbers from 1 to n, and for each number, we calculate the binary representation of the number, which takes O(log n) time.

- **Space complexity:** O(1) - We store a constant number of variables in memory, regardless of the size of n.

## Topics
Math, Bit Manipulation, Simulation

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-16
