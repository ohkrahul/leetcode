# Zigzag Conversion

## Problem Link
[LeetCode - Zigzag Conversion](https://leetcode.com/problems/zigzag-conversion/)

## Difficulty
Medium

## Problem Description
<p>The string <code>&quot;PAYPALISHIRING&quot;</code> is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)</p>

<pre>
P   A   H   N
A P L S I I G
Y   I   R
</pre>

<p>And then read line by line: <code>&quot;PAHNAPLSIIGYIR&quot;</code></p>

<p>Write the code that will take a string and make this conversion given a number of rows:</p>

<pre>
string convert(string s, int numRows);
</pre>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;PAYPALISHIRING&quot;, numRows = 3
<strong>Output:</strong> &quot;PAHNAPLSIIGYIR&quot;
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;PAYPALISHIRING&quot;, numRows = 4
<strong>Output:</strong> &quot;PINALSIGYAHRPI&quot;
<strong>Explanation:</strong>
P     I    N
A   L S  I G
Y A   H R
P     I
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;A&quot;, numRows = 1
<strong>Output:</strong> &quot;A&quot;
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 1000</code></li>
	<li><code>s</code> consists of English letters (lower-case and upper-case), <code>&#39;,&#39;</code> and <code>&#39;.&#39;</code>.</li>
	<li><code>1 &lt;= numRows &lt;= 1000</code></li>
</ul>


## Test Cases
```
"PAYPALISHIRING"
3
"PAYPALISHIRING"
4
"A"
1
```

## Initial Template
```python
# Code template not available
```

## Solution
### 1. Initial Thoughts:

- The problem asks us to convert a string into a zigzag pattern, given the number of rows, and then read line by line.
- We can visualize the pattern as a matrix, where each row represents a line in the zigzag pattern.
- A key observation is that the pattern repeats itself every 2 * (numRows - 1) characters. This means that we can divide the string into chunks of this length and process them separately.

### 2. Solution Implementation:
```python
def convert(s, numRows):
    """
    :type s: str
    :type numRows: int
    :rtype: str
    """
    if numRows == 1 or numRows >= len(s):
        return s
    
    zigzag = [[] for _ in range(numRows)]
    row, col = 0, 0
    going_down = False

    for char in s:
        zigzag[row].append(char)
        if row == 0 or row == numRows - 1:
            going_down = not going_down
        if going_down:
            row += 1
        else:
            row -= 1
    
    return ''.join(''.join(row) for row in zigzag)
```

### 3. Solution Explanation:

- We first handle edge cases where the number of rows is 1 or greater than or equal to the length of the string.
- We create a list of lists (`zigzag`) to represent the zigzag pattern, with each sublist representing a row.
- We initialize the `row` and `col` to 0, representing the top-left corner of the "matrix".
- We also keep track of whether we are currently going down (`going_down`) or going up.
- We then iterate over each character in the string and add the character to the current row's list.
- We change the `row` and `going_down` values based on the current row. If we reach the top or bottom row, we change the direction.
- Finally, we join all the rows together to form the final zigzag pattern.

### 4. Complexity Analysis:

- Time complexity: O(N), where N is the length of the string. We iterate over each character in the string once.
- Space complexity: O(N), since we create a list of lists to store the zigzag pattern.

## Topics
String

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-02-14
