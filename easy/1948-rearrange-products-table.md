# Rearrange Products Table

## Problem Link
[LeetCode - Rearrange Products Table](https://leetcode.com/problems/rearrange-products-table/)

## Difficulty
Easy

## Problem Description
<p>Table: <code>Products</code></p>

<pre>
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| product_id  | int     |
| store1      | int     |
| store2      | int     |
| store3      | int     |
+-------------+---------+
product_id is the primary key (column with unique values) for this table.
Each row in this table indicates the product&#39;s price in 3 different stores: store1, store2, and store3.
If the product is not available in a store, the price will be null in that store&#39;s column.
</pre>

<p>&nbsp;</p>

<p>Write a solution to rearrange the <code>Products</code> table so that each row has <code>(product_id, store, price)</code>. If a product is not available in a store, do <strong>not</strong> include a row with that <code>product_id</code> and <code>store</code> combination in the result table.</p>

<p>Return the result table in <strong>any order</strong>.</p>

<p>The result format is in the following example.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> 
Products table:
+------------+--------+--------+--------+
| product_id | store1 | store2 | store3 |
+------------+--------+--------+--------+
| 0          | 95     | 100    | 105    |
| 1          | 70     | null   | 80     |
+------------+--------+--------+--------+
<strong>Output:</strong> 
+------------+--------+-------+
| product_id | store  | price |
+------------+--------+-------+
| 0          | store1 | 95    |
| 0          | store2 | 100   |
| 0          | store3 | 105   |
| 1          | store1 | 70    |
| 1          | store3 | 80    |
+------------+--------+-------+
<strong>Explanation:</strong> 
Product 0 is available in all three stores with prices 95, 100, and 105 respectively.
Product 1 is available in store1 with price 70 and store3 with price 80. The product is not available in store2.
</pre>


## Test Cases
```
{"headers":{"Products":["product_id","store1","store2","store3"]},"rows":{"Products":[[0, 95, 100, 105], [1, 70, null, 80]]}}
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks us to transform the `Products` table from a wide format to a long format.  We need to pivot the store columns (store1, store2, store3) into a single 'store' column and their corresponding values into a 'price' column.
   - We should only include rows where the price is not null.
   - We can achieve this using a `UNION ALL` operation to combine the results of selecting from each store column individually.

2. Solution Implementation:
```python
import pandas as pd

def rearrange_products(products: pd.DataFrame) -> pd.DataFrame:
    """
    Rearranges the Products table to a long format.

    Args:
        products: The input Products DataFrame.

    Returns:
        The rearranged DataFrame.
    """

    store1_df = products[['product_id', 'store1']].rename(columns={'store1': 'price'})
    store1_df['store'] = 'store1'
    store1_df = store1_df[store1_df['price'].notna()]  # Filter out null prices


    store2_df = products[['product_id', 'store2']].rename(columns={'store2': 'price'})
    store2_df['store'] = 'store2'
    store2_df = store2_df[store2_df['price'].notna()]


    store3_df = products[['product_id', 'store3']].rename(columns={'store3': 'price'})
    store3_df['store'] = 'store3'
    store3_df = store3_df[store3_df['price'].notna()]

    result_df = pd.concat([store1_df, store2_df, store3_df], ignore_index=True)
    
    return result_df[['product_id', 'store', 'price']]  # Ensure correct column order
```

3. Solution Explanation:
   - We create three separate DataFrames, `store1_df`, `store2_df`, and `store3_df`, each corresponding to one store column.
   - For each DataFrame, we rename the store column to 'price' and add a new 'store' column with the store name.
   - Crucially, we filter out rows where the 'price' is null using `.notna()`. This ensures we only include available products.
   - We then concatenate these three DataFrames using `pd.concat` to get the final `result_df`.
   - Finally, we return the DataFrame with the specified column order: `product_id`, `store`, `price`.

4. Complexity Analysis:
   - Time complexity: O(n) - We iterate through the rows of the input DataFrame a constant number of times (3 times for each store). Concatenation is also linear in the number of rows.
   - Space complexity: O(n) - We create three temporary DataFrames that are roughly the same size as the input DataFrame in the worst case (if all products are available in all stores). However, if there are many null values, the space complexity could be less than O(n).  The concatenated `result_df` will also take up space proportional to the number of non-null entries.


## Topics
Database

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-20
