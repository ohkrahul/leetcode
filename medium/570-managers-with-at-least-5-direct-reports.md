# Managers with at Least 5 Direct Reports

## Problem Link
[LeetCode - Managers with at Least 5 Direct Reports](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/)

## Difficulty
Medium

## Problem Description
<p>Table: <code>Employee</code></p>

<pre>
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| id          | int     |
| name        | varchar |
| department  | varchar |
| managerId   | int     |
+-------------+---------+
id is the primary key (column with unique values) for this table.
Each row of this table indicates the name of an employee, their department, and the id of their manager.
If managerId is null, then the employee does not have a manager.
No employee will be the manager of themself.
</pre>

<p>&nbsp;</p>

<p>Write a solution to find managers with at least <strong>five direct reports</strong>.</p>

<p>Return the result table in <strong>any order</strong>.</p>

<p>The result format is in the following example.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> 
Employee table:
+-----+-------+------------+-----------+
| id  | name  | department | managerId |
+-----+-------+------------+-----------+
| 101 | John  | A          | null      |
| 102 | Dan   | A          | 101       |
| 103 | James | A          | 101       |
| 104 | Amy   | A          | 101       |
| 105 | Anne  | A          | 101       |
| 106 | Ron   | B          | 101       |
+-----+-------+------------+-----------+
<strong>Output:</strong> 
+------+
| name |
+------+
| John |
+------+
</pre>


## Test Cases
```
{"headers": {"Employee": ["id", "name", "department", "managerId"]}, "rows": {"Employee": [[101, "John", "A", null],[102, "Dan", "A", 101], [103, "James", "A", 101], [104, "Amy", "A", 101], [105, "Anne", "A", 101], [106, "Ron", "B", 101]]}}
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem requires us to find managers who have at least 5 direct reports.  
   - Direct reports mean employees whose `managerId` matches the `id` of the manager.
   - We can use grouping and aggregation to count the number of reports for each manager.
   - We'll need to join the `Employee` table with itself to relate managers and their reports.  A self join.
   - Finally, we filter the result to only include managers with 5 or more reports.

2. Solution Implementation:
```python
import pandas as pd

def find_managers(employee: pd.DataFrame) -> pd.DataFrame:
    """
    Finds managers with at least 5 direct reports.

    Args:
        employee: The Employee table as a Pandas DataFrame.

    Returns:
        A DataFrame with the names of managers having at least 5 reports.
    """
    
    # Rename columns for clarity in the self-join
    managers = employee.rename(columns={'id': 'managerId', 'name': 'managerName'})
    reports = employee.rename(columns={'id': 'employeeId', 'name': 'employeeName'})

    # Perform a left join to match managers with their reports. 
    # We use a left join to keep all managers, even if they don't have any reports.
    merged_df = pd.merge(managers, reports, on='managerId', how='left')

    # Group by manager name and count the number of reports
    report_counts = merged_df.groupby('managerName')['employeeId'].count().reset_index()

    # Filter for managers with at least 5 reports. Rename count column
    #   to conform to Leetcode expected output.
    result = report_counts[report_counts['employeeId'] >= 5][['managerName']].rename(columns={'managerName':'name'})
    
    return result
```

3. Solution Explanation:
   - The code first renames columns in the `employee` dataframe to avoid confusion during the self-join.  This makes the join condition clearer.
   - Then it joins the table with itself using a left join on `managerId`. This connects each employee record with their manager's record (if they have one).  
   - It then groups the resulting data by `managerName` and counts the number of reports each manager has using `count()`. 
   - Finally, it filters the grouped data to include only managers with 5 or more reports and selects only the 'name' column as required by the problem description.

4. Complexity Analysis:
   - Time complexity: O(n log n) - The dominant factor is the sorting during the merge operation in `pd.merge()`, which has a time complexity of O(n log n) in the worst case, where n is the number of rows in the `employee` table. The grouping and filtering operations have a time complexity of O(n).
   - Space complexity: O(n) -  The space complexity is dominated by the merged DataFrame created by the `pd.merge()` operation which can be at most n^2 in the worst case scenario (everyone reports to one person) but more likely n*r where r is the average number of reports per manager. The `groupby` and filtering operations require additional space proportional to the number of managers, which is at most O(n).  Since Leetcode's test case has a much smaller r, we simplified to O(n).


## Topics
Database

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-04-09
