# Binary Watch

## Problem Link
[LeetCode - Binary Watch](https://leetcode.com/problems/binary-watch/)

## Difficulty
Easy

## Problem Description
<p>A binary watch has 4 LEDs on the top to represent the hours (0-11), and 6 LEDs on the bottom to represent&nbsp;the minutes (0-59). Each LED represents a zero or one, with the least significant bit on the right.</p>

<ul>
	<li>For example, the below binary watch reads <code>&quot;4:51&quot;</code>.</li>
</ul>

<p><img alt="" src="https://assets.leetcode.com/uploads/2021/04/08/binarywatch.jpg" style="width: 500px; height: 500px;" /></p>

<p>Given an integer <code>turnedOn</code> which represents the number of LEDs that are currently on (ignoring the PM), return <em>all possible times the watch could represent</em>. You may return the answer in <strong>any order</strong>.</p>

<p>The hour must not contain a leading zero.</p>

<ul>
	<li>For example, <code>&quot;01:00&quot;</code> is not valid. It should be <code>&quot;1:00&quot;</code>.</li>
</ul>

<p>The minute must&nbsp;consist of two digits and may contain a leading zero.</p>

<ul>
	<li>For example, <code>&quot;10:2&quot;</code> is not valid. It should be <code>&quot;10:02&quot;</code>.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> turnedOn = 1
<strong>Output:</strong> ["0:01","0:02","0:04","0:08","0:16","0:32","1:00","2:00","4:00","8:00"]
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> turnedOn = 9
<strong>Output:</strong> []
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= turnedOn &lt;= 10</code></li>
</ul>


## Test Cases
```
1
9
```

## Initial Template
```python
# Code template not available
```

## Solution
## Binary watch with 10 LEDs on.

### Initial Thoughts:
- The problem requires us to find all possible times the watch could represent, given the number of LEDs that are currently on and considering that each LED represents a zero or one.
- Each LED is a bit, and the binary representation of the number of LEDs on gives us the time directly.
- We can loop through all possible binary numbers from 0 to 2^10 and check if the number of 1s in the binary representation is equal to the given number of LEDs on.
- If it is, we convert the binary representation to the time and add it to the list of possible times.

### Solution Implementation:
```python
def readBinaryWatch(turnedOn: int) -> list[str]:
    result = []

    # Loop through all possible numbers from 0 to 2^10
    for i in range(0, 2**10):
        # Count the number of 1s in the binary representation of i
        bits = bin(i)[2:]
        num_ones = bits.count("1")

        # If the number of 1s is equal to the given number of LEDs on
        if num_ones == turnedOn:
            # Convert the binary representation to the time
            hours = bits[:4].lstrip("0") or "0"
            minutes = bits[4:].lstrip("0") or "00"

            # Add the time to the list of possible times
            result.append(f"{hours}:{minutes}")

    return result
```

### Solution Explanation:
The solution works by looping through all possible binary numbers from 0 to 2^10 (which represents 10 LEDs) and checking if the number of 1s in the binary representation of the number is equal to the given number of LEDs on. If it is, the binary representation is converted to the time and added to the list of possible times.

### Complexity Analysis:
- Time complexity: O(2^10 * 10) = O(2^10) since we loop through all possible binary numbers from 0 to 2^10 and each number takes O(10) time to convert to the time.
- Space complexity: O(2^10) since we store all possible times in the list of possible times.

### Test Cases:
1. Input: turnedOn = 1
   - Expected Output: ["0:01","0:02","0:04","0:08","0:16","0:32","1:00","2:00","4:00","8:00"]

2. Input: turnedOn = 9
   - Expected Output: []

## Topics
Backtracking, Bit Manipulation

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-02-17
