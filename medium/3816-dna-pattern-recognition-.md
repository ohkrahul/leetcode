# DNA Pattern Recognition 

## Problem Link
[LeetCode - DNA Pattern Recognition ](https://leetcode.com/problems/dna-pattern-recognition/)

## Difficulty
Medium

## Problem Description
<p>Table: <code>Samples</code></p>

<pre>
+----------------+---------+
| Column Name    | Type    | 
+----------------+---------+
| sample_id      | int     |
| dna_sequence   | varchar |
| species        | varchar |
+----------------+---------+
sample_id is the unique key for this table.
Each row contains a DNA sequence represented as a string of characters (A, T, G, C) and the species it was collected from.
</pre>

<p>Biologists are studying basic patterns in DNA sequences. Write a solution to identify <code>sample_id</code> with the following patterns:</p>

<ul>
	<li>Sequences that <strong>start</strong> with <strong>ATG</strong>&nbsp;(a common <strong>start codon</strong>)</li>
	<li>Sequences that <strong>end</strong> with either <strong>TAA</strong>, <strong>TAG</strong>, or <strong>TGA</strong>&nbsp;(<strong>stop codons</strong>)</li>
	<li>Sequences containing the motif <strong>ATAT</strong>&nbsp;(a simple repeated pattern)</li>
	<li>Sequences that have <strong>at least</strong> <code>3</code> <strong>consecutive</strong> <strong>G</strong>&nbsp;(like <strong>GGG</strong>&nbsp;or <strong>GGGG</strong>)</li>
</ul>

<p>Return <em>the result table ordered by&nbsp;</em><em>sample_id in <strong>ascending</strong> order</em>.</p>

<p>The result format is in the following example.</p>

<p>&nbsp;</p>
<p><strong class="example">Example:</strong></p>

<div class="example-block">
<p><strong>Input:</strong></p>

<p>Samples table:</p>

<pre class="example-io">
+-----------+------------------+-----------+
| sample_id | dna_sequence     | species   |
+-----------+------------------+-----------+
| 1         | ATGCTAGCTAGCTAA  | Human     |
| 2         | GGGTCAATCATC     | Human     |
| 3         | ATATATCGTAGCTA   | Human     |
| 4         | ATGGGGTCATCATAA  | Mouse     |
| 5         | TCAGTCAGTCAG     | Mouse     |
| 6         | ATATCGCGCTAG     | Zebrafish |
| 7         | CGTATGCGTCGTA    | Zebrafish |
+-----------+------------------+-----------+
</pre>

<p><strong>Output:</strong></p>

<pre class="example-io">
+-----------+------------------+-------------+-------------+------------+------------+------------+
| sample_id | dna_sequence     | species     | has_start   | has_stop   | has_atat   | has_ggg    |
+-----------+------------------+-------------+-------------+------------+------------+------------+
| 1         | ATGCTAGCTAGCTAA  | Human       | 1           | 1          | 0          | 0          |
| 2         | GGGTCAATCATC     | Human       | 0           | 0          | 0          | 1          |
| 3         | ATATATCGTAGCTA   | Human       | 0           | 0          | 1          | 0          |
| 4         | ATGGGGTCATCATAA  | Mouse       | 1           | 1          | 0          | 1          |
| 5         | TCAGTCAGTCAG     | Mouse       | 0           | 0          | 0          | 0          |
| 6         | ATATCGCGCTAG     | Zebrafish   | 0           | 1          | 1          | 0          |
| 7         | CGTATGCGTCGTA    | Zebrafish   | 0           | 0          | 0          | 0          |
+-----------+------------------+-------------+-------------+------------+------------+------------+
</pre>

<p><strong>Explanation:</strong></p>

<ul>
	<li>Sample 1 (ATGCTAGCTAGCTAA):
	<ul>
		<li>Starts with ATG&nbsp;(has_start = 1)</li>
		<li>Ends with TAA&nbsp;(has_stop = 1)</li>
		<li>Does not contain ATAT&nbsp;(has_atat = 0)</li>
		<li>Does not contain at least 3 consecutive &#39;G&#39;s (has_ggg = 0)</li>
	</ul>
	</li>
	<li>Sample 2 (GGGTCAATCATC):
	<ul>
		<li>Does not start with ATG&nbsp;(has_start = 0)</li>
		<li>Does not end with TAA, TAG, or TGA&nbsp;(has_stop = 0)</li>
		<li>Does not contain ATAT&nbsp;(has_atat = 0)</li>
		<li>Contains GGG&nbsp;(has_ggg = 1)</li>
	</ul>
	</li>
	<li>Sample 3 (ATATATCGTAGCTA):
	<ul>
		<li>Does not start with ATG&nbsp;(has_start = 0)</li>
		<li>Does not end with TAA, TAG, or TGA&nbsp;(has_stop = 0)</li>
		<li>Contains ATAT&nbsp;(has_atat = 1)</li>
		<li>Does not contain at least 3 consecutive &#39;G&#39;s (has_ggg = 0)</li>
	</ul>
	</li>
	<li>Sample 4 (ATGGGGTCATCATAA):
	<ul>
		<li>Starts with ATG&nbsp;(has_start = 1)</li>
		<li>Ends with TAA&nbsp;(has_stop = 1)</li>
		<li>Does not contain ATAT&nbsp;(has_atat = 0)</li>
		<li>Contains GGGG&nbsp;(has_ggg = 1)</li>
	</ul>
	</li>
	<li>Sample 5 (TCAGTCAGTCAG):
	<ul>
		<li>Does not match any patterns (all fields = 0)</li>
	</ul>
	</li>
	<li>Sample 6 (ATATCGCGCTAG):
	<ul>
		<li>Does not start with ATG&nbsp;(has_start = 0)</li>
		<li>Ends with TAG&nbsp;(has_stop = 1)</li>
		<li>Starts with ATAT&nbsp;(has_atat = 1)</li>
		<li>Does not contain at least 3 consecutive &#39;G&#39;s (has_ggg = 0)</li>
	</ul>
	</li>
	<li>Sample 7 (CGTATGCGTCGTA):
	<ul>
		<li>Does not start with ATG&nbsp;(has_start = 0)</li>
		<li>Does not end with TAA, &quot;TAG&quot;, or &quot;TGA&quot; (has_stop = 0)</li>
		<li>Does not contain ATAT&nbsp;(has_atat = 0)</li>
		<li>Does not contain at least 3 consecutive &#39;G&#39;s (has_ggg = 0)</li>
	</ul>
	</li>
</ul>

<p><strong>Note:</strong></p>

<ul>
	<li>The result is ordered by sample_id in ascending order</li>
	<li>For each pattern, 1 indicates the pattern is present and 0 indicates it is not present</li>
</ul>
</div>


## Test Cases
```
{"headers":{"Samples":["sample_id","dna_sequence","species"]},"rows":{"Samples":[[1,"ATGCTAGCTAGCTAA","Human"],[2,"GGGTCAATCATC","Human"],[3,"ATATATCGTAGCTA","Human"],[4,"ATGGGGTCATCATAA","Mouse"],[5,"TCAGTCAGTCAG","Mouse"],[6,"ATATCGCGCTAG","Zebrafish"],[7,"CGTATGCGTCGTA","Zebrafish"]]}}
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem requires us to check for specific patterns within DNA sequences stored in a table.
   - We need to check for start codon (ATG), stop codons (TAA, TAG, TGA), the motif ATAT, and at least three consecutive Gs.
   - We can use string manipulation functions in SQL (or any other language) like `startswith`, `endswith`, `LIKE`, and regular expressions to achieve this.
   - The final result needs to be ordered by `sample_id`.

2. Solution Implementation:
```python
import pandas as pd

def solve():
    data = pd.DataFrame({
        'sample_id': [1, 2, 3, 4, 5, 6, 7],
        'dna_sequence': ['ATGCTAGCTAGCTAA', 'GGGTCAATCATC', 'ATATATCGTAGCTA', 'ATGGGGTCATCATAA', 'TCAGTCAGTCAG', 'ATATCGCGCTAG', 'CGTATGCGTCGTA'],
        'species': ['Human', 'Human', 'Human', 'Mouse', 'Mouse', 'Zebrafish', 'Zebrafish']
    })

    data['has_start'] = data['dna_sequence'].apply(lambda x: 1 if x.startswith('ATG') else 0)
    data['has_stop'] = data['dna_sequence'].apply(lambda x: 1 if x.endswith(('TAA', 'TAG', 'TGA')) else 0)
    data['has_atat'] = data['dna_sequence'].apply(lambda x: 1 if 'ATAT' in x else 0)
    data['has_ggg'] = data['dna_sequence'].apply(lambda x: 1 if 'GGG' in x else 0)  # Could use regex for more flexibility (e.g., G{3,})

    print(data)


solve()

```

3. Solution Explanation:
   - I used pandas DataFrame for a convenient way to manipulate the data (assuming we have the data available in a compatible format).  This could be directly implemented with SQL as well.
   - `startswith()` and `endswith()` methods are used to check the start and end codons respectively. `endswith()` conveniently accepts a tuple of strings.
   - The `in` operator is used to check if 'ATAT' exists in the sequence.
   - Similarly, `in` checks for the presence of 'GGG'. (Note: Using a regular expression `G{3,}`  would allow matching three or *more* consecutive 'G's if that's the strict requirement).
   - The results are stored as new columns ('has_start', 'has_stop', 'has_atat', 'has_ggg') with values 1 or 0 based on pattern presence.


4. Complexity Analysis:
   - Time complexity: O(N*M) - where N is the number of rows in the table, and M is the average length of the `dna_sequence`. This is due to string operations like `startswith`, `endswith`, and `in` having a time complexity proportional to the length of the string.
   - Space complexity: O(N) -  We are creating new columns to store the pattern match results, so the space complexity grows linearly with the number of rows in the input table. If we were doing this in-place in a database, the space complexity might be lower.


## Topics
Database

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-21
