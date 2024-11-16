# Maximum Population Year

## Problem Link
[LeetCode - Maximum Population Year](https://leetcode.com/problems/maximum-population-year/)

## Difficulty
Easy

## Problem Description
<p>You are given a 2D integer array <code>logs</code> where each <code>logs[i] = [birth<sub>i</sub>, death<sub>i</sub>]</code> indicates the birth and death years of the <code>i<sup>th</sup></code> person.</p>

<p>The <strong>population</strong> of some year <code>x</code> is the number of people alive during that year. The <code>i<sup>th</sup></code> person is counted in year <code>x</code>&#39;s population if <code>x</code> is in the <strong>inclusive</strong> range <code>[birth<sub>i</sub>, death<sub>i</sub> - 1]</code>. Note that the person is <strong>not</strong> counted in the year that they die.</p>

<p>Return <em>the <strong>earliest</strong> year with the <strong>maximum population</strong></em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> logs = [[1993,1999],[2000,2010]]
<strong>Output:</strong> 1993
<strong>Explanation:</strong> The maximum population is 1, and 1993 is the earliest year with this population.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> logs = [[1950,1961],[1960,1971],[1970,1981]]
<strong>Output:</strong> 1960
<strong>Explanation:</strong> 
The maximum population is 2, and it had happened in years 1960 and 1970.
The earlier year between them is 1960.</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= logs.length &lt;= 100</code></li>
	<li><code>1950 &lt;= birth<sub>i</sub> &lt; death<sub>i</sub> &lt;= 2050</code></li>
</ul>


## Test Cases
```
[[1993,1999],[2000,2010]]
[[1950,1961],[1960,1971],[1970,1981]]
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts:
- The problem asks us to find the earliest year with the maximum population.
- The population of a year is the number of people alive during that year, which is equal to the number of people whose birth year is less than or equal to the year and whose death year is greater than or equal to the year.
- We can iterate over all the logs and count the number of people alive in each year.
- The year with the maximum number of people alive is the answer.

## 2. Solution Implementation:
```python
def maximumPopulation(logs):
    # Initialize a dictionary to store the population of each year
    population = {}

    # Iterate over all the logs
    for log in logs:
        # Get the birth year and death year from the log
        birth, death = log
        # Increment the population of each year from the birth year to the death year - 1
        for year in range(birth, death):
            if year not in population:
                population[year] = 0
            population[year] += 1

    # Find the year with the maximum population
    max_population = 0
    max_year = -1
    for year, population in population.items():
        if population > max_population:
            max_population = population
            max_year = year

    return max_year
```

## 3. Solution Explanation:
- The solution iterates over all the logs and counts the number of people alive in each year.
- It uses a dictionary to store the population of each year.
- For each log, it increments the population of each year from the birth year to the death year - 1.
- After iterating over all the logs, the solution finds the year with the maximum population.

## 4. Complexity Analysis:
- Time complexity: O(N * L), where N is the number of logs and L is the number of years.
- Space complexity: O(N), since the dictionary can store up to N elements.

## Topics
Array, Counting, Prefix Sum

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-11-16
