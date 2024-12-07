# Triangle Judgement

## Problem Link
[LeetCode - Triangle Judgement](https://leetcode.com/problems/triangle-judgement/)

## Difficulty
Easy

## Problem Description
<p>Table: <code>Triangle</code></p>

<pre>
+-------------+------+
| Column Name | Type |
+-------------+------+
| x           | int  |
| y           | int  |
| z           | int  |
+-------------+------+
In SQL, (x, y, z) is the primary key column for this table.
Each row of this table contains the lengths of three line segments.
</pre>

<p>&nbsp;</p>

<p>Report for every three line segments whether they can form a triangle.</p>

<p>Return the result table in <strong>any order</strong>.</p>

<p>The&nbsp;result format is in the following example.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> 
Triangle table:
+----+----+----+
| x  | y  | z  |
+----+----+----+
| 13 | 15 | 30 |
| 10 | 20 | 15 |
+----+----+----+
<strong>Output:</strong> 
+----+----+----+----------+
| x  | y  | z  | triangle |
+----+----+----+----------+
| 13 | 15 | 30 | No       |
| 10 | 20 | 15 | Yes      |
+----+----+----+----------+
</pre>


## Test Cases
```
{"headers":{"Triangle":["x","y","z"]},"rows":{"Triangle":[[13,15,30],[10,20,15]]}}
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**

   - **Problem analysis:** The problem presents a table containing the lengths of three line segments and asks us to determine if they can form a valid triangle.
   - **Key observations:** For a valid triangle, the sum of the lengths of any two sides must be greater than the length of the remaining side. In other words, x + y > z, x + z > y, and y + z > x.
   - **Possible approaches:** We can check all three conditions for each row and conclude whether it represents a valid triangle or not.

2. **Solution Implementation:**

```python
# Import the necessary package for database operations
import pandas as pd

# Create a function to check if three line segments can form a triangle
def is_triangle(x, y, z):
    # Check if the sum of any two sides is greater than the remaining side
    if x + y <= z or x + z <= y or y + z <= x:
        return 'No'
    else:
        return 'Yes'

# Read the input data into a Pandas DataFrame
df = pd.DataFrame({"x": [13, 10], "y": [15, 20], "z": [30, 15]})

# Apply the is_triangle function to each row of the DataFrame
df["triangle"] = df.apply(lambda row: is_triangle(*row.values), axis=1)

# Print the result
print(df)
```

3. **Solution Explanation:**

   - The provided Python function `is_triangle` takes three integers `x`, `y`, and `z`, representing the lengths of the line segments. It checks if any two sides' sum is less than the remaining side. If so, it returns 'No' to indicate that the segments cannot form a valid triangle. Otherwise, it returns 'Yes'.
   - The main program reads the input data into a Pandas DataFrame with columns `x`, `y`, and `z`.
   - It then uses the `apply` function to apply the `is_triangle` function to each row of the DataFrame, adding a new column named `triangle` with the result.
   - Finally, the program prints the DataFrame, which contains the input segments and a column indicating whether they can form a triangle.

4. **Complexity Analysis:**

   - **Time complexity:** O(`n`), where `n` is the number of rows in the input table. The solution involves a single pass over the data.
   - **Space complexity:** O(1). The solution does not require any additional space beyond that of the input data.

## Topics
Database

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-12-07
