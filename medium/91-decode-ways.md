# Decode Ways

## Problem Link
[LeetCode - Decode Ways](https://leetcode.com/problems/decode-ways/)

## Difficulty
Medium

## Problem Description
<p>You have intercepted a secret message encoded as a string of numbers. The message is <strong>decoded</strong> via the following mapping:</p>

<p><code>&quot;1&quot; -&gt; &#39;A&#39;<br />
&quot;2&quot; -&gt; &#39;B&#39;<br />
...<br />
&quot;25&quot; -&gt; &#39;Y&#39;<br />
&quot;26&quot; -&gt; &#39;Z&#39;</code></p>

<p>However, while decoding the message, you realize that there are many different ways you can decode the message because some codes are contained in other codes (<code>&quot;2&quot;</code> and <code>&quot;5&quot;</code> vs <code>&quot;25&quot;</code>).</p>

<p>For example, <code>&quot;11106&quot;</code> can be decoded into:</p>

<ul>
	<li><code>&quot;AAJF&quot;</code> with the grouping <code>(1, 1, 10, 6)</code></li>
	<li><code>&quot;KJF&quot;</code> with the grouping <code>(11, 10, 6)</code></li>
	<li>The grouping <code>(1, 11, 06)</code> is invalid because <code>&quot;06&quot;</code> is not a valid code (only <code>&quot;6&quot;</code> is valid).</li>
</ul>

<p>Note: there may be strings that are impossible to decode.<br />
<br />
Given a string s containing only digits, return the <strong>number of ways</strong> to <strong>decode</strong> it. If the entire string cannot be decoded in any valid way, return <code>0</code>.</p>

<p>The test cases are generated so that the answer fits in a <strong>32-bit</strong> integer.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">s = &quot;12&quot;</span></p>

<p><strong>Output:</strong> <span class="example-io">2</span></p>

<p><strong>Explanation:</strong></p>

<p>&quot;12&quot; could be decoded as &quot;AB&quot; (1 2) or &quot;L&quot; (12).</p>
</div>

<p><strong class="example">Example 2:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">s = &quot;226&quot;</span></p>

<p><strong>Output:</strong> <span class="example-io">3</span></p>

<p><strong>Explanation:</strong></p>

<p>&quot;226&quot; could be decoded as &quot;BZ&quot; (2 26), &quot;VF&quot; (22 6), or &quot;BBF&quot; (2 2 6).</p>
</div>

<p><strong class="example">Example 3:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">s = &quot;06&quot;</span></p>

<p><strong>Output:</strong> <span class="example-io">0</span></p>

<p><strong>Explanation:</strong></p>

<p>&quot;06&quot; cannot be mapped to &quot;F&quot; because of the leading zero (&quot;6&quot; is different from &quot;06&quot;). In this case, the string is not a valid encoding, so return 0.</p>
</div>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 100</code></li>
	<li><code>s</code> contains only digits and may contain leading zero(s).</li>
</ul>


## Test Cases
```
"12"
"226"
"06"
```

## Initial Template
```python
# Code template not available
```

## Solution
### 1. Initial Thoughts:

The key observation of this problem is that we can break down the decoding problem into subproblems, where each subproblem is to decode a substring of `s`. We can use a bottom-up approach to solve these subproblems, starting from the smallest substring of length 1 and gradually building up to the entire string `s`.

### 2. Solution Implementation:

```python
def numDecodings(s):
    """
    Calculates the number of ways to decode a string `s` of digits into a sequence of letters.

    Args:
        s (str): A string containing only digits.

    Returns:
        int: The number of ways to decode the string.
    """

    # Initialize a dp array to store the number of ways to decode each substring of `s`.
    dp = [0] * (len(s) + 1)

    # Base case: There is only one way to decode an empty string.
    dp[0] = 1

    # Iterate over the string `s`.
    for i in range(1, len(s) + 1):
        # If the current character is not '0', then we can decode it independently.
        if s[i - 1] != '0':
            dp[i] += dp[i - 1]

        # If the current character and the previous character together form a valid two-digit code, then we can decode them together.
        if i > 1 and '10' <= s[i - 2:i] <= '26':
            dp[i] += dp[i - 2]

    # Return the number of ways to decode the entire string.
    return dp[len(s)]
```

### 3. Solution Explanation:

The solution uses dynamic programming to solve the problem. We define a dp array `dp` where `dp[i]` stores the number of ways to decode the substring `s[0:i]`. We initialize `dp[0]` to 1 since there is only one way to decode an empty string.

We then iterate over the string `s`. For each character `s[i]`, we check if it is not '0'. If it is not '0', then we can decode it independently, so we increment `dp[i]` by `dp[i - 1]`.

We also check if the current character and the previous character together form a valid two-digit code. If they do, then we can decode them together, so we increment `dp[i]` by `dp[i - 2]`.

Finally, we return `dp[len(s)]`, which is the number of ways to decode the entire string.

### 4. Complexity Analysis:

* **Time Complexity:** O(n), where n is the length of the string `s`. We iterate over the string once, and each iteration takes constant time.
* **Space Complexity:** O(n). We store the dp array, which has a size of n+1.

## Topics
String, Dynamic Programming

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-01-27
