# Delete Duplicate Emails

## Problem Link
[LeetCode - Delete Duplicate Emails](https://leetcode.com/problems/delete-duplicate-emails/)

## Difficulty
Easy

## Problem Description
<p>Table: <code>Person</code></p>

<pre>
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| id          | int     |
| email       | varchar |
+-------------+---------+
id is the primary key (column with unique values) for this table.
Each row of this table contains an email. The emails will not contain uppercase letters.
</pre>

<p>&nbsp;</p>

<p>Write a solution to<strong> delete</strong> all duplicate emails, keeping only one unique email with the smallest <code>id</code>.</p>

<p>For SQL users, please note that you are supposed to write a <code>DELETE</code> statement and not a <code>SELECT</code> one.</p>

<p>For Pandas users, please note that you are supposed to modify <code>Person</code> in place.</p>

<p>After running your script, the answer shown is the <code>Person</code> table. The driver will first compile and run your piece of code and then show the <code>Person</code> table. The final order of the <code>Person</code> table <strong>does not matter</strong>.</p>

<p>The result format is in the following example.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> 
Person table:
+----+------------------+
| id | email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |
+----+------------------+
<strong>Output:</strong> 
+----+------------------+
| id | email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
+----+------------------+
<strong>Explanation:</strong> john@example.com is repeated two times. We keep the row with the smallest Id = 1.
</pre>


## Test Cases
```
{"headers": {"Person": ["id", "email"]}, "rows": {"Person": [[1, "john@example.com"], [2, "bob@example.com"], [3, "john@example.com"]]}}
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts:
- This problem is about deleting duplicate emails from a table. Each row in the table represents a person, and the primary key is the `id` column. 
- We need to keep the row with the smallest `id` for each unique email. 
- We can achieve this using a `DELETE` statement with subqueries.

## 2. Solution Implementation:
```python
# Get the minimum IDs for each unique email.
min_ids = (Person
    .groupby('email')
    ['id']
    .min()
    .reset_index()
)

# Rename the 'id' column to 'min_id'.
min_ids = min_ids.rename(columns={'id': 'min_id'})

# Join the minimum IDs table with the original table.
result = Person.merge(min_ids, on='email')

# Get the rows where the 'id' column is equal to the 'min_id' column.
result = result[result['id'] == result['min_id']]

# Delete the duplicate rows.
Person.drop(Person.index.difference(result.index), inplace=True)
```

## 3. Solution Explanation:
- The first subquery finds the minimum `id` for each unique email.
- We then rename the `id` column to `min_id`.
- We join the minimum IDs table with the original table.
- We then get the rows where the `id` column is equal to the `min_id` column. This gives us the rows that we want to keep.
- Finally, we delete all the other rows.
```
assert Person.equals(pd.DataFrame(
    {"id": [1, 2],
     "email": ["john@example.com", "bob@example.com"]}
))
```

## 4. Complexity Analysis:
- Time complexity: [O(n log n)] - We have to sort the table by `email` first, which takes O(n log n) time. Then we have to iterate through the table, which takes O(n) time.
- Space complexity: [O(n)] - We need to store the sorted table in memory.

## Topics
Database

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-23
