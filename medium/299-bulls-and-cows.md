# Bulls and Cows

## Problem Link
[LeetCode - Bulls and Cows](https://leetcode.com/problems/bulls-and-cows/)

## Difficulty
Medium

## Problem Description
<p>You are playing the <strong><a href="https://en.wikipedia.org/wiki/Bulls_and_Cows" target="_blank">Bulls and Cows</a></strong> game with your friend.</p>

<p>You write down a secret number and ask your friend to guess what the number is. When your friend makes a guess, you provide a hint with the following info:</p>

<ul>
	<li>The number of &quot;bulls&quot;, which are digits in the guess that are in the correct position.</li>
	<li>The number of &quot;cows&quot;, which are digits in the guess that are in your secret number but are located in the wrong position. Specifically, the non-bull digits in the guess that could be rearranged such that they become bulls.</li>
</ul>

<p>Given the secret number <code>secret</code> and your friend&#39;s guess <code>guess</code>, return <em>the hint for your friend&#39;s guess</em>.</p>

<p>The hint should be formatted as <code>&quot;xAyB&quot;</code>, where <code>x</code> is the number of bulls and <code>y</code> is the number of cows. Note that both <code>secret</code> and <code>guess</code> may contain duplicate digits.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> secret = &quot;1807&quot;, guess = &quot;7810&quot;
<strong>Output:</strong> &quot;1A3B&quot;
<strong>Explanation:</strong> Bulls are connected with a &#39;|&#39; and cows are underlined:
&quot;1807&quot;
  |
&quot;<u>7</u>8<u>10</u>&quot;</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> secret = &quot;1123&quot;, guess = &quot;0111&quot;
<strong>Output:</strong> &quot;1A1B&quot;
<strong>Explanation:</strong> Bulls are connected with a &#39;|&#39; and cows are underlined:
&quot;1123&quot;        &quot;1123&quot;
  |      or     |
&quot;01<u>1</u>1&quot;        &quot;011<u>1</u>&quot;
Note that only one of the two unmatched 1s is counted as a cow since the non-bull digits can only be rearranged to allow one 1 to be a bull.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= secret.length, guess.length &lt;= 1000</code></li>
	<li><code>secret.length == guess.length</code></li>
	<li><code>secret</code> and <code>guess</code> consist of digits only.</li>
</ul>


## Test Cases
```
"1807"
"7810"
"1123"
"0111"
```

## Initial Template
```python
# Code template not available
```

## Solution
1. **Initial Thoughts:**

   - The problem is asking for the number of bulls and cows in a guess given a secret number.
   - Bulls are digits in the guess that are in the correct position, while cows are digits in the guess that are in the secret number but are in the wrong position.
   - A straightforward approach would be to iterate over the digits of the guess and compare them with the corresponding digits in the secret number.

2. **Solution Implementation:**
```python
def getHint(secret, guess):
    """
    :type secret: str
    :type guess: str
    :rtype: str
    """
    bulls = 0
    cows = 0
    secret_dict = {}
    
    # Count the number of bulls and cows
    for i in range(len(secret)):
        if secret[i] == guess[i]:
            bulls += 1
        else:
            if secret[i] not in secret_dict:
                secret_dict[secret[i]] = 0
            secret_dict[secret[i]] += 1
            if guess[i] in secret_dict and secret_dict[guess[i]] > 0:
                cows += 1
                secret_dict[guess[i]] -= 1
    
    return str(bulls) + "A" + str(cows) + "B"
```

3. **Solution Explanation:**

   - The solution starts by initializing two variables, `bulls` and `cows`, to 0.
   - It then creates a dictionary, `secret_dict`, to store the count of each digit in the secret number.
   - The solution then iterates over the digits of the guess and compares them with the corresponding digits in the secret number.
   - If the digits match, the solution increments the `bulls` count.
   - If the digits do not match, the solution checks if the secret digit is in the `secret_dict` dictionary. If it is, the solution increments the `cows` count and decrements the count of the secret digit in the dictionary.
   - Finally, the solution returns a string containing the number of bulls and cows, in the format "xAyB", where x is the number of bulls and y is the number of cows.

4. **Complexity Analysis:**

   - **Time complexity:** The time complexity of the solution is O(n), where n is the length of the secret and guess strings. The solution iterates over the digits of the guess and compares them with the corresponding digits in the secret number.
   - **Space complexity:** The space complexity of the solution is O(n), where n is the number of unique digits in the secret number. The solution uses a dictionary to store the count of each digit in the secret number.

## Topics
Hash Table, String, Counting

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-11-14
