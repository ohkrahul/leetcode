# Student Attendance Record I

## Problem Link
[LeetCode - Student Attendance Record I](https://leetcode.com/problems/student-attendance-record-i/)

## Difficulty
Easy

## Problem Description
<p>You are given a string <code>s</code> representing an attendance record for a student where each character signifies whether the student was absent, late, or present on that day. The record only contains the following three characters:</p>

<ul>
	<li><code>&#39;A&#39;</code>: Absent.</li>
	<li><code>&#39;L&#39;</code>: Late.</li>
	<li><code>&#39;P&#39;</code>: Present.</li>
</ul>

<p>The student is eligible for an attendance award if they meet <strong>both</strong> of the following criteria:</p>

<ul>
	<li>The student was absent (<code>&#39;A&#39;</code>) for <strong>strictly</strong> fewer than 2 days <strong>total</strong>.</li>
	<li>The student was <strong>never</strong> late (<code>&#39;L&#39;</code>) for 3 or more <strong>consecutive</strong> days.</li>
</ul>

<p>Return <code>true</code><em> if the student is eligible for an attendance award, or </em><code>false</code><em> otherwise</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;PPALLP&quot;
<strong>Output:</strong> true
<strong>Explanation:</strong> The student has fewer than 2 absences and was never late 3 or more consecutive days.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;PPALLL&quot;
<strong>Output:</strong> false
<strong>Explanation:</strong> The student was late 3 consecutive days in the last 3 days, so is not eligible for the award.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 1000</code></li>
	<li><code>s[i]</code> is either <code>&#39;A&#39;</code>, <code>&#39;L&#39;</code>, or <code>&#39;P&#39;</code>.</li>
</ul>


## Test Cases
```
"PPALLP"
"PPALLL"
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts:
- **Problem analysis**: This problem asks us to check if a student is eligible for an attendance award based on their attendance record. The student must have fewer than 2 absences and never be late for 3 or more consecutive days.
- **Key observations**: We need to count the number of absences and check for consecutive late records.
- **Possible approaches**: One approach is to iterate over the string and count the number of absences and consecutive late days. Another approach is to use regular expressions to match the patterns we are looking for.

## 2. Solution Implementation:
```python
def checkRecord(s: str) -> bool:
    """
    Checks if a student is eligible for an attendance award based on their attendance record.

    Args:
        s (str): The student's attendance record.

    Returns:
        bool: True if the student is eligible for the award, False otherwise.
    """
    # Count the number of absences
    absences = 0
    # Count the number of consecutive late days
    consecutive_late = 0

    for c in s:
        # Increment the absences count if the character is 'A'
        if c == 'A':
            absences += 1
            # Reset the consecutive late days count to 0
            consecutive_late = 0
        # Increment the consecutive late days count if the character is 'L'
        elif c == 'L':
            consecutive_late += 1
        # Reset the consecutive late days count to 0 if the character is 'P'
        else:
            consecutive_late = 0

        # Check the eligibility criteria
        if absences >= 2 or consecutive_late >= 3:
            return False

    return True
```

## 3. Solution Explanation:
- The solution iterates over the string and counts the number of absences and consecutive late days.
- If either the number of absences or the number of consecutive late days is greater than or equal to the specified threshold, the student is not eligible for the award.
- Otherwise, the student is eligible for the award.

## 4. Complexity Analysis:
- **Time complexity**: O(n), where n is the length of the string.
- **Space complexity**: O(1), as no additional data structures are used.

## Topics
String

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-11-13
