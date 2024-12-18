# Implement Rand10() Using Rand7()

## Problem Link
[LeetCode - Implement Rand10() Using Rand7()](https://leetcode.com/problems/implement-rand10-using-rand7/)

## Difficulty
Medium

## Problem Description
<p>Given the <strong>API</strong> <code>rand7()</code> that generates a uniform random integer in the range <code>[1, 7]</code>, write a function <code>rand10()</code> that generates a uniform random integer in the range <code>[1, 10]</code>. You can only call the API <code>rand7()</code>, and you shouldn&#39;t call any other API. Please <strong>do not</strong> use a language&#39;s built-in random API.</p>

<p>Each test case will have one <strong>internal</strong> argument <code>n</code>, the number of times that your implemented function <code>rand10()</code> will be called while testing. Note that this is <strong>not an argument</strong> passed to <code>rand10()</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> n = 1
<strong>Output:</strong> [2]
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> n = 2
<strong>Output:</strong> [2,8]
</pre><p><strong class="example">Example 3:</strong></p>
<pre><strong>Input:</strong> n = 3
<strong>Output:</strong> [3,8,10]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 10<sup>5</sup></code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong></p>

<ul>
	<li>What is the <a href="https://en.wikipedia.org/wiki/Expected_value" target="_blank">expected value</a> for the number of calls to <code>rand7()</code> function?</li>
	<li>Could you minimize the number of calls to <code>rand7()</code>?</li>
</ul>


## Test Cases
```
1
2
3
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**

   - **Problem analysis:** The problem asks us to create a function that generates random numbers between 1 and 10 using an API that only generates random numbers between 1 and 7.
   - **Key observations:** We can use the fact that there is a 1/7 chance of getting any number between 1 and 7. We can use this to create a function that generates random numbers between 1 and 10.
   - **Possible approaches:** One possible approach is to simply generate 7 random numbers and then map them to a number between 1 and 10. However, this approach is not very efficient as it requires generating 7 random numbers for each random number that we want to generate. A more efficient approach is to use the `Rejection Sampling` technique.

2. **Solution Implementation:**
```python
import random
def rand10():
    while True:
        num1 = rand7()
        num2 = rand7()
        idx = (num1 - 1) * 7 + num2
        if idx <= 40:
            return idx % 10 + 1
```

3. **Solution Explanation:**

   - The `rand10()` function first generates two random numbers, `num1` and `num2`, between 1 and 7 using the `rand7()` function.
   - It then calculates the index `idx` using the formula `idx = (num1 - 1) * 7 + num2`.
   - If `idx` is less than or equal to 40, it means that we have generated a random number between 1 and 40. We then return the remainder of `idx` divided by 10 plus 1. This gives us a random number between 1 and 10.
   - If `idx` is greater than 40, we discard the generated numbers and repeat the process until we get a valid `idx`.

4. **Complexity Analysis:**

   - **Time complexity:** The time complexity of the `rand10()` function is O(1). This is because the function generates a random number in constant time.
   - **Space complexity:** The space complexity of the `rand10()` function is O(1). This is because the function does not store any additional data structures.

## Topics
Math, Rejection Sampling, Randomized, Probability and Statistics

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-12-18
