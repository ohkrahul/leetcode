# Bank Account Summary II

## Problem Link
[LeetCode - Bank Account Summary II](https://leetcode.com/problems/bank-account-summary-ii/)

## Difficulty
Easy

## Problem Description
<p>Table: <code>Users</code></p>

<pre>
+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| account      | int     |
| name         | varchar |
+--------------+---------+
account is the primary key (column with unique values) for this table.
Each row of this table contains the account number of each user in the bank.
There will be no two users having the same name in the table.
</pre>

<p>&nbsp;</p>

<p>Table: <code>Transactions</code></p>

<pre>
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| trans_id      | int     |
| account       | int     |
| amount        | int     |
| transacted_on | date    |
+---------------+---------+
trans_id is the primary key (column with unique values) for this table.
Each row of this table contains all changes made to all accounts.
amount is positive if the user received money and negative if they transferred money.
All accounts start with a balance of 0.
</pre>

<p>&nbsp;</p>

<p>Write a solution to report the name and balance of users with a balance higher than <code>10000</code>. The balance of an account is equal to the sum of the amounts of all transactions involving that account.</p>

<p>Return the result table in <strong>any order</strong>.</p>

<p>The result format is in the following example.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> 
Users table:
+------------+--------------+
| account    | name         |
+------------+--------------+
| 900001     | Alice        |
| 900002     | Bob          |
| 900003     | Charlie      |
+------------+--------------+
Transactions table:
+------------+------------+------------+---------------+
| trans_id   | account    | amount     | transacted_on |
+------------+------------+------------+---------------+
| 1          | 900001     | 7000       |  2020-08-01   |
| 2          | 900001     | 7000       |  2020-09-01   |
| 3          | 900001     | -3000      |  2020-09-02   |
| 4          | 900002     | 1000       |  2020-09-12   |
| 5          | 900003     | 6000       |  2020-08-07   |
| 6          | 900003     | 6000       |  2020-09-07   |
| 7          | 900003     | -4000      |  2020-09-11   |
+------------+------------+------------+---------------+
<strong>Output:</strong> 
+------------+------------+
| name       | balance    |
+------------+------------+
| Alice      | 11000      |
+------------+------------+
<strong>Explanation:</strong> 
Alice&#39;s balance is (7000 + 7000 - 3000) = 11000.
Bob&#39;s balance is 1000.
Charlie&#39;s balance is (6000 + 6000 - 4000) = 8000.
</pre>


## Test Cases
```
{"headers": {"Users": ["account", "name"], "Transactions": ["trans_id", "account", "amount", "transacted_on"]}, "rows": {"Users": [[900001, "Alice"], [900002, "Bob"], [900003, "Charlie"]], "Transactions": [[1, 900001, 7000, "2020-08-01"], [2, 900001, 7000, "2020-09-01"], [3, 900001, -3000, "2020-09-02"], [4, 900002, 1000, "2020-09-12"], [5, 900003, 6000, "2020-08-07"], [6, 900003, 6000, "2020-09-07"], [7, 900003, -4000, "2020-09-11"]]}}
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:

 - The problem requires us to find the users with a balance greater than `10000` and return their names and balances.
 - We need to combine the data from two tables, `Users` and `Transactions`.
 - To calculate the balance, we need to group the transactions by account and sum up the amounts.
 - We can use a dictionary to store the balances for each user, then filter the dictionary to find the users with a balance greater than `10000`.

2. Solution Implementation:
```python
from collections import defaultdict
from typing import List, Dict, Tuple

class BankAccountSummary:

    def summary(self, users: List[Tuple[int, str]], 
                transactions: List[Tuple[int, int, int, str]]) -> List[Tuple[str, int]]:
        """
        Finds the users with a balance greater than a given threshold.

        :param users: List of tuples representing users. Each tuple contains the user's account number and name.
        :param transactions: List of tuples representing transactions. Each tuple contains the transaction ID, account number, amount, and transaction date.
        :return: List of tuples representing users with a balance greater than a given threshold. Each tuple contains the user's name and balance.
        """
        account_balances = defaultdict(int)

        # Iterate over the transactions and update the account balances
        for _, account, amount, _ in transactions:
            account_balances[account] += amount

        # Filter the account balances to find the users with a balance greater than the threshold
        result = []
        for account, balance in account_balances.items():
            if balance > 10000:
                user_name = [user[1] for user in users if user[0] == account][0]
                result.append((user_name, balance))

        return result
```

3. Solution Explanation:

   - The solution uses a `defaultdict` to store the balances for each user. The `defaultdict` is initialized with a default value of `0`, so if an account is not found in the dictionary, it is automatically added with a balance of `0`.
   - The solution then iterates over the transactions and updates the balances for each account.
   - After all the transactions have been processed, the solution filters the `defaultdict` to find the users with a balance greater than `10000`.

4. Complexity Analysis:
   - Time Complexity: O(N), where N is the total number of transactions. The solution iterates over the transactions once to update the account balances and again to find the users with a balance greater than `10000`.
   - Space Complexity: O(N), where N is the number of users. The solution uses a dictionary to store the balances for each user.

## Topics
Database

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-28
