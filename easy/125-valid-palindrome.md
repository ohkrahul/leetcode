# Valid Palindrome

## Problem Link
[LeetCode - Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

## Difficulty
Easy

## Problem Description
<p>A phrase is a <strong>palindrome</strong> if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.</p>

<p>Given a string <code>s</code>, return <code>true</code><em> if it is a <strong>palindrome</strong>, or </em><code>false</code><em> otherwise</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;A man, a plan, a canal: Panama&quot;
<strong>Output:</strong> true
<strong>Explanation:</strong> &quot;amanaplanacanalpanama&quot; is a palindrome.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;race a car&quot;
<strong>Output:</strong> false
<strong>Explanation:</strong> &quot;raceacar&quot; is not a palindrome.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> s = &quot; &quot;
<strong>Output:</strong> true
<strong>Explanation:</strong> s is an empty string &quot;&quot; after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 2 * 10<sup>5</sup></code></li>
	<li><code>s</code> consists only of printable ASCII characters.</li>
</ul>


## Test Cases
```
"A man, a plan, a canal: Panama"
"race a car"
" "
```

## Initial Template
```python
# Code template not available
```

## Solution
1. Initial Thoughts:
   - The problem asks us to check if a given string is a palindrome after cleaning it up (removing non-alphanumeric characters and converting to lowercase).
   - Key observation: We only care about alphanumeric characters and their case doesn't matter.
   - Possible approaches:
     - **Two pointers:** We can have two pointers, one starting from the beginning and the other from the end of the cleaned string.  We move them inwards, comparing characters at each step. If they ever differ, it's not a palindrome.
     - **Filter and Reverse:**  We could filter out the non-alphanumeric characters, convert to lowercase, then reverse the resulting string and compare with the original (cleaned) string. This might be slightly less efficient due to string reversal. I'll go with the two-pointer approach.


2. Solution Implementation:
```python
def isPalindrome(s):
    """
    Checks if a string is a palindrome after cleaning (alphanumeric and lowercase).

    Args:
        s: The input string.

    Returns:
        True if it's a palindrome, False otherwise.
    """
    left, right = 0, len(s) - 1

    while left < right:
        # Skip non-alphanumeric characters from the left
        while left < right and not s[left].isalnum():
            left += 1

        # Skip non-alphanumeric characters from the right
        while left < right and not s[right].isalnum():
            right -= 1

        # Compare the characters (case-insensitive)
        if s[left].lower() != s[right].lower():
            return False

        left += 1
        right -= 1

    return True  # If the loop completes without finding mismatches, it's a palindrome
```

3. Solution Explanation:
   - The `isPalindrome` function takes a string `s` as input.
   - We initialize two pointers, `left` and `right`, to the beginning and end of the string, respectively.
   - The `while left < right` loop continues as long as the pointers haven't crossed each other.
   - Inside the loop, we skip over any non-alphanumeric characters by incrementing `left` or decrementing `right`.
   - Once we have alphanumeric characters at both pointers, we convert them to lowercase using `.lower()` and compare them.  If they are not equal, we return `False`.
   - If the loop completes without returning `False`, it means all corresponding characters matched, and the cleaned string is a palindrome.  We return `True`.


4. Complexity Analysis:
   - Time complexity: O(n) - We traverse the string at most once. Even though we have nested while loops for skipping non-alphanumeric characters, each character is checked at most once.
   - Space complexity: O(1) - We only use a few extra variables (pointers and temporary characters for comparison), so the space used is constant regardless of the input string size.


## Topics
Two Pointers, String

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2025-03-01
