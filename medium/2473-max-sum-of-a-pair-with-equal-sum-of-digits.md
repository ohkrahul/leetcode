# Max Sum of a Pair With Equal Sum of Digits

## Problem Link
[LeetCode - Max Sum of a Pair With Equal Sum of Digits](https://leetcode.com/problems/max-sum-of-a-pair-with-equal-sum-of-digits/)

## Difficulty
Medium

## Problem Description
<p>You are given a <strong>0-indexed</strong> array <code>nums</code> consisting of <strong>positive</strong> integers. You can choose two indices <code>i</code> and <code>j</code>, such that <code>i != j</code>, and the sum of digits of the number <code>nums[i]</code> is equal to that of <code>nums[j]</code>.</p>

<p>Return <em>the <strong>maximum</strong> value of </em><code>nums[i] + nums[j]</code><em> that you can obtain over all possible indices </em><code>i</code><em> and </em><code>j</code><em> that satisfy the conditions.</em></p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [18,43,36,13,7]
<strong>Output:</strong> 54
<strong>Explanation:</strong> The pairs (i, j) that satisfy the conditions are:
- (0, 2), both numbers have a sum of digits equal to 9, and their sum is 18 + 36 = 54.
- (1, 4), both numbers have a sum of digits equal to 7, and their sum is 43 + 7 = 50.
So the maximum sum that we can obtain is 54.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [10,12,19,14]
<strong>Output:</strong> -1
<strong>Explanation:</strong> There are no two numbers that satisfy the conditions, so we return -1.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>1 &lt;= nums[i] &lt;= 10<sup>9</sup></code></li>
</ul>


## Test Cases
```
[18,43,36,13,7]
[10,12,19,14]
```

## Initial Template
```python
# Code template not available
```

## Solution
### 1. Initial Thoughts:

- **Problem analysis**: The problem is asking us to find the maximum sum of two numbers in an array such that the sum of their digits is the same.
- **Key observations**: 
    - We can use a dictionary to store the sum of digits of each number in the array.
    - We can iterate over the array and for each number, check if the sum of its digits is in the dictionary. If it is, we can update the maximum sum if the sum of the current number and the number with the same sum of digits is greater than the current maximum sum.
- **Possible approaches**: 
    - Brute force: Iterate over all pairs of numbers in the array and calculate the sum of their digits. If the sum of their digits is the same, update the maximum sum.
    - Using a dictionary: Use a dictionary to store the sum of digits of each number in the array. For each number, check if the sum of its digits is in the dictionary. If it is, update the maximum sum if the sum of the current number and the number with the same sum of digits is greater than the current maximum sum.

### 2. Solution Implementation:
```python
def maxSumOfPairWithEqualSumOfDigits(nums):
    """
    :type nums: List[int]
    :rtype: int
    """
    # Dictionary to store the sum of digits of each number
    sum_of_digits = {}
    # Maximum sum of two numbers with the same sum of digits
    max_sum = -1
    
    for num in nums:
        # Calculate the sum of digits of the current number
        sum = 0
        for digit in str(num):
            sum += int(digit)
        
        # Check if the sum of digits is in the dictionary
        if sum in sum_of_digits:
            # Update the maximum sum if necessary
            max_sum = max(max_sum, num + sum_of_digits[sum])
        else:
            # Add the current number to the dictionary
            sum_of_digits[sum] = num
    
    return max_sum
```

### 3. Solution Explanation:

The provided Python solution leverages a dictionary to efficiently store and access the sum of digits for each number in the `nums` array. Here's how the solution works:

1. It initializes a dictionary called `sum_of_digits` to store the sum of digits for each number in the array.

2. The `max_sum` variable is initialized to -1. This will be used to keep track of the maximum sum of two numbers with the same sum of digits.

3. A `for` loop iterates through each number (`num`) in the `nums` array.

4. For each number, we calculate its sum of digits (`sum`) by iterating through its digits (converted to strings) and adding each digit's value to the `sum`.

5. We then check if `sum` is already present in the `sum_of_digits` dictionary. If it is, we have found another number with the same sum of digits, and we can update `max_sum` if the sum of `num` and the number with the same digits sum is greater than the current `max_sum`.

6. If `sum` is not in the dictionary, we add `num` to the dictionary with `sum` as the key.

7. Finally, the function returns `max_sum`, which represents the maximum sum of two numbers with the same sum of digits found in the array.

### 4. Complexity Analysis:

- **Time complexity**: O(N), where N is the number of elements in the `nums` array. This is because we iterate through the array once to calculate the sum of digits for each number and update the `sum_of_digits` dictionary. Looking up in a dictionary takes O(1) time.

- **Space complexity**: O(M), where M is the number of unique sums of digits encountered in the array. This is because the `sum_of_digits` dictionary stores the sum of digits for each unique number we encounter in the array.

## Topics
Array, Hash Table, Sorting, Heap (Priority Queue)

Solved on: 2024-11-09
